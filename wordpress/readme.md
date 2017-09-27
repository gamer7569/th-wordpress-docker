# WordPress Docker Container

*This is part of the [gamer7569/th-wordpress-docker](https://github.com/gamer7569/th-wordpress-docker).*

A collection of customized containers for a Docker web development stack. Where possible the containers are build on top of [Alpine Linux](http://alpinelinux.org/) for a small footprint.

## th-wordpress-docker containers

- **gamer7569/nginx:** [latest](https://github.com/gamer7569/th-wordpress-docker/blob/master/nginx/Dockerfile)
- **gamer7569/php:** [5.6](https://github.com/gamer7569/th-wordpress-docker/blob/master/php/5.6/Dockerfile) ([Alpine Linux](https://pkgs.alpinelinux.org/packages?name=php5*&branch=edge&arch=x86_64)), [7.1](https://github.com/gamer7569/th-wordpress-docker/blob/master/php/7.1/Dockerfile) ([7.1.x-dev Source](https://github.com/php/php-src/tree/PHP-7.1))
- **gamer7569/mysql:** [latest](https://github.com/gamer7569/th-wordpress-docker/blob/master/mysql/Dockerfile)

## Structure

Create this dir structure:

	project_root
	├── data
	│   ├── mysql       -> Persitent MySQL data
	│   └── wordpress   -> WordPress source code
	├── themes
	├── plugins
	└── uploads

The `data/mysql/` and `data/wordpress/` dirs are optional and only required if you want to save the data locally. Or, in case for the WordPress source, if you need it for code completion in your (PhpStorm) IDE.

## Usage

Replace the regular datastore with this in your `docker-compose.yml` file:

```yaml
datastore:
  image: gamer7569/wordpress
  container_name: ${PROJECT_ID}-datastore
  volumes:
    - ./data/mysql:/var/lib/mysql		# Optional for persistent DB
    - ./data/wordpress:/app/public		# Optional for IDE code completion
    - ./plugins:/app/public/wp-content/plugins
    - ./themes:/app/public/wp-content/themes
    - ./uploads:/app/public/wp-content/uploads
```

## Access from terminal:

It's a volumes datastore. Once it has done it's job it exits and you can't access it anymore.
