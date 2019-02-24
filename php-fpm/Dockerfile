FROM laradock/php-fpm:2.2-7.2

COPY ./laravel.ini /usr/local/etc/php/conf.d
COPY ./laravel.pool.conf /usr/local/etc/php-fpm.d/

RUN usermod -u 1000 www-data

RUN docker-php-ext-install bcmath

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000
