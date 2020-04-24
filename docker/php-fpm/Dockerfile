FROM php:fpm-alpine

ENV TERM=ansi
ENV LC_ALL=C.UTF-8
WORKDIR /home/www/memorix

# Update all packages & install bash/curl
RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories
RUN apk update
RUN apk upgrade
RUN apk add bash curl git

# Install php-ext
COPY vendor/bin/composer-ext-install /usr/bin/composer-ext-install
COPY composer.lock /etc/php/composer.lock
RUN composer-ext-install --lockfile /etc/php/composer.lock

# Install composer
RUN curl https://getcomposer.org/installer | php -- --install-dir=/usr/bin
RUN ln -s /usr/bin/composer.phar /usr/bin/composer

# Debug logs
RUN php --version
RUN php -m

# How to start
EXPOSE 9000
CMD /usr/local/sbin/php-fpm --fpm-config /etc/php/php-fpm.conf
