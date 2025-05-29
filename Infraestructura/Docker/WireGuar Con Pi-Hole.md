
### Paso 1: Configurar el Servidor VPN

Asegúrate de que el servidor VPN (en este caso `wg-easy`) esté configurado para permitir el reenvío de tráfico a la red local.

### Paso 2: Configuración del `docker-compose.yml`

Ajustemos tu archivo `docker-compose.yml` para asegurarnos de que todo esté configurado correctamente.
```
version: "3.8"

services:
  wg-easy:
    environment:
      # ⚠️ Change the server's hostname (clients will connect to):
      - WG_HOST=myhost.com

      # ⚠️ Change the Web UI Password:
      - PASSWORD=foobar123

      # 💡 This is the Pi-Hole Container's IP Address
      - WG_DEFAULT_DNS=10.8.1.3
      - WG_DEFAULT_ADDRESS=10.8.0.x
    image: ghcr.io/wg-easy/wg-easy
    container_name: wg-easy
    volumes:
      - ~/.wg-easy:/etc/wireguard
    ports:
      - "51820:51820/udp"
      - "51821:51821/tcp"
    restart: unless-stopped
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    sysctls:
      - net.ipv4.ip_forward=1
      - net.ipv4.conf.all.src_valid_mark=1
    networks:
      wg-easy:
        ipv4_address: 10.8.1.2

  pihole:
    image: pihole/pihole
    container_name: pihole
    environment:
      # ⚠️ Change the Web UI Password:
      - WEBPASSWORD=foobar123
    volumes:
      - '~/.pihole/etc-pihole:/etc/pihole'
      - './.pihole/etc-dnsmasq.d:/etc/dnsmasq.d'
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "5353:80/tcp"
    restart: unless-stopped
    networks:
      wg-easy:
        ipv4_address: 10.8.1.3

networks:
  wg-easy:
    ipam:
      config:
        - subnet: 10.8.1.0/24
```


### Paso 3: Habilitar el Reenvío de IP

Asegúrate de que el reenvío de IP esté habilitado en el sistema host. Esto puede hacerse agregando o modificando la siguiente línea en `/etc/sysctl.conf`:


```
net.ipv4.ip_forward=1
```

Luego, aplica los cambios con:

```
sudo sysctl -p
```

### Paso 4: Configuración del Firewall

Asegúrate de que las reglas de firewall permitan el tráfico entre la red VPN y la red local. Aquí hay un ejemplo usando `iptables`:

```
# Permitir el reenvío de la VPN a la red local
sudo iptables -A FORWARD -i wg0 -o eth0 -j ACCEPT
sudo iptables -A FORWARD -i eth0 -o wg0 -m state --state RELATED,ESTABLISHED -j ACCEPT

# Hacer NAT (Network Address Translation) para permitir que el tráfico salga desde la red VPN a la red local
sudo iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE

```


Reemplaza `eth0` con la interfaz de red de tu servidor que está conectada a la red local.

### Paso 5: Configuración del Cliente VPN

En la configuración del cliente VPN, asegúrate de que las rutas a la red local estén definidas. Por ejemplo, en la configuración de WireGuard del cliente, agrega:

```
[Peer] PublicKey = <Servidor-PublicKey> Endpoint = myhost.com:51820 AllowedIPs = 10.8.0.0/24, 192.168.1.0/24  # Incluye la red local aquí
```

### Verificación

Después de realizar estos pasos, los clientes que se conecten a la VPN deberían poder acceder a los dispositivos en la red local (192.168.1.0/24).

### Notas Adicionales

- Asegúrate de que no haya políticas de firewall adicionales en el host que bloqueen el tráfico entre las subredes.
- Revisa los registros de WireGuard y las reglas de `iptables` para solucionar cualquier problema de conectividad.

Con esta configuración, deberías poder conectarte a la VPN y acceder a los dispositivos en tu red local desde los clientes VPN.

