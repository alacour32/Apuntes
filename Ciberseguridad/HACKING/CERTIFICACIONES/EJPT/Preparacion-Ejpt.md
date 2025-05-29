- **Metodologia de penetratios testing

![[Pasted image 20240802205805.png]]
- **Tipos de escaneo

![[Pasted image 20240802210017.png]]

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
[Reverse-shell](Reverse-Shell.md)
[[Service Exploits]]
[[Permisos de archivos débiles-Legible]]
[[Permisos de archivos débiles- Escribible]]
[[Sudo - Environment Variables (variable de entorno)]]
[[Sudo - Shell Escape Sequences]]
[[Cron Jobs - File Permissions]] 
[[SUID - SGID Executables  Known - Exploits]]
[[SUID - SGID Executables - Abusing Shell Features (1)]]
[[SUID - SGID Executables - Abusing Shell Features (2)]]
[[SUID - SGID Executables - Shared Object Injection]]
[[SUID - SGID Executables - Environment Variables]]
[[Passwords & Keys - History Files]]
[[Passwords & Keys - Config Files]]
[[Passwords & Keys - SSH Keys]] 
[[NFS]]
[[Generate a Reverse Shell Executable]]
[[SQLMAP]]
[[John The Riper]]
[[HYDRA 1]]
[[Hash identifier]]