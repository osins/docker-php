FROM php:7.1.14-fpm-stretch

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    apt-utils iputils-ping \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libmemcached-dev \
    libxml2-dev \
    libbz2-dev \
    librabbitmq-dev \
    libzip-dev \
    zlib1g-dev \
    libz-dev \
    libpq-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libicu-dev \
    libssl-dev \
    libmcrypt-dev \
    libonig-dev \
    libcurl3 \
    libcurl3-openssl-dev \
    locales \
    supervisor \
    jpegoptim optipng pngquant gifsicle \
    nano \
    unzip \
    zip \
    curl \
    git \
    && echo "apt-get install complete!" \
    && docker-php-source extract \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql \
    && docker-php-ext-configure bcmath --enable-bcmath \
    && docker-php-ext-configure pcntl --enable-pcntl \
    && docker-php-ext-configure mbstring --enable-mbstring \
    && docker-php-ext-install bcmath pdo_mysql mbstring mysqli pcntl soap sockets \
    && echo "pdo_mysql bcmath pcntl mbstring install complete!" \
    && echo "\nyes" | pecl install mcrypt \
    && docker-php-ext-enable mcrypt \
    && echo "install memcached" \
    && mkdir /usr/src/php/ext/memcached \
    && curl -L https://github.com/php-memcached-dev/php-memcached/archive/v3.0.4.tar.gz | tar xvz -C /usr/src/php/ext/memcached --strip 1  \
    && docker-php-ext-configure memcached \
    && docker-php-ext-install memcached \
    && echo "install redis" \
    && mkdir /usr/src/php/ext/redis \
    && curl -L https://github.com/phpredis/phpredis/archive/3.0.0.tar.gz | tar xvz -C /usr/src/php/ext/redis --strip 1 \
    && docker-php-ext-configure redis \
    && docker-php-ext-install redis \
    && echo "install zip" \
    && docker-php-ext-install zip \
    && echo "install gd" \
    && docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install opcache \
    && docker-php-ext-enable opcache \
    && echo "installl igbinary msgpack xdebug amqp" \
    && pecl install igbinary msgpack xdebug amqp  \
    && echo "enable igbinary msgpack xdebug amqp" \
    && docker-php-ext-enable igbinary msgpack xdebug amqp \
    && curl -L https://github.com/unicode-org/icu/releases/download/release-68-2/icu4c-68_2-src.tgz | tar xvz -C /usr/src/php/ext/intl --strip 1 \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl \
    && echo "install composer" \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && echo "clear temp files" \
    && docker-php-source delete \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* \
    && apt-get clean 

