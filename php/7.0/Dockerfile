FROM php:7.0-fpm
MAINTAINER IOXICO <admin@ioxico.com>

RUN apt-get update

RUN apt-get install -y --no-install-recommends \
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
    nano \
    git \
    mysql-client

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

RUN apt-get -y install libmemcached11 libmemcachedutil2 libmemcached-dev \
    && cd /usr/local/share \
    && git clone --branch php7 https://github.com/php-memcached-dev/php-memcached \
    && cd php-memcached \
    && phpize \
    && ./configure \
    && make \
    && echo "extension=/usr/local/share/php-memcached/modules/memcached.so" > /usr/local/etc/php/conf.d/memcached.ini

RUN curl -OsSL https://phar.phpunit.de/phpunit.phar \
    && chmod +x phpunit.phar \
    && mv phpunit.phar /usr/local/bin/phpunit
    
RUN apt-get -y purge git \
    && apt-get -y autoclean \
    && apt-get -y autoremove \
    && rm -rf /var/lib/apt/lists/*
