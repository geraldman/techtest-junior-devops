FROM mysql:8.4

RUN mkdir -p /var/lib/mysql /var/run/mysqld \
    && chown -R 10001:10001 /var/lib/mysql /var/run/mysqld

COPY --chown=10001:10001 init.sql /docker-entrypoint-initdb.d/init.sql

USER 10001:10001
EXPOSE 3306