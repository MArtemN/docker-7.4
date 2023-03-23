FROM php:7.4-apache

RUN apt-get update && apt-get install -y \
        default-mysql-client zlib1g-dev libzip-dev libicu-dev libxml2-dev \
		libfreetype6-dev libjpeg62-turbo-dev libxpm-dev libwebp-dev libpng-dev \
		graphviz libcurl3-openssl-dev zip openssl curl \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
	&& docker-php-ext-configure gd --with-webp=/usr/include/ --with-jpeg=/usr/include/ --with-freetype=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-install mysqli && \
    docker-php-ext-install curl && \
    docker-php-ext-install tokenizer && \
    docker-php-ext-install json && \
    docker-php-ext-install opcache && \
    docker-php-ext-install zip && \
    docker-php-ext-install -j$(nproc) intl && \
    docker-php-ext-install soap && \
    docker-php-ext-install gettext

RUN pecl install xdebug  xhprof \
    docker-php-ext-enable xdebug \
    docker-php-ext-enable xhprof

#ADD xdebug.ini $PHP_INI_DIR/conf.d/docker-php-ext-xdebug.ini
#ADD php.ini $PHP_INI_DIR/php.ini

RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

WORKDIR /var/www/html

EXPOSE 9000
