# MySQL Docker Container

*This is part of the [gamer7569/th-wordpress-docker](https://github.com/gamer7569/th-wordpress-docker).*

A collection of customized containers for a Docker web development stack. Where possible the containers are build on top of [Alpine Linux](http://alpinelinux.org/) for a small footprint.

## th-wordpress-docker containers

- **gamer7569/nginx:** [latest](https://github.com/gamer7569/th-wordpress-docker/blob/master/nginx/Dockerfile)
- **gamer7569/php:** [5.6](https://github.com/gamer7569/th-wordpress-docker/blob/master/php/5.6/Dockerfile) ([Alpine Linux](https://pkgs.alpinelinux.org/packages?name=php5*&branch=edge&arch=x86_64)), [7.1](https://github.com/gamer7569/th-wordpress-docker/blob/master/php/7.1/Dockerfile) ([7.1.x-dev Source](https://github.com/php/php-src/tree/PHP-7.1))
- **gamer7569/mysql:** [latest](https://github.com/gamer7569/th-wordpress-docker/blob/master/mysql/Dockerfile)

## Usage

Add this to your `docker-compose.yml` file:

```yaml
db:
  image: gamer7569/mysql
  container_name: ${PROJECT_ID}-db
  ports:
    - "3306:3306"
  env_file: .env
  #volumes:
  #  - ./resources/mysql-dump:/docker-entrypoint-initdb.d  # Import .sql files
  #  - ./data/mysql-data:/var/lib/mysql                    # persistent database
  volumes_from:
    - datastore
```

## CLI commands

```bash
# Access container
docker exec -ti <PROJECT_ID>-db /bin/sh
```

## Creating a new database and user

```bash
# Change UNIQUE_NAME-db with the name that is used in `docker-compose.yml` -> `services:db:container_name`
docker exec UNIQUE_NAME-db mysql -h"db" -P"3306" -uroot -p"docker" -e "CREATE DATABASE IF NOT EXISTS develop;"
docker exec UNIQUE_NAME-db mysql -h"db" -P"3306" -uroot -p"docker" -e "CREATE USER IF NOT EXISTS 'develop'@'%' IDENTIFIED BY 'develop';"
docker exec UNIQUE_NAME-db mysql -h"db" -P"3306" -uroot -p"docker" -e "GRANT ALL PRIVILEGES ON develop.* TO 'develop'@'%';"
```
