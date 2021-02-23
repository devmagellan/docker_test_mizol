FROM php:7.3-apache

#RUN apt-get update \
# && apt-get install -y bzip2 git vim wget \
#        libxslt1.1 libxslt1-dev \
#        libicu-dev \
#        libmcrypt-dev \
#        libfreetype6-dev libjpeg62-turbo-dev libzmq3-dev \
#
#         && apt install --no-install-recommends -yqq apt-utils libzip-dev zip unzip coreutils \
#            && docker-php-ext-configure zip \
#            && docker-php-ext-install zip \
#            && php -m | grep -q 'zip' \
# && apt-get clean
##RUN docker-php-ext-install zip
##RUN pecl install zmq-beta \
##  && docker-php-ext-enable zmq
#RUN apt-get update && apt-get -y install bsdtar libaio1 && \
# wget -qO- https://raw.githubusercontent.com/caffeinalab/php-fpm-oci8/master/oracle/instantclient-basic-linux.x64-12.2.0.1.0.zip | bsdtar -xvf- -C /usr/local && \
# wget -qO- https://raw.githubusercontent.com/caffeinalab/php-fpm-oci8/master/oracle/instantclient-sdk-linux.x64-12.2.0.1.0.zip | bsdtar -xvf-  -C /usr/local && \
# wget -qO- https://raw.githubusercontent.com/caffeinalab/php-fpm-oci8/master/oracle/instantclient-sqlplus-linux.x64-12.2.0.1.0.zip | bsdtar -xvf- -C /usr/local && \
# ln -s /usr/local/instantclient_12_2 /usr/local/instantclient && \
# ln -s /usr/local/instantclient/libclntsh.so.* /usr/local/instantclient/libclntsh.so && \
# ln -s /usr/local/instantclient/lib* /usr/lib && \
# ln -s /usr/local/instantclient/sqlplus /usr/bin/sqlplus && \
# docker-php-ext-configure oci8 --with-oci8=instantclient,/usr/local/instantclient && \
# docker-php-ext-install oci8 && \
#
# rm -rf /var/lib/apt/lists/* && \
# php -v
#
#RUN wget http://php.net/distributions/php-7.4.15.tar.gz && \
#    mkdir php_oci && \
#    mv php-7.4.15.tar.gz ./php_oci
#WORKDIR php_oci
#RUN tar xfvz php-7.4.15.tar.gz
#WORKDIR php-7.4.15/ext/pdo_oci
#RUN phpize && \
#    ./configure --with-pdo-oci=instantclient,/usr/local/instantclient,12.1 && \
#    make && \
#    make install && \
#    echo extension=pdo_oci.so > /usr/local/etc/php/conf.d/pdo_oci.ini && \
#    php -v
ARG WEB_USER
ARG WEB_GROUP
ARG APACHE_ROOT_DIR

COPY ./docker/apache/httpd-vhosts.conf ${APACHE_ROOT_DIR}/conf/extra/httpd-vhosts.conf
COPY ./docker/apache/httpd.conf ${APACHE_ROOT_DIR}/conf/httpd.conf

RUN chgrp -R ${WEB_GROUP} ${APACHE_ROOT_DIR}/conf/httpd.conf \
 && chgrp -R ${WEB_GROUP} ${APACHE_ROOT_DIR}/conf/extra/httpd-vhosts.conf

RUN usermod -u 1000 ${WEB_USER} \
 && groupmod -g 1000 ${WEB_GROUP} \
 && chgrp -R ${WEB_GROUP} ${APACHE_ROOT_DIR}
