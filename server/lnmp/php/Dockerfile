FROM php:8.0-fpm-alpine

# 设置容器时区和宿主机相同
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

#  更新安装依赖包和 php 核心拓展
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories && apk update && apk upgrade \
&& apk add \
vim \
bash \
freetype-dev \
libjpeg-turbo-dev \
libpng-dev \
libzip-dev \
supervisor \ 
&& docker-php-ext-configure gd --with-freetype --with-jpeg \
&& docker-php-ext-install -j$(nproc) gd \
&& docker-php-ext-install zip \
&& docker-php-ext-install pdo_mysql \
&& docker-php-ext-install opcache \
&& docker-php-ext-install mysqli \
&& apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev libzip-dev

#源码包不存在的扩展用 pecl 装
RUN apk add --no-cache $PHPIZE_DEPS \ 
&& pecl install redis \
&& pecl install xdebug \
&& docker-php-ext-enable redis xdebug

# 安装 composer 替换镜像
RUN cd / \
&& php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" \
&& php composer-setup.php \
&& php -r "unlink('composer-setup.php');" \
&& chmod a+x composer.phar \
&& mv ./composer.phar /usr/local/bin/composer \
&& composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

WORKDIR /data