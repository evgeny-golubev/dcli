FROM php:5.4-fpm
MAINTAINER IOXICO <admin@ioxico.com>

RUN apt-get update

RUN pecl install zendopcache-7.0.5
RUN echo "extension=opcache.so" > /usr/local/etc/php/conf.d/opcache.ini

RUN docker-php-ext-install dba

RUN apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd

RUN apt-get install -y libmcrypt-dev
RUN docker-php-ext-install mcrypt

RUN docker-php-ext-install iconv
RUN docker-php-ext-install mbstring

RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mysqli

RUN apt-get install -y libxslt-dev
RUN docker-php-ext-install xsl

RUN docker-php-ext-install xmlrpc

RUN apt-get install -y libicu-dev

RUN apt-get install -y geoip-bin geoip-database libgeoip-dev
RUN apt-get install -y php5-geoip
