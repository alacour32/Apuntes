- `rpcclient` es una herramienta de línea de comandos que forma parte del paquete Samba y se utiliza para interactuar con el servicio RPC (Remote Procedure Call) de servidores Windows y sistemas que ejecutan Samba. Este comando permite realizar diversas operaciones administrativas y de gestión en un servidor, como enumerar usuarios, grupos, recursos compartidos, y más.

	- ### Uso de `rpcclient`
	
		- `rpcclient` permite enviar comandos de procedimiento remoto a servidores que soportan SMB/CIFS, lo cual es útil para tareas de administración de sistemas y auditorías de seguridad.
	- ### Parametros:
		- `-U`

			- El parámetro `-U` especifica el nombre de usuario que `rpcclient` utilizará para autenticarse en el servidor. Este nombre de usuario puede ser necesario para acceder a ciertos recursos protegidos en el servidor.
			```
			rpcclient 192.168.1.10 -U administrator
			```

		- `-N`
			- El parámetro `-N` permite a `rpcclient` intentar una autenticación anónima, es decir, sin especificar un nombre de usuario o contraseña. Esto es útil cuando se desea acceder a información que está disponible públicamente en el servidor sin necesidad de credenciales.
			```
			rpcclient 192.168.1.10 -N
			```
	- ### Comandos:
		- lookupnames
			- El comando `lookupnames` en `rpcclient` se utiliza para resolver nombres de usuario o grupos en sus correspondientes identificadores de seguridad (SIDs) en sistemas Windows. `rpcclient` es una herramienta de línea de comandos proporcionada por el paquete Samba que permite interactuar con servicios de Windows a través del protocolo Remote Procedure Call (RPC).
		- enumdomgroups
			- El comando `enumdomgroups` realiza una consulta al servidor remoto para obtener una lista de todos los grupos de seguridad que existen en el dominio. Estos grupos pueden incluir tanto grupos predeterminados de Windows (como "Domain Admins", "Domain Users", etc.) como grupos personalizados que han sido creados por administradores de dominio.
		- 