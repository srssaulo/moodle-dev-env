FROM ubuntu:16.04

# Repository/Image Maintainer
MAINTAINER Saulo Rufino de Sá<srssaulo@gmail.com>


# Install apache, PHP, and supplimentary programs. curl and lynx-cur are for debugging the container.
RUN apt-get update -y && apt-get install -y software-properties-common language-pack-en-base

RUN LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php

RUN apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get -y install apache2 libapache2-mod-php5.6 php5.6-mysql php5.6-pgsql php5.6-gd php-pear php-apcu php5.6-curl php5.6-ldap curl lynx-cur php5.6-zip php5.6-opcache php5.6-intl php5.6-xmlrpc

# Enable apache mods.
RUN a2enmod rewrite

# Update the PHP.ini file, enable <? ?> tags and quieten logging.
#RUN sed -i "s/short_open_tag = Off/short_open_tag = On/" /etc/php5.6/apache2/php.ini
#RUN sed -i "s/error_reporting = .*$/error_reporting = E_ERROR | E_WARNING | E_PARSE/" /etc/php5.6/apache2/php.ini

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

EXPOSE 80

# Copy site into place.
#ADD app /var/www/site/app

# Update the default apache site with the config we created.
#ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf

RUN echo ">-----Iniciando a configuração do MoodleData ------<" && \
    mkdir /var/moodledatas &&\
    chown www-data /var/moodledatas && \
    chmod 770 /var/moodledatas

RUN echo "Install vim" && \
    apt-get install -y vim

RUN echo "Set php5.6 alternatives" && \
    update-alternatives --set php /usr/bin/php5.6   && \
    update-alternatives --set phar /usr/bin/phar5.6  && \
    update-alternatives --set phar.phar /usr/bin/phar.phar5.6  && \
    service apache2 restart



WORKDIR /var/www/html

# By default, simply start apache.
CMD /usr/sbin/apache2ctl -D FOREGROUND