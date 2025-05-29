Esta configuración es para un servidor **NGINX** que maneja solicitudes HTTPS en el puerto **443** y retransmite algunas de estas solicitudes a otro servidor interno mediante un **proxy inverso**. A continuación se explican las partes principales:

---

### 1. Escucha en HTTPS (Puerto 443)

nginx

`listen 443 ssl; server_name MODO.BSE.COM.AR;`

- **listen 443 ssl**: El servidor escucha en el puerto **443** (estándar para HTTPS) y utiliza SSL.
- **server_name MODO.BSE.COM.AR**: Define el nombre del dominio para el cual responde este bloque de servidor.

---

### 2. Configuración de SSL

nginx

`ssl_certificate         /etc/nginx/ssl/modo.bse.com.ar.crt; ssl_certificate_key     /etc/nginx/ssl/modo.bse.com.ar.key;  ssl_protocols TLSv1.1 TLSv1.2; ssl_ciphers HIGH:!aNULL:!MD5;`

- **ssl_certificate** y **ssl_certificate_key**: Especifican los archivos del certificado y la clave privada para cifrar las conexiones.
- **ssl_protocols TLSv1.1 TLSv1.2**: Limita los protocolos TLS aceptados. En este caso, permite solo **TLS 1.1** y **TLS 1.2** (deberías considerar habilitar **TLS 1.3** por seguridad).
- **ssl_ciphers**: Configura los algoritmos de cifrado permitidos. La lista incluye solo cifrados fuertes (**HIGH**) y excluye cifrados inseguros como **aNULL** y **MD5**.

---

### 3. Directorio raíz y registro de logs

nginx

`root /var/QNet24/web/QNetEsb; index index.php;  error_log /var/QNet24/logs/web/error_modo.log; access_log /var/QNet24/logs/web/access_modo.log;`

- **root**: Define el directorio donde se encuentran los archivos servidos por este servidor para solicitudes directas.
- **index**: El archivo predeterminado para servir solicitudes directas es `index.php`.
- **error_log** y **access_log**: Configuran los archivos donde se registran errores y accesos.

---

### 4. Bloques de ubicaciones (location)

#### a) **Errores**

nginx

`location ^~ /errors/ {     internal; }`

- Este bloque apunta a una carpeta `/errors/` con archivos de respuesta para diferentes códigos de error HTTP.
- **internal**: Hace que esta ubicación sea accesible solo desde el servidor, no desde los clientes externos.

---

#### b) **Proxy inverso para API**

nginx

`location ~* /QNet24/services/api/(.*) {     proxy_pass https://modoprodbse:54005; }`

- **proxy_pass**: Redirige las solicitudes que coincidan con el patrón `/QNet24/services/api/` al servidor interno `modoprodbse` en el puerto **54005** usando HTTPS.
- **~***: Indica una expresión regular insensible a mayúsculas/minúsculas.

---

#### c) **Validación de tarjetas**

nginx
`location = /cards/validate {     proxy_pass https://modoprodbse:54005/QNet24/services/api/rest/modo/cards/validate; }`

- Este bloque sirve específicamente para el endpoint exacto `/cards/validate`.
- Redirige la solicitud al servidor interno `modoprodbse` hacia una ruta específica en el backend.

---

### 5. **Páginas de error personalizadas**

nginx

`error_page 400 errors/400.json; error_page 401 errors/401.json; ... error_page 504 errors/504.json;`

- Define respuestas personalizadas en formato JSON para varios códigos de error HTTP (400, 401, 403, etc.). Los archivos están en la carpeta `/errors/`.

---

### Resumen de Funcionamiento

1. **Seguridad HTTPS**:
    - Utiliza certificados SSL para cifrar el tráfico y protocolos seguros (TLS 1.1 y 1.2).
2. **Proxy inverso**:
    - Reenvía solicitudes específicas al backend interno (`modoprodbse`) en el puerto **54005**.
3. **Páginas de error**:
    - Personaliza las respuestas de error en formato JSON.
4. **Logs**:
    - Registra accesos y errores en rutas específicas.

---

Este servidor está configurado para recibir solicitudes HTTPS, manejarlas localmente (archivos estáticos) o reenviarlas al backend según los endpoints, mientras asegura el cifrado y un manejo adecuado de errores. Si tienes preguntas adicionales o necesitas ajustes, házmelo saber.

Nota: cualquier cambio de configuracion que se realice se debe reiniciar el servicio de nginx y luego corroborar la configuracion con los siguientes comandos:

```
nginx -t 
systemctl restart nginx.service
```