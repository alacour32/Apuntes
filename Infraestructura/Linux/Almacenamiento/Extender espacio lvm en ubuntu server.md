*situación: hay espacio no asignado al volum group*

Para poder ver los bloques de datos:

```
lsblk
```

![[Apuntes/Imagenes/Pasted image 20240429103953.png]]

Chequear que el volumn group tenga espacio libre no asignado

```
vgs
```

![[Apuntes/Imagenes/Pasted image 20240429104113.png]]

Asignarle espacio libre
```
sudo lvextend -L +"TAMAÑO EN GB QUE SE LE QUIERE ASIGNAR" "DIRECCION DEL VG"
```

![[Apuntes/Imagenes/Pasted image 20240429105224.png]]

despues redefenir el sistema de archivos para que tome el espacio libre:

```
sudo resize2fs "DIRECCION DEL VG"
```

![[Apuntes/Imagenes/Pasted image 20240429105418.png]]

Verificar espacio asignado:

```
df-h
```

![[Apuntes/Imagenes/Pasted image 20240429105515.png]]