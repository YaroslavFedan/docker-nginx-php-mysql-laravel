FROM php:7.4-fpm-alpine

ADD ./www.conf /usr/local/etc/php-fpm.d/

RUN addgroup -g 1000 laravel && adduser -G laravel -g laravel -s /bin/sh -D laravel

RUN mkdir -p /var/www/html

RUN chown laravel:laravel /var/www/html

WORKDIR /var/www/html

RUN apk update \
    php7.4-pgsql php7.4-sqlite3 php7.4-gd \
    php7.4-curl php7.4-memcached \
    php7.4-imap php7.4-mysql php7.4-mbstring \
    php7.4-xml php7.4-zip php7.4-bcmath php7.4-soap \
    php7.4-intl php7.4-readline php7.4-pcov \
    php7.4-msgpack php7.4-igbinary php7.4-ldap \
    php7.4-redis

# Setup GD extension
RUN apk add --no-cache \
      freetype \
      libjpeg-turbo \
      libpng \
      freetype-dev \
      libjpeg-turbo-dev \
      libpng-dev \
    && docker-php-ext-configure gd \
      --with-freetype=/usr/include/ \
      # --with-png=/usr/include/ \ # No longer necessary as of 7.4; https://github.com/docker-library/php/pull/910#issuecomment-559383597
      --with-jpeg=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-enable gd \
    && apk del --no-cache \
      freetype-dev \
      libjpeg-turbo-dev \
      libpng-dev \
    && rm -rf /tmp/*


# Install intl extension
RUN apk add --no-cache \
    icu-dev \
    && docker-php-ext-install -j$(nproc) intl \
    && docker-php-ext-enable intl \
    && rm -rf /tmp/*

# Install mbstring extension
RUN apk add --no-cache \
    oniguruma-dev \
    && docker-php-ext-install mbstring \
    && docker-php-ext-enable mbstring \
    && rm -rf /tmp/*

# Install zip extension
RUN apk add --no-cache \
    zip libzip-dev \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-enable zip \
    && rm -rf /tmp/*

# imagick
RUN apk add --update --no-cache autoconf g++ imagemagick-dev libtool make pcre-dev \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && apk del autoconf g++ libtool make pcre-dev   

RUN apk update && apk add bash

# Get latest Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer    

# Configure PHP
COPY php.ini $PHP_INI_DIR/conf.d/php.ini

RUN docker-php-ext-install pdo pdo_mysql