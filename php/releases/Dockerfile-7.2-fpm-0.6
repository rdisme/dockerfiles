# 定义PHP基础来源
FROM registry.cn-beijing.aliyuncs.com/rdisme/php:7.2-fpm-0.5

# 安装PHP扩展
RUN apt-get update \
	&& apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        unzip \
        libzip-dev \
        zip \
    && docker-php-ext-configure gd \
        --with-gd \
        --with-freetype-dir \
        --with-jpeg-dir \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install \
        -j$(nproc) \
        gd \
        pdo_mysql \
        mysqli \
        zip \
        bcmath