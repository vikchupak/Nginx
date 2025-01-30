- By default, Nginx listens on 127.0.0.1
- If we want Nginx to listen on another/additional ip, it has to be explicitly configured
  - `/etc/nginx/nginx.conf`
    ```nginx
    server {
        listen 127.0.0.41:80;  # HTTP
        listen 127.0.0.41:443 ssl;  # HTTPS
        
        server_name yourdomain.com;
    
        ssl_certificate /path/to/cert.pem;
        ssl_certificate_key /path/to/key.pem;
    
        location / {
            proxy_pass http://backend_server;
        }
    }
    ```

