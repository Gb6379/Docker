FROM php:7.2-fpm-alpine

RUN apk add postgresql-dev
RUN docker-php-ext-install bcmath mbstring pdo pdo_pgsql
RUN curl -sL https://getcomposer.org/installer | php -- --install-dir /usr/bin --filename composer
RUN sed -i 's/www-data/nobody/' /usr/local/etc/php-fpm.d/www.conf
RUN apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ --allow-untrusted gnu-libiconv
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php
EXPOSE 9000
