FROM php:8.1-fpm

ENV TZ=Asia/Shanghai

#COPY ./sources.list /etc/apt/sources.list

RUN apt-get update && apt-get install -y -f --allow-downgrades \
        sudo \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        zip \
        zlib1g-dev \
        net-tools \
        procps \
        curl \
        wget \
        libzip-dev

RUN  docker-php-ext-install -j$(nproc) iconv mysqli pdo_mysql zip pcntl bcmath

RUN  docker-php-ext-configure gd --with-freetype --with-jpeg

RUN docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-install -j$(nproc)  exif

RUN pecl install -o -f mcrypt && \
docker-php-ext-enable mcrypt

RUN pecl install -o -f redis \
&&  docker-php-ext-enable redis

RUN pecl install -o -f xlswriter \
&&  docker-php-ext-enable xlswriter

RUN rm -rf /tmp/pear

COPY ./php.ini /usr/local/etc/php/conf.d/zz-php.ini
COPY ./php-fpm.conf /usr/local/etc/php-fpm.d/zz-php-fpm.conf