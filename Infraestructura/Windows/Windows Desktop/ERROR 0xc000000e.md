El error **0xc000000e** indica que Windows no puede encontrar el dispositivo de arranque correcto. Esto suele ocurrir después de clonar un disco si la configuración de arranque no es correcta. Aquí hay algunos pasos para solucionarlo:

### 1. Verificar la configuración del BIOS/UEFI

- Accede al BIOS/UEFI presionando **ESC, F2, F12 o SUPR** (según el fabricante).
- Verifica que el disco clonado esté seleccionado como **dispositivo de arranque principal**.
- Si el sistema original usaba **UEFI**, asegúrate de que el modo de arranque no haya cambiado a **Legacy** (o viceversa).

### 2. Reconstruir el gestor de arranque (BCD)

Si la clonación no copió correctamente el sector de arranque, necesitas repararlo:

1. Arranca desde un **USB de instalación de Windows**.
2. Selecciona **Reparar el equipo > Solucionar problemas > Símbolo del sistema**.
3. Ejecuta los siguientes comandos:
    
	```cmd
    bootrec /scanos
    bootrec /fixmbr 
    bootrec /fixboot 
    bootrec /rebuildbcd
	```
    
4. Reinicia y prueba.

### 3. Comprobar la asignación de particiones

Si el disco clonado no tiene la partición de arranque activa:

1. Arranca desde un **USB de instalación de Windows**.
2. En el símbolo del sistema, ejecuta:
	```cmd
    
    diskpart 
    list disk select disk X  (reemplaza X con el número del disco clonado) 
    list partition select partition Y  (reemplaza Y con la partición del sistema) 
    active 
    exit
	```
    
3. Reinicia el equipo.

Si el problema persiste, dime qué software usaste para clonar el disco y el tipo de disco (HDD/SSD, SATA/NVMe).


En caso de dar el error **"Acceso denegado"** al ejecutar `bootrec /fixboot` suele ocurrir si la partición del sistema está dañada o si el sistema está en modo UEFI y la partición EFI necesita ser reparada. Aquí hay algunas soluciones:

---

### **Solución 1: Reparar la partición EFI manualmente**

Si tu sistema usa **UEFI**, necesitas reparar la partición EFI.

4. **Abrir el Símbolo del sistema** desde un USB de instalación de Windows.
    
5. **Ejecutar `diskpart` para identificar la partición EFI**:
    
	```cmd
    diskpart
    list disk
    select disk X   # Reemplaza X con el disco donde está Windows list partition
	```
    
	Busca la partición de **100-500 MB** con formato **FAT32** (esa es la partición EFI).
    
6. **Seleccionar y asignar una letra a la partición EFI**:
    
```cmd
    select partition Y   # Reemplaza Y con el número de la partición EFI 
    assign letter=Z exit
```
    
7. **Reparar el gestor de arranque**:
    
    
	```cmd
    bcdboot C:\Windows /s Z: /f UEFI
	```
    
    (Si tu Windows está en otra unidad, reemplaza `C:\Windows` por la correcta).
    
8. **Reiniciar el equipo y probar**.
    

---

### **Solución 2: Reformatear la partición EFI (si sigue sin funcionar)**

Si `bcdboot` no arregla el problema, intenta formatear la partición EFI antes de reconstruirla:

9. **Accede a `diskpart` nuevamente** y ejecuta:
    
	```cmd
    select disk X 
    select partition Y 
    format fs=fat32 quick
    assign letter=Z 
    exit
	```
    
10. **Reconstruye la EFI con**:
    
	```cmd
    bcdboot C:\Windows /s Z: /f UEFI
	```
    

Después de estos pasos, reinicia y verifica si el sistema arranca correctamente.

