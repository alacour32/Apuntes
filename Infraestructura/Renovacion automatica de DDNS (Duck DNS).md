## Paso 1
si estás corriendo [http://www.raspbmc.com/](http://www.raspbmc.com/) entonces debes seguir el [raspbmc](https://www.duckdns.org/install.jsp?tab=raspbmc&domain=silver32) instrucciones  
primero permite iniciar sesión en su raspberrypi sobre ssh

```
ssh pi@raspberrypi
```
## Paso 2
luego, hagamos un directorio para colocar sus archivos, muévase a él y haga nuestro script principal
```

mkdir duckdns
cd duckdns
vi duck.sh
```
## Paso 3
ahora copie este texto y póngalo en el archivo (en vi usted golpeó el **yo** llave para insertar, **ESC** entonces **u** deshacer) El siguiente ejemplo es para el dominio **silver32**  
si desea la configuración para un dominio diferente, utilice el cuadro desplegable de arriba  
puede pasar una lista de dominios separados por comas (sin espacios)  
puede hacerlo si necesita codificar una IP (mejor no hacerlo, déjela en blanco y detectamos su ip remoto)  
golpear **ESC** luego use las teclas de flecha para mover el cursor **x** elimina, **yo** lo pone de nuevo en modo de inserción
```

echo url="https://www.duckdns.org/update?domains=silver32&token=2948af9d-8403-45f7-9e7e-277327e8e630&ip=" | curl -k -o ~/duckdns/duck.log - K -
```
## Paso 4
ahora guarde el archivo (en vi hit **ESC** entonces **:wq!** entonces **ENTRAR**)  
este script realizará una solicitud https y registrará la salida en el archivo duck.log  
ahora haga que el archivo duck.sh sea ejecutable

```
chmod 700 duck.sh
```
## Paso 5
a continuación, usaremos el proceso cron para hacer que el script se ejecute cada 5 minutos

```
crontab -e
```
## Paso 6
copie este texto y péguelo en la parte inferior del crontab

```
*/5 * * * * ~/duckdns/duck.sh >/dev/null 2>&1
```

ahora guarde el archivo (**CTRL+o** entonces **CTRL+x**)  
## Paso 7
probemos el script

```
./duck.sh
```

esto debería simplemente volver a un mensaje  
también podemos ver si el último intento fue exitoso (**OK** o malo **KO**)

```
cat duck.log
```

si es KO, verifique que su Token y Dominio sean correctos en el **duck.sh** guión  
La tarea final para Raspbmc es hacer que el cron se inicie automáticamente en el reinicio para Raspbian no es necesario hacer esto  
primero simplemente comenzamos manualmente el crontab

```
sudo service cron start
```

Luego, para iniciar automáticamente cron en el reinicio, en Raspmbc marca la opción en el menú Programas Raspbmc en XBMC