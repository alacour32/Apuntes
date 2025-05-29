# Pre-requisitos:

- Crear la VM que sera el nuevo controlador de dominio
- Colocarle ip fija
- instalar rol de ad en la nueva vm
- Subirla al domio del que posteriormente sera el nuevo controlador
- asegurarse que se hay comunicación entre los dos servidores 
```
	ping
```

# Detalles luego de la migración
- En caso de tener un dhcp andando en otro servidor entra en el rol de DHCP  hacer click derecho en scope options y seleccionar configure options, en la ventana que se abrira seleccionar la pestaña avanzed en el listado de opciones selleccionar la opcion DNS Servers, debajo se desplegara un listado de ips de las cuales hay que agregar el nuevo servidor DC y eliminar el enterior
- Una vez migrado habilitar la característica smb 1.0 en el nuevo ad dc para que los 2003 y xp puedan acceder
- En caso de migrar el servidor dns el server nuevo tiene que quedar en su configuracion de dns como servidor dns
- El usuario administrador local quedara deshabilitado 


# 1. Chequeo de los Servidores

- Intentar agregar  al nuevo servidor (2019) como controlador de dominio, al hacerlo se visualizara el error que se puede observar en la captura
![[Pasted image 20240321185426.png]]

- Ir a ***tools administrative*** y dentro elegir la opcion ***Active directory users and* computers**, Dentro seleccionar la opcion ***domain controler*** y se podra visualizar el controlador vigente en el dominio (equipo con windows server 2008)

![[Pasted image 20240321195130.png]]

- Dentro de el equipo con windows server 2008 ejecuta cmd con privilegios de administrador y dentro ejecutar el comando:

```
netdom query fsmo
```

Se podra visualizar el dueño de los roles de los distintos esquemas de configuraciones en el actual controlador de dominio 

- En el equipo con windows server 2008 ir a ***Tools administrative*** y dentro a la herramienta active ***Directory domains and trusts***, en la mismo hacer click derecho sobre el nombre del equipo y elegir la opcion ***Raise forest functional level***

![[Pasted image 20240321201716.png]]

- En ambos servidores accedes al regedit y ubicarse en la clave de registro schema version en la direccion:

```
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\NTDS\Parameters\Schema Version
```
![[Pasted image 20240321202150.png]]

NOTA: El valor de `Schema Version` es importante para determinar la compatibilidad del esquema de Active Directory entre diferentes controladores de dominio y para asegurarse de que todos los controladores de dominio estén actualizados con la versión correcta del esquema.

# 2. Preparar windows server 2019

- Una vez hecho todos los chequeos hay que preparar el nuevo controlador de dominio para la elevacion.  

- Montar la imagen de windows server 2019 en el mismo para poder acceder al aplicativo ***adprep.exe***. Abrir powershell y ubicarse en la carpeta donde se encuentra el aplicativo, luego escribir el comando:

```
 .\adprep.exe /forestprep
```

![[Pasted image 20240321211048.png]]

Nota: Cuando ejecutas `adprep.exe /forestprep`, se realizan las siguientes acciones:

1. **Actualización del esquema del bosque:** Se actualiza el esquema de Active Directory para incluir los cambios necesarios para admitir la nueva versión del sistema operativo de Windows Server y las características asociadas.
2. **Agrega nuevos atributos y clases de esquema:** Se agregan nuevos atributos y clases de esquema que pueden ser necesarios para admitir características adicionales o actualizadas del sistema operativo de Windows Server.
3. **Prepara el bosque para nuevas funciones de Active Directory:** Se prepara el bosque para admitir nuevas funciones y capacidades que pueden estar disponibles en la nueva versión del sistema operativo de Windows Server.

- luego ejecutar el comando:
```
.\adprep.exe /domainprep
```

![[Pasted image 20240321211105.png]]

Nota: Cuando ejecutas `adprep.exe /domainprep`, se realizan las siguientes acciones:

