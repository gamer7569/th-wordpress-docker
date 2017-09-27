# th-wordpress-docker

*This is part of the [gamer7569/th-wordpress-docker](https://github.com/gamer7569/th-wordpress-docker).*

A collection of customized containers for a Docker web development stack. Where possible the containers are build on top of [Alpine Linux](http://alpinelinux.org/) for a small footprint.

## th-wordpress-docker containers

- **gamer7569/nginx:** [latest](https://github.com/gamer7569/th-wordpress-docker/blob/master/nginx/Dockerfile)
- **gamer7569/php:** [5.6](https://github.com/gamer7569/th-wordpress-docker/blob/master/php/5.6/Dockerfile) ([Alpine Linux](https://pkgs.alpinelinux.org/packages?name=php5*&branch=edge&arch=x86_64)), [7.1](https://github.com/gamer7569/th-wordpress-docker/blob/master/php/7.1/Dockerfile) ([7.1.x-dev Source](https://github.com/php/php-src/tree/PHP-7.1))
- **gamer7569/mysql:** [latest](https://github.com/gamer7569/th-wordpress-docker/blob/master/mysql/Dockerfile)

## Usage

1. Use a custom [docker-compose.yml](docker-compose.yml) file to do the work for you. Adjust the settings needed for the project.
2. Copy `.env.dist` to `.env` and change at least the project id.
3. Start the container with `docker-compose up -d`.

- For consistency the source code lives in the `/app` dir.
- The app is available at [http://localhost/](http://localhost/).
- [MailHog](https://github.com/mailhog/MailHog) is used to catch emails and can be accessed at [http://localhost:8025/](http://localhost:8025/).

## Fixing "Permission Denied" Issues

Use setfacl to set permission on the host

    sudo setfacl -Rm g:82:rwX,d:g:82:rwX /home/<username>/projects

Setup permissions for docker so the files can be accessed and deleted.
The trick is to use the uid's from the docker processes.
*www-data/nginx: 82 - docker: 999 - mysql: 28*

    # Preserve default permissions for new files and folders
    sudo setfacl -dR -m u:28:rwx -m u:82:rwx -m u:33:rwx -m u:999:rwx -m u:$(whoami):rwx data
    # Set permissions
    sudo setfacl -R -m u:28:rwx -m u:82:rwx -m u:33:rwx -m u:999:rwx -m u:$(whoami):rwx data

## Docker commands

```bash
# Start containers
$ docker-compose up

# Start and force rebuilding the containers
$ docker-compose up --build

# Stop containers
$ docker-compose stop

# Update containers
$ docker-compose pull

# Stream logs from all containers to the console
$ docker-compose logs -t -f

# Start a terminal for <container_name>
$ docker exec -ti <container_name> /bin/bash   # Ubuntu/Debian based
$ docker exec -ti <container_name> /bin/sh     # Alpine Linux based

# List containers
$ docker ps
```

## Docker maintenance commands

```bash
# Show used space, similar to the unix tool df
$ docker system df

# Remove development junk: unused volumes, networks, exited containers and unused images
$ docker system prune --force --all

# List all images
$ docker images

# Remove dangling images:
$ docker images -qf dangling=true --no-trunc | grep '<none>' | awk '{ print $3 }' | xargs -r docker rmi

# Remove exited containers:
$ docker ps -aq --filter status=dead --filter status=exited | xargs -r docker rm -v

# Remove dangling volumes:
$ docker volume ls -qf dangling=true | xargs -r docker volume rm
```
