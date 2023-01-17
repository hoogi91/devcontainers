FROM mcr.microsoft.com/vscode/devcontainers/php:8.1-bullseye

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    libfreetype6-dev \
    libtool \
    libjpeg-dev \
    libpng-dev \
    libxml2-dev \
    libicu-dev \
    libyaml-dev \
    libzip-dev \
    imagemagick \
    ghostscript && \
    rm -rf /var/lib/apt/lists/* && \
    pecl install apcu && \
    docker-php-ext-configure gd --enable-gd --with-freetype=/usr --with-jpeg=/usr && \
    docker-php-ext-configure intl --enable-intl && \
    docker-php-ext-install gd intl zip && \
    docker-php-ext-enable apcu && \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false

RUN a2enmod rewrite expires headers && \
    echo "max_execution_time = 240\nmemory_limit = 512M\npost_max_size = 32M\nupload_max_filesize = 32M\nmax_input_vars = 2000\nxdebug.max_nesting_level=400" > /usr/local/etc/php/conf.d/typo3.ini
