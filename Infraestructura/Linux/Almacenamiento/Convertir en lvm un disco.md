###  1. Identificar el disco actual

```bash
lsblk
df -h /opt/apps/
# Anotar el dispositivo (ej: /dev/sdb1)
```

### 2. Desmontar el filesystem

```bash
umount /opt/apps/
```

### 3. Eliminar la partición existente y crear LVM

```bash
# Usar fdisk o parted (ejemplo con /dev/sdb)
fdisk /dev/sdb
# Dentro de fdisk:
# - d (eliminar partición)
# - n (nueva partición)
# - t (cambiar tipo a 8e - Linux LVM)
# - w (guardar cambios)

# Alternativamente con parted:
parted /dev/sdb
(parted) mklabel gpt
(parted) mkpart primary 0% 100%
(parted) set 1 lvm on
(parted) quit

```
### 4. Crear volumen físico LVM

```bash
pvcreate /dev/sdb1
```

### 5. Crear grupo de volúmenes

```bash
vgcreate vg_opt /dev/sdb1
```

### 6. Crear volumen lógico

```bash
# Calcular espacio disponible (en MB)
vgdisplay vg_opt | grep "Free"

# Crear LV usando todo el espacio (ajustar según necesidad)
lvcreate -l 100%FREE -n lv_apps vg_opt

```
### 7. Formatear el nuevo volumen

```bash
# Elegir filesystem (xfs recomendado para LVM)
mkfs.xfs /dev/vg_opt/lv_apps
```