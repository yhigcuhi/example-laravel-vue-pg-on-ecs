# php
FROM php:8.1.15-fpm

# 独自の php.ini
COPY ./docker/app/php.ini /usr/local/etc/php/php.ini
# Composer install:PHP ライブラリ管理とかのやつ
COPY --from=composer /usr/bin/composer /usr/bin/composer

# install Node.js: Vue開発用
COPY --from=node:18.14 /usr/local/bin /usr/local/bin
COPY --from=node:18.14 /usr/local/lib /usr/local/lib

# UbuntuのOSとして必要なやつインストール
RUN apt-get update && \
    apt-get -y install \
    git \
    zip \
    unzip \
    vim \
    libpq-dev \
    libmemcached-dev \
    zlib1g-dev \
    && docker-php-ext-install pgsql pdo_pgsql bcmath

# docker compose exec xxx bash とかの 最初のカレントディレクトリの設定
WORKDIR /var/www/html