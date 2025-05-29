* Nota: ser paciente hasta que se actualice el espacio en disco luego de haberlo ampliado con el vcenter
*  en caso de no actualizarce ejecutar:
```bash
	 echo 1 > /sys/class/block/sdx/ device/rescan 
```
- o se pued utilizar:
```bash
	 for i in /sys/class/scsi_host/host*; do echo "- - -" > "$i/scan"; done
```

### Paso 1: Verificar el Espacio Libre en el Disco

Primero, verifica el espacio libre en tu disco. Esto te ayudará a determinar cuánto espacio puedes añadir al VG.

```
sudo fdisk -l /dev/sdX
```

Reemplaza `/dev/sdX` con el nombre de tu disco.

### Paso 2: Ampliar la Partición (si es necesario)

Si todo el espacio del disco aún no está asignado a una partición, necesitas ampliar la partición existente o crear una nueva.

1. **Usar `fdisk` para modificar la tabla de particiones**:
        
    `sudo fdisk /dev/sdX`
    
    Dentro de `fdisk`:
    
    - **Eliminar la partición existente (sin borrar los datos)**: Esto es seguro siempre y cuando no formatees o borres los datos. Solo cambia el tamaño de la partición.
    - **Crear una nueva partición que use todo el espacio disponible**.
    - **Cambiar el tipo de partición a LVM** (si es necesario).
    - **Escribir los cambios y salir**: `w`.

* O utilizar el comando `parted`
```
parted /dev/sda
resizepart NUMBER END`
quit
```
Reemplaza `NUMBER` con el número de la partición y `END` con el tamaño final (por ejemplo, `100%`).
### Paso 3: Extender el Espacio al VG

Una vez que tengas el espacio disponible en la partición, añádelo al VG.

```
sudo vgextend vg_name /dev/sdX1
```

Reemplaza `/dev/sdX1` con el nombre de la partición que has ampliado. (en el caso de dar un error de que la particion no puede asignar el espacion libre, reiniciar el equipo)

### Paso 4: Verificar el VG

Verifica que el VG reconozca el espacio adicional.

```
sudo vgdisplay vg_name
```

Reemplaza `vg_name` con el nombre de tu VG.

### Paso 5: Ampliar el LV (si es necesario)

Si necesitas más espacio en un LV específico, amplíalo utilizando `lvextend`.

```
sudo lvextend -l +100%FREE /dev/vg_name/lv_name
```

Reemplaza `vg_name` con el nombre de tu VG y `lv_name` con el nombre de tu LV.

### Paso 6: Redimensionar el Sistema de Archivos (si es necesario)

Si has ampliado un LV que contiene un sistema de archivos, deberás redimensionar el sistema de archivos para que utilice el nuevo espacio.

- **Para XFS**:
           
    `sudo xfs_growfs /mount/point`
    
    Reemplaza `/mount/point` con el punto de montaje del sistema de archivos XFS.
    
- **Para ext4 u otro sistema de archivos**:
           
    `sudo resize2fs /dev/vg_name/lv_name`
    

### Paso 7: Verificar

Verifica que el proceso fue exitoso revisando el tamaño del LV y el espacio disponible en el sistema de archivos.

```
sudo lvdisplay /dev/vg_name/lv_name df -h /mount/point`
```