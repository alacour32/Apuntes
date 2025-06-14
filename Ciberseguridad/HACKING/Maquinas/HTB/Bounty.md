- Hacemos escaneo de puertos:
```bash
map -sV -sC -Pn -p- --min-rate 5000 -n -sS --open 10.10.10.93 -oN Escaneo
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-13 17:43 EDT
Nmap scan report for 10.10.10.93
Host is up (0.56s latency).
Not shown: 65534 filtered tcp ports (no-response)
Some closed ports may be reported as filtered due to --defeat-rst-ratelimit
PORT   STATE SERVICE VERSION
80/tcp open  http    Microsoft IIS httpd 7.5
|_http-title: Bounty
|_http-server-header: Microsoft-IIS/7.5
| http-methods: 
|_  Potentially risky methods: TRACE
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 48.70 seconds
```
- Chequeamos la tecnologia de la maquina remota:
```bash
	- whatweb 10.10.10.93
http://10.10.10.93 [200 OK] Country[RESERVED][ZZ], HTTPServer[Microsoft-IIS/7.5], IP[10.10.10.93], Microsoft-IIS[7.5], Title[Bounty], X-Powered-By[ASP.NET]
```
- Fuzzeamos en los directorios de la maquina victima:
```bash
	gobuster dir -u http://10.10.10.93 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x aspx -o gobuste.log
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.10.93
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              aspx
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/transfer.aspx        (Status: 200) [Size: 941]
```
- Encontramos el directorio "/transfer.aspx"
	- ![[Pasted image 20250613204540.png]]
- Procedemos a usar burpsuit para identificar las posibles extenciones que acepta la pagina:
	- ![[Pasted image 20250613204751.png]]
- Usamos la opcion de intruder para poder enviar una lista de posibles extenciones 
	- ![[Pasted image 20250613204849.png]]
- Podemos observar que la extension .config es aceptada
	- ![[Pasted image 20250613204947.png]]
- 