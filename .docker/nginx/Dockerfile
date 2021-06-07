FROM nginx:1.19-alpine

ADD ./nginx.conf /etc/nginx/

ADD ./default.conf /etc/nginx/conf.d/

RUN mkdir -p /var/www/html

RUN addgroup -g 1000 laravel && adduser -G laravel -g laravel -s /bin/sh -D laravel

RUN chown laravel:laravel /var/www/html

# Install packages
RUN apk --update --no-cache add openssl