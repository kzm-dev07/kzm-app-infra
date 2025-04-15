FROM php:8.3-fpm AS base

RUN apt-get update && apt-get upgrade -y \
  && apt-get install -y zlib1g-dev vim libzip-dev \
  && docker-php-ext-install zip pdo_mysql


RUN cp "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

COPY ./conf.d "$PHP_INI_DIR/conf.d"

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

COPY ./todo-app-api /var/www/app/

COPY ./script/startup.sh /var/tmp/startup.sh

WORKDIR /var/www/app

### 開発環境 ###
FROM base AS dev

RUN composer install

RUN php artisan config:clear

# 権限の設定
RUN chown -R www-data:www-data /var/www \
  && chmod -R 755 /var/www/app/storage

### 本番環境 ###
FROM base AS prd

RUN composer install --no-dev --optimize-autoloader

RUN php artisan config:clear \
  && php artisan config:cache

COPY ./todo-app-api/.env.example /var/www/app/.env

# 権限の設定
RUN chown -R www-data:www-data /var/www \
  && chmod -R 755 /var/www/app/storage

