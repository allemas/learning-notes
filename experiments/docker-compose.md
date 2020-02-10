# docker-compose

## Commands
- docker-compose up
- docker-compose rm

### example
```
web:
    image: nginx:latest
    ports:
        - "8080:80"
    volumes:
        - ./<dir>:/var/www/html/
        - ./site.conf:/etc/nginx/conf.d/site.conf
    links:
        - php
php:
    image: php:7-fpm
    volumes:
        - ./<dir>:/var/www/html/
```

```

server {
    listen 80;
    index index.php index.html;
    server_name 127.0.0.1;
    error_log  /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;
    root /var/www/html/;

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass php:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }
}
```


## Link
- http://geekyplatypus.com/dockerise-your-php-application-with-nginx-and-php7-fpm/