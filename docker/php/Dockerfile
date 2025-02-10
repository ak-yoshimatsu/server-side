FROM php:8.2-fpm-buster

ARG USERNAME
ARG GROUPNAME
ARG UID
ARG GID

ENV COMPOSER_ALLOW_SUPERUSER=1 \
    COMPOSER_HOME=/composer

COPY --from=composer:2.2 /usr/bin/composer /usr/bin/composer

RUN apt-get update && \
    apt-get -y install --no-install-recommends \
        git \
        unzip \
        libzip-dev \
        libicu-dev \
        libpq-dev && \
    docker-php-ext-install intl pdo_pgsql pgsql zip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

COPY ./php.ini /usr/local/etc/php/php.ini

RUN groupadd -g $GID $GROUPNAME && \
    useradd -m -s /bin/bash -u $UID -g $GID $USERNAME

USER $USERNAME

WORKDIR /app
