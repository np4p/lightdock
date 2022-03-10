ARG CLI_VERSION
FROM php:${CLI_VERSION}-cli

ARG TZ=PRC
ENV TZ ${TZ}

# If you're in China, or you need to change sources, will be set CHANGE_SOURCE to true in .env.
ARG CHANGE_SOURCE=false
RUN if [ ${CHANGE_SOURCE} = true ]; then \
    # Change application source from deb.debian.org to aliyun source
    sed -i 's/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/mirrors.tuna.tsinghua.edu.cn/' /etc/apt/sources.list && \
    sed -i 's/security-cdn.debian.org/mirrors.tuna.tsinghua.edu.cn/' /etc/apt/sources.list \
;fi

RUN set -eux \
    # Install "PHP Extentions", "libraries", "Software's"
    && apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y --allow-downgrades --allow-remove-essential \
        --allow-change-held-packages \
        pkg-config \
        libcurl4-openssl-dev \
        libedit-dev \
        libssl-dev \
        libxml2-dev \
        xz-utils \
        libsqlite3-dev \
        rsync \
        sqlite3 \
        git \
        curl \
        wget \
        vim \
        nano \
        tree \
    && apt-get clean

# install redis
RUN pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis

# overwrite php.ini
COPY ./php.ini /usr/local/etc/php/conf.d/php.ini

# install composer
RUN wget https://mirrors.aliyun.com/composer/composer.phar -O /usr/bin/composer
RUN chmod +x /usr/bin/composer
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

#Give permission
RUN chown -R www-data:www-data /var/www/

# Clean up
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    rm /var/log/lastlog /var/log/faillog

###########################################################################
# Crontab
###########################################################################
COPY ./crontab /etc/cron.d
RUN chmod -R 644 /etc/cron.d

# Set default work directory
WORKDIR /var/www/