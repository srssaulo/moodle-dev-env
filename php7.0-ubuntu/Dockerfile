FROM ubuntu:16.04

# Repository/Image Maintainer
MAINTAINER Saulo Rufino de Sá<srssaulo@gmail.com>

# Install PHP From DotDeb, Common Extensions, Composer and then cleanup
RUN apt-get update
RUN apt-get -y upgrade

# Install apache, PHP, and supplimentary programs. curl and lynx-cur are for debugging the container.
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install apache2 libapache2-mod-php7.0 php7.0-mysql php7.0-pgsql php7.0-gd php-pear php-apcu php7.0-curl php7.0-ldap curl lynx-cur php7.0-zip php7.0-opcache php7.0-intl php7.0-xmlrpc

# Enable apache mods.
#RUN php7.0enmod openssl
#RUN a2enmod php7.0
RUN a2enmod rewrite

# Update the PHP.ini file, enable <? ?> tags and quieten logging.
#RUN sed -i "s/short_open_tag = Off/short_open_tag = On/" /etc/php7.0/apache2/php.ini
#RUN sed -i "s/error_reporting = .*$/error_reporting = E_ERROR | E_WARNING | E_PARSE/" /etc/php7.0/apache2/php.ini

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

WORKDIR /var/www/html

# By default, simply start apache.
CMD /usr/sbin/apache2ctl -D FOREGROUND