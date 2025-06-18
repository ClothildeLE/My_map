# Use an official PHP-FPM image with a specific version
FROM php:8.2-fpm-alpine

# Install necessary extensions for common PHP applications and PostgreSQL
RUN apk add --no-cache \
    nginx \
    postgresql-dev \
    && docker-php-ext-install pdo_pgsql opcache \
    && docker-php-ext-enable opcache \
    && rm -rf /var/cache/apk/*

# Set working directory inside the container
WORKDIR /var/www/html

# Copy your PHP application code into the container
COPY . .

# Install Composer dependencies
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer
RUN composer install --no-dev --optimize-autoloader

# Expose port 9000 for PHP-FPM
EXPOSE 9000

# Start PHP-FPM
CMD ["php-fpm"]