1. **Actualización del dominio:** Se realizan actualizaciones en el dominio de Active Directory para incluir los cambios necesarios para admitir la nueva versión del sistema operativo de Windows Server y las características asociadas.
2. **Configuración de permisos y configuración:** Se realizan configuraciones adicionales en el dominio para asegurar que esté correctamente preparado para admitir el nuevo controlador de dominio, incluyendo la configuración de permisos y la actualización de las ACLs (listas de control de acceso).
3. **Prepara el dominio para nuevas funciones de Active Directory:** Se prepara el dominio para admitir nuevas funciones y capacidades que pueden estar disponibles en la nueva versión del sistema operativo de Windows Server.

ejecutar el comando:

```
.\adprep.exe /domainprep /gpprep
```

![[Pasted image 20240321211509.png]]
Nota: Cuando ejecutas `adprep.exe /domainprep /gpprep`, se realizan las siguientes acciones adicionales:

1. **Preparación del dominio para Políticas de Grupo de preferencia:** Se realizan cambios en el esquema de Active Directory y se actualizan los objetos de Política de Grupo para admitir las preferencias de Política de Grupo.
2. **Habilitación de nuevas funcionalidades de Política de Grupo:** Se habilitan las nuevas funcionalidades de Política de Grupo que están disponibles a través de las preferencias de Política de Grupo.


En el equipo windows server 2008 ejecutar cmd.exe y ejecutar el comando :

```
dcdiag /e /test:sysvolcheck /test:advertising
```

![[Pasted image 20240321212155.png]]
Nota: El comando `dcdiag /e /test:sysvolcheck /test:advertising` es una herramienta de diagnóstico de Active Directory que se utiliza para verificar la salud y el estado de los controladores de dominio en un entorno de Active Directory. Este comando específico realiza dos pruebas:

1. **Prueba de SysVolCheck (`/test:sysvolcheck`):** Esta prueba verifica la replicación del contenido de SYSVOL entre los controladores de dominio en el dominio. SYSVOL es una carpeta compartida que contiene datos y archivos de inicio de sesión de usuarios, scripts de inicio de sesión de usuario y políticas de grupo (GPO) en un entorno de Active Directory. La prueba de SysVolCheck verifica que todos los controladores de dominio tengan una réplica actualizada y coherente de la carpeta SYSVOL.
2. **Prueba de Advertising (`/test:advertising`):** Esta prueba verifica la capacidad de un controlador de dominio para anunciarse correctamente en el dominio y responder a las solicitudes de los clientes. Verifica que el controlador de dominio esté respondiendo adecuadamente a las consultas DNS y que esté anunciando su presencia en el dominio para que otros clientes y controladores de dominio puedan localizarlo correctamente.

- luego ejecutar:

```
Dfsrmig /setglobalstate 1
```
![[Pasted image 20240321212236.png]]

- luego consultar con el comando:

```
Dgsrmig /getmigrationstate
```

![[Pasted image 20240321212516.png]]

- luego ejecutar:
```
Dfsrmirg /setglobalstate 2
```

![[Pasted image 20240321212703.png]]

- Consultar nuevamente con el comando:

```
Dgsrmig /getmigrationstate
```

![[Pasted image 20240321212957.png]]

- Y por ultimo ejecutar

```
Dfsrmirg /setglobalstate 3
```

![[Pasted image 20240321213103.png]]

- Consultar por ultima vez con el comando:

```
Dfsrmig /getmigrationstate
```

![[Pasted image 20240321213204.png]]

# 3.  Desplegar a windows server como como controlador de dominio

- Nuevamente en el equipo con windows server 2019, volver a intentar desplegar el equipo como controlador de dominio, en este caso no deberia presentar error y seguir los pasos que se observan en las capturas

![[Pasted image 20240321213750.png]]

![[Pasted image 20240321213823.png]]Password DSRM: S0porte321

- Ubicarse en la opcion active directory users and computes y en la carpeta domain controllores se tendria que poder visualizar los contoladores de dominio (2008 y 2019)

![[Pasted image 20240321214027.png]]

- Ahora en la herramienta active ***directory domains and trusts*** hacer click derecho en el equipo y elegir la opcion ***raise domain funcional level***, se podra observar el mensaje de advertencia detallando que existe en el dominio una version avanzada de active directory
![[Pasted image 20240321214311.png]]


