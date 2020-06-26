FROM composer:1 AS composer
FROM php:7.2-fpm

ARG FPM_MAX_CHILDREN=100

COPY --from=composer /usr/bin/composer /usr/bin/
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/

RUN chmod ug+x /usr/bin/composer; \
    chmod ug+x /usr/bin/install-php-extensions; \
    sync

RUN install-php-extensions amqp \
    apcu \
    apcu_bc \
    bcmath \
    bz2

RUN install-php-extensions calendar \
    cmark\
    dba\
    decimal\
    enchant

RUN install-php-extensions exif\
    gd\
    gettext\
    gmp\
    grpc

RUN install-php-extensions http\
    igbinary\
    imagick\
    imap\
    interbase

RUN install-php-extensions intl\
    ldap\
    mailparse\
    mcrypt\
    memcache

RUN install-php-extensions memcached\
    mongodb \
    msgpack\
    mysqli\
    oauth

RUN install-php-extensions odbc \
    opcache \
    opencensus \
    pcntl \
    pcov

RUN install-php-extensions pdo_dblib \
    pdo_firebird \
    pdo_mysql \
    pdo_odbc \
    pdo_pgsql

RUN install-php-extensions pdo_sqlsrv \
    pgsql \
    propro \
    protobuf \
    pspell

RUN install-php-extensions raphf \
    rdkafka \
    recode \
    redis \
    shmop

RUN install-php-extensions snmp \
    snuffleupagus \
    soap \
    sockets \
    solr

RUN install-php-extensions sqlsrv \
    ssh2 \
    sysvmsg \
    sysvsem \
    sysvshm

RUN install-php-extensions tdlib \
    tidy \
    timezonedb \
    uopz \
    uuid

RUN install-php-extensions wddx \
    xdebug \
    xhprof \
    xmlrpc \
    xsl

RUN install-php-extensions yaml \
    zip

RUN apt-get update; \
    apt-get install wget git tar -y --no-install-recommends; \
    rm -rf /var/lib/apt/lists/*; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false;

RUN sed 's@pm.max_children = [0-9]*@pm.max_children = ${FPM_MAX_CHILDREN}@g' /usr/local/etc/php-fpm.d/www.conf -i;

CMD [ "php-fpm" ]