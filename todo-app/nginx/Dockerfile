FROM nginx:latest

COPY ./default.conf.template /etc/nginx/templates/

RUN mkdir -p /var/www/app/public && touch /var/www/app/public/index.php
