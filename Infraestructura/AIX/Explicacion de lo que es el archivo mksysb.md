### **¿Qué es `mksysb` en AIX?**

`mksysb` es una utilidad de AIX que genera una copia de seguridad del sistema raíz (`/`), permitiendo restaurar o clonar sistemas. Su principal función es crear una imagen bootable con todos los archivos del sistema operativo, incluyendo configuraciones y paquetes instalados.

---

### **¿Qué contiene una imagen `mksysb`?**

Un `mksysb` es básicamente una imagen de backup de un sistema AIX. Dentro de esta imagen se encuentran:

1. **El Boot Image**
    - Permite que el sistema arranque en caso de restauración desde un medio como cinta, DVD o red.
2. **El Volume Group Information (`vginfo`)**
    - Contiene los metadatos sobre los discos y volúmenes lógicos.
3. **El Archivo `bosinst.data`**
    - Controla el comportamiento de la restauración, como si se hará un "overwrite install" o una clonación.
4. **El Archivo `image.data`**
    - Define la estructura de los volúmenes lógicos, discos y sistema de archivos.
5. **El Backup de los archivos del sistema (`/`, `/usr`, `/var`, `/home`)**
    - Excluye `/tmp`, `/proc`, y otros directorios temporales.

---

### **¿Qué pasa al crear un nuevo `mksysb`?**

6. **No afecta a los anteriores**:
    
    - Puedes tener múltiples imágenes `mksysb` almacenadas en el servidor NIM sin que se sobrescriban entre sí, a menos que guardes el nuevo backup con el mismo nombre en la misma ubicación.
7. **Impacto en la LPAR origen**:
    
    - `mksysb` es un proceso de lectura, por lo que no altera ni afecta el sistema que se está respaldando.
    - Puede generar una carga de I/O en el sistema, pero sigue funcionando normalmente.

---

### **¿Qué le hace `mksysb` a la LPAR origen?**

- Toma una foto exacta del sistema en ese momento.
- No la reinicia ni la modifica.
- No afecta procesos en ejecución (pero puede consumir recursos).

---

### **¿Cómo se usa `mksysb` en la práctica?**

8. Para crear una imagen `mksysb` local en la LPAR:
    
	```sh
    mksysb -i /backup/mksysb_lpar1
	```
    
9. Para definir la imagen `mksysb` en un servidor NIM:
    
	```sh
    nim -o define -t mksysb -a server=master -a location=/nim/mksysb/lpar1.mksysb lpar1_mksysb
	```
    
10. Para restaurar una LPAR desde `mksysb`:
    
	```sh
    nim -o bos_inst -a source=mksysb -a spot=<nombre_del_spot> lpar1
	```
    

Si necesitas más detalles sobre cómo restaurar o clonar un sistema, dime qué estás intentando hacer con `mksysb`.