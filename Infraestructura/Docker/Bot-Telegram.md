Docker compose:
```
version: '3.3'
services:
    docker-controller-bot:
        environment:
            - TELEGRAM_TOKEN=
            - TELEGRAM_ADMIN=
            - CONTAINER_NAME=docker-controller-bot
            - TZ=Europe/Madrid
            #- TELEGRAM_GROUP=
            #- TELEGRAM_THREAD=1
            #- TELEGRAM_NOTIFICATION_CHANNEL=
            #- CHECK_UPDATES=1
            #- CHECK_UPDATE_EVERY_HOURS=4
            #- BUTTON_COLUMNS=2
            #- LANGUAGE=ES
            #- EXTENDED_MESSAGES=0
        volumes:
            - /var/run/docker.sock:/var/run/docker.sock # NO CAMBIAR
            - /ruta/para/guardar/las/programaciones:/app/schedule # CAMBIAR LA PARTE IZQUIERDA
        image: dgongut/docker-controller-bot:latest
        container_name: docker-controller-bot
        restart: always
        network_mode: host
        tty: true
```

- Activar el bot en telegram en buscando @bot-father (te pedira nombre del bot y nombre de usuario) y te otorgara el telegram_token
- buscar el contacto @get_id_bot para conseguir el id admin de telegram

fuente: https://github.com/dgongut/docker-controller-bot