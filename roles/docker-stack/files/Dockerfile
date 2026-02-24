# /opt/ai-stack/lamp/Dockerfile
FROM php:8.1-apache

# Install system dependencies needed for PostgreSQL & MariaDB extensions
RUN apt-get update && apt-get install -y \
    lynx \
    cron \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Install PHP extensions:
# - mysqli + pdo_mysql   (MariaDB/MySQL) — already in base image, but we force-enable
# - pgsql + pdo_pgsql    (PostgreSQL)
RUN docker-php-ext-install \
    mysqli \
    pdo_mysql \
    pgsql \
    pdo_pgsql

# Enable Apache modules you commonly need
RUN a2enmod \
    rewrite \
    headers \
    expires \
    deflate

# Optional: install composer (very common in PHP projects)
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

# Optional: custom php.ini overrides (create this file on host if needed)
# COPY php.ini /usr/local/etc/php/conf.d/custom.ini
