# Docker Images Repository

## Overview

This repository contains custom Docker images for personal and professional projects, providing flexible and reproducible development environments. The images are designed to be easily customizable and suitable for various PHP-based applications.

## Prerequisites

Before you begin, ensure you have the following installed:

- Docker (version 20.10 or higher)
- Docker Hub account (optional, for pushing images)

## PHP Image Build Process

### Directory Navigation

Navigate to the specific image directory:

```bash
cd php-app/fpm-alpine #or
cd php-app/apache
```

### Building Images

#### Default Build

Build a default PHP image with predefined configurations:

```bash
docker build -t mariuszstroz/php8.4-fpm-alpine .
```

#### Custom Build with Arguments

Customize your PHP image by specifying version and variant:

```bash
# Build PHP 8.3 with Apache
cd php-app/apache
docker build --build-arg PHP_VERSION=8.3.36 -t mariuszstroz/php8.3-apache .

# Build PHP 8.2 with FPM Alpine
cd php-app/fpm-alpine
docker build --build-arg PHP_VERSION=8.2.35 -t mariuszstroz/php8.2-fpm-alpine .
```

### Available Build Arguments

- `PHP_VERSION`: Exact PHP patch version. Default: `8.4.27`. Supported: `8.2.35`, `8.3.36`, `8.4.27`, `8.5.12` (October 2026 security release). PHP 8.1 is EOL and is no longer supported.
  - **Known issue:** `8.5.12` does not build yet, because `pecl install mongodb-1.19.4` fails on PHP 8.5. The MongoDB extension must be upgraded before you can build 8.5 images.

### Pushing Images to Docker Hub

#### Login to Docker Hub

```bash
docker login
```

#### Push Built Image

```bash
# Push the image you just built
docker push mariuszstroz/php8.4-fpm-alpine
```

### Pushing Images to GitHub Container Registry (ghcr.io)

#### Export GitHub Token to ENV variables

```bash
export GITHUB_TOKEN=YOUR_TOKEN
```

#### Login to GitHub Container Registry

```bash
echo $GITHUB_TOKEN | docker login ghcr.io -u USERNAME --password-stdin
```

#### Tag and Push Built Image

```bash
# Tag the image you just built
docker tag mariuszstroz/php8.4-fpm-alpine ghcr.io/USERNAME/php8.4-fpm-alpine

# Push the tagged image
docker push ghcr.io/USERNAME/php8.4-fpm-alpine
```
