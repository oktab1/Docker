FROM ubuntu:16.04
MAINTAINER Tolu Okuboyejo
RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get install software-properties-common -y
RUN apt-get install python-software-properties -y

RUN apt-get update

RUN LC_ALL=C.UTF-8 apt-add-repository ppa:ondrej/php -y

RUN apt-get update -y
RUN apt-get install php7.2 php7.2-common php7.2-mbstring php7.2-xmlrpc $RUN rm -rf /var/lib/apt/lists/*

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

# Configure apache
RUN a2enmod rewrite
RUN chown -R www-data:www-data /var/www

VOLUME [ "/var/www/html" ]
WORKDIR /var/www/html

ENV APACHE_RUN_USER  www-data
ENV APACHE_RUN_GROUP www-dataENV APACHE_LOG_DIR   /var/log/apache2
ENV APACHE_PID_FILE  /var/run/apache2/apache2.pid
ENV APACHE_RUN_DIR   /var/run/apache2
ENV APACHE_LOCK_DIR  /var/lock/apache2
ENV APACHE_LOG_DIR   /var/log/apache2

RUN mkdir -p $APACHE_RUN_DIR
RUN mkdir -p $APACHE_LOCK_DIR
RUN mkdir -p $APACHE_LOG_DIR

RUN echo "<?php phpinfo(); ?>" > /var/www/html/info.php

EXPOSE 80
# ENTRYPOINT [ "/usr/sbin/apachectl", "-D", "FOREGROUND" ]
# CMD ["-D", "FOREGROUND"]
CMD ["apache2ctl", "-D", "FOREGROUND"]