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
&& rm -rf /tmp/pear \
&& echo 'deb http://packages.dotdeb.org jessie all' > /etc/apt/sources.list.d/dotdeb.list \
&& apt-get install -y apt-transport-https \
&& curl http://www.dotdeb.org/dotdeb.gpg | apt-key add - \
&& apt-get update -y \
&& apt-get install -y php7.0 \ 
&& apt-get install -y php7.0-curl \ 
&&  ln -s /etc/php/7.0/cli/php.ini /usr/local/etc/php/php.ini


RUN pecl install -o -f redis xdebug     && rm -rf /tmp/pear     && echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini     && echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20121212/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini
