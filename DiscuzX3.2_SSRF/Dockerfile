FROM ubuntu:14.04

# Install Apache2 & PHP & Redis & mysql
# Test: docker run  --rm -p 80:80 -it ubuntu:14.04 /bin/bash
RUN sudo apt-get update \
	&& apt-get install -y apache2 redis-server php5-dev wget unzip libapache2-mod-php5 php5-curl php5-mysql \
	&& wget http://download.comsenz.com/DiscuzX/3.2/Discuz_X3.2_SC_GBK.zip \
	&& unzip Discuz_X3.2_SC_GBK.zip -d /var/www/html/ \
	&& chmod -R 777 /var/www/html/upload \
	&& rm -rf /var/lib/apt/lists/*
	
COPY config_global_default.php /var/www/html/upload/config/config_global_default.php

RUN wget https://github.com/nicolasff/phpredis/zipball/master -O /tmp/php-redis.zip \
	&& cd /tmp \
	&& unzip php-redis.zip \
	&& cd phpredis-phpredis-4c8cf98 \
	&& phpize \
	&& ./configure \
	&& make \
	&& make install \
	&& echo "extension=redis.so" >> /etc/php5/apache2/php.ini

CMD service apache2 start && service redis-server start && tail -f /var/log/apache2/access.log

