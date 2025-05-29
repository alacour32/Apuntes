- # Instalacion / Uso de NGROK :
	-  Instalar **Ngrok** en Kali Linux es sencillo y directo. Sigue estos pasos:
		 - ### Descargar el Binario de Ngrok
			 1. Visita el sitio oficial de **Ngrok**:  
			    https://ngrok.com/download
			2. Copia el enlace de descarga para Linux.
		
			- En tu terminal de Kali, descarga el binario con `wget`:		
			`wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz`
	
		
		- ### Extraer el Archivo Descargado**
	
			- Descomprime el archivo:
					
				`tar -xvzf ngrok-v3-stable-linux-amd64.tgz`
				
			- Esto generará un archivo ejecutable llamado `ngrok`.
				
		- ###  Mover el Binario a un Directorio del Sistema
	
			- Para que sea accesible desde cualquier lugar, mueve el archivo `ngrok` al directorio `/usr/local/bin`:
	
				`sudo mv ngrok /usr/local/bin/`
	
		- ### verificar la Instalación
	
			- Asegúrate de que Ngrok se instaló correctamente ejecutando:
			
				`ngrok --version`
	
			- Deberías ver algo como:
	
				`ngrok version 3.x.x`
	
		
		- ### Configurar Ngrok
	
			- Para usar Ngrok, necesitas una cuenta. Crea una en https://ngrok.com/signup.  
			 - Después de registrarte, obtendrás un **authtoken**.
	
			- Configura tu token en Kali:
		
				`ngrok config add-authtoken TU_AUTHTOKEN`
	
	
		- ###  Usar Ngrok
	
			- Ejemplo de cómo iniciar un túnel HTTP en el puerto 8080:
	
				`ngrok http 8080`
	
			- Ngrok generará una URL pública que redirige a tu servicio local.
	
		- ### Opcional: Instalar Dependencias Adicionales
	
			- Ngrok no suele requerir dependencias, pero si encuentras problemas:
	
				`sudo apt update sudo apt install -y wget tar`

- # Instalacion / Uso de Httrack:

	- **HTTrack** es una herramienta de código abierto que permite descargar sitios web completos a tu computadora, replicándolos localmente para navegarlos sin conexión. Aquí te explico cómo usarla para clonar un sitio:
		- ### Instalación de HTTrack:
			- #### En Linux:
				- Usa el administrador de paquetes de tu distribución:

					`sudo apt install httrack  # En Debian/Ubuntu sudo dnf install httrack  # En Fedora sudo pacman -S httrack    # En Arch`

			- #### **En Windows**:
				
				1. Descarga el instalador desde [la página oficial](https://www.httrack.com/).
				2. Instala HTTrack siguiendo las instrucciones.

		- ### Clonar un Sitio Web

			- #### Comando Básico:
						
				`httrack "https://ejemplo.com"`
				
				- Este comando descargará el sitio completo en una carpeta con el nombre del dominio.

		- ### Comando Personalizado

			- Para más control, usa los siguientes parámetros:

				`httrack "https://ejemplo.com" -O "./mi_sitio_clonado" "+*.ejemplo.com/*" "-*.pdf"`

			- #### Explicación:
				- `"https://ejemplo.com"`: URL del sitio que deseas clonar.
				- `-O "./mi_sitio_clonado"`: Especifica la carpeta donde se guardará el contenido descargado.
				- `"+*.ejemplo.com/*"`: Incluye solo las páginas del dominio especificado.
				- `"-*.pdf"`: Excluye archivos PDF (puedes cambiar por otros tipos de archivo).
		- ### Parámetros Útiles
			
			- `-r`: Activa el modo recursivo para descargar todo el sitio.
			- `--depth=NUM`: Especifica la profundidad máxima de los enlaces (por defecto, no hay límite).
			- `--mirror`: Descarga todo el contenido estático.
			- `--continue`: Continua una descarga interrumpida.
			
		- ### Ejemplo Completo

			- Si quieres clonar un sitio web, incluyendo todos los enlaces internos pero excluyendo recursos externos como scripts de terceros:

				`httrack "https://ejemplo.com" -O "./mi_sitio_clonado" "+*.ejemplo.com/*" "-*facebook.com*" "-*twitter.com*"`
				
- # Montar un sitio clonado:
	- Para montar un sitio web clonado con **HTTrack** y exponerlo públicamente utilizando **Ngrok**, sigue estos pasos:

	- ### 1. Clonar el Sitio con HTTrack

		- Si no has clonado el sitio todavía, usa HTTrack para descargarlo:

			`httrack "https://ejemplo.com" -O "./sitio_clonado"`

		 - Esto creará una carpeta llamada `sitio_clonado` que contendrá los archivos del sitio.

	- ### 2. Configurar un Servidor Local

		- Para servir los archivos del sitio clonado, necesitas un servidor HTTP local. Puedes usar Python para esto:

		- #### Para Python 3.x:

			`cd sitio_clonado python3 -m http.server 8080`

			- Esto iniciará un servidor HTTP en el puerto **8080**.

		- #### Para Python 2.x:

			`cd sitio_clonado python -m SimpleHTTPServer 8080`

	- ### 3. Exponer el Servidor Local con Ngrok

		- Usa Ngrok para crear un túnel público hacia el puerto donde corre tu servidor local.

		- Ejecuta:

			`ngrok http 8080`

		- Ngrok te proporcionará una URL pública similar a esta:

		- arduino

			`http://abc123.ngrok.io`


	- ### 4. Probar el Sitio
		
		1. Copia la URL pública proporcionada por Ngrok.
		2. Pégala en un navegador web.
		3. Ahora tu sitio clonado estará accesible desde Internet a través de la URL de Ngrok.

	- ### 5. Opcional: Personalizar el Subdominio de Ngrok

		- Si tienes una cuenta gratuita o de pago en Ngrok, puedes personalizar el subdominio:

			`ngrok http --subdomain=mi-sitio 8080`

		- Esto generará una URL como:

		- arduino

			`http://mi-sitio.ngrok.io`

	- ### 6. Detener el Servidor

		- Para detener el servidor HTTP o Ngrok:
			- En la terminal donde corre el servidor, presiona **Ctrl+C**.
			- En la terminal de Ngrok, también usa **Ctrl+C**.

	- ### Notas Importantes

		- Ngrok genera URL temporales en su versión gratuita, por lo que cambiarán cada vez que lo inicies.
		- Asegúrate de que el contenido del sitio clonado no infrinja derechos de autor ni términos de uso del sitio original.