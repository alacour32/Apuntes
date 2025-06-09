
Descargar los archivos del certificado (.crt y .key) hacia la carpeta /etc/ssl/certs

**Configurar Nginx:**
- /etc/nginx/nginx.conf
```
user www-data;
worker_processes auto;
pid /run/nginx.pid;
include /etc/nginx/modules-enabled/*.conf;

events {
	worker_connections 768;
}

http {
	sendfile on;
	tcp_nopush on;
	types_hash_max_size 2048;
	
	include /etc/nginx/mime.types;
	default_type application/octet-stream;
	
	more_set_headers "Server: INTEGRA";
	server_tokens off;
	
	add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload";
	add_header Cache-Control "no-cache, must-revalidate";
	add_header X-Frame-Options DENY;
	add_header X-Content-Type-Options nosniff;
	add_header X-XSS-Protection "1; mode=block";
	
	access_log /var/log/nginx/access.log;
	error_log /var/log/nginx/error.log;
	
	gzip on;
	
	include /etc/nginx/conf.d/*.conf;
	include /etc/nginx/sites-enabled/*;
}
```

- /etc/nginx/snippets/ssl-cert.conf
```
ssl_certificate /etc/ssl/certs/Integra.crt;
ssl_certificate_key /etc/ssl/certs/Integra.key;
```

- /etc/nginx/snippets/ssl-params.conf
```
ssl_protocols TLSv1.2 TLSv1.3;
ssl_prefer_server_ciphers on;

ssl_session_timeout 10m;
ssl_session_cache shared:SSL:10m;
ssl_session_tickets off;

resolver 8.8.8.8 8.8.4.4 valid=300s;
resolver_timeout 5s;
```

- /etc/nginx/sites-available/default
```
map $http_connection $connection_upgrade {
	"~*Upgrade" $http_connection;
	default keep-alive;
}

server {
	listen 80;
	listen [::]:80;

	server_name integra.bse.com.ar;

	return 301 https://$server_name$request_uri;

}

server {
	listen 443 ssl;
	listen [::]:443 ssl;

	server_name integra.bse.com.ar;

	include /etc/nginx/snippets/ssl-cert.conf;
	include /etc/nginx/snippets/ssl-params.conf;

	location / {
			root /var/www/sgefront;
			index index.html index.htm;
			try_files $uri $uri/ /index.html;
	}
}

```

