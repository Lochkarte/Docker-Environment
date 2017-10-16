FROM php:7.1.6-fpm
RUN apt-get update && apt-get install -y \
		libfreetype6-dev \
		libjpeg62-turbo-dev \
		libmcrypt-dev \
		libpng12-dev \
		libxml2-dev \
	&& docker-php-ext-install -j$(nproc) iconv mcrypt mbstring zip pdo pdo_mysql xml \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd

RUN curl -sS https://getcomposer.org/installer | php

RUN apt-get update && apt-get -y install libz-dev libmemcached-dev libmemcached11 libmemcachedutil2 build-essential \
&& pecl install memcached \
&& echo extension=memcached.so >> /usr/local/etc/php/conf.d/memcached.ini \
&& apt-get remove -y build-essential libmemcached-dev libz-dev \
&& apt-get autoremove -y \
&& apt-get clean \
&& rm -rf /tmp/pear

RUN pecl install -o -f redis xdebug     && rm -rf /tmp/pear     && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini     && echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20121212/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini
