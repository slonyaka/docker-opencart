FROM php:7.3-apache

RUN a2enmod rewrite

RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libpng-dev \
  && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr --with-png-dir=/usr \
  && docker-php-ext-install -j "$(nproc)" gd


RUN docker-php-ext-install pdo_mysql mysqli && docker-php-ext-enable pdo_mysql

RUN apt-get update && \
    apt-get install -y \
        zlib1g-dev

RUN apt-get update \
     && apt-get install -y libzip-dev \
     && docker-php-ext-install zip
