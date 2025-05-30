- Los archivos de configuración suelen contener contraseñas en texto sin formato u otros formatos reversibles.

- Enumere el contenido del directorio de inicio del usuario:

```
ls /home/user
```
 
 - Tenga en cuenta la presencia de un archivo de configuración myvpn.ovpn. Ver el contenido del archivo:

```
 cat /home/user/myvpn.ovpn
```

- El archivo debe contener una referencia a otra ubicación donde se puedan encontrar las credenciales del usuario raíz. Cambie al usuario root, usando las credenciales:

```
su root
```

enlace:
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Passwords & Keys - History Files]]
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]