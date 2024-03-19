FROM httpd:alpine

WORKDIR /var/www/html

RUN apk --no-cache --update \
    add curl \
    apache2-ssl \
    alpine-sdk \
    supervisor \
    libpng-dev \ 
    libpq-dev \ 
    libxml2-dev \ 
    libzip-dev \ 
    autoconf \ 
    gcc \
    tzdata \
    mysql-client \
    php82-apache2 \
    php82-curl \
    php82-ffi \
    php82-ftp \
    php82-fileinfo \
    php82-gd \
    php82-gettext \
    php82-gmp \
    php82-intl \
    php82-imap \
    php82-mbstring \
    php82-exif \
    php82-mysqli \
    php82-mysqlnd \
    php82-odbc \
    php82-openssl \
    php82-pdo_mysql \
    php82-pdo_odbc \
    php82-pdo_pgsql \
    php82-pdo_sqlite \
    php82-pgsql \
    php82-shmop \
    php82-snmp \
    php82-soap \
    php82-sockets \
    php82-sodium \
    php82-sqlite3 \
    php82-tidy \
    php82-xsl \
    php82-zip 

RUN apk --no-cache \
    add php82-bcmath \
    php82-bz2 \
    php82-calendar \
    php82-common \
    php82-ctype \
    php82-dom \
    php82-gd \
    php82-iconv \
    php82-phar \
    php82-session \
    php82-xml \
    php82-tokenizer \
    php82-xmlreader \
    php82-xmlwriter \
    php82-fileinfo \
    php82-simplexml \
    php82-redis \
    htop

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
COPY . /var/www/html
RUN composer self-update && composer update
RUN composer install

ENV TZ=Asia/Tashkent
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ /etc/timezone

RUN sed  -i 's/memory_limit = 128M/memory_limit = 4096M/g' /etc/php82/php.ini
RUN sed  -i 's/max_execution_time = 30/max_execution_time = 600/g' /etc/php82/php.ini
RUN sed  -i 's/max_input_time = 60/max_input_time = 600/g' /etc/php82/php.ini

EXPOSE 80 443

RUN chown -R apache:apache /var/www/html/

HEALTHCHECK CMD wget -q --no-cache --spider localhost

# ENTRYPOINT ["/docker-entrypoint.sh"]