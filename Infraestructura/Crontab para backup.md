- script de backup:

```bash
#!/bin/bash  
  
# Variables  
NAS_IP="192.168.1.32"  # IP del NAS  
SHARE_NAME="/alvaro/Documentos/Backup_Server/"    # Nombre del recurso compartido  
MOUNT_POINT="/mnt/backup" # Punto de montaje  
BACKUP_SOURCE="/home/alvaro/Documents"  # Directorio a respaldar  
BACKUP_DEST="$MOUNT_POINT/backup_$(date +%Y%m%d_%H%M%S)"  # Destino del respaldo  
USERNAME="alvaro"     # Usuario del NAS  
PASSWORD="Spiderred32"  # Contraseña del NAS  
  
# Montar el recurso compartido SMB  
sudo mount -t cifs //$NAS_IP/$SHARE_NAME $MOUNT_POINT -o username=$USERNAME,password=$PASSWORD,uid=0,gid=0,file_mode=0777,dir_mode=0777,vers=3.0  
  
# Crear el directorio de respaldo  
sudo mkdir -p $BACKUP_DEST  
  
# Realizar el respaldo con rsync  
sudo rsync -av --progress $BACKUP_SOURCE $BACKUP_DEST  
  
# eliminacion de backup con mas de 7 dias  
find $MOUNT_POINT -type d -name "backup_*" -mtime +7 -exec rm -rf {} \;  
  
# mensjae de finalizacion  
echo "Respaldo completado en $BACKUP_DEST"

```
- Luego  configurar :
```bash
	crontab -e
```
- colocando la siguiente linea:
```
0 2 * * * /home/alvaro/scripts/Backup_nas.sh >> /home/alvaro/scripts/Backup.log 2>&1
```
