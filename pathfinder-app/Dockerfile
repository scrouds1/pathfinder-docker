FROM 7.2-fpm-alpine
RUN apt-get update &&  apt-get install -y libjpeg62-turbo-dev libpng-dev libzmq5 libzmq3-dev git unzip zlib1g-dev libevent-dev libssl-dev \
&& docker-php-ext-install sockets \
&& pecl channel-update pecl.php.net \
&& pecl install event-2.4.2 \
&& docker-php-ext-enable event \
&& printf "\n" | pecl install -f zmq-beta \
&& docker-php-ext-enable zmq \
&& pecl install -f redis \
&& docker-php-ext-enable redis \
&& docker-php-ext-configure gd \
&& docker-php-ext-install -j$(nproc) gd pdo_mysql
WORKDIR ~
run curl -sS https://getcomposer.org/installer -o composer-setup.php && php composer-setup.php --install-dir=/usr/local/bin --filename=composer
WORKDIR /var/www/html
RUN git clone https://github.com/exodus4d/pathfinder.git
WORKDIR /var/www/html/pathfinder
RUN composer install
WORKDIR /var/www/html
RUN chmod 777 -R /var/www/html

