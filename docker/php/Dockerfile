FROM php:8.3-apache

RUN apt-get update && apt-get install -y \
    git unzip curl \
    libpng-dev libjpeg-dev libfreetype6-dev \
    libonig-dev libxml2-dev libzip-dev \
    zip nodejs npm \
    && docker-php-ext-configure gd --with-freetype --with-jpeg

RUN docker-php-ext-install \
    pdo pdo_mysql mbstring bcmath gd zip
FROM php:8.3-apache

RUN apt-get update && apt-get install -y \
    git unzip curl \
    libpng-dev libjpeg-dev libfreetype6-dev \
    libonig-dev libxml2-dev libzip-dev \
    zip nodejs npm \
    && docker-php-ext-configure gd --with-freetype --with-jpeg

# PHP extensions (EXIF MUHIM)
RUN docker-php-ext-install \
    pdo \
    pdo_mysql \
    mbstring \
    bcmath \
    gd \
    zip \
    exif

RUN a2enmod rewrite

COPY docker/php/000-default.conf /etc/apache2/sites-available/000-default.conf

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html

# Apache rewrite
RUN a2enmod rewrite

# Apache virtual host
COPY docker/php/000-default.conf /etc/apache2/sites-available/000-default.conf

# Composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html
