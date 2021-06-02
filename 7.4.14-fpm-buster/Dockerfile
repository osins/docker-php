FROM php:7.4.14-fpm-buster

COPY ./sources.list /etc/apt/sources.list
RUN apt update; \
    apt install -y apt-utils iputils-ping zip unzip git; \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"; \
    php -r "if (hash_file('sha384', 'composer-setup.php') === '756890a4488ce9024fc62c56153228907f1545c228516cbf63f885e036d37e9a59d27d63f46af1d4d07ee0f76181c7d3') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"; \
    php composer-setup.php; \
    php -r "unlink('composer-setup.php');"; \
    mv composer.phar /usr/local/bin/composer; \
    composer global require laravel/installer; \
    ln -s /root/.composer/vendor/bin/laravel /usr/local/bin/laravel; \
    curl --location --output /usr/local/bin/phpunit "https://phar.phpunit.de/phpunit.phar"; \
    chmod +x /usr/local/bin/phpunit; \
    phpunit --version
