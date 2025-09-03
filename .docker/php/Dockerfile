# Chọn image PHP phù hợp (Laravel 12 yêu cầu PHP >= 8.2)
FROM php:8.4-fpm

# Cài đặt các package cần thiết
RUN apt-get update && apt-get install -y \
    git curl libpng-dev libjpeg-dev libfreetype6-dev libonig-dev \
    libxml2-dev zip unzip libzip-dev libpq-dev libicu-dev g++ \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd intl zip \
    && docker-php-ext-enable opcache

# Cài composer
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Tạo thư mục app
WORKDIR /var/www/html

# Copy file project vào container
COPY . .

# Đảm bảo storage & bootstrap/cache tồn tại rồi mới chmod/chown
RUN mkdir -p storage bootstrap/cache \
    && chown -R www-data:www-data storage bootstrap/cache \
    && chmod -R 775 storage bootstrap/cache

# Cổng chạy PHP-FPM
EXPOSE 9000

CMD ["php-fpm"]
