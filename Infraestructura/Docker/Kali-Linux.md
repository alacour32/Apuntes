- descarga de la imagen (en este caso se bajo la que es para raspberry)

```
docker pull kalilinux/kali-rolling:arm64
```
- Ejecutar contenedor :

```
docker run -it --name kali-wifi --hostname kali [imagen descargada]
```

- Crear una imagen personalizada :
```
docker commit [nombre del contenedor] [nombre que va a tener la nueva imagen]
```

- Crear contenedor sacando a red del host

```
 docker run -it  --network=host  --name kali-wifi --hostname kali-wifi kali-wifi
```

