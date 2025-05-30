- En pocas palabras, a **Dominio windows** es un grupo de usuarios y computadoras bajo la administración de un negocio determinado. La idea principal detrás de un dominio es centralizar la administración de componentes comunes de una red informática de Windows en un único repositorio llamado **Directorio Activo (AD)**. El servidor que ejecuta los servicios de Active Directory se conoce como **Controlador de Dominio (DC)**.

![[Apuntes/Imagenes/Pasted image 20240327195302.png]]

- Las principales ventajas de tener un dominio de Windows configurado son:

	- **Gestión centralizada de la identidad:** Todos los usuarios de la red se pueden configurar desde Active Directory con el mínimo esfuerzo.
	- **Gestión de políticas de seguridad:** Puede configurar las políticas de seguridad directamente desde Active Directory y aplicarlas a usuarios y equipos en toda la red según sea necesario.

## **Active Directory**


﻿- El núcleo de cualquier dominio de Windows es el **Servicio de dominio de Active Directory (ANUNCIO DS)**. Este servicio actúa como un catálogo que contiene la información de todos los "objetos" que existen en su red. Entre los muchos objetos compatibles con AD, tenemos usuarios, grupos, máquinas, impresoras, acciones y muchos otros. Veamos algunos de ellos:
﻿
	﻿**_Usuarios_**

	- Los usuarios son uno de los tipos de objetos más comunes en Active Directory. Los usuarios son uno de los objetos conocidos como **principios de seguridad**, lo que significa que pueden ser autenticados por el dominio y se les pueden asignar privilegios **recursos** como archivos o impresoras. Se podría decir que un principal de seguridad es un objeto que puede actuar sobre los recursos en la red.

	- Los usuarios pueden ser utilizados para representar dos tipos de entidades:

		- **Personas:** los usuarios generalmente representarán a personas en su organización que necesitan acceder a la red, como los empleados.
		- **Servicios:** también puede definir usuarios para ser utilizados por servicios como IIS o MSSQL. Cada servicio requiere que un usuario se ejecute, pero los usuarios del servicio son diferentes de los usuarios habituales, ya que solo tendrán los privilegios necesarios para ejecutar su servicio específico.

	**_Máquinas_**

	- Las máquinas son otro tipo de objeto dentro de Active Directory; para cada computadora que se une al dominio de Active Directory, se creará un objeto de máquina. Las máquinas también se consideran "principales de seguridad" y se les asigna una cuenta como cualquier usuario habitual. Esta cuenta tiene derechos algo limitados dentro del propio dominio.

	- Las cuentas de la máquina en sí mismas son administradores locales en la computadora asignada, generalmente no se supone que nadie las acceda, excepto la computadora en sí, sino como con cualquier otra cuenta, si tiene la contraseña, puede usarla para iniciar sesión.

		**Nota:** Las contraseñas de la cuenta de la máquina se rotan automáticamente y generalmente se componen de 120 caracteres aleatorios.

	- Identificar cuentas de máquinas es relativamente fácil. Siguen un esquema de nombres específico. El nombre de la cuenta de la máquina es el nombre de la computadora seguido de un signo de dólar. Por ejemplo, una máquina llamada `DC01` tendrá una cuenta de máquina llamada `DC01$`.

## **Grupos de Seguridad**

- Si está familiarizado con Windows, probablemente sepa que puede definir grupos de usuarios para asignar derechos de acceso a archivos u otros recursos a grupos completos en lugar de usuarios individuales. Esto permite una mejor capacidad de administración, ya que puede agregar usuarios a un grupo existente y heredarán automáticamente todos los privilegios del grupo. Los grupos de seguridad también se consideran principios de seguridad y, por lo tanto, pueden tener privilegios sobre los recursos en la red.	 

- Los grupos pueden tener usuarios y máquinas como miembros. Si es necesario, los grupos también pueden incluir otros grupos.

- Varios grupos se crean de forma predeterminada en un dominio que se puede utilizar para otorgar privilegios específicos a los usuarios. Como ejemplo, estos son algunos de los grupos más importantes en un dominio:

