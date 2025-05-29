- Verificar Puntos de Montaje con el comando:

```
df -l
```

![[Pasted image 20240327193615.png]]


- Visualizar la información de los discos, particiones y puntos de montaje con el comando:

```
lsblk
```
Ejemplo: Sdb /HOT 

-  Se procede a desmontar el disco/particion con el comando: 
```
 Umount /dev/sdXN /”Punto de montaje”
```
 Desmontar Discos con particiones estándar.

 - Hacer crecer discos desde V-Center.
 ![[Pasted image 20240327194217.png]]

 
 - Listar discos y particiones
```
 fdisk –l 
```

 - Verificar y repara el estados de discos con el comando:
```
  e2fsck –f /dev/”dispositivo (sdXN)” 
```
X=disco – N=Particion. (Verificar con fdisk -l)

![[Pasted image 20240327194309.png]]

- Redimencionar discos con el comando:
```
resize2fs / dev/”dispositivo (sdXN)” 
```
X=disco – N=Particion. (Verificar con fdisk -l) – _ mount /dev/sdXN /”Punto de Montaje”- Montar Directorio dentro de la unidad redimencionada.

![[Pasted image 20240327194342.png]]


- Montar disco/particion redimensionada.
```
 mount /dev/sdXN /”Punto de Montaje”- 
```


