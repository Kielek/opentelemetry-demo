# Copyright The OpenTelemetry Authors
# SPDX-License-Identifier: Apache-2.0


FROM ghcr.io/mlocati/php-extension-installer:2.11.9@sha256:24b0e392309d7085c05b3dc2429bf1c0d934b7d07ded31d212367405e4554a84 AS installer

FROM docker.io/library/composer:2.10.1@sha256:e8fdff913656c23e90ebbe0d7c55ab078c2aefdbb53ff79a73af5cc0921d5b81 AS vendor

WORKDIR /tmp/

COPY ./src/quote/composer.json composer.json

RUN composer install \
    --ignore-platform-reqs \
    --no-interaction \
    --no-plugins \
    --no-scripts \
    --no-dev \
    --prefer-dist

FROM docker.io/library/php:8.5.7-cli-alpine3.22@sha256:d4db4138a7adb7cb7b0152b5e12b121c473ea37195170a4c498058fd3b16e480

COPY --from=installer /usr/bin/install-php-extensions /usr/local/bin/

RUN install-php-extensions opcache pcntl protobuf opentelemetry

WORKDIR /var/www

USER www-data

COPY --from=vendor /tmp/vendor/ vendor/

COPY ./src/quote/app/ app/
COPY ./src/quote/public/ public/
COPY ./src/quote/src/ src/

EXPOSE ${QUOTE_PORT}

CMD ["php", "public/index.php"]
