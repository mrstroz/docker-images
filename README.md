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
docker build -t mariuszstroz/php8.1-fpm-alpine .
```

#### Custom Build with Arguments

Customize your PHP image by specifying version and variant:

```bash
# Build PHP 8.3 with Apache
cd php-app/apache
docker build --build-arg PHP_VERSION=8.3 -t mariuszstroz/php8.3-apache .

# Build PHP 8.2 with FPM Alpine
cd php-app/fpm-alpine
docker build --build-arg PHP_VERSION=8.2 -t mariuszstroz/php8.2-fpm-alpine .
```

### Available Build Arguments

- `PHP_VERSION`: Specify PHP version (e.g., 8.1, 8.2, 8.3)
- `PHP_VARIANT`: Choose image variant (e.g., `fpm-alpine`, `apache`)

### Pushing Images to Docker Hub

#### Login to Docker Hub

```bash
docker login
```

#### Push Built Image

```bash
# Push the image you just built
docker push mariuszstroz/php8.1-fpm-alpine
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
docker tag mariuszstroz/php8.1-fpm-alpine ghcr.io/USERNAME/php8.1-fpm-alpine

# Push the tagged image
docker push ghcr.io/USERNAME/php8.1-fpm-alpine
```
