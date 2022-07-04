FROM composer:latest AS composer
FROM php:7.4-fpm

RUN apt-get update && apt-get install -y \
    git \
    curl \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

RUN pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis



WORKDIR /var/www

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN composer install --no-interaction

RUN chown -R www-data:www-data /var/www
RUN chmod -R 755 /var/www/storage



EXPOSE 9000
