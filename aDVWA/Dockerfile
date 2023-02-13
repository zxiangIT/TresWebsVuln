#Web with php version 7.4
FROM php:7.4-apache
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo pdo_mysql
RUN apt-get update && apt-get -y install libpng-dev
RUN docker-php-ext-install gd
COPY ./DVWA/ /var/www/html/DVWA/
RUN chmod 777 /var/www/html/DVWA/hackable/uploads/
RUN chmod 777 /var/www/html/DVWA/external/phpids/0.6/lib/IDS/tmp/phpids_log.txt
RUN chmod 777 /var/www/html/DVWA/config
RUN cp /var/www/html/DVWA/config/config.inc.php.dist /var/www/html/DVWA/config/config.inc.php
#COPY dvwa.conf /etc/apache2/sites-available/dvwa.conf
#RUN a2dissite 000-default.conf
#RUN a2ensite dvwa.conf


#RUN chown -R www-data:www-data /var/www/html/
#CMD apachectl -D FOREGROUND

EXPOSE 80


