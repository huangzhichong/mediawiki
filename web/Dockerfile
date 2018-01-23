FROM daocloud.io/huangzhichong/mediawiki:latest

MAINTAINER pastakhov@yandex.ru

ENV MW_VERSION=REL1_29 \
    MW_HOME=/var/www/html/w \
    MW_VOLUME=/mediawiki \
    WWW_USER=www-data \
    WWW_GROUP=www-data \
    APACHE_LOG_DIR=/var/log/apache2

#### Run maintenance sripts
# Increase value for run maintenance script before web service started
ENV MW_AUTOUPDATE=true \
    MW_MAINTENANCE_UPDATE=3 \
    MW_MAINTENANCE_CIRRUSSEARCH_UPDATECONFIG=1 \
    MW_MAINTENANCE_CIRRUSSEARCH_FORCEINDEX=1 \
    MW_MAINTENANCE_ULS_INDEXER=1 \
    MW_SCRIPT_CLDR_REBUILD=1 \
    MW_SITE_NAME=My\ MediaWiki\ Site \
    MW_SITE_LANG=en \
    MW_DEFAULT_SKIN=vector \
    MW_MAIN_CACHE_TYPE=CACHE_ACCEL \
    MW_REST_DOMAIN=localhost \
    MW_REST_RESTBASE_PROXY_PATH=/api/rest_ \
    MW_REST_RESTBASE_PORT=7231 \
    MW_SHOW_EXCEPTION_DETAILS=true \
    PHP_LOG_ERRORS=On \
    PHP_ERROR_REPORTING=E_ALL

EXPOSE 80

COPY php.ini /etc/php/7.0/apache2/conf.d/mediawiki.ini

COPY mediawiki.conf /etc/apache2/sites-available/000-mediawiki.conf
RUN set -x; ln -s /etc/apache2/sites-available/000-mediawiki.conf /etc/apache2/sites-enabled/000-mediawiki.conf

COPY run-apache.sh /run-apache.sh
RUN chmod -v +x /run-apache.sh

COPY DockerSettings.php $MW_HOME/DockerSettings.php

COPY favicon.ico $MW_HOME/favicon.ico
COPY logo.png $MW_HOME/logo.png
COPY CustomSettings.php $MW_HOME/CustomSettings.php

CMD ["/run-apache.sh"]

VOLUME ["$MW_HOME/images", "$MW_VOLUME"]
