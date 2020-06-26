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
    uuid \
    xdebug
# These extensions are the low priorities of the extensions' installation
# These extensions are the rest extensions that need to be installed
# If there is a new extension, try to add here
# If it's fail, then move it to the part of the must be installed first extensions
RUN install-php-extensions amqp \
    apcu \
    apcu_bc \
    bcmath \
    bz2 \
    calendar \
    cmark \
    dba \
    decimal \
    enchant \
    exif \
    gd \
    gettext \
    gmp \
    http \
    igbinary \
    imagick \
    imap \
    interbase \
    intl \
    ldap \
    mailparse \
    mcrypt \
    memcache \
    memcached \
    mongodb \
    msgpack \
    mysqli \
    oauth \
    odbc \
    opcache \
    opencensus \
    pcntl \
    pcov \
    pdo_dblib \
    pdo_firebird \
    pdo_mysql \
    pdo_odbc \
    pdo_pgsql \
    pdo_sqlsrv \
    pgsql \
    propro \
    protobuf \
    pspell \
    raphf \
    rdkafka \
    recode \
    redis \
    shmop \
    snmp \
    snuffleupagus \
    soap \
    sockets \
    sysvmsg \
    sysvsem \
    sysvshm \
    tidy \
    wddx \
    xhprof \
    xmlrpc \
    xsl \
    yaml \
    zip

RUN apt-get update; \
    apt-get install wget git tar -y --no-install-recommends; \
    rm -rf /var/lib/apt/lists/*; \
    apt-get purge -y --auto-remove apt-utils; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false

RUN sed 's@pm.max_children = [0-9]*@pm.max_children = ${FPM_MAX_CHILDREN}@g' /usr/local/etc/php-fpm.d/www.conf -i

CMD [ "php-fpm" ]