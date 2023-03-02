ARG PHP_VERSION=${PHP_VERSION:-8.2}
FROM php:${PHP_VERSION}-fpm-alpine

RUN apk -U upgrade
RUN apk add --no-cache rsync gcc linux-headers freetype-dev libjpeg-turbo-dev libpng-dev libzip-dev $PHPIZE_DEPS openssl-dev

RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install opcache gd pdo_mysql zip
RUN docker-php-ext-enable opcache gd zip
RUN wget https://getcomposer.org/download/latest-stable/composer.phar
RUN chmod a+x composer.phar
RUN mv composer.phar /usr/local/bin/composer


ARG ENV=${ENV:-production}

RUN if [ "$ENV" = "dev" ] ; then pecl install xdebug-3.2.0 && docker-php-ext-enable xdebug && cp $PHP_INI_DIR/php.ini-development $PHP_INI_DIR/php.ini; fi

RUN if [ "$ENV" = "production" ] ; then cp $PHP_INI_DIR/php.ini-production $PHP_INI_DIR/php.ini; fi


CMD ["php-fpm"]