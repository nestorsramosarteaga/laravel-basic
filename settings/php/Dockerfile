FROM php:8.4-fpm-alpine

ARG PUID=1000
ARG PGID=1000

RUN apk add --no-cache \
  bash \
  nano \
  linux-headers \
  libpng-dev \
  zlib-dev \
  freetype-dev \
  libjpeg-turbo-dev \
  libzip-dev \
  zip \
  unzip \
  curl \
  nodejs \
  npm \
  $PHPIZE_DEPS \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install -j$(nproc) pdo pdo_mysql gd zip \
  && pecl install xdebug \
  && docker-php-ext-enable xdebug \
  && apk del $PHPIZE_DEPS

RUN cp "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN addgroup -g ${PGID} appuser \
    && adduser -u ${PUID} -G appuser -s /bin/bash -D appuser

RUN mkdir -p /var/www/app/storage /var/www/app/bootstrap/cache \
    && chown -R appuser:appuser /var/www/app \
    && chmod -R 775 /var/www/app/storage /var/www/app/bootstrap/cache

USER appuser
WORKDIR /var/www/app

COPY ./conf.d/custom.ini /usr/local/etc/php/conf.d/
