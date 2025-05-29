- `enum4linux` es una herramienta de línea de comandos basada en Linux utilizada para la enumeración de información en servidores que ejecutan servicios de Windows, como SMB (Server Message Block), NetBIOS y RPC (Remote Procedure Call). Es ampliamente utilizada en pruebas de penetración y auditorías de seguridad para recopilar información sobre un sistema objetivo de forma no intrusiva.
	
	- ### Uso de `enum4linux`
		
		- `enum4linux` permite obtener una variedad de información útil sobre un servidor Windows o un sistema que ejecuta Samba, como:
		
			- Usuarios y grupos del sistema.
			- Recursos compartidos disponibles.
			- Detalles de la política de contraseñas.
			- Información del dominio y de la máquina.
	- ### Parametros:
		- ### `-o`
	
			- El parámetro `-o` en `enum4linux` se utiliza para intentar enumerar las cuentas de usuario a través del servicio **LDAP** (Lightweight Directory Access Protocol). Este parámetro intenta conectarse al puerto 389 (LDAP) del servidor de destino y listar las cuentas de usuario que están expuestas públicamente.
		- -U
			- El parámetro `-U` de `enum4linux` se utiliza para enumerar los usuarios en un sistema remoto que está ejecutando el servicio SMB. Este comando intenta obtener una lista de todos los usuarios disponibles en un servidor Windows al interactuar con el protocolo SMB.
		- -S
			- El parámetro `-S` en `enum4linux` se utiliza para obtener información sobre los grupos de usuarios en un dominio o en una máquina Windows. Más específicamente, este parámetro realiza una consulta para enumerar los grupos de seguridad y sus miembros.
		- -G
			- Cuando ejecutas `enum4linux` con el parámetro `-G`, la herramienta realiza una consulta al servidor SMB para obtener una lista de los grupos de seguridad existentes y sus respectivos miembros. Esto puede incluir grupos predeterminados como "Administradores" y "Usuarios", así como cualquier grupo personalizado que haya sido creado en el servidor.
		- -i 
			- El parámetro `-i` en `enum4linux` se utiliza para realizar consultas individuales y obtener información detallada sobre usuarios específicos en un servidor SMB. En lugar de recopilar información general sobre todos los usuarios o recursos, esta opción permite enfocarse en un usuario individual, extrayendo datos como su SID (Security Identifier) y otra información relevante.