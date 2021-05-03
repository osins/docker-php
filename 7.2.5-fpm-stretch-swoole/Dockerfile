FROM wangsying/php:7.2.5-fpm-stretch AS base_image

RUN export http_proxy=http://192.168.3.32:1080 \
    && export https_proxy=http://192.168.3.32:1080 \
    && mkdir -p /usr/src/swoole \
    && curl -L https://github.com/swoole/swoole-src/archive/v4.6.2.tar.gz | tar xvz -C /usr/src/swoole --strip 1  \
    && cd /usr/src/swoole \
    && phpize \
    && ./configure --enable-openssl --enable-http2 --enable-sockets \
    && make && make install \
    && docker-php-ext-enable swoole