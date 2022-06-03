FROM php:7.4-apache

RUN apt-get update \
    && docker-php-ext-install mysqli \
    && docker-php-ext-enable mysqli

WORKDIR /app
ENV APACHE_CONFDIR /etc/apache2
ENV APACHE_ENVVARS $APACHE_CONFDIR/envvars