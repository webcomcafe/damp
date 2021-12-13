FROM php:7.0.33-fpm

RUN apt-get update \
    && apt-get install -y git iputils-ping \
    && pecl install xdebug-2.7.2 \
    && docker-php-ext-install sockets \
    && docker-php-ext-enable xdebug \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer 

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

COPY ./php.ini /usr/local/etc/php/conf.d/00-app.ini