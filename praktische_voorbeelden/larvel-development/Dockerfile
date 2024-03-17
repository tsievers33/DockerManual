FROM php:8.2-apache

# clean apt repo
RUN apt clean

# Install dependencies
RUN apt-get update && apt-get --no-install-recommends install -y build-essential


RUN apt-get -y --no-install-recommends install curl libzip-dev zip nodejs npm --fix-missing

# Enable mod_rewrite
RUN a2enmod rewrite

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql zip

ENV APACHE_DOCUMENT_ROOT=/var/www/html/public
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf

# Copy the application code
COPY . /var/www/html
COPY composer.json composer.json

# Set the working directory
WORKDIR /var/www/html

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install project dependencies
RUN composer install --ignore-platform-req=ext-gd --optimize-autoloader
RUN npm ci --ignore-scripts \
    && npm run build
    
# Set permissions
RUN chown -R www-data:www-data /var/www/html/storage /var/www/html/bootstrap/cache

# Safety feature?
RUN rm composer.json && rm composer.lock
