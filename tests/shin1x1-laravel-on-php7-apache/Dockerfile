FROM shin1x1/laravel-on-php7-apache:latest
LABEL authors="Mouhamed Aymen Hammami <MouhamedAymenHammami@gmail.com>"

COPY . /var/www/html

RUN cd /var/www/html && composer install && rm -f public/storage && php artisan storage:link

WORKDIR /var/www/html