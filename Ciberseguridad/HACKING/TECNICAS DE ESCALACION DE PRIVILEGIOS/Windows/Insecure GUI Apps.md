- Inicie una sesión RDP como la cuenta "usuario:

```
rdesktop -u user -p password321 10.10.94.6
```

- Haga doble clic en el acceso directo "AdminPaint" en su escritorio. Una vez que se esté ejecutando, abra un símbolo del sistema y tenga en cuenta que Paint se está ejecutando con privilegios de administrador:

```
tasklist /V | findstr mspaint.exe
```

- En Pintura, haga clic en "Archivo" y luego en "Abrir". En el cuadro de diálogo abrir archivo, haga clic en la entrada de navegación y pegue: archivo://c:/windows/system32/cmd.exe

- Presione Entrar para generar un símbolo del sistema que se ejecuta con privilegios de administrador.

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Herramientas]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Generate a Reverse Shell Executable]]