FROM php:7.3-fpm-alpine

RUN apk add postgresql-dev

WORKDIR /var/www/html

COPY --chown=nobody:nobody ./src /var/www/html
RUN chown nobody:nobody /var/www/html

RUN docker-php-ext-install bcmath mbstring pdo pdo_pgsql
RUN curl -sL https://getcomposer.org/installer | php -- --install-dir /usr/bin --filename composer
RUN sed -i 's/www-data/nobody/' /usr/local/etc/php-fpm.d/www.conf
RUN apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted gnu-libiconv
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php
RUN cp .env.example .env
RUN php artisan key:generate

RUN sed -i 's/DB_CONNECTION=mysql/DB_CONNECTION=pgsql/' .env
RUN sed -i 's/DB_DATABASE=laravel/DB_DATABASE=postgres/' .env
RUN sed -i 's/DB_PORT=3306/DB_PORT=5433/' .env
RUN sed -i 's/DB_USERNAME=root/DB_USERNAME=postgres/' .env
RUN sed -i 's/DB_PASSWORD=/DB_PASSWORD=secret/' .env

## DEV Only
RUN adduser -D php
RUN composer install --no-dev --no-cache --prefer-dist --no-interaction
RUN sed -i 's/nobody/php/' /usr/local/etc/php-fpm.d/www.conf
VOLUME /var/www/html

RUN artisan migrate

EXPOSE 9000
