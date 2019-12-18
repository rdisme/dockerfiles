# 定义PHP基础来源
FROM php:7.2-fpm

### set timezome
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# 更换apt-get源
RUN  sed -i "s@/archive.ubuntu.com/@/mirrors.aliyun.com/@g" /etc/apt/sources.list \
        && sed -i "s@http://deb.debian.org@http://mirrors.aliyun.com@g" /etc/apt/sources.list \
        && apt-get clean

# 安装composer
# 配置中国镜像
RUN cd ~ \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://packagist.laravel-china.org

# 安装PHPRedis扩展
RUN cd ~ \
    && curl -L -o 4.2.0.tar.gz https://github.com/phpredis/phpredis/archive/4.2.0.tar.gz \
    && tar -zxvf 4.2.0.tar.gz \
    && rm -rf 4.2.0.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv phpredis-4.2.0 /usr/src/php/ext/redis \
    && docker-php-ext-install redis

# 安装swoole扩展
RUN cd ~ \
    && curl -L -o v4.2.12.tar.gz https://github.com/swoole/swoole-src/archive/v4.2.12.tar.gz \
    && tar -zxvf v4.2.12.tar.gz \
    && rm -rf v4.2.12.tar.gz \
    && mkdir -p /usr/src/php/ext \
    && mv swoole-src-4.2.12 /usr/src/php/ext/swoole \
    && docker-php-ext-install swoole

# install seaslog扩展
RUN pecl install https://pecl.php.net/get/SeasLog-2.0.2.tgz \
    && docker-php-ext-enable seaslog

# 安装PHP扩展
RUN apt-get update \
	&& apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        unzip \
        libzip-dev \
        zip \
        libmcrypt-dev \
        supervisor \
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
        bcmath \
        sockets \
    && pecl install mcrypt-1.0.2 \
    && docker-php-ext-enable mcrypt