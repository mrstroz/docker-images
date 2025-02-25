ARG PHP_VERSION=8.1

FROM php:${PHP_VERSION}-apache

# System dependencies
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
    g++ \
    gcc \
    libxml2 \
    libxslt-dev \
    #        nodejs \
    #        npm \
    autoconf \
    automake \
    make \
    bash \
    libicu-dev \
    libzip-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libwebp-dev \
    libfreetype6-dev \
    libcurl4-openssl-dev \
    openssl \
    git \
    nano \
    wget \
    unzip \
    linux-headers-amd64

# PHP extensions
RUN docker-php-ext-configure gd --with-jpeg --with-webp --with-freetype && \
    docker-php-ext-install -j$(nproc) \
    bcmath \
    opcache \
    intl \
    zip \
    pdo_mysql \
    fileinfo \
    dom \
    gd \
    sockets \
    xml \
    curl

# MongoDB extension
RUN pecl install mongodb-1.19.4 && \
    docker-php-ext-enable mongodb

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer