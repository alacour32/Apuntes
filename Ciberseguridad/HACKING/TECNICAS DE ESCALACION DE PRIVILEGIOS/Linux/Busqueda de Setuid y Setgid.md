
Comando:

```
 find / -perm +6000 2>/dev/null | grep '/bin/'
```

![[Pasted image 20240407020908.png]]

Este comando busca archivos con permisos establecidos en el sistema de archivos que tienen el bit setuid o setgid activado y que están ubicados en el directorio `/bin/` o sus subdirectorios.

Aquí está desglosado el comando:

- `find / -perm +6000 2>/dev/null`: Este comando utiliza `find` para buscar archivos en todo el sistema de archivos (`/`) que tienen permisos establecidos y activados (con el bit setuid o setgid) utilizando el formato octal. El `+` indica que busca archivos con cualquier combinación de los permisos especificados. El `2>/dev/null` redirige cualquier mensaje de error (`stderr`) a `/dev/null`, lo que significa que los mensajes de error no se mostrarán en la salida.
    
- `|`: Este es el operador de tubería, que toma la salida del comando anterior y la pasa como entrada al siguiente comando.
    
- `grep '/bin/'`: Este comando `grep` filtra las líneas de texto que contienen la cadena `/bin/`. En este contexto, busca archivos que estén ubicados en el directorio `/bin/` o en sus subdirectorios.
    

En resumen, este comando busca archivos con permisos setuid/setgid en todo el sistema de archivos y filtra los resultados para mostrar solo aquellos que están ubicados en el directorio `/bin/` o sus subdirectorios. Esto puede ser útil para identificar archivos ejecutables con permisos elevados que se encuentran en ubicaciones específicas del sistema.