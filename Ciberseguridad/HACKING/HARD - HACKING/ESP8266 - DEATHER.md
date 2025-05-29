- Un **ESP8266 Deauther** es un dispositivo que utiliza el microcontrolador ESP8266 para realizar ataques de desautenticación en redes Wi-Fi. Aunque esta herramienta puede tener aplicaciones educativas y de pruebas de seguridad (como pentesting), **es crucial utilizarla únicamente con fines éticos y en redes donde tengas permiso explícito**.
- ### Materiales Necesarios

	1. **Microcontrolador ESP8266**:
		- Ejemplo: NodeMCU, Wemos D1 Mini.
	2. **Cable micro-USB** (para programar el ESP8266 desde tu PC).
	3. **Software**:
		- Arduino IDE (o una herramienta similar).
		- Biblioteca y scripts del Deauther (disponibles en GitHub).

- ### Pasos para Configurar el ESP8266 Deauther

	- #### 1. Instalar Arduino IDE
		
		1. Descarga Arduino IDE desde su sitio oficial: https://www.arduino.cc/en/software.
		2. Instálalo en tu sistema operativo.

	- #### 2. Configurar Arduino IDE para ESP8266
		
		1. Abre Arduino IDE.
		    
		2. Ve a **Archivo > Preferencias**.
		    
		3. En la sección **Gestor de URLs Adicionales de Tarjetas**, añade:
		    
		    `https://arduino.esp8266.com/stable/package_esp8266com_index.json`
		    
		4. Haz clic en **OK**.
		    
		5. Ve a **Herramientas > Placa > Gestor de Tarjetas**, busca `esp8266` e instala el paquete.
		    

	- #### 3. Descargar el Proyecto Deauther
		
		1. Ve al repositorio oficial del Deauther:  
		    [https://github.com/SpacehuhnTech/esp8266_deauther](https://github.com/SpacehuhnTech/esp8266_deauther).
		2. Descarga el código fuente como un archivo ZIP.
		3. Extrae los archivos a una carpeta.

	- #### 4. Abrir y Configurar el Sketch
		
		1. Abre Arduino IDE.
		2. Ve a **Archivo > Abrir** y selecciona el archivo `esp8266_deauther.ino` desde el repositorio descargado.
		3. Configura la placa ESP8266:
		    - **Placa**: NodeMCU 1.0 o Wemos D1 Mini (según tu hardware).
		    - **Velocidad de subida**: 115200.
		    - **Puerto COM**: Selecciona el puerto donde está conectado tu ESP8266.

	- #### 5. Subir el Código
		
		1. Haz clic en el botón de **Verificar** (el check) para compilar el código.
		2. Si no hay errores, haz clic en **Subir** (la flecha) para cargar el programa al ESP8266.
		
	- #### 6. Conectar al Deauther

		1. Una vez cargado el firmware, el ESP8266 emitirá una red Wi-Fi llamada algo como `pwned`.
		2. Conéctate a esta red Wi-Fi (la contraseña suele ser `deauther`).
		3. Abre un navegador y ve a la dirección:
		    
		    Copiar código
		    
		    `192.168.4.1`
		    
		4. Accederás a la interfaz web del Deauther, donde podrás seleccionar redes Wi-Fi y ejecutar funciones como:
		    - Escanear redes.
		    - Enviar paquetes de desautenticación.
		    - Realizar pruebas con redes específicas.