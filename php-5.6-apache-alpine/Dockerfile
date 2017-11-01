FROM php:5.6.32-alpine
MAINTAINER Amine

# Add repos
# RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
# RUN echo "ipv6" >> /etc/modules

# Add basics first
RUN apk update && apk upgrade && apk add \
    bash apache2 php5-apache2 curl ca-certificates git php5 php5-phar tzdata openntpd nano \
    php5-json \
    php5-iconv \
    php5-openssl \
    php5-curl \
    php5-mysql \
    php5-mysqli \
    php5-pdo_mysql \
    php5-gd \
    php5-ftp \
    php5-intl \
    php5-calendar \
    php5-memcache \
    php5-xml \
    php5-opcache \
    php5-mcrypt \
    php5-gmp \
    php5-dom \
    php5-pdo \
    php5-zip \
    php5-bcmath \
    php5-gettext \
    php5-xmlreader \
    php5-bz2 \
    php5-ctype \
    php5-pgsql \
    php5-pdo_pgsql \

    # php5-fileinfo \
    # php5-mbstring \
    # php5-xmlwriter \
    # php5-tokenizer \
    # php5-session \

    && rm -f /var/cache/apk/*

# Add Composer
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer && composer clearcache

# Setup apache and php
# RUN apk add \
#   php5-ftp \
#   php5-fileinfo \
#   php5-mbstring \
#   php5-xmlwriter \
#   php5-xml \
#   php5-tokenizer \
#   php5-mcrypt \
#   php5-gmp \
#   php5-dom \
#   php5-pdo \
#   php5-zip \
#   php5-bcmath \
#   php5-gd \
#   php5-pdo_mysql \
#   php5-mysql \
#   php5-gettext \
#   php5-xmlreader \
#   php5-bz2 \
#   php5-curl \
#   php5-ctype \
#   php5-session \
#   # php5-mysqli \
#   # php5-sqlite3 \
#   # php5-pdo_pgsql \
#   # php5-pdo_sqlite \
#   # php5-xmlrpc \
#   # php5-redis \
#   && cp /usr/bin/php5 /usr/bin/php \
#     && rm -f /var/cache/apk/*

# Add apache to run and configure
RUN mkdir /run/apache2 \
    && sed -i "s/#LoadModule\ rewrite_module/LoadModule\ rewrite_module/" /etc/apache2/httpd.conf \
    && sed -i "s/#LoadModule\ session_module/LoadModule\ session_module/" /etc/apache2/httpd.conf \
    && sed -i "s/#LoadModule\ session_cookie_module/LoadModule\ session_cookie_module/" /etc/apache2/httpd.conf \
    && sed -i "s/#LoadModule\ session_crypto_module/LoadModule\ session_crypto_module/" /etc/apache2/httpd.conf \
    && sed -i "s/#LoadModule\ deflate_module/LoadModule\ deflate_module/" /etc/apache2/httpd.conf \
    && sed -i "s#^DocumentRoot \".*#DocumentRoot \"/app/public\"#g" /etc/apache2/httpd.conf \
    && sed -i "s#/var/www/localhost/htdocs#/app/public#" /etc/apache2/httpd.conf \
    && printf "\n<Directory \"/app/public\">\n\tAllowOverride All\n</Directory>\n" >> /etc/apache2/httpd.conf

RUN mkdir -p /bootstrap /app /app/public \
    && chown -R apache:apache /app && chmod -R 755 /app

# RUN mkdir -p /app/public

ADD index.html /app/public/
ADD start.sh /bootstrap/
RUN chmod +x /bootstrap/start.sh

EXPOSE 80
ENTRYPOINT ["/bootstrap/start.sh"]