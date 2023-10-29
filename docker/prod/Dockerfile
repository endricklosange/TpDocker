# Use the php:8.2-apache as the base image
FROM php:8.2-apache

# Set the Apache server name to "localhost" in the Apache configuration
RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

# Update package repositories and install necessary packages
RUN apt-get update \
    && apt-get install -y --no-install-recommends locales git libicu-dev g++ libpng-dev libxml2-dev libzip-dev libonig-dev libxslt-dev;

# Generate and configure UTF-8 locales
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Configure and install PHP extensions
RUN docker-php-ext-configure intl
RUN docker-php-ext-install pdo pdo_mysql gd opcache intl zip calendar dom mbstring zip gd xsl

# Install and enable APCu extension
RUN pecl install apcu && docker-php-ext-enable apcu

# Change ownership of the /var/www directory to the www-data user and group
RUN chown -R www-data:www-data /var/www

# Set the working directory to /var/www/app
WORKDIR /var/www/app

# Remove unnecessary packages and clean up
RUN apt-get remove -y git g++ libicu-dev libpng-dev libxml2-dev libzip-dev libonig-dev libxslt-dev && \
    apt-get autoremove -y && \
    apt-get clean

# Delete Composer installer
RUN rm /usr/local/bin/composer

# Disable default Apache site and remove default index.html
RUN a2dissite 000-default.conf && \
    rm /var/www/html/index.html

# Copy your Symfony application into the container
COPY . /var/www/app

# Ensure that the container runs with limited permissions
USER www-data

# Expose port 80
EXPOSE 80

# Start Apache server
CMD ["apache2-foreground"]
