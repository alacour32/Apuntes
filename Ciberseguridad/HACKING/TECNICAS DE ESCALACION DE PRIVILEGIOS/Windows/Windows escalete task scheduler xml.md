- La escalación de privilegios en Windows puede llevarse a cabo a través de diversas técnicas, y una de ellas implica el uso de **Task Scheduler** (Programador de Tareas) y archivos XML maliciosos. Aquí te explico en detalle cómo se puede llevar a cabo esta técnica y su funcionamiento.

- ### ¿Qué es el Programador de Tareas?

	- El **Programador de Tareas** de Windows permite a los administradores programar tareas para que se ejecuten bajo ciertas condiciones o en momentos específicos. Esto incluye la ejecución de scripts, programas y procesos en segundo plano, y puede configurarse para que se ejecute con los privilegios del usuario o, en algunos casos, con privilegios elevados.

- ### Técnica de Escalación de Privilegios con XML en Task Scheduler

	- La escalación de privilegios mediante el Programador de Tareas y archivos XML generalmente consiste en crear una tarea programada que se ejecute con privilegios elevados (o con los privilegios de otro usuario) utilizando un archivo XML que especifica la tarea. A continuación, se describen los pasos típicos que se pueden seguir para realizar esta técnica:

	- #### Pasos para la Escalación de Privilegios

		1. **Creación de un Payload**: Primero, se necesita un payload o script que se ejecutará cuando se dispare la tarea. Este podría ser un script de PowerShell, un ejecutable, etc.
		    
		2. **Creación de un Archivo XML**: Se debe crear un archivo XML que contenga la configuración de la tarea programada. Este archivo especifica:
		    
		    - El nombre de la tarea.
		    - Cómo y cuándo se ejecutará la tarea.
		    - El directorio y el ejecutable que se ejecutará.
		    
		    Aquí tienes un ejemplo simple de un archivo XML para crear una tarea que ejecuta un script de PowerShell:
		    
			```
		    
			<?xml version="1.0" encoding="UTF-16"?>   <Task version="1.3" xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task">       <RegistrationInfo>           <Date>2024-11-24T12:00:00</Date>           <Author>example_user</Author>       </RegistrationInfo>       <Triggers>           <LogonTrigger>               <Enabled>true</Enabled>           </LogonTrigger>       </Triggers>       <Actions>           <Exec>               <Command>powershell.exe</Command>               <Arguments>-ExecutionPolicy Bypass -File C:\path\to\your\script.ps1</Arguments>           </Exec>       </Actions>   </Task>
			```
		    
		3. **Registrar la Tarea con el Archivo XML**: Usando el comando `schtasks`, puedes registrar una nueva tarea utilizando el archivo XML. Esto se puede hacer con el siguiente comando:
		    		    		    
		    `schtasks /Create /TN "MyMaliciousTask" /XML "C:\path\to\your\task.xml" /RU "SYSTEM" /RL HIGHEST`  
		    
		    - `/TN` especifica el nombre de la tarea.
		    - `/XML` indica la ubicación del archivo XML.
		    - `/RU` establece el usuario con el cual se ejecutará la tarea (en este caso el sistema).
		    - `/RL` especifica el nivel de ejecución (HIGHEST para ejecutar con privilegios elevados).
		4. **Activar la Tarea**: Dependiendo de la configuración, la tarea puede ejecutarse en el próximo inicio de sesión del usuario o se puede disparar manualmente.
		    
		5. **Ejecutar la Escalación**: Una vez creada la tarea programada y activada, cuando se ejecute, ejecutará el payload con los privilegios especificados.