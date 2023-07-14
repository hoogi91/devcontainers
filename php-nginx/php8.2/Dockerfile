FROM php:8.2-fpm-bullseye
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN apt -y update \
    && apt -y --no-install-recommends install nginx \
    && rm -rf /var/lib/apt/lists/* \
    && install-php-extensions apcu bcmath bz2 calendar decimal exif gd gettext gmp imagick imap intl opcache pcntl pdo_mysql redis soap sockets xdebug-stable xsl zip \
    && echo "php_admin_value[disable_functions] = getmyuid,passthru,leak,listen,diskfreespace,tmpfile,link,ignore_user_abord,dl,set_time_limit,system,highlight_file,source,show_source,fpaththru,virtual,posix_ctermid,posix_getcwd,posix_getegid,posix_geteuid,posix_getgid,posix_getgrgid,posix_getgrnam,posix_getgroups,posix_getlogin,posix_getpgid,posix_getpgrp,posix_getpid,posix,_getppid,posix_getpwnam,posix_getpwuid,posix_getrlimit,posix_getsid,posix_getuid,posix_isatty,posix_mkfifo,posix_setegid,posix_seteuid,posix_setgid,posix_setpgid,posix_setsid,posix_setuid,posix_times,posix_ttyname,posix_uname" >> /usr/local/etc/php-fpm.conf \
    && echo "xdebug.mode=debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_host = host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "apc.enabled=1" >> /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini \
    && echo "apc.enable_cli=1" >> /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini \
    && echo "apc.use_request_time=0" >> /usr/local/etc/php/conf.d/docker-php-ext-apcu.ini

COPY site.conf /etc/nginx/sites-enabled/default
COPY entrypoint.sh /opt/entrypoint.sh
EXPOSE 80
CMD ["sh", "/opt/entrypoint.sh"]