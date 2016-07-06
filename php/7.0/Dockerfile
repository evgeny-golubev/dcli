FROM php:7.0-fpm
MAINTAINER IOXICO <admin@ioxico.com>

RUN apt-get update

RUN apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng12-dev \
    libmcrypt-dev \
    libxslt-dev \
    libicu-dev \
    unzip \
    geoip-bin \
    geoip-database \
    libgeoip-dev \
    php5-geoip

RUN rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install \
    opcache \
    dba \
    gd \
    iconv \
    mcrypt \
    mbstring \
    pdo_mysql \
    mysqli \
    soap \
    zip \
    xsl \
    xmlrpc

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

RUN php -r "readfile('http://files.drush.org/drush.phar');" > drush \
    && chmod +x drush \
    && mv drush /usr/local/bin
