FROM php:7.4.1-fpm
LABEL maintainer Arkadiusz Daniel <arkadiusz.daniel@gmail.com>

# Install fpm extension
RUN apt-get update && apt-get install -y \
        libzip-dev \
        libc-client-dev \
        libfreetype6-dev \
        libicu-dev \
        libonig-dev \
        libjpeg62-turbo-dev \
        libkrb5-dev \
        libmcrypt-dev \
        libpcre3-dev \
        libgmp3-dev \
        libpng-dev \
        libxml2-dev \
        libxml2-utils \
        libcairo2 \
        libfontconfig1 \
        libfreetype6 \
        libgif7 \
        libgomp1 \
        libpixman-1-0 \
        liblcms2-dev \
        libtiff5 \
        libxml2 \
        nano \
        wget \
        make \
        git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install  -j$(nproc) bcmath calendar exif gmp intl json mysqli pdo pdo_mysql soap xml zip \
    && pecl channel-update pecl.php.net \
    && pecl install apcu redis xdebug \
    && docker-php-ext-enable apcu redis xdebug

# Install fonts
RUN sed -i 's/$/ contrib/' /etc/apt/sources.list \
  && apt-get update && apt-get install --assume-yes \
    fontconfig \
    msttcorefonts \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Install libssl1.0.2
RUN wget http://ftp.br.debian.org/debian/pool/main/o/openssl1.0/libssl1.0.2_1.0.2s-1~deb9u1_amd64.deb \
 && apt-get install ./libssl1.0.2_1.0.2s-1~deb9u1_amd64.deb \
 && rm -r ./libssl1.0.2_1.0.2s-1~deb9u1_amd64.deb