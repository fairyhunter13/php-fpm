FROM composer:1 AS composer
FROM php:7.2-fpm

ARG FPM_MAX_CHILDREN=100

COPY --from=composer /usr/bin/composer /usr/bin/

COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/

RUN chmod ug+x /usr/bin/composer ; \
    chmod ug+x /usr/bin/install-php-extensions ; \
    sync

RUN install-php-extensions amqp
RUN  install-php-extensions apcu
RUN install-php-extensions apcu_bc
RUN install-php-extensions bcmath
RUN install-php-extensions bz2
RUN install-php-extensions calendar
RUN install-php-extensions cmark
RUN install-php-extensions dba
RUN install-php-extensions decimal
RUN install-php-extensions enchant
RUN install-php-extensions exif
RUN install-php-extensions gd
RUN install-php-extensions gettext
RUN install-php-extensions gmp
RUN install-php-extensions grpc
RUN install-php-extensions http
RUN install-php-extensions igbinary
RUN install-php-extensions imagick
RUN install-php-extensions imap
RUN install-php-extensions interbase
RUN install-php-extensions intl
RUN install-php-extensions ldap
RUN install-php-extensions mailparse
RUN install-php-extensions mcrypt
RUN install-php-extensions memcache
RUN install-php-extensions memcached
RUN install-php-extensions mongodb
RUN install-php-extensions msgpack
RUN install-php-extensions mysqli
RUN install-php-extensions oauth
RUN install-php-extensions odbc
RUN install-php-extensions opcache
RUN install-php-extensions opencensus
RUN install-php-extensions pcntl
RUN install-php-extensions pcov
RUN install-php-extensions pdo_dblib
RUN install-php-extensions pdo_firebird
RUN install-php-extensions pdo_mysql
RUN install-php-extensions pdo_odbc
RUN install-php-extensions pdo_pgsql
RUN install-php-extensions pdo_sqlsrv
RUN install-php-extensions pgsql
RUN install-php-extensions propro
RUN install-php-extensions protobuf
RUN install-php-extensions pspell
RUN install-php-extensions raphf
RUN install-php-extensions rdkafka
RUN install-php-extensions recode
RUN install-php-extensions redis
RUN install-php-extensions shmop
RUN install-php-extensions snmp
RUN install-php-extensions snuffleupagus
RUN install-php-extensions soap
RUN install-php-extensions sockets
RUN install-php-extensions ssh2
RUN install-php-extensions sysvmsg
RUN install-php-extensions sysvsem
RUN install-php-extensions sysvshm
RUN install-php-extensions tdlib
RUN install-php-extensions tidy
RUN install-php-extensions timezonedb
RUN install-php-extensions uopz
RUN install-php-extensions uuid
RUN install-php-extensions wddx
RUN install-php-extensions xdebug
RUN install-php-extensions xhprof
RUN install-php-extensions xmlrpc
RUN install-php-extensions xsl
RUN install-php-extensions yaml
RUN install-php-extensions zip

RUN apt-get update; \
    apt-get install wget git tar -y --no-install-recommends; \
    rm -rf /var/lib/apt/lists/*; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false;

RUN sed 's@pm.max_children = [0-9]*@pm.max_children = ${FPM_MAX_CHILDREN}@g' /usr/local/etc/php-fpm.d/www.conf -i;

CMD [ "php-fpm" ]