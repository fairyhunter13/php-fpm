FROM composer:1 AS composer
FROM php:7.2-fpm

ARG FPM_MAX_CHILDREN=100

COPY --from=composer /usr/bin/composer /usr/bin/composer

ADD https://raw.githubusercontent.com/mlocati/docker-php-extension-installer/master/install-php-extensions /usr/local/bin/

RUN export $PATH=$PATH:/usr/local/bin; \
    export $PATH=$PATH:/usr/bin; \
    chmod ug+x /usr/bin/composer ; \
    chmod ug+x /usr/local/bin/install-php-extensions ; \
    sync ; \
    install-php-extensions \
    amqp \
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
    gmagick \
    gmp \
    grpc \
    http \
    igbinary \
    imagick \
    imap \
    interbase \
    intl \
    ldap \
    mailparsed \
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
    solr \
    sqlsrv \
    ssh2 \
    sysvmsg \
    sysvsem \
    sysvshm \
    tidy \
    timezonedb \
    uopz \
    uuid \
    wddx \
    xdebug \
    xhprof \
    xmlrpc \
    xsl \
    yaml \
    zip

RUN apt-get update; \
    apt-get install wget git tar -y --no-install-recommends; \
    rm -rf /var/lib/apt/lists/*; \
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false;

RUN sed 's@pm.max_children = [0-9]*@pm.max_children = ${FPM_MAX_CHILDREN}@g' /usr/local/etc/php-fpm.d/www.conf -i;

CMD [ "php-fpm" ]