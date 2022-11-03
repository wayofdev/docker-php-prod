# Auto-generated via Ansible: edit src/Dockerfiles/prod/Dockerfile.j2 instead.

FROM wayofdev/php-base:8.0-fpm-alpine-latest

# Labels
# https://github.com/opencontainers/image-spec/blob/main/annotations.md
LABEL "maintainer"="lotyp <lotyp7@gmail.com>"
LABEL "vendor"="wayofdev"
LABEL "org.opencontainers.image.authors"="lotyp <lotyp7@gmail.com>"
LABEL "org.opencontainers.image.url"="https://hub.docker.com/r/wayofdev/php-prod"
LABEL "org.opencontainers.image.documentation"="https://github.com/wayofdev/docker-php-prod"
LABEL "org.opencontainers.image.source"="https://github.com/wayofdev/docker-php-prod"
LABEL "org.opencontainers.image.vendor"="wayofdev"
LABEL "org.opencontainers.image.licenses"="MIT"
LABEL "org.opencontainers.image.ref.name"="8.0-prod"
LABEL "org.opencontainers.image.title"="PHP-FPM 8.0-prod"
LABEL "org.opencontainers.image.description"="PHP-FPM 8.0-prod"

RUN set -eux; \
    rm -rf /var/cache/apk/* \
    && rm -rf /tmp/* \
    && apk -U upgrade -a \
    # Add production dependencies
    # Temporary build dependencies for compiling Pecl extensions
    && apk add --no-cache --virtual .temp-build-deps \
        $PHPIZE_DEPS \
    # Soap Messaging Protocol
    && apk add --no-cache libxml2-dev \
    && docker-php-ext-install -j$(nproc) soap \
    && apk del libxml2-dev \
    ### Image Processing
    # https://www.php.net/manual/en/refs.utilspec.image.php
    # Exif - (Exchangeable image information) / Image Meta Data
    && docker-php-ext-install -j$(nproc) exif \
    # GD
    && apk add --no-cache \
        freetype libjpeg-turbo libpng libxpm libwebp \
        freetype-dev libjpeg-turbo-dev libpng-dev libxpm-dev libwebp-dev \
    && docker-php-ext-configure gd --enable-gd --with-webp --with-jpeg --with-xpm --with-freetype \
    && docker-php-ext-install -j$(nproc) gd \
    && apk del freetype-dev libjpeg-turbo-dev libpng-dev libxpm-dev libwebp-dev \
    ####################################################################################################################
    # Pecl Dependencies
    # Imagick
    && apk add --no-cache \
        imagemagick libgomp \
        imagemagick-dev \
    && pecl install imagick-3.7.0 \
    && docker-php-ext-enable imagick \
    && apk del imagemagick-dev \
    # Client for Apache Kafka
    && apk add --no-cache \
        librdkafka \
        librdkafka-dev \
    && pecl install rdkafka-6.0.3 \
    && docker-php-ext-enable rdkafka \
    && apk del librdkafka-dev \
    # AMQP - Communicate with any amqp compliant server
    && apk add --no-cache \
        rabbitmq-c \
        rabbitmq-c-dev \
    && pecl install amqp-1.11.0 \
    && docker-php-ext-enable amqp \
    && apk del rabbitmq-c-dev \
    # Protobuf - Google's extensible mechanism for serializing structured data.
    # https://spiral.dev/docs/grpc-configuration#toolkit-installation-install-protobuf-extension-optional
    && pecl install protobuf-3.21.9 \
    && docker-php-ext-enable --ini-name docker-php-ext-10-protobuf.ini protobuf \
    # Yaml parser and emitter
    && apk add --no-cache \
        yaml \
        yaml-dev \
    && pecl install yaml-2.2.2 \
    && docker-php-ext-enable yaml \
    && apk del yaml-dev \
    && apk del -f .temp-build-deps \
    && rm -rf /var/www/html \
    && mkdir /app \
    && chown www-data:www-data /app

COPY ./configs/php-fpm.d/ /usr/local/etc/php-fpm.d/

WORKDIR /app

USER www-data

