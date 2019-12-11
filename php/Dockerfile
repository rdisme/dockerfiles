# 定义PHP基础来源
FROM rdisme/php:7.2-fpm-1.1

# 安装composer
# 配置中国镜像
RUN cd ~ \
    && curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer config -g repo.packagist composer https://packagist.laravel-china.org