- El comando `mysql` es una utilidad de línea de comandos utilizada para interactuar con servidores de bases de datos MySQL y MariaDB. Permite realizar tareas como la gestión de bases de datos, la ejecución de consultas, la administración de usuarios y la configuración de la base de datos.
- ### Uso Básico del Comando `mysql`

	1. **Conectar a un Servidor MySQL**
		- Para conectarte a un servidor MySQL o MariaDB, puedes usar el comando `mysql` seguido de algunos parámetros:
	```
		mysql -u <usuario> -p
	```
	2. **Conectar a un Servidor Remoto**
		- Para conectarte a un servidor MySQL en una máquina remota, debes especificar el host:
	```
		mysql -h <host> -u <usuario> -p
	```
	3. **Ejecutar Consultas desde la Línea de Comandos**
		- Puedes ejecutar comandos SQL directamente desde la línea de comandos utilizando el flag `-e`:
	```
		mysql -u <usuario> -p -e "SQL_QUERY"
	```
	4. **Especificar una Base de Datos por Defecto**
		- Para seleccionar una base de datos por defecto al conectarte, puedes usar el flag `-D`:
	```
		mysql -u <usuario> -p -D <base_de_datos>
	```
	5. **Importar y Exportar Datos**
	
		- **Importar datos desde un archivo SQL:**
		    - Esto importará el contenido de `archivo.sql` a la base de datos `base_de_datos`.
				```
			    mysql -u <usuario> -p < base_de_datos < archivo.sql
				```
		- **Exportar datos a un archivo SQL:**
			- Esto creará un archivo `archivo.sql` con el contenido de la base de datos `base_de_datos`.
				```
				mysqldump -u <usuario> -p base_de_datos > archivo.sql
				```
- ### Comandos Básicos en el Prompt de MySQL

	- Una vez dentro del prompt de MySQL, puedes usar varios comandos para gestionar bases de datos y realizar consultas:
	
	- **Mostrar bases de datos:**
	        
	    `SHOW DATABASES;`
	    
	- **Seleccionar una base de datos:**
	    
	    `USE <base_de_datos>;`
	    
	- **Mostrar tablas en la base de datos actual:**
	        
	    `SHOW TABLES;`
	    
	- **Mostrar estructura de una tabla:**
	        
	    `DESCRIBE <tabla>;`
	    
	- **Ejecutar una consulta SQL:**
	          
	    `SELECT * FROM <tabla>;`
	    
	- **Salir del prompt de MySQL:**
	      
	    `EXIT;`
- ### Opciones Adicionales
	- El comando `mysql` es fundamental para la administración y el desarrollo en entornos que utilizan MySQL o MariaDB, proporcionando una interfaz poderosa para gestionar datos y configurar servidores de bases de datos.
		- `--host=<host>` o `-h <host>`: Dirección del servidor MySQL.
		- `--port=<puerto>` o `-P <puerto>`: Puerto del servidor MySQL (por defecto es 3306).
		- `--protocol=<protocol>`: Protocolo de conexión (por ejemplo, TCP, SOCKET).
		- `--ssl`: Usa conexiones seguras (SSL/TLS) si el servidor MySQL está configurado para ello.


	
	    
	
	
	
