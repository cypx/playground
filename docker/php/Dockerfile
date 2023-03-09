FROM php:8.2

RUN apt-get update \
    && apt-get install -y git zip \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/apt/* 

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --quiet \
    && rm composer-setup.php \
    && mv composer.phar /usr/local/bin/composer \
    && composer --version


RUN adduser --disabled-password --gecos "" phpuser
USER phpuser

RUN composer global require "squizlabs/php_codesniffer=*"
ENV PATH=/home/phpuser/.composer/vendor/bin/:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
