# wordpress-nginx-docker

This repository is quick start for [Wordpress](https://wordpress.org/) using [docker-compose](https://docs.docker.com/compose/)

### get started

- clone or fork this repository
- `$ cd /path/to/checkout`
- check `.env` file

```
NGINX_PORT=80
MYSQL_PORT=3306

MYSQL_ROOT_PASSWORD=somewordpress
MYSQL_DATABASE=wordpress
MYSQL_USER=wordpress
MYSQL_PASSWORD=wordpress
```

- adjust values with your needs
- run `$ docker-compose up --build -d`
- open your Browser http://localhost/

### to stop

- run `$ docker-compose down`

### version

Tested with :

- Docker Version 17.06.2-ce
- ...
- Docker Version 25.0.3

### check php configuration

just create a simple `phpinfo.php` file in `wordpress` folder

```php
<?php phpinfo(); ?>
```

then open your browser on http://localhost/phpinfo.php

### Increase file upload size limit

```bash
$ docker-compose exec nginx /bin/sh
/ vi /etc/nginx/nginx.conf
```

Add following line to `http{..}` block in nginx config:

```
http {
	#...
        client_max_body_size 100m;
	#...
}
```

`$ exit`

now increase limit in php-fpm

```bash
$ docker-compose exec wordpress bash
bash-4.3# vi /usr/local/etc/php/conf.d/upload.conf
```

```
upload_max_filesize = 100M
post_max_size = 100M
```

```
bash-4.3# exit
$ docker-compose stop wordpress
$ docker-compose start wordpress
```

### Licensing

Licensed under the MIT License

A copy of the license is available in the repository's [LICENSE](LICENSE.md) file.
