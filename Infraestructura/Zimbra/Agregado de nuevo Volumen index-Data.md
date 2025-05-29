Para incorporar un nuevo disco virtual a un servidor Zimbra que ya tiene 3 volúmenes definidos, y que este nuevo volumen será utilizado tanto para `store` como para `index`, puedes seguir los siguientes pasos tanto por terminal como por la consola de administración de Zimbra.


### **Por Terminal (CLI)**
Nota: ser paciente hasta que se actualice el espacio en disco luego de haberlo ampliado con el vcenter
*  en caso de no actualizarce ejecutar:
```bash
	 echo 1 > /sys/class/block/sdx/ device/rescan 
```
- o se pued utilizar:
```bash
	 for i in /sys/class/scsi_host/host*; do echo "- - -" > "$i/scan"; done
```

1. **Preparar el nuevo disco virtual:**
    
    - Asegúrate de que el nuevo disco virtual esté montado y disponible en el sistema. Puedes verificar esto con el comando `df -h` o `lsblk`.
        
    - Si el disco no está montado, montalo en un directorio específico:
	```bash
		    mkfs.ext4 /dev/sdx
		    mkdir -p /"punto de montaje"
		    mount /dev/sdb1 /"punto de montaje"
	```
        
2. **Crear los directorios necesarios:**
    
    - Crea los directorios para `store` y `index` en el nuevo disco:
                 
```bash
        mkdir -p /mnt/new_disk/store
        mkdir -p /mnt/new_disk/index
```
        
3. **Cambiar los permisos:**
    
    - Asegúrate de que los directorios tengan los permisos correctos para que Zimbra pueda acceder a ellos:
        
         
```bash
        chown -R zimbra:zimbra /mnt/new_disk/store
        chown -R zimbra:zimbra /mnt/new_disk/index
```
        
4. **Configurar el nuevo volumen en Zimbra:**
    
    - Ejecuta los siguientes comandos como usuario `zimbra`:
               
```bash
      su - zimbra
      zmprov ms `zmhostname` +zimbraVolumePath /mnt/new_disk/store
	  zmprov ms `zmhostname` +zimbraVolumePath /mnt/new_disk/index
```
        
5. **Verificar la configuración:**
    
    - Verifica que los nuevos volúmenes hayan sido agregados correctamente:
        
```bash
         zmprov gs `zmhostname` zimbraVolumePath
```
        
6. **Mover los datos (opcional):**
    
    - Si deseas mover los datos existentes al nuevo volumen, puedes usar el comando `zmmailboxdctl` para mover los datos de `store` y `index` al nuevo volumen.
        

### **Por Consola de Administración (Web)**

1. **Acceder a la consola de administración:**
    
    - Inicia sesión en la consola de administración de Zimbra ([https://tudominio.com:7071](https://tudominio.com:7071/)).
        
2. **Navegar a la configuración del servidor:**
    
    - Ve a `Configuración` > `Servidores`.
        
    - Selecciona el servidor al que deseas agregar el nuevo volumen.
        
3. **Agregar el nuevo volumen:**
    
    - En la sección `Volúmenes`, haz clic en `Agregar Volumen`.
        
    - Especifica la ruta del nuevo volumen para `store` y `index` (por ejemplo, `/mnt/new_disk/store` y `/mnt/new_disk/index`).
        
    - Guarda los cambios.
        
4. **Verificar la configuración:**
    
    - Verifica que los nuevos volúmenes aparezcan en la lista de volúmenes del servidor.
        
5. **Mover los datos (opcional):**
    
    - Si deseas mover los datos existentes al nuevo volumen, puedes usar la opción de mover datos desde la consola de administración o desde la terminal como se mencionó anteriormente.
        

### **Consideraciones Finales**

- **Espacio y rendimiento:** Asegúrate de que el nuevo disco tenga suficiente espacio y que esté optimizado para el rendimiento, especialmente si se va a utilizar para `index`, que puede ser intensivo en operaciones de I/O.
    
- **Backup:** Antes de realizar cambios importantes, siempre es recomendable hacer un backup de tu configuración y datos de Zimbra.
    
- **Pruebas:** Si es posible, realiza pruebas en un entorno de desarrollo antes de aplicar los cambios en producción.
  

