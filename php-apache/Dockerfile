FROM php:7.2.1-apache
LABEL Description="Smart Vote Apache"
RUN rm -rf /etc/apache2/sites-available/*
RUN rm -rf /etc/apache2/sites-enabled/*
RUN mkdir -p /var/www/html/public
COPY ./vhost/smartvote.local.conf /etc/apache2/sites-available/
RUN apt-get update -y
RUN apt-get install -y libgmp-dev re2c libmhash-dev libmcrypt-dev file
RUN ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/
RUN docker-php-ext-configure gmp 
RUN docker-php-ext-install gmp
RUN docker-php-ext-install pdo pdo_mysql mysqli
RUN a2enmod rewrite
RUN a2ensite smartvote.local.conf
RUN service apache2 restart
RUN apt-get install -y --no-install-recommends git zip
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version