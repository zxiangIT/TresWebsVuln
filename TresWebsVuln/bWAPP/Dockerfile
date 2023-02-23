#Web with php version 7.4
FROM php:7.4-apache
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo pdo_mysql
RUN apt-get update && apt-get -y install libpng-dev
RUN docker-php-ext-install gd
COPY ./bWAPP/ /var/www/html/bWAPP/
RUN chmod 777 /var/www/html/bWAPP/passwords/
RUN chmod 777 /var/www/html/bWAPP/images/
RUN chmod 777 /var/www/html/bWAPP/documents/
#RUN chmod 777 /var/www/html/bWAPP/logs/
EXPOSE 80


