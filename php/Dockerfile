ARG PHP_VERSION
ARG SWOOLE_VERSION
ARG AMQP_VERSION

FROM php:$PHP_VERSION-fpm-alpine

COPY config/php.ini /usr/local/etc/php

#RUN apk add autoconf gcc \
#    && wget https://github.com/phpredis/phpredis/archive/3.1.3.tar.gz \
#    && tar -zxvf 3.1.3.tar.gz \
#    && cd phpredis-3.1.3 \
#    && /usr/local/bin/phpize \
#    && ./configure --with-php-config=/usr/local/bin/php-config \
#    && make \
#    && make install \

ARG PHPREDIS_VERSION
#安装想要的扩展
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN cd ~ \
    && wget https://codeload.github.com/phpredis/phpredis/tar.gz/refs/tags/$PHPREDIS_VERSION \
    && tar -zxvf $PHPREDIS_VERSION \
    && mkdir -p /usr/src/php/ext \
    && mv phpredis-$PHPREDIS_VERSION /usr/src/php/ext/redis \
    && docker-php-ext-install redis \
#   && wget https://pecl.php.net/get/amqp-$AMQP_VERSION.tgz \
#   && tar -zxvf amqp-$AMQP_VERSION.tgz \
#   && mv amqp-$AMQP_VERSION /usr/src/php/ext/amqp \
#   && apk add rabbitmq-c-dev \
#   && docker-php-ext-install amqp \

    && apk add libstdc++ libpng-dev \

#   && cd ~ \
#   && wget https://github.com/swoole/swoole-src/archive/v$SWOOLE_VERSION.tar.gz \
#   && tar -zxvf v$SWOOLE_VERSION.tar.gz \
#   && mkdir -p /usr/src/php/ext \
#   && mv swoole-src-$SWOOLE_VERSION /usr/src/php/ext/swoole \
#   && docker-php-ext-install swoole \

    && docker-php-ext-install pdo_mysql mysqli pcntl gd bcmath opcache \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
