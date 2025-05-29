c- La herramienta **cadaver** es un cliente de línea de comandos para WebDAV (Web-based Distributed Authoring and Versioning), que es un protocolo HTTP que permite a los usuarios gestionar archivos en un servidor remoto de manera similar a como se haría con FTP o SCP. WebDAV añade capacidades de autoría distribuida a HTTP, permitiendo a los usuarios editar, mover, copiar, y borrar archivos en un servidor remoto.

- ### Principales Funciones de cadaver

	- Cadaver permite realizar una serie de operaciones sobre un servidor WebDAV, incluyendo:
		
		1. **Navegación por Directorios**:
		    
		    - Similar a cómo se navega en un sistema de archivos local, puedes listar el contenido de los directorios en el servidor remoto.
		2. **Subir y Descargar Archivos**:
		    
		    - Puedes subir archivos desde tu máquina local al servidor remoto y viceversa.
		3. **Borrar Archivos y Directorios**:
		    
		    - Permite borrar archivos y directorios en el servidor remoto.
		4. **Copiar y Mover Archivos**:
		    
		    - Puedes copiar o mover archivos de un directorio a otro dentro del servidor remoto.
		5. **Bloquear y Desbloquear Recursos**:
		    
		    - WebDAV permite el bloqueo de archivos para evitar que varios usuarios modifiquen el mismo archivo al mismo tiempo. Cadaver permite bloquear y desbloquear estos archivos.
		6. **Crear Directorios**:
		    
		    - Puedes crear nuevos directorios en el servidor remoto.

- ### Uso Básico

	- A continuación te explico cómo usar **cadaver** para realizar algunas de las tareas básicas:
		
		1. **Conectarse a un servidor WebDAV**:
		    
		    `cadaver http://example.com/webdav/`
		    
		    Una vez conectado, cadaver te mostrará un prompt donde puedes ejecutar comandos para interactuar con el servidor.
		    
		2. **Navegar por directorios**:
		    
		    - **Listar contenido**:
		       
		        `ls`
		        
		    - **Cambiar de directorio**:
		       
		        `cd nombre_del_directorio`
		        
		3. **Subir un archivo**:
		    
		    
		    `put archivo_local.txt`
		    
		4. **Descargar un archivo**:
		    
			`get archivo_remoto.txt`
		    
		5. **Borrar un archivo**:
		    
		    `delete archivo.txt`
		    
		6. **Crear un directorio**:
		    	    
		    `mkcol nuevo_directorio`
		    
		7. **Salir de cadaver**:
		    
		    - Para salir de la sesión de cadaver, simplemente escribe `quit` o `exit`.