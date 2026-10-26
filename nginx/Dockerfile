FROM nginxinc/nginx-unprivileged:stable
COPY --chown=10001:10001 nginx.conf /etc/nginx/conf.d/default.conf
USER 10001:10001
EXPOSE 8080