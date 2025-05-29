- `CrackMapExec` (CME) es una herramienta potente y versátil utilizada por equipos de **red team** y profesionales de **pentesting** para evaluar la seguridad de redes que utilizan el protocolo SMB (Server Message Block). Permite realizar múltiples ataques en redes Windows, Linux y Samba, y está diseñada para automatizar tareas comunes relacionadas con la gestión de credenciales y control de acceso en dominios y redes corporativas.

- ### Funciones clave de CrackMapExec
	
	1. **Enumeración**:  
	    CME puede enumerar información valiosa sobre la red, como:
	    
	    - Usuarios y grupos de dominio.
	    - Políticas de seguridad locales.
	    - Versiones de software.
	    - Comparticiones SMB accesibles.
	2. **Autenticación**:  
	    Puede verificar credenciales (usuarioclave, hashes NTLM) en múltiples objetivos dentro de una red para comprobar si son válidas.
	    
	3. **Ejecutar comandos de forma remota**:  
	    CME permite la ejecución de comandos en sistemas remotos mediante técnicas como:
	    
	    - **PSExec** (ejecución de comandos a través de SMB).
	    - **WMIC** (herramienta de gestión de sistemas remotos).
	    - **DCE/RPC** (Distributed Computing Environment / Remote Procedure Calls).
	4. **Movimientos laterales y pivoting**:  
	    Una vez que CME ha validado credenciales, puede utilizarlas para acceder a otros equipos en la red, realizar movimientos laterales, y ejecutar comandos en máquinas comprometidas.
	    
	5. **Pass-the-Hash y Pass-the-Ticket**:  
	    CME soporta ataques de **Pass-the-Hash** (usando el hash NTLM en lugar de la contraseña) y **Pass-the-Ticket** (usando tickets Kerberos robados) para autenticarse y moverse lateralmente por la red.
    

- ### Sintaxis y uso de CrackMapExec

	- La sintaxis básica para CME es la siguiente:
	
		`crackmapexec <protocolo> <objetivo> -u <usuario> -p <contraseña>`
	
	- Donde:
		
		- `<protocolo>`: Especifica el protocolo a utilizar, como `smb`, `rdp`, `ssh`, `ldap`, entre otros.
		- `<objetivo>`: Dirección IP o rango de IP de los sistemas a atacar.
		- `-u <usuario>`: Nombre de usuario.
		- `-p <contraseña>`: Contraseña o lista de contraseñas.

- ### Ejemplos de uso
	
	1. **Enumerar usuarios del dominio**
	      
	    `crackmapexec smb 192.168.1.100 -u usuario -p password --users`
	    
	2. **Verificar credenciales en un rango de IPs**
	       
	    `crackmapexec smb 192.168.1.0/24 -u usuario -p password`
	    
	3. **Ejecutar un comando remoto en un equipo específico**
	       
	    `crackmapexec smb 192.168.1.100 -u usuario -p password -x "ipconfig"`
	    
	4. **Autenticarse usando un hash NTLM (Pass-the-Hash)**
	    
	    `crackmapexec smb 192.168.1.100 -u usuario -H <NTLM_hash>`
	    
	5. **Forzar la autenticación de SMB a través de un ataque con NTLM relay**
	
	    `crackmapexec smb 192.168.1.100 --ntlm`