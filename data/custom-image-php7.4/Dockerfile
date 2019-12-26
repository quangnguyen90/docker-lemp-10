# Gunakan bas image resmi dari PHP
FROM php:7.4-fpm-alpine

# Install beberapa library tambahan yang dibutuhkan oleh ektensi GD dan ZIP
RUN apk add --no-cache \
    freetype libjpeg-turbo libpng libwebp \
    freetype-dev libjpeg-turbo-dev libpng-dev libwebp-dev \
    libzip-dev

# Lakukan konfigurasi awal sebelum menginstal ektensi GD
RUN docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg \
    --with-webp

# Install ektensi yang kita butuhkan
RUN docker-php-ext-install -j $(nproc) \
    gd mysqli opcache pdo_mysql zip

# Urutkan ulang ektensi yang baru saja diinstall
RUN rm -f /usr/local/etc/php/conf.d/docker-php-ext-*.ini \
    && docker-php-ext-enable --ini-name 20-gd.ini gd \
    && docker-php-ext-enable --ini-name 10-mysqli.ini mysqli \
    && docker-php-ext-enable --ini-name 05-opcache.ini opcache \
    && docker-php-ext-enable --ini-name 10-pdo_mysql.ini pdo_mysql \
    && docker-php-ext-enable --ini-name 20-sodium.ini sodium \
    && docker-php-ext-enable --ini-name 20-zip.ini zip
