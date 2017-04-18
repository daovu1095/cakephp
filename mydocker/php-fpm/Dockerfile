FROM laradock/php-fpm:5.6--1.2

ARG INSTALL_MYSQL=false
COPY ./mysql.ini /usr/local/etc/php/conf.d/mysql.ini
RUN if [ ${INSTALL_MYSQL} = true ]; then \
    # Install the php mysql extension
    docker-php-ext-install mysql && \
    docker-php-ext-install mysqli && \
    docker-php-ext-enable mysql && \
    docker-php-ext-enable mysqli \
;fi

ARG INSTALL_MYSQLI=false
RUN if [ ${INSTALL_MYSQLI} = true ]; then \
     docker-php-ext-install mysqli \
;fi


RUN rm -r /var/lib/apt/lists/*

RUN usermod -u 1000 www-data

WORKDIR /var/www

CMD ["php-fpm"]

EXPOSE 9000