FROM ubuntu:18.04

RUN export LANG=en_US.UTF-8

RUN apt update
RUN apt install -y software-properties-common
RUN apt install -y apt-utils
RUN DEBIAN_FRONTEND=noninteractive \
    apt update && \
    apt install -y language-pack-en-base &&\
    export LC_ALL=en_US.UTF-8 && \
    export LANG=en_US.UTF-8


RUN DEBIAN_FRONTEND=noninteractive apt update && apt install -y software-properties-common
RUN DEBIAN_FRONTEND=noninteractive LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php

RUN apt clean

RUN apt update && DEBIAN_FRONTEND=noninteractive apt upgrade -y

RUN DEBIAN_FRONTEND=noninteractive apt install -y --force-yes \
        php7.2-cli \
        php7.2-fpm \
        php7.2-common \
        php7.2-curl \
        php7.2-json \
        php7.2-xml \
        php7.2-mbstring \
        php7.2-mysql \
        php7.2-pgsql \
        php7.2-sqlite3 \
        php7.2-zip \
        php7.2-bcmath \
        php7.2-gd \
        php7.2-dev \
        php7.2-gmp \
        openssl \
        libcurl4-openssl-dev \
        libedit-dev \
        libssl-dev \
        libxml2-dev \
        xz-utils \
        libsqlite3-dev \
        sqlite3 \
        git \
        curl \
        wget \
        postgresql-client \
        libxml2-dev \
        php7.2-soap \
        php7.2-ldap \
        php7.2-imap \
        php7.2-xmlrpc \
        php7.2-mailparse \
        php7.2-xdebug \
        php-memcached \
        libxrender1 \
    && apt clean

# Install latest nginx version from community maintained ppa
RUN add-apt-repository ppa:nginx/stable

# Update packages after adding ppa
RUN apt-get update

# Install nginx
RUN apt-get install -y nginx

RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
RUN tar xf wkhtmltox-*
RUN mv wkhtmltox/bin/wkhtmltopdf /usr/local/bin/
RUN mv wkhtmltox/bin/wkhtmltoimage /usr/local/bin/
RUN chmod +x /usr/local/bin/wkhtmltopdf
RUN chmod +x /usr/local/bin/wkhtmltoimage
RUN rm -rf wkhtmltox

RUN curl -s http://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt install nodejs -y

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt update && \
    apt install yarn

RUN apt install -y supervisor
RUN apt remove ca-certificates -y
RUN apt install openssl ca-certificates -y

RUN addgroup -gid 1000 docker && adduser docker -gid 1000 --uid 1000 --disabled-password --gecos ""

RUN apt install nodejs -y --force-yes
RUN npm install cross-env -g

RUN apt install libpng-dev -y --no-install-recommends

RUN apt install nano -y

RUN mkdir -p /var/www/html
RUN chown -Rf docker:docker /var/www/html
RUN gpasswd -a www-data docker
RUN phpenmod memcached

RUN echo 'export PS1="\[\\033[38m\]\u\[\\033[32m\] \w\[\\033[31m\]\`git branch 2>/dev/null | grep \"^\*\" | sed -r \"s/\*\ (.*)/ \(\\1\)/\"\`\[\\033[37m\]$\[\\033[00m\] "' >> /home/docker/.bashrc

RUN echo 'alias phpunit=vendor/bin/phpunit' >> /home/docker/.bashrc

RUN echo 'su docker'

WORKDIR /var/www/html