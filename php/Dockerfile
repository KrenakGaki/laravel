FROM php:8.4-apache

# Instala dependências necessárias para Laravel
RUN apt-get update && apt-get install -y \
    build-essential \
    libpq-dev \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    git \
    curl \
&& docker-php-ext-install pdo pdo_pgsql mbstring exif pcntl bcmath gd

# Habilita mod_rewrite do Apache para Laravel
RUN a2enmod rewrite

WORKDIR /var/www

# Usuário opcional (para desenvolvimento)
RUN useradd -G www-data,root -u 1000 developer
RUN chown -R developer:developer /var/www

USER developer

COPY laravel.conf /etc/apache2/sites-available/000-default.conf
RUN a2enmod rewrite

EXPOSE 80

# Apache já é entrypoint na imagem php:*-apache
