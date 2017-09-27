# NGINX Docker Container

*This is part of the [gamer7569/th-wordpress-docker](https://github.com/gamer7569/th-wordpress-docker).*

A collection of customized containers for a Docker web development stack. Where possible the containers are build on top of [Alpine Linux](http://alpinelinux.org/) for a small footprint.

## th-wordpress-docker containers

- **gamer7569/nginx:** [latest](https://github.com/gamer7569/th-wordpress-docker/blob/master/nginx/Dockerfile)
- **gamer7569/php:** [5.6](https://github.com/gamer7569/th-wordpress-docker/blob/master/php/5.6/Dockerfile) ([Alpine Linux](https://pkgs.alpinelinux.org/packages?name=php5*&branch=edge&arch=x86_64)), [7.1](https://github.com/gamer7569/th-wordpress-docker/blob/master/php/7.1/Dockerfile) ([7.1.x-dev Source](https://github.com/php/php-src/tree/PHP-7.1))
- **gamer7569/mysql:** [latest](https://github.com/gamer7569/th-wordpress-docker/blob/master/mysql/Dockerfile)

## Usage

The documents are served from `.:/app/public` and can be accessed at http://127.0.0.1/.

Add this to your `docker-compose.yml` file:

```yaml
web:
  image: gamer7569/nginx
  container_name: ${PROJECT_ID}-web
  ports:
    - "80:80"
  volumes_from:
    - datastore
  links:
    - php
```

## CLI commands

```bash
# Access container
docker exec -ti <PROJECT_ID>-web /bin/sh
```
