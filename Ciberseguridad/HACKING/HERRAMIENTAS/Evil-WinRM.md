- Es una herramienta popular en el ámbito de pruebas de penetración y hacking ético que se utiliza para interactuar con sistemas Windows de manera remota a través del servicio **WinRM (Windows Remote Management)**. WinRM es una interfaz de administración que permite a los administradores gestionar remotamente los equipos Windows y ejecutar comandos, y **Evil-WinRM** se aprovecha de este servicio para proporcionar una **shell interactiva** en máquinas Windows.
- ### Características Principales de Evil-WinRM
	
	1. **Shell Interactiva**:
	    
	    - Evil-WinRM permite obtener una shell interactiva en el sistema remoto, facilitando la ejecución de comandos de manera muy similar a como se haría desde el propio sistema.
	2. **Gestión de Archivos**:
	    
	    - La herramienta permite cargar (upload) y descargar (download) archivos hacia y desde el sistema remoto, facilitando la transferencia de herramientas, scripts, y resultados de ejecución de comandos.
	3. **Ejecución de Scripts y Carga de Módulos**:
	    
	    - Evil-WinRM permite ejecutar scripts en PowerShell y cargar módulos directamente en el sistema remoto. Esto es útil para ejecutar scripts personalizados, cargar herramientas como **Mimikatz** para la extracción de credenciales, o realizar tareas de post-explotación.
	4. **Autenticación NTLM y Kerberos**:
	    
	    - Evil-WinRM es compatible con credenciales en texto plano y hashes NTLM, permitiendo el uso de técnicas como **Pass-The-Hash**.
	    - También soporta autenticación Kerberos si está configurada en el entorno, lo que es útil en redes de Active Directory.
	5. **Interacción con Credenciales en PowerShell**:
	    
	    - Al funcionar en el entorno de PowerShell, Evil-WinRM facilita la interacción con credenciales y la automatización de tareas de gestión remota en sistemas Windows.
	6. **Uso en Escenarios de CTF y Auditorías**:
	    
	    - Evil-WinRM es ampliamente usado en entornos de Capture The Flag (CTF) y en auditorías de red, especialmente en redes Windows. Su simplicidad y efectividad la convierten en una herramienta de elección para obtener y mantener acceso en sistemas Windows.

- ### Instalación de Evil-WinRM
	
	- Para utilizar Evil-WinRM, necesitas **Ruby** instalado en el sistema, ya que el script está escrito en este lenguaje.
	
	- Para instalar Evil-WinRM en Linux:
		
		`sudo gem install evil-winrm`
	
	- Este comando instala Evil-WinRM y sus dependencias en el sistema.

- ### Uso Básico de Evil-WinRM
	
	- La sintaxis básica de Evil-WinRM es la siguiente:
		 `evil-winrm -i <IP_del_Equipo> -u <Usuario> -p <Contraseña>` 

- #### Ejemplos de Uso
	
	1. **Conectar a un Equipo Remoto**:
	    
	    bash
	    
	    Copiar código
	    
	    `evil-winrm -i 192.168.1.10 -u administrator -p Password123`
	    
	    Este comando conecta a la IP `192.168.1.10` usando el usuario `administrator` y la contraseña `Password123`.
	    
	2. **Autenticación Pass-The-Hash**:
	    
	    bash
	    
	    Copiar código
	    
	    `evil-winrm -i 192.168.1.10 -u administrator -H <hash_NTLM>`
	    
	    Esto permite conectarse utilizando un hash NTLM en lugar de una contraseña en texto plano, una técnica conocida como Pass-The-Hash.
	    
	3. **Transferir Archivos**:
	    
	    - **Subir un Archivo**:
	        
	        bash
	        
	        Copiar código
	        
	        `upload /ruta/local/archivo.txt C:\ruta\remota\archivo.txt`
	        
	    - **Descargar un Archivo**:
	        
	        bash
	        
	        Copiar código
	        
	        `download C:\ruta\remota\archivo.txt /ruta/local/archivo.txt`
	        
	4. **Ejecutar un Script en PowerShell**:
	    
	    - Puedes ejecutar scripts de PowerShell para realizar tareas automatizadas, o cargar herramientas de post-explotación como Mimikatz en el sistema remoto.
	5. **Autenticación Kerberos**:
	    
	    - Evil-WinRM también soporta autenticación Kerberos en entornos de dominio, lo que se puede configurar usando un ticket Kerberos (usualmente con la variable `KRB5CCNAME` en Linux).

- ### Ejemplo en un Escenario de Pentesting

	- Supón que tienes acceso a un hash NTLM de un administrador en un entorno de Active Directory. Puedes usar Evil-WinRM para conectarte al sistema remoto:
	
		`evil-winrm -i 192.168.1.10 -u administrator -H d3adbeef1234567890abcdef12345678`

	- Una vez dentro del sistema remoto, puedes ejecutar comandos, transferir herramientas como Mimikatz para extraer credenciales de la memoria, o buscar archivos sensibles en el equipo.