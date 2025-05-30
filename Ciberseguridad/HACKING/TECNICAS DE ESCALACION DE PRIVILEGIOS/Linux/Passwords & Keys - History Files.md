
- Si un usuario escribe accidentalmente su contraseña en la línea de comando en lugar de en una solicitud de contraseña, es posible que quede registrada en un archivo de historial.

- Vea el contenido de todos los archivos de historial ocultos en el directorio de inicio del usuario:

```
cat ~/.*history | less
```
Tenga en cuenta que el usuario ha intentado conectarse a un servidor MySQL en algún momento, utilizando el nombre de usuario "root" y una contraseña enviada a través de la línea de comando. Tenga en cuenta que no hay espacio entre la opción -p y la contraseña.

Cambie al usuario root, usando la contraseña:

```
su root
```

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]