| **Grupo de Seguridad**           | **Descripción**                                                                                                                                                                      |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Administradores de Dominio       | Los usuarios de este grupo tienen privilegios administrativos en todo el dominio. De forma predeterminada, pueden administrar cualquier computadora en el dominio, incluidas las DC. |
| Operadores de Servidores         | Los usuarios de este grupo pueden administrar Controladores de dominio. No pueden cambiar ninguna membresía administrativa del grupo.                                                |
| Operadores de Copia de Seguridad | Los usuarios de este grupo pueden acceder a cualquier archivo, ignorando sus permisos. Se utilizan para realizar copias de seguridad de datos en computadoras.                       |
| Operadores de Cuenta             | Los usuarios de este grupo pueden crear o modificar otras cuentas en el dominio.                                                                                                     |
| Usuarios de Dominio              | Incluye todas las cuentas de usuario existentes en el dominio.                                                                                                                       |
| Computadoras de Dominio          | Incluye todas las computadoras existentes en el dominio.                                                                                                                             |
| Controladores de Dominio         | Incluye todas las DC existentes en el dominio.                                                                                                                                       |
Puede obtener la lista completa de grupos de seguridad predeterminados de la [Documentación de microsoft](https://docs.microsoft.com/en-us/windows/security/identity-protection/access-control/active-directory-security-groups).

## **Usuarios y Computadoras de Active Directory**

- Para configurar usuarios, grupos o máquinas en Active Directory, debemos iniciar sesión en el Controlador de dominio y ejecutar "Usuarios y equipos de Active Directory" en el menú de inicio:

![[Apuntes/Imagenes/Pasted image 20240327202123.png]]

- Esto abrirá una ventana donde se puede ver la jerarquía de usuarios, ordenadores y grupos que existen en el dominio. Estos objetos están organizados en **Unidades Organizacionales (OU)** cuáles son objetos de contenedor que le permiten clasificar usuarios y máquinas. Las OU se utilizan principalmente para definir conjuntos de usuarios con requisitos policiales similares. Es probable que las personas en el departamento de ventas de su organización tengan un conjunto diferente de políticas aplicadas que las personas en TI, por ejemplo. Tenga en cuenta que un usuario solo puede ser parte de un solo OU a la vez.

- Comprobando nuestra máquina, podemos ver que ya hay un OU llamado `THM` con cuatro OU infantiles para los departamentos de TI, Gestión, Marketing y Ventas. Es muy típico ver que las OU imitan la estructura del negocio, ya que permite implementar de manera eficiente políticas de referencia que se aplican a departamentos completos. Recuerde que si bien este sería el modelo esperado la mayor parte del tiempo, puede definir OU arbitrariamente. Siéntase libre de hacer clic derecho en el `THM` OU y crear un nuevo OU debajo de él llamó `Students` solo por diversión.

![[Apuntes/Imagenes/Pasted image 20240327202214.png]]

- Si abre cualquier OU, puede ver los usuarios que contienen y realizar tareas simples como crearlos, eliminarlos o modificarlos según sea necesario. También puede restablecer las contraseñas si es necesario (bastante útil para el servicio de asistencia):

![[Apuntes/Imagenes/Pasted image 20240327202232.png]]

- Probablemente ya haya notado que hay otros contenedores predeterminados aparte del THM OU. Estos contenedores son creados por Windows automáticamente y contienen lo siguiente:

	- **Construido:** Contiene grupos predeterminados disponibles para cualquier host de Windows.
	- **Computadoras:** Cualquier máquina que se una a la red se colocará aquí de forma predeterminada. Puedes moverlos si es necesario.
	- **Controladores de Dominio:** Predeterminado OU eso contiene los DC en su red.
	- **Usuarios:** Usuarios y grupos predeterminados que se aplican a un contexto de todo el dominio.
	- **Cuentas de Servicio Administradas:** Posee cuentas utilizadas por los servicios en su dominio de Windows.

## **Grupos de Seguridad vs OUs**

- Probablemente se esté preguntando por qué tenemos grupos y OU. Si bien ambos se utilizan para clasificar usuarios y computadoras, sus propósitos son completamente diferentes:

	- **OUs** son útiles para **aplicación de políticas** a usuarios y computadoras, que incluyen configuraciones específicas que pertenecen a conjuntos de usuarios dependiendo de su rol particular en la empresa. Recuerde, un usuario solo puede ser miembro de una sola OU a la vez, ya que no tendría sentido tratar de aplicar dos conjuntos diferentes de políticas a un solo usuario.
	- **Grupos de Seguridad**, por otro lado, están acostumbrados a **conceder permisos sobre recursos**. Por ejemplo, usará grupos si desea permitir que algunos usuarios accedan a una carpeta compartida o impresora de red. Un usuario puede ser parte de muchos grupos, lo cual es necesario para otorgar acceso a múltiples recursos.


## **Administrar usuarios en AD**

Su primera tarea como nuevo administrador de dominio es verificar lo existente ANUNCIO OU y usuarios, ya que algunos cambios recientes le han sucedido al negocio. Se le ha dado el siguiente organigrama y se espera que realice cambios en el ANUNCIO para que coincida:

![[Apuntes/Imagenes/Pasted image 20240403193228.png]]

### **Eliminar OU y usuarios adicionales**

Lo primero que debe notar es que hay una OU de departamento adicional en su configuración de AD actual que no aparece en el gráfico. Nos han dicho que se cerró debido a recortes presupuestarios y que debería eliminarse del dominio. Si intenta hacer clic con el botón derecho y eliminar el OU, obtendrá el siguiente error:

![[Apuntes/Imagenes/Pasted image 20240403194013.png]]

Por defecto, las OU están protegidas contra la eliminación accidental. Para eliminar el OU, necesitamos habilitar el **Características Avanzadas** en el menú Ver:

![[Apuntes/Imagenes/Pasted image 20240403194037.png]]

Esto le mostrará algunos contenedores adicionales y le permitirá desactivar la protección de eliminación accidental. Para hacerlo, haga clic con el botón derecho en el OU y ve a Propiedades. Encontrará una casilla de verificación en la pestaña Objeto para deshabilitar la protección:

![[Apuntes/Imagenes/Pasted image 20240403194051.png]]

Asegúrese de desmarcar la casilla e intente eliminar el OU de nuevo. Se le pedirá que confirme que desea eliminar el OU, y como resultado, cualquier usuario, grupo u OU bajo él también será eliminado.

Después de eliminar el OU adicional, debe notar que para algunos de los departamentos, los usuarios en el AD no coinciden con los de nuestro organigrama. Cree y elimine usuarios según sea necesario para que coincidan con ellos.

### **Delegación** 

Una de las cosas buenas que puedes hacer en ANUNCIO es dar a usuarios específicos algún control sobre algunas OU. Este proceso se conoce como **delegación** y le permite otorgar a los usuarios privilegios específicos para realizar tareas avanzadas en OU sin necesidad de un Administrador de dominio para intervenir.

Uno de los casos de uso más comunes para esto es la concesión `IT support` los privilegios para restablecer las contraseñas de otros usuarios de bajo privilegio. Según nuestro organigrama, Phillip está a cargo del soporte de TI, por lo que probablemente querríamos delegarle el control de restablecer las contraseñas sobre las OU de Ventas, Marketing y Gestión.

Para este ejemplo, delegaremos el control sobre las ventas OU a Phillip. Para delegar el control sobre un OU, puede hacer clic derecho y seleccionar **Control de Delegados**:


![[Apuntes/Imagenes/Pasted image 20240403200700.png]]

Esto debería abrir una nueva ventana donde primero se le pedirá a los usuarios a los que desea delegar el control:

**Nota:** Para evitar escribir mal el nombre del usuario, escriba "phillip" y haga clic en el **Verificar nombres** botón. Windows autocompletará al usuario por usted.

![[Apuntes/Imagenes/Pasted image 20240403200715.png]]

Haga clic en Aceptar y, en el siguiente paso, seleccione la siguiente opción:

![[Apuntes/Imagenes/Pasted image 20240403200727.png]]

Haga clic a continuación un par de veces, y ahora Phillip debería poder restablecer las contraseñas para cualquier usuario en el departamento de ventas. Si bien es probable que desee repetir estos pasos para delegar los restablecimientos de contraseñas de los departamentos de Marketing y Gestión, lo dejaremos aquí para esta tarea. Usted es libre de continuar configurando el resto de las OU si así lo desea.



##  **Gestión de computadoras en AD** 

De forma predeterminada, todas las máquinas que se unen a un dominio (excepto las DC) se colocarán en el contenedor llamado "Computadoras". Si comprobamos nuestro DC, veremos que algunos dispositivos ya están allí:

![[Apuntes/Imagenes/Pasted image 20240403211355.png]]

Podemos ver algunos servidores, algunos portátiles y algunos PC correspondientes a los usuarios de nuestra red. Tener todos nuestros dispositivos no es la mejor idea, ya que es muy probable que desee diferentes políticas para sus servidores y las máquinas que los usuarios habituales utilizan a diario.

Si bien no existe una regla de oro sobre cómo organizar sus máquinas, un excelente punto de partida es segregar los dispositivos de acuerdo con su uso. En general, esperaría ver dispositivos divididos en al menos las tres categorías siguientes:

**1. Estaciones de trabajo**

Las estaciones de trabajo son uno de los dispositivos más comunes dentro de un dominio de Active Directory. Es probable que cada usuario en el dominio inicie sesión en una estación de trabajo. Este es el dispositivo que usarán para hacer su trabajo o actividades normales de navegación. Estos dispositivos nunca deben tener un usuario privilegiado iniciado sesión en ellos.

**2. Servidores**

Los servidores son el segundo dispositivo más común dentro de un dominio de Active Directory. Los servidores se utilizan generalmente para proporcionar servicios a los usuarios u otros servidores.

**3. Controladores de Dominio**

Los controladores de dominio son el tercer dispositivo más común dentro de un dominio de Active Directory. Los controladores de dominio le permiten administrar el dominio de Active Directory. Estos dispositivos a menudo se consideran los dispositivos más sensibles dentro de la red, ya que contienen contraseñas hash para todas las cuentas de usuario dentro del entorno.

Como estamos ordenando nuestro AD, creemos dos OU separadas para `Workstations` y `Servers` (Los controladores de dominio ya están en un OU creado por Windows). Los crearemos directamente bajo el `thm.local` contenedor de dominio. Al final, debe tener lo siguiente OU estructura:

![[Apuntes/Imagenes/Pasted image 20240403211456.png]]


Ahora, mueva las computadoras personales y las computadoras portátiles a las estaciones de trabajo OU y los servidores a los servidores OU desde el contenedor de Computadoras. Hacerlo nos permitirá configurar políticas para cada uno OU más tarde.


## **Políticas del Grupo**

Hasta ahora, hemos organizado usuarios y computadoras en OU solo por el bien de él, pero la idea principal detrás de esto es poder implementar diferentes políticas para cada uno OU individualmente. De esa manera, podemos enviar diferentes configuraciones y líneas de base de seguridad a los usuarios dependiendo de su departamento.

Windows gestiona dichas políticas a través de **Objetos de Política de Grupo (GPO)**. Los GPO son simplemente una colección de configuraciones que se pueden aplicar a las OU. Los GPO pueden contener políticas dirigidas a usuarios o computadoras, lo que le permite establecer una línea de base en máquinas e identidades específicas.

Para configurar los GPO, puede usar el **Gestión de Políticas de Grupo** herramienta, disponible en el menú de inicio:

![[Apuntes/Imagenes/Pasted image 20240403211535.png]]

Lo primero que verá al abrirlo es su completo OU jerarquía, como se definió antes. Para configurar las Políticas de grupo, primero cree un GPO bajo **Objetos de Política de Grupo** y luego vincularlo a la OU donde desea que se apliquen las políticas. Como ejemplo, puede ver que hay algunos GPO ya existentes en su máquina:

![[Apuntes/Imagenes/Pasted image 20240403211545.png]]

Podemos ver en la imagen de arriba que se han creado 3 GPO. De esos, el `Default Domain Policy` y `RDP Policy` están vinculados a la `thm.local` dominio en su conjunto, y el `Default Domain Controllers Policy` está vinculado al `Domain Controllers` OU sólo. Algo importante a tener en cuenta es que cualquier GPO se aplicará a los vinculados OU y cualquier sub-OU bajo él. Por ejemplo, el `Sales` OU seguirá siendo afectado por el `Default Domain Policy`.

Examinemos el `Default Domain Policy` para ver lo que hay dentro de un GPO. La primera pestaña que verá al seleccionar un GPO muestra su **alcance**, que es donde el GPO está vinculado en el ANUNCIO. Para la política actual, podemos ver que solo se ha vinculado a la `thm.local` dominio:

![[Apuntes/Imagenes/Pasted image 20240403211555.png]]

Como puede ver, también puede aplicar **Filtrado de Seguridad** a los GPO para que solo se apliquen a usuarios/computadoras específicos bajo un OU. Por defecto, se aplicarán a la **Usuarios Autenticados** grupo, que incluye todos los usuarios/PC.

El **Configuración** la pestaña incluye el contenido real de la GPO y nos permite saber qué configuraciones específicas aplica. Como se indicó antes, cada uno GPO tiene configuraciones que se aplican solo a computadoras y configuraciones que se aplican solo a usuarios. En este caso, el `Default Domain Policy` solo contiene Configuraciones de Ordenador:

![[Apuntes/Imagenes/Pasted image 20240403211607.png]]

Siéntase libre de explorar el GPO y ampliar los elementos disponibles utilizando los enlaces "mostrar" en el lado derecho de cada configuración. En este caso, el `Default Domain Policy` indica configuraciones realmente básicas que deberían aplicarse a la mayoría de los dominios, incluidas las políticas de bloqueo de contraseñas y cuentas:

![[Apuntes/Imagenes/Pasted image 20240403211627.png]]

Dado que este GPO se aplica a todo el dominio, cualquier cambio en él afectaría a todas las computadoras. Cambiemos la política de longitud de contraseña mínima para exigir a los usuarios que tengan al menos 10 caracteres en sus contraseñas. Para hacer esto, haga clic derecho en el GPO y seleccionar **Editar**:

![[Apuntes/Imagenes/Pasted image 20240403211636.png]]

Esto abrirá una nueva ventana donde podremos navegar y editar todas las configuraciones disponibles. Para cambiar la longitud mínima de la contraseña, vaya a `Computer Configurations -> Policies -> Windows Setting -> Security Settings -> Account Policies -> Password Policy` y cambiar el valor de la política requerida:


![[Apuntes/Imagenes/Pasted image 20240403211647.png]]

Como puede ver, se pueden establecer muchas políticas en un GPO. Si bien explicar cada uno de ellos sería imposible en una sola habitación, siéntase libre de explorar un poco, ya que algunas de las políticas son sencillas. Si se necesita más información sobre cualquiera de las políticas, puede hacer doble clic en ellas y leer el **Explicar** pestaña en cada uno de ellos:

![[Apuntes/Imagenes/Pasted image 20240403211659.png]]

### **GPO distribución** 

Los GPO se distribuyen a la red a través de un recurso compartido de red llamado `SYSVOL`, que se almacena en el DC. Todos los usuarios de un dominio generalmente deben tener acceso a este recurso compartido a través de la red para sincronizar sus GPO periódicamente. El recurso compartido SYSVOL apunta de forma predeterminada al `C:\Windows\SYSVOL\sysvol\` directorio en cada uno de los DC en nuestra red.

Una vez que se ha realizado un cambio en cualquier GPO, las computadoras pueden tardar hasta 2 horas en ponerse al día. Si desea forzar a cualquier computadora en particular a sincronizar sus GPO inmediatamente, siempre puede ejecutar el siguiente comando en la computadora deseada:


```
PS C:\> gpupdate /force
```

## **Métodos de Autenticación**

Cuando se usan dominios de Windows, todas las credenciales se almacenan en los Controladores de dominio. Siempre que un usuario intente autenticarse en un servicio utilizando credenciales de dominio, el servicio deberá pedirle al Controlador de dominio que verifique si son correctos. Se pueden usar dos protocolos para la autenticación de red en dominios de Windows:

- **Kerberos:** Utilizado por cualquier versión reciente de Windows. Este es el protocolo predeterminado en cualquier dominio reciente.
- **NetNTLM:** Protocolo de autenticación heredado mantenido con fines de compatibilidad.

Si bien NetNTLM debe considerarse obsoleto, la mayoría de las redes tendrán habilitados ambos protocolos. Echemos un vistazo más profundo a cómo funciona cada uno de estos protocolos.

### **Kerberos Autenticación**

Kerberos la autenticación es el protocolo de autenticación predeterminado para cualquier versión reciente de Windows. Usuarios que inician sesión en un servicio utilizando Kerberos se asignarán boletos. Piense en los tickets como prueba de una autenticación anterior. Los usuarios con tickets pueden presentarlos a un servicio para demostrar que ya se han autenticado en la red antes y, por lo tanto, están habilitados para usarlo.

Cuando Kerberos se utiliza para la autenticación, ocurre el siguiente proceso:

1. El usuario envía su nombre de usuario y una marca de tiempo cifrada utilizando una clave derivada de su contraseña a la **Centro de Distribución de Claves (KDC)**, un servicio generalmente instalado en el Controlador de dominio a cargo de crear Kerberos tickets en la red.
    
    El KDC creará y enviará de vuelta un **Boleto de Concesión de Boleto (TGT)**, lo que permitirá al usuario solicitar tickets adicionales para acceder a servicios específicos. La necesidad de un boleto para obtener más boletos puede sonar un poco extraño, dijo, pero permite a los usuarios solicitar tickets de servicio sin pasar sus credenciales cada vez que desean conectarse a un servicio. Junto con el TGT, a **Clave de Sesión** se entrega al usuario, que necesitará para generar las siguientes solicitudes.
    
    Observar el TGT está encriptado usando el **krbtgt** hash de contraseña de la cuenta y, por lo tanto, el usuario no puede acceder a su contenido. Es esencial saber que el cifrado TGT incluye una copia de la clave de sesión como parte de su contenido, y el KDC no necesita almacenar la clave de sesión, ya que puede recuperar una copia descifrando el TGT si es necesario.

![[Apuntes/Imagenes/Pasted image 20240403212158.png]]

2. Cuando un usuario desea conectarse a un servicio en la red como un recurso compartido, sitio web o base de datos, utilizará su TGT para pedir al KDC un **Servicio de Concesión de Entradas (TGS)**. TGS son tickets que permiten la conexión solo al servicio específico para el que fueron creados. Para solicitar un TGS, el usuario enviará su nombre de usuario y una marca de tiempo cifrada utilizando la Clave de sesión, junto con el TGT y a **Nombre Principal del Servicio (SPN),** lo que indica el servicio y el nombre del servidor al que pretendemos acceder.
    
    Como resultado, el KDC nos enviará un TGS junto con un **Clave de Sesión de Servicio**, que necesitaremos autenticar al servicio al que queremos acceder. El TGS se cifra utilizando una clave derivada del **Propietario de Servicio Hash**. El Propietario del Servicio es la cuenta de usuario o máquina en la que se ejecuta el servicio. El TGS contiene una copia de la Clave de Sesión de Servicio en sus contenidos cifrados para que el Propietario del Servicio pueda acceder a ella descifrando el TGS.

![[Apuntes/Imagenes/Pasted image 20240403212232.png]]

3. El TGS se puede enviar al servicio deseado para autenticar y establecer una conexión. El servicio utilizará el hash de contraseña de su cuenta configurada para descifrar el TGS y validar la Clave de Sesión de Servicio.
![[Apuntes/Imagenes/Pasted image 20240403212254.png]]

### **Autenticación NetNTLM**

NetNTLM funciona utilizando un mecanismo de desafío-respuesta. Todo el proceso es el siguiente:


![[Apuntes/Imagenes/Pasted image 20240403212320.png]]

1. El cliente envía una solicitud de autenticación al servidor al que desea acceder.
2. El servidor genera un número aleatorio y lo envía como un desafío para el cliente.
3. El cliente combina su NTLM hash de contraseña con el desafío (y otros datos conocidos) para generar una respuesta al desafío y enviarlo de vuelta al servidor para su verificación.
4. El servidor reenvía el desafío y la respuesta al Controlador de dominio para su verificación.
5. El controlador de dominio utiliza el desafío para recalcular la respuesta y la compara con la respuesta original enviada por el cliente. Si ambos coinciden, el cliente se autentica; de lo contrario, se niega el acceso. El resultado de la autenticación se envía de vuelta al servidor.
6. El servidor reenvía el resultado de autenticación al cliente.

Tenga en cuenta que la contraseña (o hash) del usuario nunca se transmite a través de la red por seguridad.

**Nota:** El proceso descrito se aplica cuando se utiliza una cuenta de dominio. Si se utiliza una cuenta local, el servidor puede verificar la respuesta al desafío en sí sin requerir interacción con el controlador de dominio, ya que tiene el hash de contraseña almacenado localmente en su SAM.



## **Trees, Forests and Trusts**

Hasta ahora, hemos discutido cómo administrar un solo dominio, el rol de un Controlador de Dominio y cómo se une a las computadoras, servidores y usuarios.

![[Apuntes/Imagenes/Pasted image 20240403212423.png]]

A medida que las empresas crecen, también lo hacen sus redes. Tener un solo dominio para una empresa es lo suficientemente bueno como para comenzar, pero con el tiempo algunas necesidades adicionales podrían empujarlo a tener más de uno.

### **Tree**

Imagine, por ejemplo, que de repente su empresa se expande a un nuevo país. El nuevo país tiene diferentes leyes y regulaciones que requieren que actualice sus GPO para cumplir. Además, ahora tiene personas de TI en ambos países, y cada equipo de TI necesita administrar los recursos que corresponden a cada país sin interferir con el otro equipo. Mientras que usted podría crear un complejo OU estructurar y utilizar delegaciones para conseguirlo, teniendo un enorme ANUNCIO la estructura puede ser difícil de manejar y propensa a errores humanos.

Afortunadamente para nosotros, Active Directory admite la integración de múltiples dominios para que pueda dividir su red en unidades que se pueden administrar de forma independiente. Si tiene dos dominios que comparten el mismo espacio de nombres (`thm.local` en nuestro ejemplo), esos dominios se pueden unir en un **Árbol**.

Si nuestro `thm.local` el dominio se dividió en dos subdominios para las sucursales del Reino Unido y los Estados Unidos, podría construir un árbol con un dominio raíz de `thm.local` y dos subdominios llamados `uk.thm.local` y `us.thm.local`, cada uno con su ANUNCIO, computadoras y usuarios:

![[Apuntes/Imagenes/Pasted image 20240403212458.png]]

Esta estructura dividida nos da un mejor control sobre quién puede acceder a qué en el dominio. La gente de TI del Reino Unido tendrá su propio DC que administra solo los recursos del Reino Unido. Por ejemplo, un usuario del Reino Unido no podría administrar usuarios de los Estados Unidos. De esa manera, los Administradores de Dominio de cada sucursal tendrán control completo sobre sus respectivos DC, pero no sobre los DC de otras sucursales. Las políticas también se pueden configurar de forma independiente para cada dominio en el árbol.

Es necesario introducir un nuevo grupo de seguridad cuando se habla de árboles y bosques. El **Administradores de Empresas** group otorgará privilegios administrativos a un usuario sobre todos los dominios de una empresa. Cada dominio todavía tendría sus Administradores de dominio con privilegios de administrador sobre sus dominios individuales y los Administradores de empresa que pueden controlar todo en la empresa.

### **Forest**

Los dominios que administra también se pueden configurar en diferentes espacios de nombres. Supongamos que su empresa continúa creciendo y eventualmente adquiere otra empresa llamada `MHT Inc.` Cuando ambas compañías se fusionen, probablemente tendrá diferentes árboles de dominio para cada compañía, cada uno administrado por su propio departamento de TI. La unión de varios árboles con diferentes espacios de nombres en la misma red se conoce como **bosque**.

![[Apuntes/Imagenes/Pasted image 20240403212628.png]]

### **Relaciones de Confianza**

Tener múltiples dominios organizados en árboles y bosques le permite tener una buena red compartimentada en términos de gestión y recursos. Pero en cierto punto, un usuario en THM Reino Unido podría necesitar acceder a un archivo compartido en uno de los servidores de MHT ASIA. Para que esto suceda, los dominios dispuestos en árboles y bosques se unen por **relaciones de confianza**.

En términos simples, tener una relación de confianza entre dominios le permite autorizar a un usuario del dominio `THM UK` para acceder a recursos desde el dominio `MHT EU`.

La relación de confianza más simple que se puede establecer es una **relación de confianza unidireccional**. En un fideicomiso unidireccional, si `Domain AAA` fideicomisos `Domain BBB`, ésto significa que un usuario en BBB puede ser autorizado para acceder a recursos en AAA:

![[Apuntes/Imagenes/Pasted image 20240403212700.png]]


La dirección de la relación de confianza unidireccional es contraria a la dirección de acceso.

**Relaciones de confianza bidireccionales** también se puede hacer para permitir que ambos dominios autoricen mutuamente a los usuarios del otro. Por defecto, unir varios dominios debajo de un árbol o un bosque formará una relación de confianza bidireccional.

Es importante tener en cuenta que tener una relación de confianza entre dominios no otorga automáticamente acceso a todos los recursos en otros dominios. Una vez que se establece una relación de confianza, tiene la oportunidad de autorizar a los usuarios en diferentes dominios, pero depende de usted lo que realmente está autorizado o no.

