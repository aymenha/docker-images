FROM alpine:edge
MAINTAINER Amine

# Add repos
RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories

# Add basics first
RUN apk update && apk upgrade && apk add \
    php7=7.1.11-r0 \
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
RUN curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer && composer clearcache

# # Setup apache and php
# RUN apk add \
#   php7-ftp \
#   php7-fileinfo \
#   php7-mbstring \
#   php7-xmlwriter \
#   php7-xml \
#   php7-tokenizer \
#   php7-mcrypt \
#   php7-gmp \
#   php7-dom \
#   php7-pdo \
#   php7-zip \
#   php7-bcmath \
#   php7-gd \
#   php7-pdo_mysql \
#   php7-gettext \
#   php7-xmlreader \
#   php7-bz2 \
#   php7-curl \
#   php7-ctype \
#   php7-session \
#   # php7-mysqli \
#   # php7-sqlite3 \
#   # php7-pdo_pgsql \
#   # php7-pdo_sqlite \
#   # php7-xmlrpc \
#   # php7-redis \
#   && cp /usr/bin/php7 /usr/bin/php \
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


ADD index.html /app/public/
ADD start.sh /bootstrap/
RUN chmod +x /bootstrap/start.sh

EXPOSE 80
ENTRYPOINT ["/bootstrap/start.sh"]