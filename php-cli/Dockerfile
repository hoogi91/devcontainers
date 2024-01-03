ARG PHP_VERSION=8.3-cli-bullseye
FROM php:${PHP_VERSION}
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN apt -y update && apt -y --no-install-recommends install cron git jq zip wait-for-it ssh \
    && rm -rf /var/lib/apt/lists/* \
    && git config --global --add safe.directory /var/www/app \
    && install-php-extensions apcu bcmath bz2 calendar decimal exif gd gettext gmp imagick imap intl opcache pcntl pdo_mysql redis soap sockets xdebug-stable xsl zip @composer \
    && echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_host = host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "apc.enabled=1" >> /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini \
    && echo "apc.enable_cli=1" >> /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini \
    && echo "apc.use_request_time=0" >> /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini
WORKDIR /var/www/app