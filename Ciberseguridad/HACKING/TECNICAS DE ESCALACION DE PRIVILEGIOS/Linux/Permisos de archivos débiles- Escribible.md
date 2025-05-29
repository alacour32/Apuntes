# Archivo escribible:  /etc/shadow

- El archivo /etc/shadow contiene hashes de contraseñas de usuario y normalmente sólo puede leerlo el usuario root.

```
ls -l /etc/shadow
```

- Genera un nuevo hash de contraseña con una contraseña de tu elección:

```
mkpasswd -m sha-512 "nueva contraseña"
```

- Edite el archivo /etc/shadow y reemplace el hash de contraseña del usuario root original con el que acaba de generar.

- Cambie al usuario root, usando la nueva contraseña:

```
su root
```


# Archivo escribible:   /etc/passwd

- El archivo /etc/passwd contiene información sobre las cuentas de usuario. Es legible en todo el mundo. Pero generalmente sólo el usuario root puede escribirlo. Históricamente, el archivo /etc/passwd contenía hashes de contraseñas de usuario, y algunas versiones de Linux aún permitirán que los hashes de contraseñas se almacenen allí.

```
ls -l /etc/passwd
```

- Genera un nuevo hash de contraseña con una contraseña de tu elección:

```
openssl passwd "nueva contraseña"
```

- Edite el archivo /etc/passwd y coloque el hash de contraseña generado entre el primer y segundo dos puntos (:) de la fila del usuario root . Cambie al usuario root, usando la nueva contraseña:

```
su root
```

Eenlace:
[[Preparacion-Ejpt]]
[[Permisos de archivos débiles-Legible]]
