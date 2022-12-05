FROM php:8.1-fpm

LABEL Maintainer="Oluwafemi Sosami"

ENV PHPGROUP=analyst
ENV PHPUSER=analyst


#RUN add -g ${PHPGROUP} -s /bin/sh -D ${PHPUSER}
#
#RUN sed -i "s/user = www-data/user = ${PHPUSER}/g" usr/local/etc/php-fpm.d/www.conf
#RUN sed -i "s/group = www-data/group = ${PHPGROUP}/g" usr/local/etc/php-fpm.d/www.conf

#RUN mkdir -p /var/www/symfony/public

RUN apt update \
    && apt install -y --no-install-recommends \
    zlib1g-dev \
    g++ \
    git \
    libicu-dev \
    zip \
    libzip-dev \
    zip \
    && docker-php-ext-install intl opcache pdo pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

COPY /symfony /symfony

RUN chown ${PHPGROUP}:${PHPUSER} /symfony

#WORKDIR /var/www/symfony

RUN composer install

#CMD ["php-fpm", "-y", "usr/local/etc/php-fpm.conf", "-R"]