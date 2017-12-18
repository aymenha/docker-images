FROM alpine:3.7
MAINTAINER Amine

# Add repos
# RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
# RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories

# Add basics first
RUN apk update && apk upgrade && apk add \
    php7=7.1.12-r0 \
    bash apache2 php7-apache2 curl ca-certificates git php7-phar tzdata openntpd nano \
    php7-json \
    php7-iconv \
    php7-openssl \
    php7-curl \
    php7-mysqli \
    php7-pdo_mysql \
    php7-gd \
    php7-ftp \
    php7-intl \
    php7-calendar \
    php7-memcached \
    php7-xml \
    php7-opcache \
    php7-mcrypt \
    php7-gmp \
    php7-dom \
    php7-pdo \
    php7-zip \
    php7-bcmath \
    php7-gettext \
    php7-xmlreader \
    php7-bz2 \
    php7-ctype \
    php7-pgsql \
    php7-pdo_pgsql \
    php7-redis \
    php7-fileinfo \
    php7-mbstring \
    php7-xmlwriter \
    php7-tokenizer \
    php7-session \
    && rm -f /var/cache/apk/*

# Add Composer
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer && composer global require hirak/prestissimo && composer clearcache