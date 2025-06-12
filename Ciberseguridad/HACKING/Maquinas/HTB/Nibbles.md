- # Enumeracion:
	- ## Escaneo:
		- Realizamos el escaneo de todos los puertos con parametros para script, version de aplicaciones que escuchan, entre otros, y lo guardamos en un archivo "escaneo"
			```
			nmap -p- --open -sS -sC -sV --min-rate 5000 -vvv -n -Pn 10.10.10.75 -oN Escaneo
			```
		- El resultado son el puerto 22 y 80 abiertos:
			```
			PORT   STATE SERVICE REASON         VERSION
			22/tcp open  ssh     syn-ack ttl 63 OpenSSH 7.2p2 Ubuntu 4ubuntu2.2 (Ubuntu Linux; protocol 2.0)
			| ssh-hostkey: 
			|   2048 c4:f8:ad:e8:f8:04:77:de:cf:15:0d:63:0a:18:7e:49 (RSA)
			| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQD8ArTOHWzqhwcyAZWc2CmxfLmVVTwfLZf0zhCBREGCpS2WC3NhAKQ2zefCHCU8XTC8hY9ta5ocU+p7S52OGHlaG7HuA5Xlnihl1INNsMX7gpNcfQEYnyby+hjHWPLo4++fAyO/lB8NammyA13MzvJy8pxvB9gmCJhVPaFzG5yX6Ly8OIsvVDk+qVa5eLCIua1E7WGACUlmkEGljDvzOaBdogMQZ8TGBTqNZbShnFH1WsUxBtJNRtYfeeGjztKTQqqj4WD5atU8dqV/iwmTylpE7wdHZ+38ckuYL9dmUPLh4Li2ZgdY6XniVOBGthY5a2uJ2OFp2xe1WS9KvbYjJ/tH
			|   256 22:8f:b1:97:bf:0f:17:08:fc:7e:2c:8f:e9:77:3a:48 (ECDSA)
			| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBPiFJd2F35NPKIQxKMHrgPzVzoNHOJtTtM+zlwVfxzvcXPFFuQrOL7X6Mi9YQF9QRVJpwtmV9KAtWltmk3qm4oc=
			|   256 e6:ac:27:a3:b5:a9:f1:12:3c:34:a5:5d:5b:eb:3d:e9 (ED25519)
			|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIC/RjKhT/2YPlCgFQLx+gOXhC6W3A3raTzjlXQMT8Msk
			80/tcp open  http    syn-ack ttl 63 Apache httpd 2.4.18 ((Ubuntu))
			| http-methods: 
			|_  Supported Methods: GET HEAD POST OPTIONS
			|_http-title: Site doesn't have a title (text/html).
			Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
			```
		- Hacemos chequeo de las tecnologias que maneja el sitio por el puerto 80
		```
		whatweb 10.10.10.75
		http://10.10.10.75 [200 OK] Apache[2.4.18], Country[RESERVED][ZZ], HTTPServer[Ubuntu Linux][Apache/2.4.18 (Ubuntu)], IP[10.10.10.75]
		```
		- Tratamos de acceder al sitio por el explorado de internet:
		![[Pasted image 20250611193959.png]]
		- Vemos el codigo fuente y encontramos un subdirectori en el sitio:
			![[Pasted image 20250611203507.png]]
			- ![[Pasted image 20250611203557.png]]
		- Buescamos exploit posibles para el sitio hecho en NIBBLEBLOG con searchesploit:
			![[Pasted image 20250611203735.png]]
		- haciendo fuzzing encontramos la direccion "/admin.php":
			- ![[Pasted image 20250611204106.png]]
		- usamos burp para ver como es el pasaje de credenciales:
			- ![[Pasted image 20250611204329.png]]
		- podemos observar la el formato de la peticion POST e intentar usarla con hydra
			- ![[Pasted image 20250611204556.png]]
		- pero por sentido comun sacamos que el pass es nibbles (nombre de la maquina)
		- encontramos una forma de subir archivos maliciosos como por ejemplo un reverseshell en php
			![[Pasted image 20250611213539.png]]
		- Lo subimos en esta seccion del sitio
			- ![[Pasted image 20250611213703.png]]
		- en la direccion "nibbleblog/content/"  podemos ejecutar comando por intermedio de la url como por ejemplo: http://10.10.10.75/nibbleblog/content/private/plugins/my_image/image.php?cmd=whoami
			- ![[Pasted image 20250611214455.png]]
		- Vamos a la direccion "nibbleblog/content/" para ubicar el revershell recien subido y poder ejecutarlo:
