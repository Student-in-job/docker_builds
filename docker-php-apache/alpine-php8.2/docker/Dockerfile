FROM php:8.2-fpm

ARG user
ARG uid

RUN apt update && apt install -y \
    git \
    curl \
    libpng-dev \
    libpq-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    libzip-dev \
    unzip

RUN docker-php-ext-install pdo pdo_mysql bcmath zip gd
RUN pecl install redis && docker-php-ext-enable redis

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN mv /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

RUN useradd -G www-data,root -u $uid -d /home/paymart-mko-admin/ $user
RUN mkdir -p /home/paymart-mko-admin/.composer && \
    chown -R $user:$user /home/paymart-mko-admin

USER $user
