
# Cómo convertir un archivo PFX a Cert, Key y PEM

## Conversión

### 1. Extraer el archivo PEM desde el archivo `.pfx`
El archivo `.pfx` (PKCS#12) contiene tanto el certificado como la clave privada en un solo archivo. Usa OpenSSL para extraer el archivo PEM:

```bash
openssl pkcs12 -in input.pfx -out output.pem -nodes
```

### 2. Extraer la clave privada desde el archivo PEM
Una vez que tengas el archivo PEM, extrae la clave privada en un archivo `.key`:

```bash
openssl pkey -in output.pem -out private.key
```

### 3. Extraer el certificado desde el archivo PEM
Extrae el certificado en un archivo `.crt`:

```bash
openssl x509 -in output.pem -out certificate.crt
```

---

## Configuración de Nginx

### 1. Colocar el certificado y la clave privada
Copia los archivos `certificate.crt` y `private.key` en un directorio seguro del servidor, como `/etc/nginx/ssl/`.

Ejemplo:
```bash
sudo mkdir -p /etc/nginx/ssl
sudo cp certificate.crt /etc/nginx/ssl/
sudo cp private.key /etc/nginx/ssl/
sudo chmod 600 /etc/nginx/ssl/*
```

### 2. Editar la configuración de Nginx
Abre el archivo de configuración de Nginx para tu sitio. Este archivo generalmente se encuentra en `/etc/nginx/sites-available/` o `/etc/nginx/conf.d/`.

Ejemplo de configuración:
```nginx
server {
    listen 443 ssl;
    server_name your-domain.com;

    ssl_certificate /etc/nginx/ssl/certificate.crt;
    ssl_certificate_key /etc/nginx/ssl/private.key;

    location / {
        root /var/www/html;
        index index.html index.htm;
    }
}

server {
    listen 80;
    server_name your-domain.com;

    # Redirigir HTTP a HTTPS
    return 301 https://$host$request_uri;
}
```

### 3. Probar y recargar Nginx
Prueba la configuración en busca de errores:
```bash
sudo nginx -t
sudo systemctl reload nginx
```

---

## Probar con Curl
Usa `curl` para probar la conexión:

```bash
curl --key private.key --cert certificate.crt --cacert combined.pem https://dominio.com
```

---

## Verificar Certificados

### 1. Probar con OpenSSL

- **Revisar si la clave privada es válida**:
    ```bash
    openssl rsa -in /path/to/private.key -check
    ```
    Si falla, tu clave privada es inválida o está dañada.

- **Revisar si el certificado es válido**:
    ```bash
    openssl x509 -in /path/to/certificate.crt -text -noout
    ```
    Si falla, tu certificado puede estar corrupto o no estar en formato PEM.

- **Probar la clave privada y el certificado juntos**:
    ```bash
    openssl s_server -key /path/to/private.key -cert /path/to/certificate.crt -accept 443
    ```

### 2. Comprobar conexión al servidor
Verifica la conexión TLS del servidor:
```bash
openssl s_client -connect your-domain.com:443 -tls1_3
```

---

### Notas:
1. Verifica que el archivo `certificate.crt` contiene el certificado en formato PEM.
2. Revisa la configuración de Nginx para asegurarte de que apunta a las rutas correctas de los archivos.
