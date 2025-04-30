# Use official PHP image with necessary extensions
FROM php:8.3-cli

# Install dependencies and PHP extensions
RUN apt-get update && apt-get install -y \
    libsqlite3-dev \
    unzip \
    git \
    && docker-php-ext-install pdo pdo_sqlite

# Install Composer globally
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Set working directory inside container
WORKDIR /app

# Copy only backend (assuming Dockerfile is inside /backend)
COPY . /app

# Install PHP dependencies
RUN composer install --no-dev --optimize-autoloader

# Set environment variables (can also be overridden in Render settings)
ENV APP_ENV=prod

# Expose port 8000 for Symfony
EXPOSE 8000

# Set default command to run Symfony server (built-in for dev use)
CMD ["php", "-S", "0.0.0.0:8000", "-t", "public"]
