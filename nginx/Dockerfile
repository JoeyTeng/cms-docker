FROM nginx:latest
RUN apt-get update \
&&  apt-get install -y \
        php5-cgi \
        php5-fpm \
        phppgadmin
ADD ["./nginx.conf", "/etc/nginx/conf.d/nginx.conf"]
VOLUME ['/etc/nginx', '/var/log/nginx', '/var/lib/nginx']
