- ## Servicios
	- Exiten 3 servicios importantes que pueden variar entre ambientes los nombres:
		- Bantotal_"ambiente"
		- Bantotal_"ambiente"_ Btlan
		- Bantotal_"ambiente" _ procser
	- **Bantotal_"ambiente** se lo configura desde el archivo situado en: F:/"ambiente"/apache-tomcat-10.1.19/bin, se edita el archivo service.bat
		- dentro se define el tema de java colocando dos lineas:
			- set JAVA_HOME="C:/Progra~1/java/jdk-11.0.5"
			- set  JRE_HOME="C:/Progra~1/java/jdk-11.0.5" ![[Pasted image 20240912143759.png]]
		- se edita el nombre 
			- set default_service_name="nombre del servicio"![[Pasted image 20240912143851.png]]
		- se edita la linea dysplayName
			- --DisplayName="nombre del servicio"![[Pasted image 20240912143935.png]]
		- se realiza copia del ejecutable tomcat10 y se lo renombra como "Bantotal_"ambiente""
	- **Bantotal_"ambiente"_ Btland** se lo configura en la ruta F:/BTLandv2.3.3/apache-tomcat-9.0.65/bin, se edita el archivo service.bat
		- dentro se define el tema de java colocando dos lineas:
			- set JAVA_HOME="C:/Progra~1/java/jdk-11.0.5"
			- set  JRE_HOME="C:/Progra~1/java/jdk-11.0.5"![[Pasted image 20240912144143.png]]
		- se edita el nombre 
			- set default_service_name="nombre del servicio"![[Pasted image 20240912144222.png]]
		- se edita la linea dysplayName
			- --DisplayName="nombre del servicio"![[Pasted image 20240912144257.png]]
		- se realiza copia del ejecutable tomcat10 y se lo renombra como "Bantotal_"ambiente"_ Btland"
	- **Bantotal_"ambiente"_ procser** se lo configura en la ruta F:/Testing/procser/, se edita el archivo procser.bat y el server.config
		- se edita la linea %JAVA_EXEC% %JMX% %MEM% por el nombre del ambiente en la ruta que figura en la imagen
		![[Pasted image 20240912130707.png]]
		- en el archivo server.config se edita la linea donde figura el directorio la primera (ambiente) con mayuscula y la segunda con minuscula (aplicacion)
		![[Pasted image 20240912131231.png]]
		- Limpiar carpeta logs 
		- Abrir un cmd y ejecutar los comandos:
			```
			- cd  F:/Testing/procser/
			- nssm install procser 
			```
		- en la pestaña aplication hace click en "..." en la opcion de "Path" en la ventana "Locate application file" seleccionar el archivo "procser.bat" ![[Pasted image 20240912141023.png]]
		- en la pestaña "Detail" colocar el "Display name"![[Pasted image 20240912141128.png]]
		- Para finalizar hacer click en "Install service"
- **Instalacion de servicios:** Luego de haber parametrisado los 3 servicios abrir un cmd con privilegios de administrador
	- crear los servicios escibiendo el siguiente comando por cada servicio
		```
		- service install "nombre del servicio"
		```
	-  crear la dependencia del servicio procser con el servicio bantotal_"ambiente"
		```
		- sc config Bantotal_"ambiente" _ procser depende=Bantotal_"ambiente"
		```
 - Una ves creado los servicios y su dependencia configurar en cada uno el tipo de inicio y con que usuario se ejecutara
	 - ![[Pasted image 20240912132123.png]]
	 - ![[Pasted image 20240912132150.png]]
- ## APLICACION
	- **Configuracion del archivo log4j2**
		- Editar el path con el nombre de ambiente asi como figura en la image 
		![[Pasted image 20240912132615.png]]
	- **Configurar el archivo client.cfg** que se ubica en f:/"ambiente"/apache-tomcat-10.1.19/webapps/testing/WEB-INF/classes/com/dlya/bantotal/
		- Se modifican los parametros "USER_ID; DB_URL; USER_PASSWORD" segun corresponda
		- ![[Pasted image 20240912134448.png]]
		- Modificar la linea "CS_BLOB_PATH" con la ruta de la carpeta donde se almacenaran los archivos temporales en el file-server![[Pasted image 20240912141619.png]]
		- luego de haber editado el archivo dirigirse al file server y en el path //CPFLSBTTV01/Bantotal , agregar una carpeta con el nombre del ambiente a desplegar y luego copiar la carpeta "archvosbt" de alguno de los ambientes ya desplegados![[Pasted image 20240912142010.png]]
	-  **Configurar archivo eventsserver.xml** que se encuenta en  F:/"ambiente"/apache-tomcat-10.1.19/webapps/"ambiente"/WEB-INF/conf/
		- edita la linea del sqlserver colocando la ip que corresponda ![[Pasted image 20240912142359.png]]
	- **Configurar el archivo "eventsserver-encrypted"** que se encuentra F:/"ambiente"/apache-tomcat-10.1.19/webapps/"ambiente"/WEB-INF/conf/
		- Editar con el usuario y la contraseña para conectarse a la base de datos![[Pasted image 20240912142613.png]]
	- **Configurar archivo PDFReport.ini **
		- editar con el nombre del ambiente para poder utilizar las fuentes ![[Pasted image 20240912142905.png]]
	- **Configuracion de Logo:** esto se configura en la carpeta F:/"ambiente"/apache-tomcat-10.1.19/webapps/"ambiente"/images/ en el archivo Logo_banco.png![[Pasted image 20240913082940.png]]
- ## Notas
	- Si se solicitase saber la version de genexux que se esta utilizando visualisar el nombre del arhivo gxclass"ver"u"comp" ejemplo: gxclass16u9 el cual se encuentra en F:/"ambiente"/apache-tomcat-10.1.19/webapps/"ambiente"/WEB-INF/lib/![[Pasted image 20240912143202.png]]
	- Para agregar conexiones a la aplicacion se agregan en el archivo Location.xml el cual se encuentra en  F:/"ambiente"/apache-tomcat-10.1.19/webapps/"ambiente"/WEB-INF/![[Pasted image 20240912143427.png]]
	- Cuando haya problema con el servicio bantotal_ "ambiente"_ procser antes de reiniciarlo verificar en bantotal BRLand en la sección ![[image.png]]
		en esta sección hay que verificar que no haya procesos corriendo antes de reiniciar el reinicio del servicio