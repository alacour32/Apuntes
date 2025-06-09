1. Crear Directorio
```
		mkdir /opt/Cylance
```

2. Crear archivo
```
	/opt/cylance/config_defaults.txt 
```
Nota: contenido del archivo
```
InstallToken=5JCCiedNLC4jj31YEgqi5deqa
SelfProtectionLevel=2 
LogLevel=2 
VenueZone=BSE-Servers 
UiMode=2 
AWS=0
```

3. #Actualizacion-de-Kernel  en el caso de que  sea necesario de acuerdo a la tabla de copatbilidad de cylance : https://docs.blackberry.com/en/unified-endpoint-security/blackberry-ues/blackberry-protect-desktop-supported-linux-kernels/Supported-Linux-kernels (descargar excel)

4. Instalar dependencias:
```
		sudo apt-get update -y && sudo apt-get install libxml2-utils make gcc bzip2
```

5. Instalar divers:
	### Open drivers:
```
		sudo dpkg -i cylance-protect-open-driver_version.deb
```
	 
	 Driver:
	 
```
		sudo dpkg -i cylance-protect-driver_version.deb
```
6. instalar agente:
```
		sudo dpkg -i cylance-protect.2204.x86_64.deb

```

Enlace:
[[Actualizacion Kernel-Ubuntu]]