FROM php:7.1-fpm

##docker-php-ext 是php官方提供的拓展工具
##docker-php-ext-* 脚本接受任意的绝对路径（不支持相对路径，以便与系统内置的扩展程序进行区分）
##pecl 国内被墙 无法使用
##例子:  RUN curl -fsSL 'https://xcache.lighttpd.net/pub/Releases/3.2.0/xcache-3.2.0.tar.gz' -o xcache.tar.gz \
##    && mkdir -p /tmp/xcache \
##    && tar -xf xcache.tar.gz -C /tmp/xcache --strip-components=1 \
##    && rm xcache.tar.gz \
##    && docker-php-ext-configure /tmp/xcache --enable-xcache \
##    && docker-php-ext-install /tmp/xcache \
##    && rm -r /tmp/xcache

RUN apt-get update \
	# 相关依赖必须手动安装
	&& apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
    # 安装扩展
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    # 如果安装的扩展需要自定义配置时
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd