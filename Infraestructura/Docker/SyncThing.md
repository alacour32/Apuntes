- para desplegar el docker compose de Syncthing debe estar configurado asi:


```yaml
Services:  
syncthing:  
image: syncthing/syncthing:latest  
container_name: syncthing  
user: root  # Ejecutar como root  
volumes:  
- /mnt/apuntes/:/var/syncthing/ObsidianVault  
- ./syncthing-config:/var/syncthing/.config/syncthing  
ports:  
- "8384:8384"  
- "22000:22000"  
- "21027:21027/udp"  
restart: unless-stopped
```

- sin embargo tb la carpeta ubicada en la nas tiene que estar montada en la rasspberry de la siguiente manera

```shell
sudo mount -t cifs //192.168.1.32/alvaro/Documentos/Obsidian/ /home/alvaro/Documents/Syncthing/ObsidianVault/ -o username=alvaro,password=Spiderred32,vers=3.0,uid=0,gid=0,file_mode=0777,dir_mode=0777
```
