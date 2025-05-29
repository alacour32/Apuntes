## **EXPLOTACION WEB**:
```
hydra -l <usuario>  -P <archivo diccionario>  <sitio> http-post-form "<pagina del 
formulario>:log=^USER^&pwd=^PWD^:<mensage de error>" -t 30 -v 
```

- `-l <nombre_de_usuario>`: Especifica el nombre de usuario que queremos probar.
- `-P <lista_de_contraseñas>`: Especifica la lista de contraseñas que queremos probar.
- `example.com`: Es la dirección del sitio web objetivo.
- `http-post-form "/login.php:username=^USER^&password=^PASS^:F=Invalid"`: Especifica el método de ataque. En este caso, estamos utilizando el método POST para enviar los datos de inicio de sesión al formulario web en `/login.php`, con los campos `username` y `password`. El marcador `^USER^` se reemplazará con el nombre de usuario de la lista de usuarios, y `^PASS^` se reemplazará con la contraseña de la lista de contraseñas. La cadena `F=Invalid` indica a Hydra que interprete una respuesta de "Invalid" como un fallo de inicio de sesión.
- `-t <cantidad de thears>`: es la cantidad de hilos dedicados para realizar la explotacion
- `-v` : verbose

Recuerda reemplazar `<nombre_de_usuario>` con el nombre de usuario que quieras probar y `<lista_de_contraseñas>` con la ruta de la lista de contraseñas que quieras utilizar.

## **EXPLOTACION POP**:

comando:

```
hydra -l <usuario> -P <diccionario> -s <puerto> <IP> pop3
```

El comando que proporcionaste está utilizando Hydra, una herramienta de fuerza bruta para realizar ataques de fuerza bruta contra diversos servicios de red, como SSH, FTP, Telnet, HTTP, etc. Aquí está cómo funciona este comando específico:

- `hydra`: Este es el comando principal de la herramienta Hydra.
    
- `-l `: Especifica el nombre de usuario a utilizar en el intento de inicio de sesión. 
    
- `-P` : Especifica la ubicación del archivo de lista de contraseñas que se utilizará en el intento de inicio de sesión.
    
- `-s` : Especifica el número de puerto del servicio al que se intentará acceder. 
    
- `pop3`: Especifica el protocolo que se utilizará para el intento de inicio de sesión. En este caso, es POP3.
    


enlace:
[[Preparacion-Ejpt]]
