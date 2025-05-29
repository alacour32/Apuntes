
- A veces, los usuarios realizan copias de seguridad de archivos importantes pero no logran protegerlas con los permisos correctos.

- Busque archivos y directorios ocultos en la raíz del sistema:

```
ls -la /
```

- Tenga en cuenta que parece haber un directorio oculto llamado .ssh. Ver el contenido del directorio:

```
ls -l /.ssh
```
Tenga en cuenta que hay un archivo legible en todo el mundo llamado root_key. Una inspección más detallada de este archivo debería indicar que es una clave SSH privada. El nombre del archivo sugiere que es para el usuario root.

- Copie la clave en su caja Kali (es más fácil simplemente ver el contenido del archivo root_key y copiar/pegar la clave) y otorgarle los permisos correctos; de lo contrario, su cliente SSH se negará a usarla:

```
chmod 600 root_key
```

- Utilice la clave para iniciar sesión en la máquina virtual Debian como cuenta raíz (tenga en cuenta que debido a la antigüedad de la caja, se requieren algunas configuraciones adicionales al usar SSH):

```
 ssh -i root_key -oPubkeyAcceptedKeyTypes=+ssh-rsa -oHostKeyAlgorithms=+ssh-rsa root@10.10.48.215
```


enlace:
[[Preparacion-Ejpt]]

