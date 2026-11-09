FROM php:8.4-apache

RUN apt-get update && apt-get install -y --no-install-recommends \
    libcurl4-openssl-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libxml2-dev \
    libzip-dev \
    $PHPIZE_DEPS \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j"$(nproc)" \
        curl \
        dom \
        gd \
        mysqli \
        pdo_mysql \
        soap \
        simplexml \
        xml \
        zip \
    && pecl install mcrypt-1.0.9 \
    && docker-php-ext-enable mcrypt \
    && apt-get purge -y --auto-remove $PHPIZE_DEPS \
    && rm -rf /var/lib/apt/lists/*

RUN a2enmod rewrite

RUN { \
    echo 'memory_limit=256M'; \
    echo 'upload_max_filesize=32M'; \
    echo 'post_max_size=32M'; \
    echo 'max_execution_time=500'; \
    echo 'max_input_time=500'; \
    echo 'allow_url_fopen=On'; \
    echo 'date.timezone=Asia/Kolkata'; \
} > /usr/local/etc/php/conf.d/farmstay24.ini

WORKDIR /var/www/html
