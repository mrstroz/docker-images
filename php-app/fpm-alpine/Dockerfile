ARG PHP_VERSION=8.1

FROM php:${PHP_VERSION}-fpm-alpine

# System dependencies
RUN apk update && apk upgrade && \
    apk add --no-cache \
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
    icu-dev \
    libzip-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libwebp-dev \
    freetype-dev \
    curl-dev \
    openssl-dev \
    git \
    nano \
    wget \
    unzip \
    linux-headers

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