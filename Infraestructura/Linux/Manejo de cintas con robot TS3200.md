- Solicitar cinta a operaciones para que traigan de hamburgo
- Una ves en pocesion de la cinta colocar en el drive 2 del robot de cintas viejo (TS3200)
	NOTA: para comprobar en que drive hay que colocar la cinta verificarlo en el brocade especificamente en los mienbros de la zona
	
- Acceder por ssh a la vm en el power 8 donde se llama BSE_REDHAT (hostname: bcksrv)
- Ubicarse en el path "/usr/local/bcktape"
- Ejecutar el script bcktape 

```
	./bcktape
```

![[Pasted image 20240517194210.png]]
- Argumentos para utilizar con el comando:

	- **./bcktape backup**: Realiza un backup del directorio PARAMETRO1 a la unidad PARAMETRO2. Con descripcion PARAMETROS Ej: bcktape backup  /etc   /dev/st0 M_BSE DCHSARE
	  NOTA: En la descripcion se tomara on cuenta la prisara letra "M" como Mensual y no se podra volver
	-  **./bcktape backup:** Realiza un backup del directo backup del directorio PARAMETRO1 a DCHSARE la unidad PARAMETRO2. Con descripcion PARAMETROS
	  NOTA: Es la misma operacion que backup, pero backup/etc/dev/stbackup, pero onite la comprobacion si es Mensual. Ej: bcktaps
	-  **./bcktape info:**   Muetra informacion sobre la cinta insertada en la unidad PARAMETRO1
       Ej: bcktape info /dev/st0
	 - **./bcktape  lista:** Muestra la lista de archivos de la cinta insertada.
    	Ej: bcktape lista /dev/st0
        bcktape lista /dev/st0 | grep -i Archivo_de_Excel.xls
	- **./bcktape restaurar:** Restaura en la carpeta PARAMETRO01 la carpeta o archivo PARAMETRO2.
     Ej: bcktape restaurar /data/restaurados  data/servidores/bseshare/c/sistemas/documentos/proyecto.doc /dev/st0
- Antes de recuperar verificar que haya espacio en donde en la particion con el comando 
```
 df
```

![[Pasted image 20240517194112.png]]
