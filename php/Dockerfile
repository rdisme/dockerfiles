# 定义PHP基础镜像
FROM php:8.0-fpm

# 更换apt-get源
RUN  sed -i "s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g" /etc/apt/sources.list \
        && sed -i "s@http://deb.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list \
        && apt-get clean

# 安装composer
# 配置aliyun镜像源
RUN cd ~ \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

RUN apt-get update \
    && apt-get install -y \
        git \
        zip \
        unzip \
    && docker-php-ext-install \
        pdo_mysql \
        mysqli