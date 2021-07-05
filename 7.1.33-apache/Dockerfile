FROM php:7.1.33-apache-stretch

#tag： wangsying/php:7.1.33-apache

COPY ./sources.list /etc/apt/sources.list.cn
COPY ./package/wkhtmltox_0.12.6-1.stretch_amd64.deb .
COPY ./package/ImageMagick.tar.gz .

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer \
    && mv /etc/apt/sources.list /etc/apt/sources.list.bak \
    && mv /etc/apt/sources.list.cn /etc/apt/sources.list \
    && apt-get update \
    && apt-get -y upgrade \
    && apt-get install -y \
    wget \
    curl \
    libcurl4-gnutls-dev \
    libicu-dev \
    libpq-dev \
    libmcrypt-dev \
    libzip-dev \
    zlib1g-dev \
    libmemcached-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libxml2-dev \
    xfonts-base \
    xfonts-75dpi \
    fontconfig \
    libfontenc1 \
    libjpeg62-turbo \
    libx11-6 \
    libx11-data \
    libxau6 \
    libxcb1 \
    libxdmcp6 \
    libxext6 \
    libxfont1 \
    libxrender1 \
    x11-common \
    xfonts-encodings \
    xfonts-utils \
    xvfb \
    pkg-config \
    libxrender1 \
    && dpkg -i wkhtmltox_0.12.6-1.stretch_amd64.deb && apt -f install \
    && rm -rf wkhtmltox_0.12.6-1.stretch_amd64.deb \
    && tar xvzf ImageMagick.tar.gz \
    && cd ImageMagick-7.0.11-10 && ./configure && make && make install && ldconfig /usr/local/lib \
    && whereis magick && magick -version \
    && cd .. && rm -rf ImageMagick-7.0.11-10 && rm -rf ImageMagick.tar.gz \
    && pecl install xdebug-2.9.0 \
    && pecl install memcached \
    && pecl install redis \
    && pecl install imagick \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd \
    && docker-php-ext-install -j$(nproc) \
    gd \
    zip \
    intl \
    mbstring \
    mcrypt \
    pcntl \
    mysqli \
    pdo \
    pdo_mysql \
    pdo_pgsql \
    pgsql \
    opcache \
    shmop \
    soap \
    bcmath \
    calendar \
    curl \
    exif \
    iconv \
    tokenizer \
    xml \
    && docker-php-ext-enable xdebug memcached redis imagick \
    && a2enmod rewrite ssl \
    && apt-get clean -y && mv /etc/apt/sources.list.bak /etc/apt/sources.list \
    && rm -rf /tmp/* && rm -rf /var/lib/apt/lists/*
    
WORKDIR /var/www

EXPOSE 80

CMD ["apache2-foreground"]