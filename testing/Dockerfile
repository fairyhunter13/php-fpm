FROM composer:1 AS composer
FROM php:7.2-fpm

ARG FPM_MAX_CHILDREN=100

COPY --from=composer /usr/bin/composer /usr/bin/
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/

RUN chmod ug+x /usr/bin/composer; \
    chmod ug+x /usr/bin/install-php-extensions; \
    apt-get update; \
    apt-get install -y --no-install-recommends apt-utils; \
    sync

# The top priorities of the extensions' installation
# tdlib is a heavy library that should be installed separately
RUN install-php-extensions tdlib
# This part is the must be installed first extensions
# These extensions must be installed before the others extension's installation
RUN install-php-extensions grpc \
    solr \
    sqlsrv \
    ssh2 \
    timezonedb \
    uopz \
    uuid
# These extensions are the low priorities of the extensions' installation
# These extensions are the rest extensions that need to be installed
# If there is a new extension, try to add here
# If it's fail, then move it to the part of the must be installed first extensions
RUN install-php-extensions amqp \
    apcu \
    apcu_bc \
    bcmath \
    bz2
RUN install-php-extensions calendar \
    cmark \
    dba \
    decimal \
    enchant
RUN install-php-extensions exif \
    gd \
    gettext \
    gmp \
    http
RUN install-php-extensions igbinary \
    imagick \
    imap \
    interbase \
    intl
RUN install-php-extensions ldap \
    mailparse \
    mcrypt \
    memcache \
    memcached
RUN install-php-extensions mongodb \
    msgpack \
    mysqli \
    oauth \
    odbc
RUN install-php-extensions opcache \
    opencensus \
    pcntl \
    pcov \
    pdo_dblib
RUN install-php-extensions pdo_firebird \
    pdo_mysql \
    pdo_odbc \
    pdo_pgsql \
    pdo_sqlsrv
RUN install-php-extensions pgsql \
    propro \
    protobuf \
    pspell \
    raphf
RUN install-php-extensions rdkafka \
    recode \
    redis \
    shmop \
    snmp
RUN install-php-extensions snuffleupagus \
    soap \
    sockets \
    sysvmsg \
    sysvsem
RUN install-php-extensions sysvshm \
    tidy \
    wddx \
    xhprof \
    xmlrpc
RUN install-php-extensions xsl \
    yaml \
    zip \
    xdebug

RUN apt-get update; \
    apt-get install wget git tar -y --no-install-recommends; \
    rm -rf /var/lib/apt/lists/*; \
    apt-get purge -y --auto-remove apt-utils; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false

RUN sed 's@pm.max_children = [0-9]*@pm.max_children = ${FPM_MAX_CHILDREN}@g' /usr/local/etc/php-fpm.d/www.conf -i

CMD [ "php-fpm" ]