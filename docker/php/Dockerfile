FROM php:7.4-fpm

ARG WEB_USER
ARG WEB_GROUP
ARG PHP_ROOT_DIR
#
#RUN apt-get update && apt-get -y install wget bsdtar libaio1 && \
# wget -qO- https://raw.githubusercontent.com/caffeinalab/php-fpm-oci8/master/oracle/instantclient-basic-linux.x64-12.2.0.1.0.zip | bsdtar -xvf- -C /usr/local && \
# wget -qO- https://raw.githubusercontent.com/caffeinalab/php-fpm-oci8/master/oracle/instantclient-sdk-linux.x64-12.2.0.1.0.zip | bsdtar -xvf-  -C /usr/local && \
# wget -qO- https://raw.githubusercontent.com/caffeinalab/php-fpm-oci8/master/oracle/instantclient-sqlplus-linux.x64-12.2.0.1.0.zip | bsdtar -xvf- -C /usr/local && \
# ln -s /usr/local/instantclient_12_2 /usr/local/instantclient && \
# ln -s /usr/local/instantclient/libclntsh.so.* /usr/local/instantclient/libclntsh.so && \
# ln -s /usr/local/instantclient/lib* /usr/lib && \
# ln -s /usr/local/instantclient/sqlplus /usr/bin/sqlplus && \
# docker-php-ext-configure oci8 --with-oci8=instantclient,/usr/local/instantclient && \
# docker-php-ext-install oci8 && \
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

COPY ./docker/php/www.conf ${PHP_ROOT_DIR}/php-fpm.d/www.conf

RUN docker-php-ext-install mysqli

RUN usermod -u 1000 ${WEB_USER} \
 && groupmod -g 1000 ${WEB_GROUP} \
 && chgrp -R staff ${PHP_ROOT_DIR}/php-fpm.d/www.conf

COPY ./html /var/www/html
#COPY --from=composer:1.10.19 /usr/bin/composer /usr/bin/composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer
RUN echo "129"
RUN echo "$PWD"
WORKDIR /var/www/html/wdelo30/wcl_euroizol/composer
RUN echo "$PWD"
RUN ls -la $PWD
RUN php -d memory_limit=-1 /usr/local/bin/composer install -d /var/www/html/wdelo30/wcl_euroizol/composer