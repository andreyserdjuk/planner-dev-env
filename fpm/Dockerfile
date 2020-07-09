FROM php:7.4.1-fpm-alpine

ENV TZ UTC

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && apk add --update \
        libzip-dev \
        curl-dev \
        bash \
        wget \
        icu-dev \
    && echo $TZ > /etc/timezone \
    && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
    && docker-php-ext-install -j${NPROC} \
        pdo_mysql \
        bcmath \
        opcache \
        intl \
        zip \
    && docker-php-ext-configure opcache

RUN apk add --no-cache $PHPIZE_DEPS \
    && pecl install xdebug \
    && docker-php-ext-enable \
        opcache \
        xdebug

RUN addgroup -g 1000 docker && adduser -D -G docker -u 1000 docker && addgroup docker root

CMD ["php-fpm"]
EXPOSE 9000
