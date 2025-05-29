docker compose:

```
version: "3.8"
services:
  plex:
    image: lscr.io/linuxserver/plex:latest
    container_name: plex
    network_mode: host
    environment:
      - PUID=1000
      - PGID=1000
      - VERSION=docker
      - PLEX_CLAIM=tocken de plex
    volumes:
      - path de la carpeta:/config
      - path de la carpeta:/tv
      - path de la carpeta:/movies
      - path de la carpeta:/music
    restart: unless-stopped
```

Antes de ejecutar el docker compose hay que montar las carpetas de biblioteca

```
sudo mount -t cifs //path de la carpeta /mnt/carpeta de biblioteca -o username=your_username,password=your_password,vers=3.0
```


luego de montar las unidades hay que hacerlas persistentes en el archivo /etc/fstab harcodeando  la siguiente linea

```
"ip" : "path de la carpeta" "path del punto de montaje" nfs defaults 0 0
```


