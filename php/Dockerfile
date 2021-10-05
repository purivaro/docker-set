FROM php:7.4.24-fpm-buster

LABEL author="purivaro <aun.puri@gmail.com>"
LABEL version="1.0"

RUN apt-get update && apt-get install -y git unzip

RUN docker-php-ext-install mysqli pdo pdo_mysql

RUN echo '[PHP]\ndate.timezone = Asia/Bangkok' > /usr/local/etc/php/conf.d/setup_php.ini
RUN echo "error_reporting = E_ALL & ~E_NOTICE & ~E_DEPRECATED & ~E_STRICT" >> /usr/local/etc/php/conf.d/setup_php.ini
RUN echo "display_errors = On" >> /usr/local/etc/php/conf.d/setup_php.ini
RUN echo "upload_max_filesize = 30M" >> /usr/local/etc/php/conf.d/setup_php.ini
RUN echo "post_max_size = 30M" >> /usr/local/etc/php/conf.d/setup_php.ini


RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version


RUN apt-get update && apt-get install -y libmagickwand-dev --no-install-recommends && rm -rf /var/lib/apt/lists/*
RUN printf "\n" | pecl uninstall imagick
RUN printf "\n" | pecl install imagick
RUN docker-php-ext-enable imagick

RUN apt-get -yqq update
RUN apt-get -yqq install exiftool
RUN docker-php-ext-configure exif
RUN docker-php-ext-install exif
RUN docker-php-ext-enable exif

RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/ \
    && docker-php-ext-install gd

# Whatever you did in your PHP Dockerfile
# this was missing for some reason. Didn't require last time.
RUN apt-get install -y gnupg2
# Removing /var/lib/apt/lists worked
RUN rm -rf /var/lib/apt/lists/ && curl -sL https://deb.nodesource.com/setup_16.x | bash -
RUN apt-get install nodejs -y
