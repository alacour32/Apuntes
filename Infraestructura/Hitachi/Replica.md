- ### Creación de nodo 
	- Entrar en "Nodes" y precionar en el signo "+"
	![[Pasted image 20250304182813.png]]
	- Elegir el tipo: "hitachi block host" (lista de devices):
	![[Pasted image 20250304182945.png]]
		- Nota: existen los agentes para instalar en los equipos cosa que provocaría que automáticamente se den de alta en protector
		
	- Se especifica el nombre:
	 ![[Pasted image 20250304183736.png]]
	 - Se indican a protector en que storage de todos los que hay, están los volúmenes de interés:
	 ![[Pasted image 20250304183954.png]]
	 - Se especifica los logical device/host group-id que se replicaran y lo que serán excluidos:
	 ![[Pasted image 20250304184052.png]]
	 - Aparece el sumary y se le de aceptar para terminar la creación:
	  ![[Pasted image 20250304184543.png]]
	 
 - ### Creacion de Polices:
	 - Entrar en Policies en el menú de la izquierda y luego hacer click en el signo "+":
	 ![[Pasted image 20250304184900.png]]
	 - Especificar nombre y descripción:
	 ![[Pasted image 20250304185040.png]]
		 - nota: una política es posible en caso de ser genérica usarla  en distintos casos ya que en la política misma no se hacen definiciones de volúmenes
		 
	 - Aqui no se hace nada:
	 ![[Pasted image 20250304185357.png]]
	- Especificar sobre que tipo de dispositivos se van a trabajar haciendo click en el signo "+":
	![[Pasted image 20250304185536.png]]
	- Seleccionar el tipo de dispositivo en el que se va a trabajar: (lo que venimos utilizando es "hitachi block")
	![[Pasted image 20250304185711.png]]
	- Aqui no se realiza nada ya que esto esta especificado en el nodo:
	![[Pasted image 20250304185855.png]]
	- finalizacion de la clasificacion
	![[Pasted image 20250304185940.png]]
	- Especificación  de política:
	![[Pasted image 20250304190038.png]]
	- Elección de operación: (para este caso seria "Replicate")
	![[Pasted image 20250304190143.png]]
	- solamente en esta pantalla se hace "apply"
	![[Pasted image 20250304190232.png]]
		- nota: destildar la opcion: "quiesce configured applications befor backup" esta opcion se utiliza solamente cuando protector interactua con el host
	- hacer click en finish:
	![[Pasted image 20250304190303.png]]
- ### Definición de Data Flow:
	- Seleccionar la opcion "Data flows" en el menu de la izquierda y luego hacer click en el signo "+":
	![[Pasted image 20250304190627.png]]
	- Especificar nombre y descripcion:
	![[Pasted image 20250304190700.png]]
	- aqui no se hace nada:
	![[Pasted image 20250304190816.png]]
	- Arrastrar a la pizarra el host sobre el que se trtabajara
	![[Pasted image 20250304191008.png]]
	- luesgo arrastrar el storage de destino:
	![[Pasted image 20250304191108.png]]
		- Nota: al momento de arrastrarlo pasar por encima del host para que una vez colocado el storage en la pizarra ya queden asociados
		
	- seleccionar el "Transfer Type": ("continuous")
	![[Pasted image 20250304191254.png]]
	- Luego sellecionar el host para poder elegir la policy que se aplicara al data flow:
	![[Pasted image 20250304191440.png]]
	- luego seleccionar el storage para que poder elegir las acciones dentro de la policy para ejecutar:
	![[Pasted image 20250304191601.png]]
		- Nota: en caso de tener varias acciones para ejecutar en la misma pantalla tendrían que aparecer las acciones para configurar
	- Luego de seleccionar "Replicate" aparecera un panatalla para definir la replica: (seleccionar "configure new replication")
	![[Pasted image 20250304191815.png]]
	- seleccionar tipo de replica: ("Asynchronous remote clone")
	![[Pasted image 20250304192024.png]]
	- seleccionar en la forma que se almacenara en el lugar secundario: ("match source volume")
	![[Pasted image 20250304192153.png]]
	- seleccion de pool de destino:
	![[Pasted image 20250304192226.png]]
	- seleccionar  journal existentes: (select existing journals)
	![[Pasted image 20250304192307.png]]
	-  elegir journal existente
	![[Pasted image 20250304192443.png]]
	- selección de remote  path o sea atraves de que canales protector creara la replica
	![[Pasted image 20250304192511.png]]
	- elegir resource group en automatico:
	![[Pasted image 20250304192849.png]]
	- seleccionar el tipo y donde se mapeara la replica: (actualmente estamos usando host groups)
	![[Pasted image 20250304193015.png]]
	- forma en los que los host groups se mapearan en el sitio secundario:
	![[Pasted image 20250304193224.png]]
		- recomendacion 1: no usar "use automatically provisioned host group" ya que eso provocaria que en el sitio secundario cree host goups dummie
		- recomendacion 2: no usar enforce LUN ID matching ya que con esta opcion protector busca que las LUN ID del sitio primario en el secundario y en caso de no ser iguales falla
	- seleccionar los host gropu donde se quiere mapear ls volumenes secundarios:
	![[Pasted image 20250304193609.png]]
	-  seleccionar el nombre con que que se quiere creer en el sitio secundario: (mathc origin)
	![[Pasted image 20250304193753.png]]

