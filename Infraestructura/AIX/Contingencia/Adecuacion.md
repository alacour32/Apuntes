- ### Preparación de equipo de contingencia
	
	- Se hace backup de la carpeta /opt/sap, excluyendo la carpeta data y backup (lo probado y conveniente es filezilla)
	- luego se desmontan los lv: sapsystemlv y sapbackuplv: 
	```bash
		umount sapsystemlv
		umount sapbackuplv
	```
	- Luego crear nuevo punto de montaje :
	```bash
			mkdir /sybase
			mkdir /sybase/data
	```
	- Hacer una carpeta sybase_old en /sybase
			mkdir /sybase/sybase_old
	- Copiar el contenido del backup anterior mente hecho de /opt/sap en /sybase/sybase_old
	- Cambiar los permisos del contenido de la carpeta sybase_old
	```bash
			chown -R sap:adm /sybase_old
			chown root:system /lost+found
	```
	- volver a montar el sapsystemlv en el nuevos punto de montaje
	```bash
			mount /dev/SAPsystemLv /sybase/data/
	```
	- pasar la configuracion del motor de la base de /sybase/data/data/  a  /sybase/data/
	```bash
			mv /sybase/data/data/MIC/ /sybase/data/
			mv /sybase/data/data/TCM/ /sybase/data/
			mv /sybase/data/data/dbccdb/ /sybase/data/
			mv /sybase/data/data/deposito/ /sybase/data/
			mv /sybase/data/data/empty /sybase/data/
			mv /sybase/data/data/master.dat /sybase/data/
			mv /sybase/data/data/sybsysdb.dat /sybase/data/
			mv /sybase/data/data/sysprocs.dat /sybase/data/
			mv /sybase/data/data/tempdbdev.dat /sybase/data/
			
	```
	- Ahora montar el lv SAPbackupLv en  /sybase/data/backup
	```bash
			mount /dev/SAPbackupLv /sybase/backup
	```
	- Edita el archivo filesystems ubicado en /etc
		```bash
			vi /etc/filesystems
		```
		- El contenido del archivo debe quedar asi:
		```bash
				* @(#)filesystems @(#)29        1.23  src/bos/etc/filesystems/filesystems, cmdfs, bos730, initial_extract 8/16/07 17:18:35
		* IBM_PROLOG_BEGIN_TAG
		* This is an automatically generated prolog.
		*
		* bos730 src/bos/etc/filesystems/filesystems 1.23
		*
		* Licensed Materials - Property of IBM
		*
		* COPYRIGHT International Business Machines Corp. 1985,2007
		* All Rights Reserved
		*
		* US Government Users Restricted Rights - Use, duplication or
		* disclosure restricted by GSA ADP Schedule Contract with IBM Corp.
		*
		* IBM_PROLOG_END_TAG
		*
		* COMPONENT_NAME: CMDFS
		*
		* FUNCTIONS: none
		*
		* ORIGINS: 27
		*
		* (C) COPYRIGHT International Business Machines Corp. 1985, 1993
		* All Rights Reserved
		* Licensed Materials - Property of IBM
		*
		* US Government Users Restricted Rights - Use, duplication or
		* disclosure restricted by GSA ADP Schedule Contract with IBM Corp.
		*
		*
		*
		* This version of /etc/filesystems assumes that only the root file system
		* is created and ready.  As new file systems are added, change the check,
		* mount, free, log, vol and vfs entries for the appropriate stanza.
		*
		
		/:
		        dev             = /dev/hd4
		        vfs             = jfs2
		        log             = /dev/hd8
		        mount           = automatic
		        check           = false
		        type            = bootfs
		        vol             = root
		        free            = true
		
		/home:
		        dev       = /dev/hd1
		        vol       = "/home"
		        mount     = true
		        check     = true
		        free      = false
		        vfs       = jfs2
		        log       = /dev/hd8
		
		/usr:
		        dev             = /dev/hd2
		        vfs             = jfs2
		        log             = /dev/hd8
		        mount           = automatic
		        check           = false
		        type            = bootfs
		        vol             = /usr
		        free            = false
		
		/var:
		        dev             = /dev/hd9var
		        vfs             = jfs2
		        log             = /dev/hd8
		        mount           = automatic
		        check           = false
		        type            = bootfs
		        vol             = /var
		        free            = false
		
		/tmp:
		        dev       = /dev/hd3
		        vol       = "/tmp"
		        mount     = automatic
		        check     = false
		        free      = false
		        vfs       = jfs2
		        log       = /dev/hd8
		
		/admin:
		        dev       = /dev/hd11admin
		        vol       = "/admin"
		        mount     = true
		        check     = false
		        free      = false
		        vfs       = jfs2
		        log       = /dev/hd8
		
		/proc:
		        dev       = /proc
		        vol       = "/proc"
		        mount     = true
		        check     = false
		        free      = false
		        vfs       = procfs
		
		/opt:
		        dev       = /dev/hd10opt
		        vol       = "/opt"
		        mount     = true
		        check     = true
		        free      = false
		        vfs       = jfs2
		        log       = /dev/hd8
		
		/var/adm/ras/livedump:
		        dev             = /dev/livedump
		        vfs             = jfs2
		        log             = /dev/hd8
		        mount           = true
		        account         = false
		
		/sybase/data:
		        dev             = /dev/SAPsystemLv
		        vfs             = jfs2
		        log             = INLINE
		        mount           = true
		        check           = false
		        account         = false
		
		/sybase/backup:
		        dev             = /dev/SAPbackupLv
		        vfs             = jfs2
		        log             = INLINE
		        mount           = true
		        check           = false
		        account         = false
		
		```
- ### POSIBLES HERRAMIENTAS A USAR:
	- Para ver que usuario esta utilizando el punto de montaje
	```bash
			fuser -cuV  "punto de montaje"
	```
	- Eliminar proceso que utiliza punto de montaje:
	```bash
			fuser -k  "punto de montaje"
	```