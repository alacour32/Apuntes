 **Instalación Docker

Docker en: https://docs.docker.com/engine/install/debian/ 

- Instalar Docker y Docker Compose: 

```
sudo curl -fsSL https://get.docker.com/ -o get-docker.sh
sudo sh get-docker.sh 
```

- Añadir nuestro usuario al grupo Docker: 

```
sudo usermod -aG docker ${USER} 
```

- Reiniciar sistema: 

```
sudo reboot 
```


**Clonar el Repositorio**

Primero, clona el repositorio DevOps/vulnerable-web-app:

```
git clone https://github.com/GinoDevOps/vulnerable-web-app.git
```

** Construir la Imagen Docker**


```
docker build -t vulnerable-web-app .
```

 Probar la Imagen Localmente**

```
docker run -d -p 8080:80 vulnerable-web-app
```

Luego, abre un navegador y navega a http://localhost:8080 para verificar que la aplicación se está ejecutando.


**Desplegar en Heroku**


1. Instala la CLI de Heroku y crea una nueva aplicación:

```
heroku login

heroku create alvaro-lacour

```
2. Configura Heroku para usar Docker:

```
heroku stack:set container
```

3. Conectar git local en remote heroku
```
heroku git:remote -a alvaro-lacour
```
4. Build la imagen y push el container en Registry Heroku
```
heroku container:push alvaro-lacour
```
5. Ejecute la image en la aplicacion

```
heroku container:release alvaro-lacour
```

**Probar la Aplicación en Heroku**
Una vez desplegada, Heroku te proporcionará una URL para acceder a la aplicación. 

```
https://alvaro-lacour-6c5a31e0eee2.herokuapp.com/
```


