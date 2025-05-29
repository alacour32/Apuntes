## Instalacion Docker

Docker y Docker Compose en Raspberry Pi Fuente: https://docs.docker.com/engine/install/debian/ 

- Instalar Docker y Docker Compose: 

```bash
sudo curl -fsSL https://get.docker.com/ -o get-docker.sh
sudo sh get-docker.sh 
```

- Añadir nuestro usuario al grupo Docker: 

```bash
sudo usermod -aG docker ${USER} 
```

- Reiniciar sistema: 

```bash
sudo reboot 
```

- Ejecutar un contenedor de prueba: 

```bash
docker run hello-world
```
- Instalacion de docker-compose:
```bash
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
## Gestion

- Listar imagenes

```bash
docker images
```

- Eliminacion de imagenes:

```bash
 docker rmi ee301c921b8a
```
 

- Ejecutar archivo docker file:

```bash
docker build [direccion de donde esta el archivo dockerfile] -t [nombre de la imagen]
```

- Ejecutar contenedor ya en ejecucion:

```bash
 docker exec -it  [nombre del contenedor en ejecuccion] [comando como se esta ejecutando]
```

- Crear red en docker
```bash
docker network create --driver [modo en el cual se montara la red (bridge o host)] --ipam-driver=[controlador para el manejo de las ip del contenedor (default)]
```
- Crear contenedor con privilegios sobre un dispositivo 

```bash
Docker run --device=[dispositivo al que se le dara privilegios] --privileged -it [imagen del contenedor]
```
