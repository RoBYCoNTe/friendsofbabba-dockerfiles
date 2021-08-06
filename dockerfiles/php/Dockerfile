FROM php:8.0-fpm

RUN groupadd --gid 1000 boilerplate_v2 \
    && useradd --shell /sbin/nologin --gid 1000 --uid 1000 boilerplate_v2

RUN apt-get -y update \
    && apt-get install -y libicu-dev git zip unzip python python-pip \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl
RUN docker-php-ext-install mysqli pdo pdo_mysql \
    && docker-php-ext-enable pdo_mysql
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

COPY dockerfiles/php/additional.ini /usr/local/etc/php/conf.d/additional.ini

RUN curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php \
  && php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer \
  && rm -f /tmp/composer-setup.php

WORKDIR /var/www/html

# COPY composer.json /var/www/html/composer.json
# RUN composer install

VOLUME /var/www/html
COPY . /var/www/html/

RUN chown -R boilerplate_v2:boilerplate_v2 /var/www/html
