FROM ubuntu:latest

# * Varaibles for tzdata pacakge (depandance of php-fpm)
ENV DEBIAN_FRONTEND noninteractive
ENV TZ America/Los_Angeles

# * Update package cache and install necessary pacakges
RUN apt-get update \
        && apt-get install -y \
                build-essential \
                libpcre3 \
                libpcre3-dev \
                libssl-dev \
                php-fpm \
                wget \
                zlib1g \
                zlib1g-dev

# * Install nginx
ENV NGINX_VERSION 1.13.10
RUN wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz
RUN tar -zxvf nginx-${NGINX_VERSION}.tar.gz
WORKDIR /nginx-${NGINX_VERSION}
RUN ./configure \
        --conf-path=/etc/nginx/nginx.conf \
        --error-log-path=/var/nginx/error.log \
        --http-log-path=/var/log/nginx/access.log \
        --pid-path=/var/run/nginx.pid \
        --sbin-path=/usr/bin/nginx \
        --with-http_ssl_module \
        --with-pcre
RUN make && make install

EXPOSE 80

# * Copy files relative to the root
WORKDIR /
COPY . .

CMD ["nginx", "-g", "daemon off;"]