# https://hub.docker.com/_/php
FROM php:8.0.2-fpm-alpine3.13

# xdebug dependencies: autoconf, gcc, g++, make
RUN apk --update --no-cache --virtual build-dependencies add \
    autoconf \
    gcc \
    g++ \
    make

RUN pecl install xdebug-3.0.2 \
    && docker-php-ext-enable xdebug

RUN apk del build-dependencies

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php --version=2.0.9 --install-dir=/usr/local/bin --filename=composer \
    && php -r "unlink('composer-setup.php');"
