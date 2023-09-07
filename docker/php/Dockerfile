ARG PHP_BUILD_DEPS="bash coreutils ca-certificates libtool openssl curl-dev freetype-dev icu-dev libjpeg-turbo-dev libpng-dev libwebp-dev libzip-dev libsodium-dev zlib-dev libxml2-dev libssh-dev oniguruma-dev"
ARG PHP_RUNTIME_DEPS="libpng libjpeg-turbo freetype icu libzip"
ARG PHP_EXTS="exif gd curl intl zip pdo pdo_mysql bcmath mbstring"

ARG PHP_VERSION

FROM php:${PHP_VERSION}

LABEL maintainer="Wordpress <wordpress@gmail.com>"

ARG PHP_EXTS
ARG PHP_BUILD_DEPS
ARG PHP_RUNTIME_DEPS

RUN apk add --virtual build-dependencies --no-cache ${PHPIZE_DEPS} ${PHP_BUILD_DEPS} \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-configure zip \
    && docker-php-ext-install -j$(nproc) ${PHP_EXTS} \
    && apk del build-dependencies

# Install runtime dependencies
RUN apk add --no-cache ${PHP_RUNTIME_DEPS}

RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

RUN rm -rf /tmp/*

USER www-data

WORKDIR /var/www
