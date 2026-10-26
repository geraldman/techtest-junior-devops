FROM wordpress:php8.2-fpm-alpine

COPY --chown=10001:10001 html/wp-content/ /usr/src/wordpress/wp-content

RUN chown 10001:10001 /var/www/html

USER 10001:10001
EXPOSE 9000
