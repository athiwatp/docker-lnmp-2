FROM php:7-fpm
RUN docker-php-ext-install -j$(nproc) pdo_mysql mysqli

# link: https://github.com/docker-library/php/issues/77
RUN curl -L -o /tmp/redis.tar.gz https://github.com/phpredis/phpredis/archive/3.0.0-rc1.tar.gz \
    && tar xfz /tmp/redis.tar.gz \
    && rm -r /tmp/redis.tar.gz \
    && mv phpredis-3.0.0-rc1 /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
    && docker-php-ext-enable redis

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && sed -i '1 a xdebug.remote_autostart=true' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && sed -i '1 a xdebug.remote_handler=dbgp' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && sed -i '1 a xdebug.remote_connect_back=1 ' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && sed -i '1 a xdebug.remote_port=9001' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && sed -i '1 a xdebug.idekey=PhpStorm' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && sed -i '1 a xdebug.remote_enable=1' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN echo "date.timezone = Asia/Shanghai" >> /usr/local/etc/php/php.ini
