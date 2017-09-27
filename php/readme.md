# PHP-FPM Docker Container

*This is part of the [gamer7569/th-wordpress-docker](https://github.com/gamer7569/th-wordpress-docker).*

A collection of customized containers for a Docker web development stack. Where possible the containers are build on top of [Alpine Linux](http://alpinelinux.org/) for a small footprint.

## th-wordpress-docker containers

- **gamer7569/nginx:** [latest](https://github.com/gamer7569/th-wordpress-docker/blob/master/nginx/Dockerfile)
- **gamer7569/php:** [5.6](https://github.com/gamer7569/th-wordpress-docker/blob/master/php/5.6/Dockerfile) ([Alpine Linux](https://pkgs.alpinelinux.org/packages?name=php5*&branch=edge&arch=x86_64)), [7.1](https://github.com/gamer7569/th-wordpress-docker/blob/master/php/7.1/Dockerfile) ([7.1.x-dev Source](https://github.com/php/php-src/tree/PHP-7.1))
- **gamer7569/mysql:** [latest](https://github.com/gamer7569/th-wordpress-docker/blob/master/mysql/Dockerfile)

## Includes

- PHP-FPM + CLI
- Extensions: bcmath, curl, ctype, dom, gd, iconv, intl, json, mbstring, mcrypt, mysql *(5.6 only)*, mysqli, opcache, openssl, pcntl, pdo, pdo_mysql, pdo_sqlite, phar, session, sockets, xdebug, xml, xmlreader, redis, zip, zlib
- [composer](https://getcomposer.org/doc/)
- [ssmtp](http://linux.die.net/man/8/ssmtp) to catch php mail() and forward to [MailHog](https://github.com/mailhog/MailHog)

## Usage

Add this to your `docker-compose.yml` file:

```yaml
php:
  image: gamer7569/php:latest      # Use for PHP 7.1.x
  #image: gamer7569/php:7.0        # Use for PHP 7.0.x
  #image: gamer7569/php:5.6        # Use for PHP 5.6.x
  container_name: ${PROJECT_ID}-php
  volumes_from:
    - datastore
  links:
    - db        # Optional
    - redis     # Optional
    - mailhog   # Optional
```

## CLI commands

```bash
# Access container
docker exec -ti <PROJECT_ID>-php /bin/sh

# Run composer
docker exec -ti <PROJECT_ID>-php composer <arguments>
```
