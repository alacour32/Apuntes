- # Para crear una Shell estable con Python: 

```
$ python3 -c 'import pty;pty.spawn("/bin/bash")'
```

- # Generador de reverse-Shell

	https://www.revshells.com/
	
Nota: Reverse Shell común en php (pentest monkey): 
- ## Estabilizar Shell:

- ### Ejecute uno (1) de los siguientes comandos para actualizar su Shell:
```
	1.
	$ python -c "import pty; pty.spawn('/bin/bash')" 
	$ ruby -e "exec '/bin/bash'" 
	$ perl -e "exec '/bin/bash';"
```
- ### Ahora, poner en segundo plano (suspender sessión):

```
	2.
	ctrl+z
```
- ### En la maquina atacante:
	- Deshabilitar la visualización de texto en la maquina atacante y luego cambiar al proceso en primer plano (la maquina objetivo):
```
	3.
	$ stty raw -echo && fg
```
- ### En la maquina objetivo:
	- configurar el entorno del terminal a algo más atractivo (por ejemplo, xterm, xterm-256, etc.)
```
	4.
	$ export TERM=xterm-256-color

```


Etiqueta:
[Preparacion-Ejpt](Preparacion-Ejpt.md)




