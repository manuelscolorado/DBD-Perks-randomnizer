# Usa la versión de PHP que necesites (por ejemplo, PHP 8.2)
FROM php:8.2-fpm

# Instala las dependencias básicas, la extensión de MongoDB, git y zip
RUN apt-get update && apt-get install -y \
    libssl-dev \
    git \
    zip \
    unzip \
    nginx \
    && pecl install mongodb \
    && docker-php-ext-enable mongodb

# Instala Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copia los archivos de la aplicación
WORKDIR /var/www
COPY . .

# Ejecuta el comando para instalar las dependencias de Composer
RUN composer install

# Copia el archivo de configuración de Nginx
COPY nginx.conf /etc/nginx/nginx.conf

# Exponer puertos para Nginx
EXPOSE 9000

# Comando para iniciar PHP-FPM y Nginx
CMD ["php-fpm"]
