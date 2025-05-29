- El comando `smbclient` es una herramienta de línea de comandos que forma parte del paquete Samba. Se utiliza para interactuar con servidores SMB/CIFS (Common Internet File System) y permite acceder a recursos compartidos en servidores Windows y sistemas que ejecutan Samba. Es similar a un cliente FTP, pero para el protocolo SMB.

- ### Uso de `smbclient`
	
	`smbclient` permite realizar varias operaciones en recursos compartidos de red, como listar archivos, descargar y cargar archivos, y navegar por directorios.
- ### Parametros:
	- -L
		- La opción `-L` en `smbclient` se utiliza para listar todos los recursos compartidos disponibles en un servidor SMB. Es una forma rápida de ver qué recursos están accesibles en un servidor sin necesidad de autenticarse en cada recurso individual.
	-  `-N`
	
		- Descripción: La opción `-N` se utiliza para especificar que no se debe utilizar autenticación (es decir, no se debe proporcionar un nombre de usuario o contraseña).
		-  Uso: Útil para acceder a recursos compartidos que permiten acceso anónimo.
	- -G
	
		- Descripción: La opción `-G` se utiliza para enumerar los grupos de seguridad y sus miembros en el servidor SMB.
		- Uso: Permite obtener información sobre los grupos de seguridad configurados en el servidor, así como los miembros de esos grupos. Esta información es útil para entender la estructura de permisos y las políticas de seguridad en el servidor.