docker-lnmp
==============

Just a litle Docker POC in order to have a complete stack for running LNMP stack(Linux, Nginx, MySQL, PHP7) into Docker containers using docker-compose tool.


# Include

- Linux
- Nginx 1.9 (You can change <code>image: nginx:1.9.14</code> in docker-compose.yml to the version you want)
- MySQL 5.7 (You can change <code>image: mysql</code> in docker-compose.yml to the version you want)
- PHP 5.6 (You can change <code>FROM php:5-fpm</code> in php-fpm/Dockerfile to the version you want  e.g. <code>FROM php:7-fpm</code>)

# Installation

First, clone this repository:

```bash
$ git clone git@github.com:ykcin/docker-lnmp.git
```

Next, create `www.example.com` folder and put your application into `code/www.example.com` folder

```
$ mkdir -p code/www.example.com
```

Do not forget to add your local domain e.g. `www.example.com` in your `hosts` file.

* Linux

Add to `/etc/hosts` file

* Windows

Add to `C:\Windows\System32\drivers\etc\hosts` file

Then, run:

```bash
$ docker-compose up
```

You are done, you can visit your application on the following URL: `http://www.example.com`

_Note :_ you can rebuild all Docker images by running:

```bash
$ docker-compose build
```

# How it works?

Here are the `docker-compose` built images:

* `db`: This is the MySQL database container (can be changed to postgresql or whatever in `docker-compose.yml` file),
* `php`: This is the PHP-FPM container including the application volume mounted on,
* `nginx`: This is the Nginx webserver container in which php volumes are mounted too

This results in the following running containers:

```bash
> $ docker-compose ps
        Name                      Command               State              Ports
        -------------------------------------------------------------------------------------------
        docker_db_1            /entrypoint.sh mysqld            Up      0.0.0.0:3306->3306/tcp
        docker_nginx_1         nginx                            Up      443/tcp, 0.0.0.0:80->80/tcp
        docker_php_1           php5-fpm -F                      Up      9000/tcp
```

# Read logs

You can access Nginx logs in the following directories into your host machine:

* `logs/nginx`

## License

MIT
