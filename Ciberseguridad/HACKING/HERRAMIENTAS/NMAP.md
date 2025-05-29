******- ## Busqueda de host en la red con nmap (ping sweeps):
	- **Técnicas de Descubrimiento de Hosts**
		- Barridos de Ping (Solicitudes ICMP Echo): Envío de solicitudes ICMP Echo (ping) a un rango de direcciones IP para identificar hosts activos. Este es un método rápido y comúnmente utilizado.
	    - Escaneo ARP: Uso de solicitudes del Protocolo de Resolución de Direcciones (ARP) para identificar hosts en una red local. El escaneo ARP es efectivo para descubrir hosts dentro del mismo dominio de difusión.
	    - Ping TCP SYN (Escaneo a Medio Abrir): Envío de paquetes TCP SYN a un puerto específico (a menudo el puerto 80) para comprobar si un host está activo. Si el host está activo, responde con un TCP SYN-ACK. Esta técnica es más sigilosa que el ping ICMP.
		```
		nmap -sn -Pn 10.10.10.0/24
		```
	- **Busqueda SYN ping en uno o varios host:**
		```
		nmap -PS (puertos) "host"
		```
	- **Busqueda ACK ping en uno o varios host:**
		```
		nmap -PA (puertos) "host"
		```
	- **Busqueda ICMP Echo Request en uno o varios host:**
		```
		nmap -PE (puertos) "host"
		```
	- **Busqueda UDP:**
		```
		nmap -PU "host"
		```
	- **Busqueda de host basada en un listado en un archivo**
		```
		nmap -sn -iL "archivo.txt"
		```
