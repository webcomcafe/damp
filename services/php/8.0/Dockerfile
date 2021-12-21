FROM php:8.0.13-fpm

ARG user
ARG uid

RUN apt-get update \
    && apt-get install -y git iputils-ping libfreetype6-dev libjpeg62-turbo-dev libpq-dev libzip-dev zip \
    && pecl install xdebug \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install sockets pdo_mysql mysqli pdo_pgsql pgsql zip \
    && docker-php-ext-enable xdebug pdo_mysql mysqli pdo_pgsql pgsql zip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer 

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

COPY ./php.ini "$PHP_INI_DIR/php.ini"

COPY ./00-dev.ini "$PHP_INI_DIR/conf.d/00-dev.ini"

# Permissões
RUN useradd -G www-data,root -u $uid -d /home/$user $user
RUN mkdir -p /home/$user/.composer && \
    chown -R $user:$user /home/$user

# Set working directory
WORKDIR /var/www

USER $user