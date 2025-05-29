
Fuente: https://docs.portainer.io/start/install-ce/server/docker/linux 

- Crear volumen Docker que contendrá los datos gestionados por el servidor Portainer:
```
docker volume create portainer_data 
```

- Descargar e instalar contenedor Portainer: 

```
docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest

```

-Ver contenedores instalados: 

```
docker ps 
```

- Acceso a Portainer: https://[IP del equipo]:9443 