- ### Agregar volumenes a la replica:
	- Requisitos: no pausar la replica
	1. suspender el data flow:
		![[Pasted image 20250304195108.png]]
		![[Pasted image 20250304195152.png]]
		- Nota: cuandos se suspende el data flow no se se ejecuta ninguna accion sobre la replica o sea que la replica sigue activa
	2.   Mapear el disco nuevo:
		- ir a administrator e ubicarse en el servidor al que se le agregara los discos nuevos:
			![[Pasted image 20250304195949.png]]
		- hacer click en el icono con el simbolo de base de datos con un + y luego en atch existing volummes
			![[Pasted image 20250304200113.png]]
		- Seleccionar discos a attachar:
			![[Pasted image 20250304200208.png]]
		- aqui no se hace nada:
			![[Pasted image 20250304200306.png]]
		- aquí tampoco (se tiene que presionar submit, ya que si se preciosa next, ira a otra pantalla donde mostrara las acciones que realizara)
			![[Pasted image 20250304200333.png]]
	3. Activar nuevamente el Data Flow:
		![[Pasted image 20250304200736.png]]
- ### Eliminacion de volumen
	1. hacer click en el menu de la izquierda, seleccionar el data flow y luego detenerlo:
		![[Pasted image 20250304203005.png]]
		![[Pasted image 20250304203116.png]]
	2. luego ir a nodes y hacer click en editar:
		![[Pasted image 20250304203218.png]]
	3. llegar a la pantalla de specify logical device y en la parte de excluded logical devices anotar el volumen a editar
		![[Pasted image 20250304203410.png]]
	4. activar data flow nuevamente
		![[Pasted image 20250304203601.png]]
- ### Operaciones de Fail Over:
	- Entrar en el storage luego en replications and clones y luego en la operacion de replica a hacer las operaciones
		![[Pasted image 20250304204231.png]]
	- Pausado de replica:
		- hacer click en el simbolo de pausa:
			![[Pasted image 20250304204444.png]]
			![[Pasted image 20250304204507.png]]
			- nota: al intentar pausar la replica aparece un mensaje que da la opcion de dejar los volumenes secundarios como read/write 
		- en la opeacion de replica, en la opcion de pairs se puede consultar el estado de los volumnes secundarios y las diferencias de cambios que hay entre el primario y el secundario:
			![[Pasted image 20250304204836.png]]
	- Convertir el sitio secundario en primario: (SIN DETENER LA REPLICA)
		- Requisitos: 
			- poner los discos offline del sitio primario 
			- chquear el estado y el sentido de replica de la operacion 
		1. hacer click en swap y escribir en la ventana siguiende SWAP y seleccionar la nueva direccion que tendra la replica
			![[Pasted image 20250304210531.png]]
			![[Pasted image 20250304210626.png]]
