
**Comando whatis host
```
whatis host
```

**Comando host
```
host "equipo/pagina we"
```

**Chequear el archivo robot-txt
 - Arhivo que se busca entre las paginas web de un sitio para poder confiramar las paginas  a las que se puede y no acceder por url
 
**Chequear archivo page-sitemap.xml 
* es el archivo en el cual esta de forma organizada se indexan las paginas web en el sitio

**Chequear tecnologia con addons en las paginas web
- esto se realiza para observar como estan constituidas las pagianas web se suelen utilizar addons como:
	- wapanalaizer
	- builtwith
- tb se puede utilizar la herramienta whatweb o httrack
```
	whatwheb "pagina web"
	httrack
```

-  httrack permite crear una pagina a en la cual se analizar las paginas atacantes

**Comando whois
- Sirve para poder ver toda la informacion del mismo sitio como  dominio, server, url, creacion, etc
```
		whois "sitio web"
```

**Herramienta web: www.netcraft.com
- sirve para ver informacion de y realizar data mining de un sitio

**Dns recon:
- Herramienta para levantar informacion sobre el dominio:
```
	- dnsrecon -d "sitioweb"
```
- tb se puede usar la herramienta web: https://dnsdumpster.com/

**Herramienta para detectar si el sitio victima esta siendo protegido por un firewall
- instalar herramienta: wafw00f
- utilizarla :
```
	- wafw00f  "sitio web"
```

**Herramienta para enumerar subdominios:
- se trata de la herramienta sublist3r:
-  enumeracion comun
```
	-  sublist3r -d "dominio"
```
- enumeracion con fuerza bruta:
```
	- sublist3r -d "dominio" -b
```
- enumeracion utilizando buscadores
```
	- sublist3r -d "dominio" -e "buscador"
```

**Google Dorks:
- operadores:
	- site: para espesificar un sitio
	- inurl: para buscar dentro de una url
	- filetype: espesifica un tipo de archivo
	- intitle: busqueda en los titulos de resultado
	- cache: si se desea ver como se veia un sitio hace un tiempo (tb se puede ustilizar la pagina: https://web.archive.org/)
**Herramientas para enumerar dominios de email:
-  theHarvester : sirve para localizar cuentas de correo atraves de distintos buscadores:
```
	-  theHarvester -d "dominio" -b "buscador"
```

**Búsqueda  de password filtradas
- se pude utilizar la pagina: https://haveibeenpwned.com/

**Búsqueda de dns 
- utilizando la herramienta dnsenum: 
```
	- dnsenum "pagina web"
```
- utilizando la herramienta fierce:
```
	-  fierce -dns "dominio" -wordlist "diccionario"
```

**Búsqueda de host en la red  (ping sweeps):
```
		fping -a -g 10.10.10.0/24 2>/dev/null
		netdiscover -i "interfase" -r "sub-net"
		
```

- **Servicios Web:
```

		- nmap --script=http-enum -p80 10.10.14.16 -oN webScan
			- wfuzz -c --hc=404 -w /usr/share/wordlists/dirbuster/directory-|list-2.3-medium.txt -u https://10.10.14.15/FUZZ
		- wfuzz -c --hc=404 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.14.15/FUZZ.php

```
- **XSS:
```

		- <script>alert(xss)</script>
		- <h1>H1</h1>
```


- **Enumeración de SMB:
```

		- smbclient -L 10.10.14.12 -N
		- smbmap -H 10.10.14.12 -u 'null'
		- nmap --script=smb-vuln* -p445 10.10.14.15 -oN smbScan
		- smbmap -H 10.10.14.15 -R backups -u 'null' 
		- smbclient //10.10.14.15/backups

```

- **Enumeración de POP###
```
nc 10.10.39.167 55007
+OK GoldenEye POP3 Electronic-Mail System
USER
+OK
Boris
-ERR Unknown command.
LOGIN boris InvincibleHack3r
-ERR Unknown command.
LOGIN   
-ERR Unknown command.
USER
+OK
boris
-ERR Unknown command.
USER boris
+OK
PASS InvincibleHack3r
-ERR [AUTH] Authentication failed.
-ERR Disconnected for inactivity.
```

- **Enumeración de Windows:

Una vez hayas comprometido el activo, deberás enumerar lo, los siguientes comandos te serán de gran ayuda:
```
		- dir /b/s "\*.conf*"
		- dir /b/s "\*.txt*"
		- dir /b/s "\*secret*"
		- route print
		- netstat -r
		- fsutil fsinfo drives
		- wmic logicaldisk get Caption,Description,providername

```