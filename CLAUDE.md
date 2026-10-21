# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository contains custom Docker images for PHP-based applications. Two image variants are available:
- **fpm-alpine**: Lightweight PHP-FPM on Alpine Linux
- **apache**: PHP with Apache web server on Debian

## Build Commands

Build images from their respective directories:

```bash
# FPM Alpine variant
cd php-app/fpm-alpine
docker build --build-arg PHP_VERSION=8.3.36 -t mariuszstroz/php8.3-fpm-alpine .

# Apache variant
cd php-app/apache
docker build --build-arg PHP_VERSION=8.3.36 -t mariuszstroz/php8.3-apache .
```

### Build Arguments
- `PHP_VERSION`: exact PHP patch version (default: 8.4.27). Supported: 8.2.35, 8.3.36, 8.4.27, 8.5.12 (October 2026 security release). Pin exact patch versions, not floating minor tags. 8.1 is EOL and no longer supported.
  - Known issue: 8.5.12 does not build yet, because `pecl install mongodb-1.19.4` fails on PHP 8.5. Upgrade the MongoDB extension before building 8.5 images.

## Architecture

Both Dockerfiles follow the same structure:
1. Base image from official PHP Docker images
2. System dependencies (build tools, libraries)
3. PHP extensions configured and installed
4. MongoDB extension via PECL
5. Composer installed from official image

### Key Differences Between Variants
- **fpm-alpine**: Uses `apk` package manager, Alpine-specific packages (e.g., `linux-headers`, `icu-dev`)
- **apache**: Uses `apt-get` package manager, Debian packages (e.g., `linux-headers-amd64`, `libicu-dev`)

### Installed PHP Extensions
bcmath, opcache, intl, zip, pdo_mysql, fileinfo, dom, gd (with jpeg/webp/freetype), sockets, xml, curl, mongodb
