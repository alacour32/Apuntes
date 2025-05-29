- `nmblookup` es una herramienta de línea de comandos utilizada en sistemas Linux y Unix para consultar nombres NetBIOS a través de la red. Es parte del paquete Samba, que proporciona interoperabilidad de servicios de archivos e impresión entre sistemas Windows y Unix/Linux. `nmblookup` permite buscar nombres NetBIOS para obtener sus direcciones IP asociadas, similar a cómo funciona el sistema DNS para nombres de dominio.

- ### Características de `nmblookup`
	
	1. **Resolución de Nombres NetBIOS**:
	    
	    - `nmblookup` busca en la red el nombre NetBIOS proporcionado y devuelve la dirección IP correspondiente.
	    - Puede utilizarse para resolver nombres de equipos Windows y otros dispositivos que usen el protocolo NetBIOS.
	2. **Consulta de Nombres de Grupo**:
	    
	    - Permite consultar nombres de grupos de trabajo o dominios en una red.
	    - Puede ayudar a identificar grupos o dominios activos en la red local.
	3. **Soporte de Broadcasting y Servidores WINS**:
	    
	    - `nmblookup` puede realizar consultas mediante broadcasting (difusión) en la red local.
	    - También puede utilizar servidores WINS (Windows Internet Name Service) si están configurados.
- ### Parametros:
	1. -A
		- La opción `-A` en el comando `nmblookup` permite realizar una consulta inversa de NetBIOS utilizando una dirección IP. Específicamente, el comando `nmblookup -A <IP>` se utiliza para obtener el nombre NetBIOS de un host dado su dirección IP.