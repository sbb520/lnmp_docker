FROM php:7.2-fpm
COPY sources.list /etc/apt/sources.list

RUN apt-get update 
RUN apt-get install -y \
    apt-utils \
    openssl \
    libssl1.0-dev \
    libssh-dev \
    pkg-config \
    libmemcached-dev \
    libfreetype6-dev \
    libjpeg-dev \
    libpng-dev 

RUN docker-php-ext-install zip  mbstring  pdo_mysql opcache

#新增bcmath拓展
RUN docker-php-source extract \
    && cd /usr/src/php/ext/bcmath \
    && phpize \
    && ./configure --with-php-config=/usr/local/bin/php-config \
    && make && make install \
    && docker-php-ext-enable bcmath

#新增gd库拓展
RUN docker-php-source extract \
    && cd /usr/src/php/ext/gd \
    && phpize \
    && ./configure --with-php-config=/usr/local/bin/php-config \
    --with-jpeg-dir \
    --with-png-dir=/usr/include/png/  \
    --with-freetype-dir \
    && make && make install \
    && docker-php-ext-enable gd


#新增pcntl库拓展
RUN docker-php-source extract \
    && cd /usr/src/php/ext/pcntl \
    && phpize \
    && ./configure --with-php-config=/usr/local/bin/php-config \
    && make && make install \
    && docker-php-ext-enable pcntl

# Composer
ADD composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

WORKDIR /data/wwwroot/

EXPOSE 9000

