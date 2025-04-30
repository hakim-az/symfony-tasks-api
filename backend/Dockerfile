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

# Copy Symfony project files into the container
COPY . /app

# Install PHP dependencies
RUN composer install --no-dev --optimize-autoloader

# Expose port 8000 for the Symfony server
EXPOSE 8000

# Set environment variables (can also override via Render's dashboard)
ENV APP_ENV=prod

# Start the Symfony local web server
CMD ["php", "-S", "0.0.0.0:8000", "-t", "public"]
