FROM nginx:1.27.4

COPY ./default.conf.template /etc/nginx/templates/

RUN mkdir -p /var/www/app/public && touch /var/www/app/public/index.php
