FROM composer:1 AS composer
FROM php:7.2-fpm

ARG FPM_MAX_CHILDREN=100

COPY --from=composer /usr/bin/composer /usr/bin/
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/

RUN chmod ug+x /usr/bin/composer &&\
    chmod ug+x /usr/bin/install-php-extensions &&\
    apt-get update &&\
    apt-get install -y --no-install-recommends apt-utils

RUN install-php-extensions amqp\
    apcu\
    apcu_bc\
    bcmath\
    bz2\
    calendar\
    cmark\
    dba\
    decimal\
    enchant\
    exif\
    gd\
    gettext\
    gmp\
    grpc\
    igbinary\
    imagick\
    imap\
    interbase\
    intl\
    ldap\
    mailparse\
    mcrypt\
    msgpack\
    memcache\
    memcached\
    mongodb\
    mysqli\
    oauth\
    odbc\
    opcache\
    opencensus\
    pcntl\
    pcov\
    pdo_dblib\
    pdo_firebird\
    pdo_mysql\
    pdo_odbc\
    pdo_pgsql\
    pdo_sqlsrv\
    pgsql\
    propro\
    protobuf\
    pspell\
    raphf\
    http\
    rdkafka\
    recode\
    redis\
    shmop\
    snmp\
    soap\
    sockets\
    solr \
    sqlsrv\
    ssh2\
    sysvmsg\
    sysvsem\
    sysvshm\
    tdlib\
    tidy\
    timezonedb\
    uopz\
    uuid\
    wddx\
    xhprof\
    xmlrpc\
    xsl\
    yaml\
    zip

RUN apt-get update &&\
    apt-get install wget git tar -y --no-install-recommends &&\
    rm -rf /var/lib/apt/lists/* &&\
    apt-get purge -y --auto-remove apt-utils &&\
    apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false &&\
    sed 's@pm.max_children = [0-9]*@pm.max_children = '${FPM_MAX_CHILDREN}'@g' /usr/local/etc/php-fpm.d/www.conf -i

CMD [ "php-fpm" ]