- ## Escaneos
	- **Escaneo normal**
		```
		nmap "host"
		```
	- **Escaneo Avanzado:**
		- El comando `nmap -A` se utiliza para realizar un escaneo avanzado en una red o un host específico. La opción `-A` habilita varias funcionalidades avanzadas de Nmap, proporcionando una gran cantidad de información sobre el objetivo. A continuación se detallan las características principales que se habilitan con `-A`:

		- ### Funcionalidades del comando `nmap -A`:

			1. **Detección de Sistema Operativo**:
	    		    - Nmap intenta identificar el sistema operativo que está ejecutando el host objetivo. Utiliza una combinación de técnicas como la inspección de la pila TCP/IP, entre otras, para hacer esta determinación.
			    
			1. **Detección de Versión**:
	    		    - El escaneo intenta determinar las versiones exactas de los servicios y aplicaciones que se ejecutan en los puertos abiertos del objetivo.
	    		    
			1. **Detección de Servicios**:
	    		    - Identifica los servicios que se están ejecutando en los puertos abiertos. Por ejemplo, si un puerto está abierto, Nmap intentará identificar si está ejecutando HTTP, FTP, SSH, etc.
	    		    
			1. **Scripts NSE (Nmap Scripting Engine)**:
	    		    - Ejecuta scripts predeterminados que pueden incluir la detección de vulnerabilidades conocidas, identificación de aplicaciones, y más. Estos scripts son parte del NSE y están diseñados para proporcionar información adicional sobre los servicios.
	    		    
			1. **Traza de Ruta (Traceroute)**:
	    		    - Realiza una traza de ruta para identificar el camino que toma el paquete para llegar al host objetivo. Esto puede ser útil para diagnosticar problemas de red y entender la topología de red.
	    		    
		```
		nmap -A 
		```
	- **Escaneo por fragmentacion:
			- *El comando `nmap -f` se utiliza para realizar un escaneo con **fragmentación de paquetes**, una técnica diseñada para evadir la detección por sistemas de detección de intrusos (IDS) y firewalls al dividir los paquetes de escaneo en fragmentos más pequeños.
		
		### Características del escaneo `-f`
		
		1. **Fragmentación de Paquetes**:
		    
		    - Al usar la opción `-f`, Nmap fragmenta los paquetes de escaneo en partes más pequeñas, generalmente de 8 bytes cada una.
		    - Esta técnica se basa en el hecho de que algunos IDS y firewalls tienen dificultades para reensamblar correctamente paquetes fragmentados, lo que puede permitir que el escaneo pase desapercibido.
		2. **Evasión de Detección**:
		    
		    - La fragmentación puede ayudar a evadir sistemas de seguridad que están configurados para detectar paquetes estándar de escaneo de red.
		    - Sin embargo, muchos IDS/IPS modernos están diseñados para detectar y manejar paquetes fragmentados, por lo que esta técnica puede no ser tan efectiva como en el pasado.
		3. **Impacto en el Rendimiento**:
		    
		    - Fragmentar los paquetes puede incrementar la carga de procesamiento en el sistema objetivo debido a la necesidad de reensamblar los fragmentos.
		    - Esto también puede hacer que el escaneo sea más lento y menos eficiente, especialmente si se utilizan redes con alta latencia.
		```
		nmap -f
		```
	- **Escaneo sin tener en cuenta si el host esta activo o no
		```
		nmap -PN "host"
		```
	- **Escaneo de host con puerto espesicifico:
		```
		- nmap -p "pueto" "host"
		- nmap -p  "rango de puetro" "hosto"
		```
	- **Escaneo rápido de puertos
		```
		nmap -F "host"
		```
	- **Escaneo  UDP:
			- *El comando `nmap -sU` se utiliza para realizar un escaneo de puertos **UDP** (User Datagram Protocol) en un host o una red específica. A diferencia de los escaneos TCP, los escaneos UDP son útiles para identificar servicios que funcionan sobre UDP, como DNS, SNMP, y DHCP.
		
		### Características del escaneo `-sU`
		
		1. **Escaneo de Puertos UDP**:
		    
		    - Envía paquetes UDP a los puertos objetivo para determinar su estado (abierto, cerrado o filtrado).
		    - Si un puerto está abierto, el servicio UDP correspondiente debería responder con datos relevantes.
		    - Si un puerto está cerrado, se espera recibir un paquete ICMP de "puerto inalcanzable".
		    - Si no se recibe respuesta, el puerto podría estar abierto, filtrado, o simplemente el servicio no respondió (lo cual es común en UDP).
		2. **Desafíos del Escaneo UDP**:
		    
		    - UDP es un protocolo sin conexión, lo que significa que no hay handshake para confirmar que un puerto está abierto.
		    - La falta de respuesta puede ser debido a un puerto filtrado, firewall, o simplemente a la naturaleza del protocolo UDP.
		3. **Detección de Servicios**:
		    
		    - Es utilizado para detectar servicios como DNS, SNMP, DHCP, TFTP, entre otros, que comúnmente usan puertos UDP.
		```
		nmap  -sU "host"
		```
	- **Escaneo SYN :
		- *El comando `nmap -sS` se utiliza para realizar un escaneo **SYN**, también conocido como **escaneo furtivo** o **escaneo medio abierto**, en un host o una red específica. Es uno de los tipos de escaneo más populares y eficientes que ofrece Nmap, ya que es rápido y más difícil de detectar por los sistemas de seguridad.
	
			### Características del escaneo `-sS`
			
			1. **Escaneo SYN**:
			    
			    - En lugar de establecer una conexión TCP completa, el escaneo SYN envía un paquete `SYN` al puerto objetivo y espera una respuesta.
			    - Si el puerto está abierto, el objetivo responde con un paquete `SYN-ACK`, y Nmap responde con un `RST` (reset) para no completar la conexión.
			    - Si el puerto está cerrado, el objetivo normalmente responderá con un paquete `RST`.
			2. **Eficiencia**:
			    
			    - Es más rápido que un escaneo de conexión completa (`-sT`) porque no necesita completar el establecimiento de una conexión.
			    - Al no completar la conexión, reduce la carga en el sistema objetivo.
			3. **Sigilo**:
			    
			    - Es menos probable que sea detectado por sistemas de detección de intrusos (IDS) o sistemas de prevención de intrusos (IPS), ya que no completa la conexión, lo que puede evitar la generación de registros de conexión.
			4. **Privilegios**:
			    
			    - Requiere privilegios de root (administrador) para enviar paquetes en bruto (raw packets), lo que lo hace más difícil de ejecutar sin los permisos adecuados.
		```
		nmap -sS "host"
		```
	- **Escaneo TCP :
		- *El comando `nmap -sT` realiza un escaneo de **conexión TCP completa**. Este es uno de los métodos de escaneo más básicos y confiables de Nmap, y se utiliza para identificar puertos abiertos en un host o una red.
	
			### Características del escaneo `-sT`
	
			1. **Conexión TCP Completa**:
	    
			    - El escaneo establece una conexión TCP completa con el puerto objetivo utilizando el proceso estándar de establecimiento de conexión TCP de tres vías (SYN, SYN-ACK, ACK).
			    - Es el equivalente a realizar una conexión `telnet` al puerto objetivo.
			2. **Identificación de Puertos Abiertos**:
	    
			    - Si el puerto está abierto, el objetivo responderá con un paquete `SYN-ACK`, y Nmap responderá con un `ACK` para completar la conexión.
			    - Si el puerto está cerrado, el objetivo normalmente responderá con un paquete `RST` (reset).
			3. **Facilidad de Uso**:
	    
			    - No requiere privilegios especiales, por lo que puede ser utilizado por usuarios no root. Esto es útil en entornos donde no se tienen privilegios administrativos.
			4. **Confiabilidad**:
	    
			    - Debido a que establece conexiones completas, proporciona resultados confiables sobre el estado de los puertos, a diferencia de algunos escaneos más sofisticados que pueden ser más fácilmente detectados o bloqueados por firewalls y sistemas de detección de intrusos.
		```
		nmap -sT "host"
		```
	- **Escaneo ACK:
		-*El comando `nmap -sA` se utiliza para realizar un escaneo de **ACK** (Acknowledgment) en una red o un host específico. Este tipo de escaneo está diseñado principalmente para determinar las reglas de filtrado de paquetes en cortafuegos (firewalls) y no para detectar puertos abiertos en el sentido tradicional.

		### Características del escaneo `-sA`

		1. **Detección de Cortafuegos**:
    
		    - El escaneo de ACK es útil para identificar si un cortafuegos está filtrando paquetes y si hay reglas de filtrado activas. No puede determinar si un puerto está abierto o cerrado, pero puede indicar si un paquete puede pasar a través del cortafuegos.
		2. **Comportamiento del Escaneo**:
    
		    - Envía paquetes TCP con el flag ACK activado. Este tipo de paquete se utiliza para verificar la respuesta de los sistemas intermedios, como los cortafuegos, en lugar de interactuar directamente con los servicios en los puertos del host.
		3. **Interpretación de Resultados**:
    
		    - Si un puerto es filtrado, es posible que no se reciba ninguna respuesta o que se reciba un paquete ICMP con el mensaje "puerto inalcanzable".
		    - Si el puerto está "unfiltered", se recibirá un paquete RST (reset), lo que indica que el paquete ACK ha llegado al destino sin ser bloqueado por el cortafuegos.
		```
		nmap -sA
		```
	- **Escaneo con formato verbose:
		```
		nmap -v "host"
		```
	- **Escaneo de puertos verificando versiones:
		```
		nmap -sV "host"
		```
	- **Escaneo con intensidad para ver las versiones de los servicios:
		- *Especifica cuán intensamente `nmap` debe intentar determinar la versión del servicio para los puertos abiertos. El nivel de intensidad puede variar de 0 a 9:
			- **0**: Escaneo de versión muy ligero, solo pruebas ligeras.
			- **1-4**: Aumenta gradualmente la cantidad de pruebas realizadas.
			- **5**: Nivel de intensidad por defecto, realiza un conjunto moderado de pruebas.
			- **6-8**: Más pruebas, incrementando en exhaustividad.
			- **9**: Escaneo de versión más exhaustivo, realiza todas las pruebas posibles.
		```
		nmap --version-intensity "host"
		```
	- **Escaneo de puertos con deteccion de SO:
		```
		nmap -O "host"
		```
	- **Escaneo realizando congeturas sobre el SO:
		```
		nmap --osscan-guess "host"
		```
	- **Escanero puerto con lista de scripts basicos:
		```
		nmap -sC "host"
		```
	- **Escaneo de puertos con velocidades
		- El comando `nmap -T<nivel>` se utiliza para establecer el nivel de velocidad o agresividad del escaneo. El `-T` (que significa "timing") seguido de un número del 0 al 5 controla el equilibrio entre la velocidad del escaneo y la cantidad de tráfico generado, así como la capacidad de evitar la detección en la red.

			- Descripción de los niveles de velocidad (`-T`)

				- **`-T0` (Paranoid)**:
    			    - **Uso**: Realiza el escaneo muy lentamente, con largos retrasos entre las sondas.
				    - **Propósito**: Diseñado para evitar la detección en redes donde los sistemas de seguridad pueden registrar múltiples intentos de escaneo.
				    - **Tiempo de escaneo**: Muy largo.
				- **`-T1` (Sneaky)**:
			        - **Uso**: Similar al modo paranoico, pero ligeramente más rápido.
				    - **Propósito**: Reduce la probabilidad de ser detectado por IDS/IPS.
				    - **Tiempo de escaneo**: Largo.
				- **`-T2` (Polite)**:
			        - **Uso**: Introduce retrasos más cortos que los niveles 0 y 1, pero sigue siendo cauteloso.
				    - **Propósito**: Minimiza el uso de ancho de banda y reduce el impacto en la red.
				    - **Tiempo de escaneo**: Moderado.
				- **`-T3` (Normal)**:
			        - **Uso**: Es el valor por defecto de `nmap`.
				    - **Propósito**: Ofrece un buen equilibrio entre la velocidad del escaneo y el uso de ancho de banda.
				    - **Tiempo de escaneo**: Razonable.
				- **`-T4` (Aggressive)**:
			        - **Uso**: Incrementa la velocidad y disminuye los retrasos entre sondas.
				    - **Propósito**: Útil para redes donde el escaneo rápido es una prioridad y la detección no es una preocupación.
				    - **Tiempo de escaneo**: Rápido.
				- **`-T5` (Insane)**:
			        - **Uso**: El nivel más rápido, con mínimas pausas entre sondas.
				    - **Propósito**: Diseñado para situaciones donde el tiempo es crítico y la detección no importa.
				    - **Tiempo de escaneo**: Muy rápido.
				    
		```
		nmap -t "velocidad del 1 al 5" "host"
		```
	- **Escaneo con tiempo maximo:
		- El comando `nmap --host-timeout` se utiliza para especificar un tiempo máximo que Nmap debe esperar para que un host responda antes de considerar que el escaneo ha fallado para ese host. Esta opción es útil para manejar situaciones donde los hosts en una red son lentos o están inactivos, y puedes ajustar el tiempo de espera para optimizar el escaneo.

			### Características del `--host-timeout`
			
			1. **Configuración de Tiempo de Espera**:
			    
			    - Permite definir el tiempo máximo que Nmap esperará para obtener una respuesta de un host antes de abandonarlo.
			    - Puedes ajustar el tiempo de espera para evitar largos retrasos en el escaneo si un host no responde rápidamente.
			2. **Formato del Tiempo**:
			    
			    - El tiempo se especifica en segundos, pero también puedes usar formatos más complejos como `m` para minutos, `h` para horas, o incluso combinaciones como `1h30m` para 1 hora y 30 minutos.
			3. **Optimización del Escaneo**:
			    
			    - Ajustar el tiempo de espera puede ayudar a evitar que el escaneo se quede colgado en hosts no responsivos, acelerando el proceso de escaneo en redes grandes o con hosts lentos.
			```
			nmap --host-timeout "tiempo" "host"
			```
		- **Escaneo con delay:
			- El comando `nmap --scan-delay` se utiliza para especificar un retraso entre el envío de paquetes durante un escaneo. Esta opción puede ser útil para reducir la carga en el objetivo y evitar la detección por sistemas de seguridad que podrían estar configurados para alertar sobre escaneos de red rápidos o intensivos.

			### Características de `--scan-delay`
			
			1. **Configuración de Retraso**:
			    
			    - Permite establecer un retraso específico entre el envío de cada paquete durante el escaneo. El retraso se especifica en segundos o fracciones de segundo (por ejemplo, `1s`, `500ms`).
			2. **Reducción de Carga en el Objetivo**:
			    
			    - Añadir un retraso puede ayudar a evitar la sobrecarga del sistema objetivo, especialmente en redes con alta densidad de tráfico o en sistemas que pueden detectar y bloquear escaneos rápidos.
			3. **Evasión de Sistemas de Detección**:
			    
			    - Al ralentizar el escaneo, puede ser más difícil para los sistemas de detección de intrusos (IDS) o firewalls identificar el tráfico de escaneo como una amenaza.
			4. **Prevención de Bloqueo**:
			    
			    - En redes donde los sistemas de seguridad pueden bloquear direcciones IP que realizan escaneos demasiado rápidos, añadir un retraso puede ayudar a evitar bloqueos.
			```
			nmap --scan-delay "tiempo" "host"
			```
	- **Guardado del escaneo en archivos
		```
		- nmap -oN "nombre del archivo .txt" "host"
		- nmap -oX "nombre del archivo .xml" "host"
		- nmap -oG "nombre del archivo grepeable" "host"
		```
	-  **Escaneo de puertos de cada equipo:
	 - Después de tener tu lista de host activos, lo siguiente que deberías hacer es un escaneo más exhaustivo, es decir listar los puertos abiertos con los que cuentan los host, así mismo como los servicios y versiones que están corriendo en ellos. No olvides ir guardando todos tus escaneos y datos relevantes encontrados. Ejemplos:
		```
		- nmap -p- --open -n -v -T5 10.10.14.16 -oN puertos
		- sudo nmap -sS --min-rate 200 -p- --open -n -v -Pn 10.10.14.16 -oN puertos
		- nmap -sV -sC -p21,22,80 10.10.14.16 -oN serviciosVersiones
		- nmap --script=vuln -p22,21,80,445 -v 10.10.14.16 -oN vulnScan
		- nmap --script=smb-vuln* -p445 -v 10.10.14.16 -oN smbScan
		```
	- **Escaneo camuflando paquetes:
		- El comando `nmap --data-length` se utiliza para especificar el tamaño del payload de los paquetes enviados durante un escaneo. Este parámetro permite ajustar la longitud de los datos que Nmap incluirá en los paquetes de escaneo, lo que puede ser útil para evadir sistemas de detección de intrusos (IDS) o para probar la respuesta de un objetivo a diferentes tamaños de paquetes.

		### Características del `--data-length`
		
		1. **Ajuste del Tamaño del Payload**:
		    
		    - Permite modificar el tamaño del payload en los paquetes enviados durante el escaneo. Puedes especificar un tamaño en bytes.
		    - Esto puede cambiar la forma en que los paquetes son procesados por los sistemas de seguridad y los servicios en el objetivo.
		2. **Evasión de Detección**:
		    
		    - Al cambiar el tamaño del payload, puedes hacer que el tráfico de escaneo sea menos predecible y potencialmente evadir algunos sistemas de detección que buscan patrones específicos en el tráfico de red.
		3. **Pruebas de Respuesta**:
		    
		    - Puede ser usado para probar cómo los sistemas responden a paquetes de diferentes tamaños, lo que puede ser útil para descubrir vulnerabilidades o debilidades en el manejo de paquetes.
		```
		nmap --data-length "valor"
		```
	- **Escaneo con direccion de origen enmascarada:
		- El comando `nmap -D` se utiliza para realizar un **escaneo de dirección de origen enmascarada** o **escaneo con dirección falsa**. Este método permite ocultar la dirección IP real del origen del escaneo al hacer que parezca que el tráfico proviene de varias direcciones IP diferentes. Esta técnica es útil para evadir sistemas de detección de intrusos (IDS) y firewalls que pueden estar configurados para alertar sobre el tráfico proveniente de una sola IP.

		### Características del escaneo `-D`
		
		1. **Enmascaramiento de IP**:
		       - La opción `-D` permite especificar una serie de direcciones IP falsas que Nmap utilizará para enmascarar el origen real del escaneo. Esto hace que el tráfico de escaneo parezca provenir de múltiples fuentes, complicando la identificación del origen real.
		2. **Aumenta la Privacidad**:
		       - Ayuda a proteger la identidad del origen del escaneo al hacer que sea más difícil para los administradores de red rastrear el escaneo hasta su origen.
		3. **Evasión de Detección**:
		       - Al distribuir el tráfico de escaneo entre varias direcciones IP, se reduce la posibilidad de que un IDS/IPS detecte el escaneo como una amenaza proveniente de una sola fuente.
		```
		nmap -D
		```
	- **Escaneo con puerto fuente:
		- El comando `nmap -g` se utiliza para especificar un puerto **SYN** o **ACK** para ser utilizado en el escaneo, conocido como **escaneo con puerto fuente**. Esta opción permite establecer el puerto de origen en los paquetes enviados por Nmap, lo cual puede ser útil para evadir algunas técnicas de detección de seguridad.

		### Características del escaneo `-g`
		
		1. **Puerto de Origen**:
		    
		    - La opción `-g` permite especificar un puerto de origen en los paquetes TCP enviados durante el escaneo. Puedes utilizar un puerto específico para que Nmap envíe paquetes desde ese puerto en lugar del puerto predeterminado.
		2. **Evasión de Detección**:
		    
		    - Al cambiar el puerto de origen, puedes eludir algunas reglas de firewall o IDS que podrían estar configuradas para detectar tráfico proveniente de puertos específicos.
		    - Esto también puede ayudar a evadir sistemas que están configurados para monitorizar y bloquear ciertos puertos de origen.
		3. **Formatos de Uso**:
		    
		    - El puerto especificado se usa para el tráfico de salida de Nmap. Sin embargo, es importante entender que esta opción es más relevante para el tráfico TCP que para UDP.
		```
		nmap -g "puerto"
		```
