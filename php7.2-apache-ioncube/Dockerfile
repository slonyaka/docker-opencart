FROM php:7.2-apache

RUN a2enmod rewrite

RUN apt-key update && apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
  gnupg \
  gnupg2 \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libpng-dev \
  && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-freetype-dir=/usr --with-jpeg-dir=/usr --with-png-dir=/usr \
  && docker-php-ext-install gd


RUN docker-php-ext-install pdo_mysql mysqli && docker-php-ext-enable pdo_mysql

RUN apt-get update && \
    apt-get install -y \
        zlib1g-dev

RUN apt-get update \
     && apt-get install -y libzip-dev \
     && docker-php-ext-install zip

RUN curl -o ioncube.tar.gz http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz \
    && tar -xvvzf ioncube.tar.gz \
    && ls -la \
    && cp ioncube/ioncube_loader_lin_7.2.so /usr/local/lib/php/extensions/no-debug-non-zts-20100525/ioncube_loader_lin_7.2.so \
    && echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20100525/ioncube_loader_lin_7.2.so" > /usr/local/etc/php/conf.d/00_docker-php-ext-ioncube_loader_lin_7.2.ini
