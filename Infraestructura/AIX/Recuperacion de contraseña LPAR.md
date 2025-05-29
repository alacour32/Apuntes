Si tienes acceso a una LPAR con NIM en tu IBM Power9, puedes usarla para bootear la otra LPAR en modo mantenimiento y resetear el password de root. Aquí tienes los pasos generales:

### **Opción 1: Usando NIM para Bootear en Modo Mantenimiento**

1. **Verificar si la LPAR sin acceso está registrada en el NIM Server**  
    En la LPAR NIM, revisa si la LPAR sin acceso está registrada ejecutando:
    
       
	```sh
    lsnim -l <nombre_de_la_LPAR>
	```
    
2. **Bootear la LPAR en modo mantenimiento usando NIM**
    
    - En el NIM server, ejecuta:
        
		```sh
        nim -o bos_inst -a source=mksysb -a spot=<spot_name> <nombre_de_la_LPAR>
		```
        
    - Luego, en la HMC, inicia la LPAR en modo mantenimiento (SMS Menu → Seleccionar arranque por red).
3. **Acceder al sistema de archivos y cambiar la contraseña**
    
    - Una vez que la LPAR haya arrancado en modo mantenimiento, accede a una terminal y monta la raíz del sistema:
        
               
		```sh
        mount /dev/hd4 /mnt
		```
        
    - Edita el archivo de contraseñas:
               
		```sh
        vi /mnt/etc/security/passwd
		```
        
    - Busca la línea correspondiente a root y elimínala o usa `passwd` para cambiarla manualmente.
4. **Reiniciar y probar el acceso**
    
	```sh
    shutdown -Fr
	```
    
    Luego, intenta acceder con la nueva contraseña.