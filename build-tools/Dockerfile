FROM php:5-cli

ADD php/_010_php.ini /usr/local/etc/php/conf.d/
COPY ./wait-mysql.sh /wait-mysql.sh
COPY ./wait-smtp.sh /wait-smtp.sh

RUN apt-get update && apt-get install --no-install-recommends -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        zip \
        zlib1g-dev \
        unzip \
        mysql-client \
        ssmtp \
        wget \
        tar \
        libcurl4-gnutls-dev \
        curl \
        libxml2 \
        libxml2-dev \
        openssl \
        libssl-dev \
        netcat \
        parallel \
    && docker-php-ext-install -j$(nproc) iconv mcrypt mysqli \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install mbstring \
    && docker-php-ext-install zip \
    && docker-php-ext-install ftp \
    && docker-php-ext-install soap \
    && docker-php-ext-install curl \
    && docker-php-ext-install pdo pdo_mysql \
    && echo "date.timezone = 'Europe/Berlin'" >> /usr/local/etc/php/php.ini \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && mv composer.phar /usr/local/bin/composer \
    && wget http://shopwarelabs.github.io/sw-cli-tools/sw.phar \
    && mv sw.phar /usr/local/bin/sw \
    && chmod +x /usr/local/bin/sw \
    && chmod +x /config_testing.php \
    && chmod +x /wait-mysql.sh \
    && chmod +x /wait-smtp.sh \
    && mkdir /php-config

WORKDIR /tests

CMD ["php" "-a"]