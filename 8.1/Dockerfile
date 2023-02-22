#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "update.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#
FROM php:8.1

LABEL org.opencontainers.image.source="https://github.com/MilesChou/docker-xdebug" \
    repository="https://github.com/MilesChou/docker-xdebug" \
    maintainer="MilesChou <jangconan@gmail.com>"

# install xdebug
RUN set -xe && \
        docker-php-source extract && \
        pecl install xdebug && \
        docker-php-ext-enable xdebug && \
        docker-php-source delete && \
        php -v && \
        php -m

COPY docker-xdebug-* /usr/local/bin/

# install other extenstions

# php extensions
RUN docker-php-ext-install bz2 \
    && docker-php-ext-install gd \
    && docker-php-ext-install intl \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install opcache \
    && docker-php-ext-install zip \
    && docker-php-ext-install exif \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl && docker-php-ext-install imap \
    && docker-php-ext-configure bcmath --enable-bcmath \
    && docker-php-ext-configure pcntl --enable-pcntl \
    && docker-php-ext-configure mbstring --enable-mbstring \
    && docker-php-ext-install soap \
    && docker-php-ext-configure calendar \
    && docker-php-ext-install bcmath

# configure GD
RUN docker-php-ext-configure gd --enable-gd --prefix=/usr --with-jpeg --with-freetype \
    && docker-php-ext-install -j$(nproc) gd

# memcache/redis
RUN set -ex \
  && pecl install -o -f redis \
  && docker-php-ext-enable redis \
  && git clone -b v3.2.0 https://github.com/php-memcached-dev/php-memcached /usr/src/php/ext/memcached && cd /usr/src/php/ext/memcached \
  && docker-php-ext-configure memcached   && docker-php-ext-install memcached 

RUN pecl install apcu \
    && docker-php-ext-enable apcu
