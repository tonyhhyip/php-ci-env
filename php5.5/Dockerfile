FROM php:5.5

RUN echo "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list

RUN apt-get update && \
    apt-get install -y --no-install-recommends git zip unzip zlib1g-dev libzip-dev && \
    rm -rf /var/lib/apt/lists/* && \
    docker-php-ext-install zip

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_VERSION 1.8.5

RUN curl https://composer.github.io/installer.sig | tr -d '\n' > installer.sig && \
    php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('SHA384', 'composer-setup.php') === file_get_contents('installer.sig')) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php'); unlink('installer.sig');" && \
    mv composer.phar /usr/local/bin/composer && \
    composer --ansi --version --no-interaction
