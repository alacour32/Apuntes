# #Actualizacion-de-Kernel

1.  **Verificar la disponibilidad del kernel:** Antes de realizar la actualización, asegúrate de que la versión del kernel que deseas instalar esté disponible en los repositorios de Ubuntu. Puedes hacer esto buscando en la documentación oficial de Ubuntu o utilizando comandos como `apt search`.
    
2. **Actualizar los repositorios**: Ejecuta los siguientes comandos para actualizar los repositorios de tu sistema:
          
```
    sudo apt update
```
    
3. **Instalar el kernel**: Utiliza el siguiente comando para instalar la versión específica del kernel que deseas:
        
```
    sudo apt install linux-image-5.19.0-50-generic
```
    
    nota: Reemplaza `5.19.0-50-generic` con la versión específica del kernel que deseas instalar.
    
4. **Actualizar GRUB**: Después de instalar el nuevo kernel, es importante actualizar GRUB para que reconozca el nuevo kernel durante el arranque. Ejecuta el siguiente comando:
    
```
    sudo update-grub
```
    
5. **Reiniciar el sistema**: Una vez completados los pasos anteriores, reinicia el sistema para aplicar los cambios:
    
```
    sudo reboot`
```
    

Después de reiniciar, tu sistema Ubuntu Server debería estar utilizando la versión del kernel que has instalado. Recuerda que siempre es importante realizar una copia de seguridad antes de realizar actualizaciones importantes como esta, especialmente si estás trabajando en un entorno de producción.

Enlace:
[[Instalacion Cylance-Ubuntu]]
