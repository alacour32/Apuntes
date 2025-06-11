## Tema 101: Arquitectura del sistema

### 101.1 Configuración de Hardware

- Conocer herramientas como `lspci`, `lsusb`, `dmesg`, `lsmod`, `modprobe`, `rmmod`
    
- Ubicación y uso de `/proc`, `/sys` y `/dev`
    

### 101.2 Arranque del sistema

- Diferencias entre BIOS y UEFI
    
- Conocer GRUB2: configuración básica y archivos
    
- Flujo de inicialización: POST → bootloader → kernel → init/systemd
    

### 101.3 Cambiar niveles de ejecución / objetivos de arranque

- Uso de `systemctl`, `runlevel`, `shutdown`, `reboot`, `telinit`
    
- Conocer `systemd`, `SysVinit`, `Upstart`
    

---

## Tema 102: Instalación de Linux y gestión de paquetes

### 102.1 Particionado del disco

- Tipos de particiones: primarias, extendidas, lógicas
    
- Particiones comúnmente usadas: `/`, `/boot`, `/home`, `swap`
    
- Uso de LVM y herramientas como `fdisk`, `parted`
    

### 102.2 Gestores de arranque

- `GRUB2` y su configuración
    
- Instalación en MBR o EFI
    

### 102.3 Bibliotecas compartidas

- Concepto de shared libraries
    
- Comandos: `ldd`, `ldconfig`, uso de `/etc/ld.so.conf`
    

### 102.4 y 102.5 Gestión de paquetes

- Debian: `dpkg`, `apt`, `apt-cache`, `apt-get`
    
- Red Hat: `rpm`, `yum`, `dnf`, `zypper`
    

### 102.6 Virtualización

- Conceptos: host, guest, hypervisor
    
- Herramientas: KVM, QEMU, VirtualBox, contenedores (Docker)
    

---

## Tema 103: Comandos GNU y Unix

### 103.1 Línea de comandos

- Uso de shell, historial (`history`), variables (`env`, `export`)
    

### 103.2 Filtros de texto

- Comandos: `cut`, `sort`, `uniq`, `tr`, `wc`
    

### 103.3 Administración de archivos

- Comandos: `cp`, `mv`, `rm`, `mkdir`, `rmdir`, `find`
    
- Uso de comodines (*, ?) y `basename`, `dirname`
    

### 103.4 Tuberías y redireccionamiento

- `|`, `>`, `>>`, `2>`, `tee`, `xargs`
    

### 103.5 Procesos

- `ps`, `top`, `kill`, `jobs`, `bg`, `fg`, `nice`, `renice`, `tmux`, `screen`
    

### 103.6 Prioridades

- `nice`, `renice`, niveles de prioridad (0-19)
    

### 103.7 Expresiones regulares

- `grep`, `egrep`, `sed`, patrones básicos y extendidos
    

### 103.8 Edición de archivos

- Uso de `vi`, `nano`, comandos básicos
    

---

## Tema 104: Dispositivos, sistemas de archivos y jerarquía estándar

### 104.1 Crear particiones y sistemas de archivos

- Herramientas: `fdisk`, `parted`, `mkfs`, `mkswap`
    
- Tipos de sistemas de archivos: `ext4`, `xfs`, `btrfs`, `vfat`
    

### 104.2 Mantenimiento de integridad del sistema de archivos

- Comandos: `fsck`, `du`, `df`
    
- Verificación de espacio y uso del disco
    

### 104.3 Montaje y desmontaje de sistemas de archivos

- `mount`, `umount`, `blkid`, `/etc/fstab`, UUID y etiquetas
    

### 104.4 Gestión de permisos y propiedad de archivos

- Comandos: `chmod`, `chown`, `chgrp`
    
- Permisos especiales: `suid`, `sgid`, sticky bit
    

### 104.5 Enlaces de archivos

- Crear y usar enlaces simbólicos y duros: `ln -s`, `ln`
    

### 104.6 Jerarquía estándar del sistema de archivos

- FHS: ubicaciones comunes como `/etc`, `/usr`, `/bin`, `/var`, `/tmp`, `/home`