FROM nginx:alpine

WORKDIR /var/www/html
COPY --chown=nobody ./src /var/www/html
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./nginx/sites/ /etc/nginx/sites-available
COPY ./nginx/conf.d/ /etc/nginx/conf.d
CMD ["nginx"]
EXPOSE 80 443
