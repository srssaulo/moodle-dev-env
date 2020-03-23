FROM ubuntu:16.04

# Repository/Image Maintainer
MAINTAINER Saulo Rufino de Sá<srssaulo@gmail.com>

ENV TZ 'America/Recife'
RUN echo $TZ > /etc/timezone && \
    apt-get update && apt-get install -y tzdata && \
    rm /etc/localtime && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata && \
    apt-get clean

# Install PHP From DotDeb, Common Extensions, Composer and then cleanup
RUN apt-get update && apt-get -y install  software-properties-common language-pack-en-base python-software-properties
RUN apt-get update

#
RUN LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php && \
    apt-get update

# Install apache, PHP, and supplimentary programs. curl and lynx-cur are for debugging the container.
RUN echo "INSTALAÇÃO PHP"
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install apache2 php7.2 php7.2-cli php7.2-common libapache2-mod-php7.2 php7.2-pgsql php7.2-gd php-pear php-apcu php7.2-mbstring php7.2-curl php7.2-ldap curl lynx-cur php7.2-zip php7.2-opcache php7.2-intl php7.2-xml php7.2-xmlrpc

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


RUN  echo "Create devuser >>>>>>" &&\
     adduser -u 1000 devuser && \
     chown -R devuser:devuser /var/www && \
     chown -R devuser:devuser /home/devuser




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

WORKDIR /var/www/html

# By default, simply start apache.
EXPOSE 80
#CMD /usr/sbin/apache2ctl -D FOREGROUND
CMD apachectl -D FOREGROUND

#USER devuser
