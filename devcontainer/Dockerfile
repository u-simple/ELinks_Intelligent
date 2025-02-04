# .devcontainer/Dockerfile
# 使用官方 PHP 8.1 FPM 镜像作为基础
FROM php:8.1-fpm AS base

# 安装系统依赖和 PHP 扩展
RUN apt-get update && apt-get install -y \
    libonig-dev \
    libzip-dev \
    zip \
    unzip \
    git \
    && docker-php-ext-install pdo_mysql mbstring zip

# 安装 Composer（从官方 Composer 镜像拷贝）
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# 设置工作目录
WORKDIR /var/www

# 复制 Composer 文件并利用缓存安装依赖
COPY composer.json composer.lock ./
RUN composer install --prefer-dist --no-dev --no-scripts --no-progress

# 复制项目所有文件
COPY . .

# 暴露 PHP-FPM 默认端口（注意：实际开发中可能需要调整端口映射）
EXPOSE 9000

# 默认启动 PHP-FPM 服务
CMD ["php-fpm"]
