- `dirb` es una herramienta de línea de comandos en Kali Linux que se utiliza para la enumeración y descubrimiento de contenido web. `dirb` realiza un escaneo de fuerza bruta sobre un sitio web, intentando acceder a archivos y directorios ocultos o no vinculados, que no son visibles en la estructura pública del sitio web. Esto se logra al intentar acceder a una lista predefinida de posibles nombres de directorios y archivos.
	- ### ¿Cómo Funciona `dirb`?

		- `dirb` utiliza listas de palabras (wordlists) que contienen nombres comunes de directorios y archivos. Durante el escaneo, `dirb` intenta acceder a cada uno de estos nombres en el sitio web objetivo. Si el servidor responde positivamente (por ejemplo, con un código de estado HTTP 200), `dirb` asume que el archivo o directorio existe.
		```
		dirb <URL> [wordlist] [opciones]
		```
	- ### Opciones Comunes de `dirb`

		- **`-a <user-agent>`**: Especifica el User-Agent a utilizar durante el escaneo.
		- **`-b <cookie>`**: Agrega una cookie a las solicitudes HTTP.
		- **`-c <cookies>`**: Establece cookies adicionales.
		- **`-f`**: Fuerza la inclusión de una barra al final de la URL.
		- **`-i`**: Ignora errores durante el escaneo.
		- **`-p <proxy>`**: Especifica un servidor proxy a través del cual enviar las solicitudes.
		- **`-r`**: Realiza escaneo recursivo.
		- **`-S`**: Muestra sólo las URL exitosas (omitiendo errores).
		- **`-t <seconds>`**: Establece un límite de tiempo entre solicitudes.