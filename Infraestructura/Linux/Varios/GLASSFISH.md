- ## Garbage Collector
	- ### Pasos para Ajustar el Garbage Collector desde la Consola de Administración de GlassFish
		
		1. **Acceder a la Consola de Administración:**
		    - Abre tu navegador web y accede a la consola de administración de GlassFish.
		    - La URL por defecto suele ser `http://<ip_del_servidor>:4848`.
		    - Inicia sesión con las credenciales de administrador.
		2. **Navegar a la Configuración de la JVM:**
		    - En la consola, ve al menú de la izquierda y selecciona **"Configurations"**.
		    - Bajo **"Configurations"**, selecciona la configuración correspondiente a tu servidor, que suele ser **"server-config"**.
		    - Dentro de **"server-config"**, selecciona **"JVM Settings"**.
		3. **Modificar los Parámetros de la JVM:**
		    - En la pestaña **"JVM Options"**, verás una lista de opciones de la JVM que están actualmente configuradas.
		    - Para ajustar el Garbage Collector, necesitarás agregar o modificar opciones específicas de la JVM.
		4. **Configurar las Opciones de Garbage Collection:**
		    
		    - **Ejemplos de Opciones de GC**:
		        
		        - **G1 Garbage Collector** (recomendado ):
		            `-XX:+UseG1GC
					`-XX:MaxGCPauseMillis=200
					`-XX:InitiatingHeapOccupancyPercent=45
					
		        - **Parallel Garbage Collector**:
		        
		            `-XX:+UseParallelGC`
		            
		        - **Concurrent Mark-Sweep (CMS) Garbage Collector**:
		            		            
		            `-XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -XX:+CMSIncrementalMode`
		            
		    - **Agregar una Opción de JVM**:
		        
		        - Haz clic en el botón **"Add JVM Option"**.
		        - Introduce el parámetro de la JVM que deseas agregar. Por ejemplo, para usar el Garbage Collector G1, agregarías `-XX:+UseG1GC`.
		        - Haz clic en **"Save"** para guardar los cambios.
		    - **Modificar una Opción de JVM Existente**:
		        - Busca la opción de JVM que deseas modificar en la lista.
		        - Haz clic en ella para editarla y luego guarda los cambios.
		5. **Aplicar los Cambios y Reiniciar GlassFish:**
		    - Después de ajustar las opciones de GC, deberás reiniciar GlassFish para que los cambios surtan efecto.
		    - Ve a **"Common Tasks"** en la consola y selecciona **"Restart Domain"** para reiniciar el servidor.
	- ### Parámetros de GC Comunes

		Aquí hay algunas opciones de JVM relacionadas con el Garbage Collector que podrías considerar:
		
		- **`-XX:+UseG1GC`**: Activa el Garbage Collector G1, recomendado para la mayoría de las aplicaciones modernas.
		- **`-XX:MaxGCPauseMillis=<milisegundos>`**: Establece el objetivo máximo de pausa del GC en milisegundos. Esto es útil para aplicaciones sensibles a las pausas.
		- **`-XX:InitiatingHeapOccupancyPercent=<porcentaje>`**: Define el porcentaje del heap que debe estar ocupado antes de que se inicie un ciclo de GC.
		- **`-XX:+UseParallelGC`**: Activa el Garbage Collector paralelo, que utiliza múltiples hilos para la recolección de basura.
		- **`-XX:+UseConcMarkSweepGC`**: Activa el Garbage Collector CMS, que es un recolector de baja latencia diseñado para aplicaciones que requieren tiempos de pausa más cortos.