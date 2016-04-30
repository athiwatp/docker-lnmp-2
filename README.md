docker-lnmp
==============

Just a litle Docker POC in order to have a complete stack for running LNMP stack into Docker containers using docker-compose tool.

# Installation

First, clone this repository:

```bash
$ git clone git@github.com:ykcin/docker-lnmp.git
```

Next, create `code` folder and put your application into `code` folder

For linux user, do not forget to add your local domain eg. `www.example.com` in your `/etc/hosts` file.

For windows user, do not forget to add `www.example.com` in your `C:\Windows\System32\drivers\etc\hosts` file.

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

