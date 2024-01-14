FROM php:8.1-fpm
COPY php.ini /usr/local/etc/php/

# Package & Library install
RUN apt-get update \
    && apt-get install -y zlib1g-dev mariadb-client vim libzip-dev \
    && docker-php-ext-install zip pdo_mysql

# Composer install
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN mv composer.phar /usr/local/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer
ENV PATH $PATH:/composer/vendor/bin

# Node.js install
ARG NODE_VERSION=20.x
RUN curl -sL https://deb.nodesource.com/setup_$NODE_VERSION | bash - \
  && apt-get update \
  && apt-get install -y nodejs \
  && apt-get clean \
  && npm install -g npm@10.2.4

# WorkDir Path setting
WORKDIR /var/www

# Laravel Package install
RUN composer global require "laravel/installer"