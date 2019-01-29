FROM andthensome/docker-php-5.3-fpm 
MAINTAINER Andrey Barashkov <sokolby@gmail.com> 
RUN apt-get update
RUN apt-get install -y \
    libfreetype6-dev \
    php5-gd \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libxslt-dev \
    libicu-dev \
    unzip \
#    geoip-bin \
#    geoip-database \
#    libgeoip-dev \
    nano \
    mysql-client \
    cron

RUN apt-get update \
  && apt-get install -y libmemcached11 libmemcachedutil2 build-essential libmemcached-dev libz-dev \
  && pecl install memcache \
  && echo extension=memcache.so >> /usr/local/etc/php/conf.d/memcached.ini \
  && apt-get remove -y build-essential libmemcached-dev libz-dev \
  && apt-get autoremove -y \
  && apt-get clean \
  && rm -rf /tmp/pear

RUN rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install iconv mcrypt \
    && mkdir /usr/include/freetype2/freetype \ 
    && ln -s /usr/include/freetype2/freetype.h /usr/include/freetype2/freetype/freetype.h \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ 

RUN docker-php-ext-install \
    dba \
    gd \
    mcrypt \
    iconv \
    mbstring \
    pdo_mysql \
    mysqli \
    soap \
    intl \
    zip \
    xsl \
    xmlrpc
RUN usermod -u 1000 www-data
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer
RUN cron
ENV TERM xterm