# 4-Chequear la replicacion entre ambos controladores

- entrar en tools administratives y en la misma elegir la herramienta Active Directory Sites and Services 
![[Pasted image 20240327212256.png]]

- En la misma despletar la el arbol de directorios de default-first-site-name, y al mismo tiempo desplegar ambos controladores de dominio y chequear en ambos su replicacion, haciendo click derecho en cada uno y seleccionando la opcion all tasks y luego check replicacion topology

![[Pasted image 20240327212522.png]]

![[Pasted image 20240327212530.png]]

- Un ejemplo practico para probar tb si replican entre servers es crear un usuario en el dc2008 y observar si se replico el mismo usuario en el dc 2019

# 5. Mover roles al equipo con windows server 2019

## - La movilizacion de roles se puede realizar de dos formas:
### 1. Con un solo comando
 Abrir una consola de powershell para poder ejecutar el comando 
 
```
netdom query fsmo
```

Para consultar nuevamente en donde estan ubicados los diversos roles antes de poder moverlos al nuevo controlador de dominio con el comando :

```
Move-ADDirectoryServerOperationMasterRole -Identity DCTEST2 -OperationMasterRole SchemaMaster, DomainNamingMaster, PDCEmulator, RIDMaster, InfrastructureMaster
```

![[Pasted image 20240321214742.png]]

### 2. Moviendo rol por rol

- Abrir consola de powershell en el server 2019 y colocar el comando:

```
ntdsutil
```
se desplegara una consola dentro de la misma herramienta

- En la misma colocar el comando el cual desplegara la consola de "fsmo maintenance":

```
roles
```

-  Ejecutar el comando:

```
connect to server "nombre del servidor 2019"
```

- luego de conectarse al mismo server se tiene que proceder a mover uno por uno los esquemas de cada rol ejecutando uno a uno los siguientes comandos:


```
Transfer infrastructure master
Transfer naming master
Transfer PDC
Transfer RID master
Transfer schema master
```

- luego de haber movido todos los roles se puede consultar donde se encuentran dichos roles con el comando:

```
netdom query fsmo
```


# 6. Desmonte del equipo con Windows server 2008

- Ubicarse en  el equipo con Windows server 2008 e ir a la herramienta active directory sites and services en la misma desglosar las carpetas ***default-first-site-name/servers/"nombre del viejo controlador"***, hacer click derecho y entrar en propiedades en la pestaña general destildar la opción que dice ***"Global Catalog"***

![[Pasted image 20240321223806.png]]

- De nuevo en en el equipo con Windows server 2019 ir a la herramienta ***active directory users and computers*** y en la carpeta domain controllers se podra visualizar ambos equipos y en la columna  DC Type se puede visualizar que el viejo controlador de dominio que figura como "DC" y el nuevo como "GC"
![[Pasted image 20240321223904.png]]

luego en la ventana de ejecutar poner "DCPROMO" y ahi se empezara a ejecutar la desinstalacion de el rol de active directory 

![[Pasted image 20240321224033.png]]
Nota: demora demasiado la desinstalacion

# 6. Elevacion de el nivel del dominio

- En el equipo con windows server 2019 ir a la herramienta ***active directory users an computers***, hacer click derecho y seleccionar la ***opcion raise domain functional level***

 - En la misma opción ya se puede visualizar un drop box para poder seleccionar el nuevo nivel de dominio 
 
![[Pasted image 20240321224438.png]]


- Luego en la herramienta ***Active domains and trusts*** seleccionar la misma opcion y seleccionar al nivel de bosque que quiere ir

![[Pasted image 20240321224544.png]]

- Luego de elegir el nivel no hay vuelta atras

![[Pasted image 20240321224950.png]]

- Y en las propiedades del equipo en la herramienta active directory users and computer se pueden visualizar ambos niveles
![[Pasted image 20240321225129.png]]


- herramienta para problemas :
ncutils

* Comandos post migración
	* Comando para ver desde un equipo con que servidor se autentica
		```
		 echo $logonserver
		```
	* 
Enlace:
[[Fundamentos]]

Fuentes:
https://www.youtube.com/watch?v=vuzrihbet1E