- ## Nmap Scripting Engine (NSE)
	- **Comando para solicitar ayuda sobre los scrips:
		```
		nmap --script-help="script"
		```
	- **Script para ver informacion de mongo database:
	
		```
			nmap --script=mongodb-info "host"
		```
	- **Script para conseguir banners de servicio:**
		- El script `banner` de Nmap es utilizado para obtener banners de servicios en ejecución en puertos abiertos en los sistemas remotos. Los "banners" son información que los servicios proporcionan al conectarse, como por ejemplo, el tipo de servidor y la versión de software que están utilizando.
		- ### Funcionamiento del script `banner`

			-El script intenta realizar una conexión simple a un puerto abierto y recibe la información que el servicio remoto envía al conectarse. Es común que servicios como servidores web, SSH, FTP, entre otros, envíen banners cuando un cliente se conecta, y esta información puede incluir detalles sobre el software, su versión, y a veces incluso configuraciones específicas.
			```
			nmap --script banner <dirección_ip>
			```
	- **SMB**
		- **Scrip para identificar protocolos SMB:
			- El comando `nmap --script smb-protocols` utiliza el **Nmap Scripting Engine (NSE)** para ejecutar el script `smb-protocols`, que se especializa en identificar los protocolos SMB (Server Message Block) soportados por un host. SMB es un protocolo de red utilizado para el acceso compartido a archivos, impresoras y otros recursos en redes Windows.
	
			### Características del Script `smb-protocols`
			
			1. **Identificación de Protocolos SMB**:
			    
			    - El script `smb-protocols` detecta las versiones de SMB soportadas por el host objetivo. Esto incluye versiones de SMB como SMBv1, SMBv2 y SMBv3.
			    - Proporciona información sobre los protocolos SMB habilitados y sus capacidades, lo cual es útil para evaluar la seguridad y configuración de servicios SMB.
			2. **Verificación de Configuración de Seguridad**:
			    
			    - Detectar qué versiones de SMB están habilitadas puede ser crucial para identificar posibles vulnerabilidades. Por ejemplo, SMBv1 tiene una serie de vulnerabilidades conocidas que han sido explotadas en ataques como WannaCry.
			3. **Uso de Nmap Scripting Engine (NSE)**:
			    
			    - Este script es parte de la biblioteca de scripts de NSE de Nmap, que permite la ejecución de scripts adicionales para realizar tareas específicas de auditoría y detección.
			```
			nmap --script smb-protocol
			```
		- **Scrip para identificar modo de seguridad en SMB:
			- El comando `nmap --script smb-security-mode` utiliza el **Nmap Scripting Engine (NSE)** para ejecutar el script `smb-security-mode`, el cual está diseñado para recopilar información sobre el modo de seguridad y las configuraciones de seguridad de los servicios SMB (Server Message Block) en un host objetivo.
		
				### Características del Script `smb-security-mode`
				
				1. **Detección de Modos de Seguridad SMB**:
				    
				    - El script `smb-security-mode` identifica los modos de seguridad configurados en el servicio SMB del host. Esto incluye detalles como si el servicio está usando autenticación segura y qué protocolos de cifrado están habilitados.
				2. **Información sobre Seguridad de SMB**:
				    
				    - Proporciona detalles sobre configuraciones de seguridad específicas como el uso de firmas SMB y cifrado de comunicaciones. Esto es importante para evaluar la protección contra ataques y vulnerabilidades comunes en SMB.
				3. **Identificación de Políticas de Seguridad**:
				    
				    - El script puede informar sobre políticas de seguridad como el uso de NTLM (NT LAN Manager) y si se han aplicado configuraciones de seguridad recomendadas.
				```
				nmap --script smb-security-mode "host"
				```
		- **Script para enumerar sessiones SMB:
			- El comando `nmap --script smb-enum-sessions` utiliza el **Nmap Scripting Engine (NSE)** para ejecutar el script `smb-enum-sessions`. Este script está diseñado para enumerar las sesiones SMB activas en un servidor de Windows que ejecuta el servicio SMB. Proporciona información sobre los usuarios conectados y sus sesiones activas, lo cual es útil para la administración y auditoría de redes.
		
				### Características del Script `smb-enum-sessions`
				
				1. **Enumeración de Sesiones SMB**:
				    
				    - El script intenta enumerar todas las sesiones SMB activas en el servidor de destino. Esto incluye detalles sobre las conexiones activas de los usuarios, tales como nombres de usuario, nombres de máquina y la dirección IP desde la cual están conectados.
				2. **Identificación de Usuarios Conectados**:
				    
				    - Proporciona información sobre los usuarios que actualmente tienen sesiones abiertas en el servidor, lo cual es útil para verificar quién está utilizando recursos compartidos en un momento dado.
				3. **Uso en Auditorías de Seguridad**:
				    
				    - Este script puede ser utilizado en auditorías de seguridad para identificar accesos no autorizados o anómalos a los recursos compartidos de red.
				```
				nmap --script smb-enum-sessions "host"
				nmap --script smb-enum-sessions --scripts-args smbusername= "usuario smb",smbpassword="password smb" "host"
				```
		- **Script para enumerar recursos compartidos por SMB:
			- El comando `nmap --script smb-enum-shares` utiliza el **Nmap Scripting Engine (NSE)** para ejecutar el script `smb-enum-shares`, que está diseñado para enumerar los recursos compartidos (shares) SMB (Server Message Block) en un servidor de Windows o cualquier otro sistema que soporte SMB. Este script es útil para identificar y auditar los recursos de red que se están compartiendo en un host.
		
				### Características del Script `smb-enum-shares`
				
				1. **Enumeración de Recursos Compartidos**:
				    
				    - El script `smb-enum-shares` identifica todos los recursos compartidos disponibles en el servidor SMB de destino, tanto públicos como privados.
				    - Proporciona detalles sobre cada recurso compartido, como su nombre, tipo, y a veces, los permisos asociados.
				2. **Detección de Permisos de Acceso**:
				    
				    - Aunque no siempre puede mostrar los permisos de acceso detallados, el script puede indicar si un recurso compartido es de solo lectura o si se requiere autenticación para acceder.
				3. **Identificación de Recursos Sensibles**:
				    
				    - Ayuda a identificar recursos compartidos que podrían contener información sensible o que estén expuestos indebidamente en la red.
				```
				nmap --script smb-enum-shares "host"
				nmap --script smb-enum-shares --scripts-args smbusername= "usuario smb",smbpassword="password smb" "host"		
				nmap --script smb-enum-shares,smb-ls --scripts-args smbusername= "usuario smb",smbpassword="password smb" "host"			
				```
		- **Script para enumerar usuarios en SMB:**
			-El comando `nmap --script smb-enum-users` utiliza el **Nmap Scripting Engine (NSE)** para ejecutar el script `smb-enum-users`, que está diseñado para enumerar los usuarios de un servidor SMB (Server Message Block). Este script es especialmente útil para identificar los usuarios que están configurados en un servidor Windows o en cualquier sistema que soporte SMB, proporcionando información valiosa para la administración y auditoría de redes.

			### Características del Script `smb-enum-users`
			
			1. **Enumeración de Usuarios SMB**:
			    
			    - El script `smb-enum-users` intenta listar todos los usuarios que tienen cuentas en el servidor SMB objetivo.
			    - Puede proporcionar detalles sobre cada usuario, como el nombre de usuario, el nombre completo, y a veces, información adicional sobre la cuenta.
			2. **Identificación de Cuentas de Usuario**:
			    
			    - Ayuda a identificar qué cuentas de usuario están activas en el servidor, lo cual es útil para verificar la presencia de cuentas sospechosas o no autorizadas.
			3. **Uso en Auditorías de Seguridad**:
			    
			    - Este script es útil para auditar la seguridad de un servidor al identificar cuentas de usuario que podrían no estar protegidas adecuadamente o que pueden representar un riesgo de seguridad.
			```
			nmap --script smb-enum-users "host"
			nmap --script smb-enum-users --scripts-args smbusername= "usuario smb",smbpassword="password smb" "host"	
			```
		- **Script para obtener estadisticas de servidor SMB:
			- El comando `nmap --script smb-server-stats` utiliza el **Nmap Scripting Engine (NSE)** para ejecutar el script `smb-server-stats`, que está diseñado para obtener estadísticas del servidor SMB (Server Message Block) de un host. Este script proporciona información sobre el rendimiento y la carga del servidor SMB, lo que puede ser útil para la administración y monitoreo de redes.

			### Características del Script `smb-server-stats`
			
			1. **Obtención de Estadísticas del Servidor SMB**:
			    
			    - El script `smb-server-stats` recopila estadísticas de rendimiento del servidor SMB, tales como el número de bytes transferidos, la cantidad de archivos abiertos, y el número de sesiones activas.
			    - Puede proporcionar detalles sobre la utilización de recursos y el tráfico de red gestionado por el servidor SMB.
			2. **Monitoreo de Rendimiento**:
			    
			    - Ayuda a los administradores de red a monitorear el rendimiento del servidor SMB y a identificar posibles cuellos de botella o problemas de rendimiento.
			3. **Auditoría de Uso de Recursos**:
			    
			    - Permite auditar el uso de recursos del servidor SMB, proporcionando una visión clara de cómo se están utilizando los recursos compartidos en la red.
			```
			nmap --script smb-server-stats  --scripts-args smbusername= "usuario smb",smbpassword="password smb" "host"	
			```
		- **Script para enumerar dominio en SMB:
			- El comando `nmap --script smb-enum-domains` utiliza el **Nmap Scripting Engine (NSE)** para ejecutar el script `smb-enum-domains`. Este script está diseñado para enumerar los dominios disponibles en un servidor SMB (Server Message Block) o en un controlador de dominio. Es particularmente útil en entornos de red donde se utilizan dominios de Active Directory para la gestión de usuarios y recursos.

			### Características del Script `smb-enum-domains`
			
			1. **Enumeración de Dominios**:
			    
			    - El script `smb-enum-domains` intenta listar todos los dominios disponibles en el servidor SMB de destino.
			    - Puede identificar dominios principales y de confianza asociados con el servidor, proporcionando una visión general de la estructura de dominio de la red.
			2. **Detección de Controladores de Dominio**:
			    
			    - Ayuda a identificar controladores de dominio y su relación con otros dominios en la red, lo cual es útil para mapear la jerarquía de dominio y las relaciones de confianza.
			3. **Auditorías de Seguridad**:
			    
			    - Este script puede ser utilizado en auditorías de seguridad para revisar la configuración de dominios y asegurar que no haya dominios no autorizados o configuraciones de confianza inseguras.
			```
			nmap --script smb-enum-domains  --scripts-args smbusername= "usuario smb",smbpassword="password smb" "host"	
			```
		- **Script para enumerar grupos en SMB:
			- Parece que hay un error tipográfico en el comando. El script correcto que podrías estar buscando es `smb-enum-groups`, no `smb-enum-gropus`. El comando `nmap --script smb-enum-groups` utiliza el **Nmap Scripting Engine (NSE)** para ejecutar el script `smb-enum-groups`, que está diseñado para enumerar los grupos de usuarios en un servidor SMB (Server Message Block). Este script es útil para obtener información sobre la organización de grupos dentro de un servidor Windows o cualquier sistema que soporte SMB, proporcionando detalles valiosos para la administración y auditoría de redes.

			### Características del Script `smb-enum-groups`
			
			1. **Enumeración de Grupos SMB**:
			    
			    - El script `smb-enum-groups` intenta listar todos los grupos que están configurados en el servidor SMB de destino.
			    - Puede proporcionar detalles sobre cada grupo, incluyendo el nombre del grupo y, en algunos casos, los miembros del grupo.
			2. **Identificación de Grupos y Miembros**:
			    
			    - Ayuda a identificar los grupos de usuarios en el servidor, lo cual es útil para verificar la organización de permisos y accesos en el entorno de red.
			3. **Uso en Auditorías de Seguridad**:
			    
			    - Este script puede ser utilizado para auditar la configuración de grupos en un servidor, asegurándose de que los permisos y accesos estén configurados de acuerdo a las políticas de seguridad.
			```
			nmap --script smb-enum-groups  --scripts-args smbusername= "usuario smb",smbpassword="password smb" "host"	
			```
		- **Script para enumerar servicios en un servidor SMB:
			- El comando `nmap --script smb-enum-services` utiliza el **Nmap Scripting Engine (NSE)** para ejecutar el script `smb-enum-services`. Este script está diseñado para enumerar los servicios de Windows que están instalados en un servidor SMB (Server Message Block). Esta información puede ser útil para la administración y auditoría de redes, proporcionando detalles sobre los servicios que se ejecutan en un servidor Windows.

			### Características del Script `smb-enum-services`
			
			1. **Enumeración de Servicios de Windows**:
			    
			    - El script `smb-enum-services` intenta listar todos los servicios que están instalados y posiblemente en ejecución en el servidor SMB de destino.
			    - Puede proporcionar detalles sobre cada servicio, como el nombre del servicio, su descripción, el estado (iniciado o detenido), y el tipo de inicio (automático, manual, deshabilitado).
			2. **Identificación de Servicios Activos**:
			    
			    - Ayuda a identificar qué servicios están activos en el servidor, lo cual es útil para verificar la configuración y detectar posibles servicios no autorizados o inseguros.
			3. **Uso en Auditorías de Seguridad**:
			    
			    - Este script puede ser utilizado en auditorías de seguridad para revisar los servicios que están configurados en un servidor, asegurando que no existan servicios innecesarios o vulnerables.
			```
			nmap --script smb-enum-services  --scripts-args smbusername= "usuario smb",smbpassword="password smb" "host"	
			```
		- **Script para descubrir so en servidor SMB:
			- El comando `nmap --script smb-os-discovery` utiliza el **Nmap Scripting Engine (NSE)** para ejecutar el script `smb-os-discovery`. Este script está diseñado para identificar el sistema operativo de un host remoto a través del protocolo SMB (Server Message Block). Es una herramienta útil para obtener información sobre los sistemas operativos en una red y puede ser utilizada para tareas de administración y auditoría de seguridad.

			### Características del Script `smb-os-discovery`
			
			1. **Identificación del Sistema Operativo**:
			    
			    - El script intenta determinar el sistema operativo del host remoto utilizando información disponible a través del protocolo SMB.
			    - Puede identificar detalles como la versión exacta del sistema operativo, el nombre del servidor y el dominio al que pertenece.
			2. **Recopilación de Información del Sistema**:
			    
			    - Además del sistema operativo, el script puede obtener detalles sobre la arquitectura del sistema (por ejemplo, 32 bits o 64 bits) y otra información relevante para la gestión de la red.
			3. **Detección de Versiones de SMB**:
			    
			    - El script puede ayudar a identificar la versión de SMB que el servidor está utilizando, lo cual es útil para detectar configuraciones potencialmente vulnerables.
			```
			nmap --script smb-os-discovery
			```
		- **Scrip para detectar el "pulsar backdoor":**
			- El script `smb-vuln-pulsar-backdoor.nse` de Nmap está diseñado para detectar la presencia de la **"Pulsar backdoor"** en sistemas Windows que exponen servicios SMB (Server Message Block). Esta backdoor es una variante del malware creado por el grupo Shadow Brokers que afecta a sistemas Windows, y fue utilizada por el exploit **EternalBlue**, que es conocido por haber propagado los ataques de ransomware WannaCry y NotPetya.

			- ### ¿Qué es la Pulsar Backdoor?

				- La Pulsar Backdoor es un malware que se instala en sistemas Windows explotando vulnerabilidades en SMB. Una vez instalada, la backdoor permite a los atacantes ejecutar comandos remotos y obtener acceso no autorizado al sistema infectado. Esta backdoor es particularmente peligrosa porque permite control total del sistema afectado y puede ser utilizada para realizar actividades maliciosas como la extracción de datos, la instalación de otros malware o la creación de redes de
			- ### Funcionamiento del Script `smb-vuln-pulsar-backdoor.nse`
				1. **Exploración de Puertos SMB:** El script se dirige a puertos comunes para SMB (por defecto 445/tcp) en el sistema objetivo.
				2. **Interacción con el Servicio SMB:** El script envía un paquete específico al servicio SMB del objetivo que es característico de la Pulsar Backdoor. Este paquete simula la comunicación que un atacante usaría para interactuar con la backdoor.
				3. **Detección de Respuesta:** Si el sistema objetivo responde de manera específica, el script determina que la Pulsar Backdoor está presente en el sistema.
				4. **Generación de Informe:** El script informa si se detecta la backdoor, lo que sugiere que el sistema está comprometido y puede estar controlado remotamente por atacantes.
				```
				nmap --script smb-vuln-pulsar-backdoor -p 445 <dirección_ip>
			
				```
		- **Script para chequear vulnerabilidad ms17-010**
			- El script **`smb-vuln-ms17-010`** es un script para **Nmap** que verifica si un sistema es vulnerable a la vulnerabilidad conocida como **MS17-010**, también llamada **EternalBlue**. Esta vulnerabilidad afecta al protocolo SMBv1 (Server Message Block) en varias versiones de Windows, permitiendo a los atacantes ejecutar código de forma remota sin autenticación en sistemas vulnerables.
				- ### Contexto de MS17-010 (EternalBlue):
					
					- **MS17-010** es el código asignado por Microsoft al parche que soluciona una vulnerabilidad crítica en el protocolo SMBv1. EternalBlue fue explotada en ataques de gran envergadura, como el ransomware **WannaCry** en 2017.
					- **EternalBlue** permite a un atacante aprovechar un desbordamiento de buffer en el servicio SMBv1, permitiendo la ejecución remota de código malicioso con privilegios elevados.
					- Esta vulnerabilidad afecta a versiones antiguas de Windows, incluyendo Windows XP, Windows 7 y Windows Server 2003 y 2008, entre otras.

				- ### Función del Script `smb-vuln-ms17-010`:

					- Este script de **Nmap** está diseñado para verificar si un sistema es vulnerable a EternalBlue sin explotar activamente la vulnerabilidad. Utiliza la funcionalidad de SMB para enviar un conjunto específico de mensajes que permiten deducir si el sistema está parcheado o no.

				- ### Cómo funciona el script:
					
					1. **Envía solicitudes SMB**: El script interactúa con el servicio SMB del objetivo enviando paquetes diseñados para detectar la presencia de EternalBlue.
					    
					2. **Analiza las respuestas**: Basado en la respuesta que el servidor SMB devuelve, el script intenta identificar si el sistema está vulnerable a MS17-010. Las características de las respuestas varían dependiendo de si el sistema está parcheado o no.
					    
					3. **Resultado**:
					    
					    - **Vulnerable**: Si el sistema está afectado por la vulnerabilidad, el script reportará que el sistema es vulnerable a EternalBlue.
					    - **No vulnerable**: Si el sistema ha sido parcheado o no es susceptible, el script indicará que no se ha detectado la vulnerabilidad.
					    - **Inconcluso**: En algunos casos, el resultado podría no ser concluyente si el sistema no responde de forma clara.
					```
					nmap --script smb-vuln-ms17-010 -p445 <IP_o_rango_de_IPs>
					```
	- **FTP:**
		- **Script de fuerza bruta para ftp:
			- El comando `nmap --script ftp-brute` utiliza Nmap para ejecutar un script de fuerza bruta contra un servidor FTP para intentar obtener credenciales válidas. El script `ftp-brute` forma parte del **Nmap Scripting Engine (NSE)**, que permite a Nmap utilizar scripts para realizar una variedad de tareas más allá del escaneo básico de puertos.
				- ### Caracteristicas del script:
					1. **Ataques de Fuerza Bruta**: El script `ftp-brute` intenta adivinar las contraseñas para las cuentas de usuario en un servidor FTP. Utiliza listas de contraseñas comunes para probar en combinación con nombres de usuario válidos en el servidor FTP.
    				2. **Recolección de Información**: Antes de realizar el ataque, el script puede realizar una enumeración básica para identificar usuarios válidos en el servidor FTP, si se han especificado o si se pueden inferir de la configuración del servidor.
			```
			nmap --script ftp-brute -p 21 <target_ip>
			```
		- **Script para loguear como anonymous:
			- El comando `nmap --script ftp-anon -p 21 <target_ip>` utiliza Nmap para ejecutar el script `ftp-anon` en un servidor FTP. Este script verifica si el servidor FTP permite el acceso anónimo, es decir, si los usuarios pueden conectarse al servidor FTP sin proporcionar credenciales válidas.
			### Características del Script `ftp-anon`
			1. **Verificación de Acceso Anónimo**: El script `ftp-anon` comprueba si el servidor FTP permite el acceso anónimo. El acceso anónimo es una configuración que permite a los usuarios conectarse al servidor FTP con el nombre de usuario `anonymous` (o a veces `ftp`) y una contraseña arbitraria (a menudo el correo electrónico del usuario) sin necesidad de credenciales especiales.
		    2. **Recolección de Información**: Si el acceso anónimo está permitido, el script también puede proporcionar información sobre los archivos y directorios disponibles para los usuarios anónimos, como el listado de directorios y archivos accesibles.
			```
			nmap --script ftp-anon
			
			```
	- **SSH:**
		-  **Script para enumerar :**
			- El comando `nmap --script ssh2-enum-algos` utiliza Nmap con el script `ssh2-enum-algos` para enumerar los algoritmos soportados en el protocolo SSH (Secure Shell) en un servidor remoto. Este script es parte de los Nmap Scripting Engine (NSE) y está diseñado para ayudar a los administradores de sistemas y a los evaluadores de seguridad a identificar las versiones de algoritmos criptográficos utilizados por un servidor SSH.
			### Características del Script `ssh2-enum-algos`
			1. **Enumeración de Algoritmos**: El script `ssh2-enum-algos` realiza una consulta a un servidor SSH para determinar qué algoritmos soporta en diferentes categorías, como algoritmos de cifrado, firmas, intercambios de claves y métodos de autenticación.
			2. **Recolección de Información**: Proporciona una lista detallada de los algoritmos que el servidor SSH acepta, lo que puede ser útil para identificar configuraciones seguras o vulnerables y para verificar la compatibilidad con ciertas versiones de protocolos.
			```
			nmap --script ssh2-enum-algos
			```
		- **Script para obtener clave publica SSH:**
			- El comando `nmap --script ssh-hostkey` utiliza Nmap con el script `ssh-hostkey` para obtener y mostrar las claves públicas del host SSH de un servidor. Este script forma parte del Nmap Scripting Engine (NSE) y se utiliza para recolectar información sobre las claves SSH del servidor, que son fundamentales para la autenticación y la seguridad del servicio SSH.
			### Características del Script `ssh-hostkey`
			
			1. **Obtención de Claves SSH del Host**: El script se conecta al servidor SSH y recupera las claves públicas que el servidor utiliza para la autenticación. Estas claves son utilizadas por el cliente SSH para verificar la identidad del servidor durante el proceso de conexión.
			2. **Mostrar Información sobre Claves**: El script muestra las claves públicas del servidor en formatos legibles, como RSA, DSA, ECDSA y Ed25519. Esto ayuda a verificar la autenticidad del servidor y a comparar las claves con las esperadas para asegurar que no haya cambios no autorizados.
			```
			nmap --script ssh-hostkey --script-args ssh_hostkey=full
			```
		- **Script para enumerar metodos de autenticacion soportados por ssh:**
			- El comando `nmap --script ssh-auth-methods` utiliza Nmap con el script `ssh-auth-methods` para enumerar y mostrar los métodos de autenticación soportados por un servidor SSH. Este script es parte del Nmap Scripting Engine (NSE) y proporciona información sobre las diferentes formas en que los usuarios pueden autenticar en el servidor SSH.
			### Características del Script `ssh-auth-methods`
			1. **Enumeración de Métodos de Autenticación**: El script realiza una conexión con el servidor SSH y determina qué métodos de autenticación son aceptados por el servidor. Esto incluye métodos como contraseña, autenticación basada en claves públicas, y otros métodos soportados.
		    2.  **Mostrar Información**: El script muestra una lista de métodos de autenticación soportados, proporcionando una visión de cómo el servidor permite que los usuarios se autentiquen. Esta información es útil para evaluar la configuración de seguridad y la accesibilidad del servidor.
			```
		    nmap --script ssh-auth-methods --script-args="ssh.user=" 
			```
		- **Script de fuerza bruta para ssh:
			- El comando `nmap --script ssh-brute` se utiliza con Nmap para realizar un ataque de fuerza bruta contra el servicio SSH en un servidor remoto. Este script forma parte del Nmap Scripting Engine (NSE) y su objetivo es intentar descubrir credenciales válidas (combinaciones de usuario y contraseña) para acceder al servidor mediante SSH.
			### Características del Script `ssh-brute`
			-  **Ataque de Fuerza Bruta**: `ssh-brute` intenta una serie de combinaciones de nombre de usuario y contraseña para ver si alguna de ellas permite el acceso al servidor SSH. Utiliza listas predefinidas o personalizadas de usuarios y contraseñas para realizar estos intentos.
		    - **Recolección de Credenciales**: Si el script encuentra una combinación válida de usuario y contraseña, lo reporta en la salida de Nmap, proporcionando al usuario la posibilidad de acceder al servidor.
			```
			 nmap --script ssh-brute
			```
	- **HTTP:**
		- **Scrip para enumerar en HTTP:**
			- El comando `nmap --script http-enum` se utiliza para identificar y enumerar recursos comunes y potencialmente sensibles en un servidor web. Este comando emplea el script `http-enum` de Nmap, que escanea un servidor web en busca de archivos y directorios comunes, como paneles de administración, archivos de configuración, sistemas de gestión de contenido (CMS), y otros recursos que pueden estar presentes en un servidor web pero que no son visibles a simple vista.
				- ### Qué Hace el Script `http-enum`?

					- El script `http-enum` realiza una serie de solicitudes HTTP a un servidor web, buscando patrones de archivos y directorios predefinidos en una base de datos interna. Luego, el script informa sobre cualquier recurso encontrado, proporcionando una lista de URLs que podrían ser interesantes para un auditor de seguridad o un pentester.
					```
					nmap --script http-enum -p 80 <target>
					```
		- **Script para enumarar las cabeceras HTTP:**
			- El comando `nmap --script http-headers` se utiliza para escanear y obtener los encabezados HTTP de un servidor web. Nmap es una herramienta de red poderosa y versátil que, entre otras cosas, permite realizar este tipo de análisis para descubrir información sobre la configuración de un servidor web.
			
				- ### Funcionamiento del script `http-headers`

					1. **Solicitud HTTP**: El script envía una solicitud HTTP `GET` al servidor web objetivo.
					2. **Respuesta HTTP**: El servidor web responde con un conjunto de cabeceras HTTP, que pueden incluir información como el tipo de servidor (`Server`), la política de caché (`Cache-Control`), el tipo de contenido (`Content-Type`), y otras directivas relacionadas con la seguridad o el manejo de la solicitud.
					3. **Extracción y Visualización**: El script extrae estas cabeceras de la respuesta y las muestra al usuario en el resultado del escaneo.
					
					```
					nmap --script http-headers "host"
					```
		- **Script para enumerar los metodos que puede utilizar el servidor http:**
			- El script `http-methods` de Nmap es una herramienta que te permite identificar los métodos HTTP que están habilitados en un servidor web. Los métodos HTTP son las acciones que se pueden realizar en un recurso web, como `GET`, `POST`, `PUT`, `DELETE`, entre otros.
				- ### ¿Qué hace el script?

					- El script `http-methods` envía una solicitud HTTP al servidor y analiza la respuesta para determinar qué métodos HTTP son aceptados. Esto puede ser útil para detectar configuraciones inseguras o no deseadas, como la habilitación de métodos peligrosos (por ejemplo, `DELETE`, `PUT`), que podrían permitir a un atacante modificar o eliminar recursos en el servidor.
					```
					nmap --script http-methods "host"
					```
		- **Script para detectar Webdav:**
			- El script `http-webdav-scan` de Nmap se utiliza para detectar servidores web que tienen habilitado WebDAV (Web Distributed Authoring and Versioning). WebDAV es una extensión del protocolo HTTP que permite a los usuarios crear, mover, copiar, y eliminar archivos en un servidor web remoto.

				- ### Funcionalidad del Script

					- El script `http-webdav-scan` escanea un servidor web para identificar si WebDAV está habilitado y, si es posible, lista los métodos HTTP que el servidor acepta, incluyendo los métodos extendidos de WebDAV como `PROPFIND`, `COPY`, `MOVE`, `LOCK`, `UNLOCK`, etc.
				- ### Cómo Funciona
					
					1. **Enviar una Petición HTTP:** El script envía una petición HTTP `OPTIONS` al servidor objetivo. El método `OPTIONS` solicita al servidor una lista de métodos HTTP soportados.
					    
					2. **Verificación de WebDAV:** Si el servidor responde con alguno de los métodos específicos de WebDAV, como `PROPFIND` o `MKCOL`, se confirma que WebDAV está habilitado en el servidor.
					    
					3. **Salida de Resultados:** Si WebDAV está habilitado, el script muestra en la salida de Nmap qué métodos están soportados por el servidor, lo que puede indicar el nivel de riesgo o permitir a los administradores de sistemas tomar las medidas adecuadas.
				- ### ¿Por Qué es Importante?

					- WebDAV puede representar un riesgo de seguridad si está habilitado en servidores públicos sin la configuración y las protecciones adecuadas. Por ejemplo, un servidor mal configurado podría permitir a los usuarios no autenticados modificar o eliminar archivos.
				```
				nmap --script http-webdav-scan -p 80 <objetivo>
				```
		- **Scrip para detectar shellshock**
			- El script de Nmap `http-shellshock` está diseñado para detectar vulnerabilidades de "Shellshock" (también conocidas como "Bash Bug") en servidores web que ejecutan scripts CGI en el sistema afectado. "Shellshock" es una vulnerabilidad en el shell Bash que permite a un atacante ejecutar comandos arbitrarios si este no maneja adecuadamente el procesamiento de variables de entorno.
				- ### ¿Cómo funciona el script `http-shellshock`?

					- El script `http-shellshock` de Nmap explota la vulnerabilidad enviando una solicitud HTTP maliciosa que contiene un payload diseñado para activar el error en Bash cuando el servidor vulnerable evalúa la variable de entorno. Si el servidor es vulnerable, ejecutará los comandos incluidos en el payload y el script detectará la ejecución del comando.
					 1. **Payload del ataque:**

						- El payload típico para la vulnerabilidad de Shellshock incluye código entre paréntesis que el servidor vulnerable ejecuta al procesar ciertas cabeceras HTTP (como `User-Agent`, `Referer`, etc.), o bien al manejar scripts CGI.
							
							Un ejemplo de payload es algo como:
							`() { :; }; echo vulnerable`
							Si el servidor es vulnerable, esta línea de código hará que se ejecute el comando `echo vulnerable` en el sistema.
					
					 2. **Escaneo con Nmap**:
					
						- El script `http-shellshock` de Nmap genera este tipo de payload y lo inserta en las cabeceras HTTP de la solicitud hacia el servidor. Luego, observa si hay una respuesta que indique que el comando enviado fue ejecutado. Si el servidor ejecuta el comando y devuelve la salida, el script informa que el objetivo es vulnerable.
					
					3. **Uso del script**:
						
						- Para ejecutar el script, puedes usar el siguiente comando en Nmap:
						
						- `nmap --script http-shellshock --script-args uri=/cgi-bin/vulnerable_script -p 80,443 <target>`
						- `--script http-shellshock`: Especifica el script que se debe utilizar.
						- `--script-args uri=/cgi-bin/vulnerable_script`: Indica la ruta del script CGI que podría estar expuesto a Shellshock.
						- `-p 80,443`: Puertos a escanear (80 y 443 son los puertos más comunes para HTTP/HTTPS).
						- `<target>`: La dirección IP o el dominio del servidor objetivo.
					
					4. **Detección de vulnerabilidad**:
					
						- Si el servidor es vulnerable, el script indicará que la vulnerabilidad ha sido detectada. De lo contrario, no se recibirá ninguna respuesta que sugiera ejecución de comandos.
		- **Script para detectar log4shell:**
			- El script `log4shell.nse` de Nmap está diseñado para detectar la vulnerabilidad conocida como Log4Shell (CVE-2021-44228) en aplicaciones que utilizan la biblioteca de registro Apache Log4j. Esta vulnerabilidad, descubierta a finales de 2021, permite a un atacante ejecutar código remoto en servidores vulnerables, lo que puede tener consecuencias graves como la toma de control del servidor.
			- ### ¿Qué es Log4Shell?

				- Log4Shell es una vulnerabilidad crítica que afecta a Log4j, una biblioteca ampliamente utilizada para el registro de eventos en aplicaciones Java. La vulnerabilidad reside en la forma en que Log4j maneja ciertas entradas de usuario. Si un atacante logra inyectar una cadena maliciosa en un registro que es procesado por Log4j, puede hacer que el servidor descargue y ejecute código malicioso desde un servidor remoto controlado por el atacante.
			- ### Funcionamiento del Script `log4shell.nse`
				- El script `log4shell.nse` de Nmap intenta detectar si un servidor es vulnerable a Log4Shell mediante la inyección de una carga útil (payload) especialmente diseñada en las cabeceras HTTP. Aquí está el proceso básico:
					1. **Inyección de la Carga Útil:** El script envía una solicitud HTTP al servidor objetivo, inyectando una cadena maliciosa en varias cabeceras HTTP (como `User-Agent`, `X-Forwarded-For`, entre otras). Esta cadena está diseñada para activar la vulnerabilidad de Log4j.
					2. **Monitoreo de Respuestas:** La carga útil incluye un intento de conexión a un servidor externo controlado por el atacante o por la herramienta de detección. Si el servidor objetivo es vulnerable, intentará resolver la cadena maliciosa y hacer una solicitud a un servidor remoto.
					3. **Detección de la Vulnerabilidad:** Si se detecta una conexión desde el servidor objetivo al servidor remoto (o una respuesta que indique la ejecución del código), el script marcará el objetivo como vulnerable.
			```
			nmap --script log4shell -p <puerto> <dirección_ip>
			```
	- **SQL:**
		- **Script para verificar contraseñas vacias:**
			- El script `mysql-empty-password` de Nmap es una herramienta de seguridad que se utiliza para verificar si un servidor MySQL permite conexiones con una contraseña vacía para el usuario root. Esto puede representar una grave vulnerabilidad de seguridad, ya que permitir una contraseña vacía para el usuario root facilita el acceso no autorizado a la base de datos.
				- ### Funcionalidad del Script `mysql-empty-password`
					
					1. **Verificación de Contraseña Vacía:** El script intenta conectarse al servidor MySQL usando el usuario `root` con una contraseña vacía. Si la conexión es exitosa, indica que el servidor MySQL permite el acceso al usuario root sin una contraseña.
					2. **Detección de Vulnerabilidades:** La existencia de una contraseña vacía para el usuario root es un problema de seguridad, ya que permite que cualquier persona se conecte y tenga control total sobre la base de datos.
				```
				nmap --script mysql-empty-password -p 3306 <dirección_ip_o_host>
				```
		- **Script para enumerar usuarios:**
			- El script `mysql-users` de Nmap es un script de escaneo que forma parte de la biblioteca de scripts de Nmap Scripting Engine (NSE). Su función principal es identificar usuarios de bases de datos MySQL en un servidor MySQL remoto. Este script puede ser útil para descubrir credenciales de usuario que podrían ser utilizadas en ataques posteriores, como fuerza bruta o explotación de vulnerabilidades.
				- ### Funcionamiento del Script `mysql-users`

					1. **Conexión al Servidor MySQL:** El script intenta conectarse al servidor MySQL utilizando credenciales de usuario predeterminadas o comunes.
					2. **Enumeración de Usuarios:** Una vez conectado, el script ejecuta consultas SQL para enumerar los usuarios de la base de datos MySQL. Esto se hace generalmente a través de consultas como `SELECT User FROM mysql.user`.
					3. **Obtención de Información de Usuarios:** El script recolecta y muestra los nombres de usuario encontrados en el sistema MySQL.
				```
				nmap --script mysql-users -p 3306 <dirección_ip_del_objetivo>
				```
		- **Script para enumerar base de datos:**
			- El script `mysql-databases` de Nmap es parte de su conjunto de scripts de Nmap Scripting Engine (NSE), y está diseñado para interactuar con servidores MySQL para obtener una lista de las bases de datos disponibles. Este script puede ser útil para descubrir bases de datos en un servidor MySQL y obtener información sobre las bases de datos que están siendo gestionadas.
				- ### Funcionalidad del Script `mysql-databases`

					1. **Conexión al Servidor MySQL:** Se conecta al servidor MySQL en el puerto especificado (por defecto es el puerto 3306) utilizando credenciales proporcionadas o por defecto si están disponibles.
					2. **Autenticación:** El script intenta autenticarse en el servidor MySQL usando credenciales especificadas. Si no se proporcionan credenciales, puede intentar conexiones con valores predeterminados o vacíos.
					3. **Consulta de Bases de Datos:** Una vez autenticado, el script ejecuta una consulta SQL para recuperar la lista de bases de datos presentes en el servidor.
					4. **Reporte de Resultados:** Muestra la lista de bases de datos disponibles en el servidor MySQL.
					```
					nmap -p 3306 --script mysql-databases <dirección_ip>
					```
		- **Script para enumerar variables:**
			- El script `mysql-variables` de Nmap es una herramienta útil para obtener información sobre las variables de configuración de un servidor MySQL. Las variables de configuración en MySQL son parámetros que afectan el comportamiento del servidor y la forma en que maneja las conexiones, las consultas y otros aspectos del sistema de base de datos.
				- ### Funcionalidad del Script `mysql-variables`
					- El script `mysql-variables` está diseñado para conectarse a un servidor MySQL y recuperar una lista de variables de configuración junto con sus valores actuales. Esto puede proporcionar una visión detallada de la configuración del servidor, lo que es útil para la administración, auditoría de seguridad y diagnóstico.
					```
					nmap --script mysql-variables -p 3306 <objetivo>
					```
		- **Script para realizar auditoria:**
			- El script `mysql-audit` de Nmap es un poderoso script del motor de scripts de Nmap (NSE) que se utiliza para auditar la configuración de seguridad de un servidor MySQL. Este script ayuda a identificar posibles debilidades de seguridad, malas configuraciones y prácticas que podrían ser explotadas por un atacante.
				- ### Funcionalidad del Script `mysql-audit`

					1. **Conexión al Servidor MySQL:** El script se conecta al servidor MySQL utilizando las credenciales proporcionadas. Para realizar una auditoría completa, es necesario que el usuario tenga permisos suficientes para acceder a la configuración del servidor.
					    
					2. **Revisión de Configuraciones de Seguridad:**
					    
					    - **Permisos de Usuarios:** Verifica si los usuarios tienen permisos innecesarios o peligrosos, como el acceso a todas las bases de datos o la capacidad de ejecutar comandos peligrosos.
					    - **Contraseñas:** Comprueba si hay usuarios con contraseñas débiles, contraseñas vacías, o si se está permitiendo el acceso root sin contraseña.
					    - **Configuraciones de Red:** Analiza configuraciones relacionadas con la red, como si se permite el acceso remoto al usuario root o si el servidor MySQL está accesible desde todas las interfaces de red.
					    - **Versiones de Software:** Identifica la versión de MySQL para verificar si está desactualizada y es vulnerable a ataques conocidos.
					    - **Configuraciones de Seguridad Adicionales:** Revisa otras configuraciones de seguridad como si el log-bin está habilitado, si se están usando contraseñas hash antiguas, entre otros.
					3. **Detección de Vulnerabilidades Conocidas:** Basado en la versión del servidor y su configuración, el script puede alertar sobre vulnerabilidades conocidas que puedan ser explotadas.
					```
					- nmap -p 3306 --script mysql-audit -sV <dirección_ip>
					- nmap -p 3306 --script mysql-audit --script-args mysql-audit.user=<usuario>,mysql-audit.password=<contraseña> -sV 192.168.1.10

					```
		- **Script para extraer hashes de contraseñas:**
			- El script `mysql-dump-hashes` de Nmap es una herramienta de auditoría de seguridad diseñada para extraer los "hashes" de contraseñas de los usuarios de una base de datos MySQL. Este script es parte del conjunto de scripts NSE (Nmap Scripting Engine) y se utiliza para verificar la seguridad de la configuración de MySQL, especialmente en relación con la fortaleza de las contraseñas.

				- ### Funcionalidad del Script `mysql-dump-hashes`
		
					1. **Conexión a la Base de Datos MySQL:** El script se conecta a la base de datos MySQL utilizando las credenciales proporcionadas o aprovechando configuraciones de seguridad débiles, como un acceso sin contraseña o con una contraseña predeterminada.
					2. **Consulta de Hashes de Contraseñas:** Una vez conectado, el script consulta la tabla `mysql.user`, que almacena los usuarios y los "hashes" de sus contraseñas. Los hashes de contraseñas son versiones encriptadas de las contraseñas que no deberían ser fácilmente recuperables.
					3. **Extracción de Hashes:** El script extrae estos hashes, los cuales podrían ser utilizados por un atacante para realizar un ataque de fuerza bruta o un ataque de diccionario con el fin de recuperar las contraseñas originales.
					4. **Mostrar Hashes Recuperados:** Finalmente, el script muestra los hashes extraídos junto con los nombres de usuario correspondientes.
					```
					nmap --script mysql-dump-hashes -p 3306 --script-args mysqluser=<usuario>,mysqlpass=<contraseña> <host>
					```
		- **Script para realizar querys:**
			- El script `mysql-query` de Nmap es parte de la colección de scripts NSE (Nmap Scripting Engine) y está diseñado para ejecutar consultas SQL en un servidor MySQL. Este script es útil para realizar tareas automatizadas de prueba y auditoría en bases de datos MySQL, especialmente durante actividades de pentesting o evaluaciones de seguridad.
				- ### Funcionalidad del Script `mysql-query`
					
					- El script `mysql-query` permite a los usuarios ejecutar consultas SQL arbitrarias en una base de datos MySQL a la que tienen acceso. Esto puede incluir comandos para consultar datos, verificar configuraciones o realizar otras operaciones que un usuario autenticado en MySQL podría realizar.
					```
					nmap --script mysql-query --script-args "mysql-query.query='CONSULTA_SQL',username=USUARIO,password=CONTRASEÑA" -p 3306 <host>
					```
		- **Script para ver informacion de sql en microsoft:
			- El script `ms-sql-info` de Nmap es una herramienta útil para recolectar información de servidores Microsoft SQL Server (MS SQL) que están accesibles en la red. Este script forma parte de la librería de scripts NSE (Nmap Scripting Engine) de Nmap y está diseñado para identificar y recopilar datos relevantes sobre la instancia de SQL Server, como la versión, el nombre del host, la instancia del servidor, y más.
				- ### ¿Qué hace el script `ms-sql-info`?

					- El script `ms-sql-info` realiza un escaneo sobre el puerto donde está corriendo el servicio MS SQL Server (generalmente el puerto 1433) y extrae la siguiente información:
						
						1. **Nombre del Servidor:** Identifica el nombre del servidor donde está corriendo la instancia de SQL Server.
						    
						2. **Versión del SQL Server:** Detecta la versión exacta de SQL Server que está en ejecución, lo que puede ser útil para identificar posibles vulnerabilidades específicas de esa versión.
						    
						3. **Nombre de la Instancia:** Si el servidor tiene más de una instancia de SQL Server corriendo, el script puede listar los nombres de esas instancias.
						    
						4. **Información del Sistema Operativo:** Puede incluir información sobre el sistema operativo en el que está corriendo el SQL Server.
						    
						5. **Información Adicional:** Dependiendo de la configuración del servidor, el script puede recopilar detalles adicionales, como el nombre de dominio, el tipo de servidor, entre otros.
						```
						nmap --script ms-sql-info -p 1433 <dirección_ip>
						```
		- **Script para ver informacion de sql en microsoft por NTLM:**
			- El script `ms-sql-ntlm-info` de Nmap está diseñado para obtener información sobre el servidor Microsoft SQL Server a través del protocolo NTLM (NT LAN Manager). Este script forma parte de la suite de scripts de Nmap (`nmap scripting engine` o NSE) y se utiliza principalmente para recopilar información de diagnóstico y de versión del servidor SQL.
		 			
				- ### Funcionalidad del Script `ms-sql-ntlm-info`
	
					1. **Conexión al Servidor SQL:** Se conecta al servidor Microsoft SQL Server especificado.
					2. **Autenticación NTLM:** Inicia una autenticación NTLM (una familia de protocolos de autenticación de Microsoft) con el servidor.
					3. **Recopilación de Información:** Durante la fase de negociación NTLM, el servidor puede enviar detalles importantes que pueden ser capturados por el script, como:
					    - **Nombre del Servidor:** El nombre NetBIOS del servidor SQL.
					    - **Dominio:** El dominio o grupo de trabajo al que pertenece el servidor.
					    - **Versión del Servidor:** La versión del software SQL Server que está en ejecución.
					    - **Timestamp (Marca de tiempo):** A veces, se incluye la marca de tiempo que puede ser utilizada para ataques relacionados con la sincronización de tiempo.
					```
					nmap --script ms-sql-ntlm-info -p 1433 <dirección_ip>
					```
		- **Script para ataque de fuerza bruta:**
			- El script `ms-sql-sql-brute` de Nmap es una herramienta utilizada para realizar ataques de fuerza bruta en servidores Microsoft SQL Server (MS SQL) con el objetivo de obtener credenciales válidas. Este script intenta autenticar usando una lista de nombres de usuario y contraseñas comunes para acceder a la base de datos.
				- ### Funcionamiento del Script `ms-sql-sql-brute`

					1. **Conexión al Servidor MS SQL:** El script se conecta a un servidor MS SQL a través de la red.
					2. **Intentos de Autenticación:** Utiliza un conjunto de nombres de usuario y contraseñas (ya sea predeterminado o especificado por el usuario) para intentar autenticarse en la base de datos. Si el script logra autenticarse con alguna combinación, la considera como un éxito y la reporta.
					3. **Reporta Credenciales Válidas:** Si se encuentra un par de credenciales válidas, el script lo mostrará en la salida de Nmap.
				```
				- nmap --script ms-sql-sql-brute -p 1433 <objetivo>
				- nmap --script ms-sql-sql-brute --script-args userdb=/ruta/a/usuarios.txt,passdb=/ruta/a/contrasenas.txt,ms-sql-sql-brute.threads=5 -p 1433 <objetivo>
				```
		- **Script para chequear usuarios con password vacios:**
			- El script `ms-sql-empty-password` de Nmap es una herramienta diseñada para detectar cuentas de usuario de Microsoft SQL Server (MS SQL) que tienen contraseñas vacías. Este script es útil para evaluar la seguridad de las configuraciones de bases de datos MS SQL, ya que las cuentas sin contraseña son un riesgo de seguridad significativo.
				- ### Funcionalidad del Script `ms-sql-empty-password`
					1. **Conexión a MS SQL Server:** El script intenta conectarse al servidor MS SQL en los puertos predeterminados (1433/TCP o 1434/TCP) utilizando el protocolo TDS (Tabular Data Stream), que es el protocolo de comunicación utilizado por MS SQL.
					2. **Intento de Autenticación:** El script prueba varias cuentas comunes de MS SQL (como `sa`, `administrator`, `guest`, entre otras) para ver si pueden autenticarse sin una contraseña. Esto significa que intenta conectarse con el nombre de usuario pero dejando el campo de la contraseña vacío.
					3. **Reporte de Resultados:** Si el script encuentra que alguna de las cuentas puede autenticarse sin contraseña, lo reportará como un resultado positivo, indicando que hay una cuenta sin contraseña en el servidor.
				```
				nmap --script ms-sql-empty-password -p 1433 <dirección_ip>
				```
		- **Script pra realizar consultas ms:**
			- El script `ms-sql-query` de Nmap es una herramienta que se utiliza para ejecutar consultas SQL directamente en servidores Microsoft SQL Server (MS-SQL). Este script es parte del conjunto de scripts de Nmap Scripting Engine (NSE) y es muy útil en situaciones donde un pentester o administrador necesita interactuar con una base de datos MS-SQL para realizar tareas de auditoría, obtener información, o verificar la seguridad de un sistema.
				- ### Funcionalidad del Script `ms-sql-query`

					- El script `ms-sql-query` permite enviar una consulta SQL a un servidor MS-SQL y devuelve los resultados de esa consulta. Puede ser útil en varios escenarios, como:

						- **Verificación de credenciales:** Probar si las credenciales proporcionadas tienen acceso a la base de datos.
						- **Extracción de datos:** Obtener información específica de las tablas de la base de datos.
						- **Evaluación de seguridad:** Verificar si el servidor está configurado de manera segura y si es vulnerable a ataques de inyección SQL u otras vulnerabilidades relacionadas con bases de datos.
					```
					nmap --script ms-sql-query --script-args 'mssql.username=<usuario>,mssql.password=<contraseña>,mssql.query="CONSULTA_SQL"' -p 1433 <objetivo>
					```
		- **Script para ver hashes en MS:**
			- El script `ms-sql-dump-hashes` de Nmap es una herramienta poderosa para la extracción de los hashes de contraseñas de usuarios en un servidor Microsoft SQL Server (MS SQL). Este script se utiliza para obtener los hashes de las contraseñas almacenadas en la base de datos de MS SQL, lo que podría permitir a un atacante realizar ataques de fuerza bruta o de diccionario para descifrar las contraseñas.
				- ### Funcionalidad del Script `ms-sql-dump-hashes`
					1. **Autenticación en el Servidor:** El script primero intenta autenticarse en el servidor MS SQL utilizando las credenciales proporcionadas. Puede autenticarse usando los métodos de autenticación de SQL Server (nombre de usuario y contraseña) o de Windows (si se ejecuta en un entorno Windows y se cuenta con los permisos necesarios).
					2. **Extracción de Hashes:** Si la autenticación es exitosa, el script consulta la tabla `sysxlogins` (o equivalente) en la base de datos `master`, donde se almacenan los hashes de las contraseñas de los usuarios.
					3. **Recuperación de Información:** El script extrae los hashes de las contraseñas junto con otros datos de los usuarios, como el nombre de usuario y el SID (Security Identifier).
					4. **Visualización de Resultados:** Finalmente, el script muestra los hashes extraídos, que pueden ser utilizados en ataques posteriores.
				```
				nmap --script ms-sql-dump-hashes -p 1433 --script-args mssql.username=<usuario>,mssql.password=<contraseña> <ip_objetivo>
				```
		 - **Script para explotar sql por cmd:
		 - El script `ms-sql-xp-cmdshell` de Nmap es un script de la suite de scripts NSE (Nmap Scripting Engine) diseñado para interactuar con servidores Microsoft SQL Server y explotar la funcionalidad de `xp_cmdshell`. Este script es útil en pruebas de penetración para detectar y explotar una vulnerabilidad relacionada con la ejecución de comandos del sistema operativo a través de SQL Server.
			 - ### ¿Qué es `xp_cmdshell`?
				- `xp_cmdshell` es una función extendida en Microsoft SQL Server que permite a los usuarios ejecutar comandos del sistema operativo directamente desde una consulta SQL. Esto puede ser extremadamente peligroso si no está adecuadamente restringido, ya que podría permitir a un atacante ejecutar cualquier comando en el sistema operativo subyacente, facilitando así la escalada de privilegios y la obtención de acceso no autorizado.
			- ### Funcionalidad del Script `ms-sql-xp-cmdshell`

				1. **Conexión al Servidor SQL:** El script se conecta al servidor SQL Server especificado usando las credenciales proporcionadas.
				2. **Verificación de la Funcionalidad de `xp_cmdshell`:** Comprueba si la funcionalidad `xp_cmdshell` está habilitada en el servidor SQL. Esto se hace intentando ejecutar un comando simple a través de `xp_cmdshell`.
				3. **Ejecución de Comandos:** Si `xp_cmdshell` está habilitado, el script puede intentar ejecutar comandos específicos proporcionados por el usuario para verificar la capacidad del servidor para ejecutar comandos del sistema operativo.
			```
			- nmap --script ms-sql-xp-cmdshell -p <puerto> <dirección_ip>
			- nmap --script ms-sql-xp-cmdshell --script-args 'ms_sql_xp_cmdshell.cmd="whoami"' -p <puerto> <dirección_ip>
			```
	- **SSL:**
		- **Script para enumerar y evaluar algoritmos de cifrado:**
			- El script `ssl-enum-ciphers` de Nmap es una herramienta que se utiliza para enumerar y evaluar los algoritmos de cifrado SSL/TLS soportados por un servidor. Este script proporciona información detallada sobre los cifrados y protocolos que el servidor acepta, lo cual es crucial para evaluar la seguridad de una implementación SSL/TLS.
				- ### Funcionalidad del Script `ssl-enum-ciphers`
					
					1. **Enumeración de Cifrados:** El script conecta al servidor y realiza una negociación SSL/TLS para enumerar todos los cifrados y protocolos soportados por el servidor. Esto incluye los cifrados en diferentes versiones de TLS y SSL.
					    
					2. **Evaluación de Protocolos:** Identifica qué versiones de SSL/TLS están habilitadas en el servidor, tales como TLS 1.2, TLS 1.3, SSL 3.0, etc.
					    
					3. **Categorización de Seguridad:** Clasifica los cifrados en diferentes categorías como seguros, inseguros o vulnerables, proporcionando una visión clara del nivel de seguridad del servidor en términos de cifrado.
				```
				nmap --script ssl-enum-ciphers -p <puerto> <dirección_ip>
				```
		- **Script para detectar heartbleed:**
			- El script `ssl-heartbleed` de Nmap está diseñado para detectar vulnerabilidades asociadas con el ataque Heartbleed en servidores que usan OpenSSL. Heartbleed es una vulnerabilidad crítica en la implementación de la extensión Heartbeat de OpenSSL, que permite a un atacante leer la memoria del servidor afectado, incluyendo datos sensibles como contraseñas, claves privadas y otros datos de usuarios.
			- ### ¿Qué es Heartbleed?

				- La vulnerabilidad Heartbleed (CVE-2014-0160) afecta a las versiones de OpenSSL anteriores a la 1.0.1g. Esta vulnerabilidad permite a un atacante leer hasta 64 KB de memoria del servidor en cada solicitud, lo que puede incluir información confidencial que debería estar protegida.

			- ### Funcionamiento del Script `ssl-heartbleed`

				1. **Envía una Solicitud Heartbeat:** El script envía una solicitud de Heartbeat al servidor a través de una conexión SSL/TLS. Esta solicitud contiene un "payload" o carga útil que especifica el tamaño de la respuesta esperada.
				2. **Analiza la Respuesta:** Si el servidor es vulnerable, responderá con un fragmento de memoria que podría incluir información sensible. El script analiza la respuesta para determinar si el servidor está afectado por la vulnerabilidad.
				3. **Informa Sobre la Vulnerabilidad:** Basado en la respuesta, el script informa si el servidor es vulnerable a Heartbleed y proporciona detalles relevantes sobre el hallazgo.
			```
			nmap --script ssl-heartbleed -p <puerto> <dirección_ip>
			```

