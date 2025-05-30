- **Metodologia de penetratios testing

![[Apuntes/Imagenes/Pasted image 20240802205805.png]]
- **Tipos de escaneo

![[Apuntes/Imagenes/Pasted image 20240802210017.png]]

# #Explotación: 


# #PostExplotación:

Ahora, una vez hayas realizado todo lo anterior, deberías preocuparte por descubrir nuevos activos y repetir los pasos anteriores si fuese necesario.
	
- ## Wireshark
```
		- ip.addr==192.168.12
		- ip.src == 192.168.2.11
		- ip.dst == 192.168.2.15
```

- ## IP Route

```
ip route add 10.10.10.0/24 via 10.10.11.1 dev tap0
```

 
enlace: 
[Reverse-shell](Local/Ciberseguridad/HACKING/HERRAMIENTAS/Reverse-Shell.md)
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Service Exploits]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Permisos de archivos débiles-Legible]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Permisos de archivos débiles- Escribible]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Sudo - Environment Variables (variable de entorno)]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Sudo - Shell Escape Sequences]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Cron Jobs - File Permissions]] 
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables  Known - Exploits]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Abusing Shell Features (1)]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Abusing Shell Features (2)]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Shared Object Injection]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/SUID - SGID Executables - Environment Variables]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Passwords & Keys - History Files]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Passwords & Keys - Config Files]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/Passwords & Keys - SSH Keys]] 
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Linux/NFS]]
[[Local/Ciberseguridad/HACKING/TECNICAS DE ESCALACION DE PRIVILEGIOS/Windows/Generate a Reverse Shell Executable]]
[[Local/Ciberseguridad/HACKING/HERRAMIENTAS/SQLMAP]]
[[Local/Ciberseguridad/HACKING/HERRAMIENTAS/John The Riper]]
[[Local/Ciberseguridad/HACKING/HERRAMIENTAS/HYDRA 1]]
[[Local/Ciberseguridad/Devsecops/HERRAMIENTAS/Hash identifier]]