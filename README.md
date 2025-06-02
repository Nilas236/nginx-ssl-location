# nginx-ssl-location
## Cамоподписанный SSL-сертификат
``` bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout selfsigned.key \
  -out selfsigned.crt \
  -subj "/C=RU/ST=Test/L=Dev/O=Local/CN=localhost"
```


```
server {
    listen 443 ssl;
    server_name example.com;

    ssl_certificate     /etc/nginx/ssl/selfsigned.crt; ## вставить путь к сертификату 
    ssl_certificate_key /etc/nginx/ssl/selfsigned.key; ## вставить путь к сертификату 

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

```

Создание символическую ссылку в sites-enabled

`ln -s /etc/nginx/sites-available/example.com.conf /etc/nginx/sites-enabled/example.com.conf` - если не будет файл не будет работать 


