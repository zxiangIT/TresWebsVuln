#Web with php version 7.4
FROM php:7.4-apache
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo pdo_mysql
RUN apt-get update && apt-get -y install libpng-dev
RUN docker-php-ext-install gd
#RUN a2enmod proxy_http
#COPY ./proxy/proxy.conf /etc/apache2/sites-available/proxy.conf
#RUN a2dissite 000-default.conf
#RUN a2ensite proxy.conf
#RUN /etc/init.d/apache2 reload
COPY ./mutillidae/ /var/www/html/mutillidae/

EXPOSE 80


