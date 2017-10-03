FROM php:7-fpm
RUN apt-get update \
    && apt-get install apt-utils git nginx -y \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && curl -sL https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update && apt-get install yarn \
    && apt-get install --reinstall zlibc zlib1g zlib1g-dev \
    && docker-php-ext-install mbstring zip pdo pdo_mysql \
    && apt-get clean \
    && rm *.* \
    && adduser --gecos '' --disabled-password koel \
    && chown -R koel /var/www/html \
    && cd /var/www/html/ \
    && git clone https://github.com/phanan/koel.git . \
    && git checkout v3.6.2 \
    && composer install \
    && npm install yarn@0.25.4 -g \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY files/.env files/run.sh ./

RUN chmod 700 run.sh

VOLUME ["/music"]

WORKDIR /var/www/html/

EXPOSE 8000

CMD ./run.sh
