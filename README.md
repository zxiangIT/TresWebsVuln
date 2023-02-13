# Tree_Vul_Webs
# 1. DVWA

Descomprimir el archivo bWAPP que hemos descargado en la página web.
https://github.com/digininja/DVWA
Guarda en el directorio /examen/DVWA.

FROM mysql:5.7
LABEL mantainer=zxiang@iessacolomina.es
ENV MYSQL_ROOT_PASSWORD=root

/Examen/DVWA/mysql/Dockerfile
Crear un Dockerfile en el directorio examen/bWAPP/mysql.
Las funciones de este Dockerfile son:
Crear un mysql de la versión 5.7 para evitar el conflicto de autentificación.
Generar una contraseña del usuario root.

$_DVWA = array();
$_DVWA[ 'db_server' ]   = 'dvwams';
$_DVWA[ 'db_database' ] = 'dvwa';
$_DVWA[ 'db_user' ]     = 'root';
$_DVWA[ 'db_password' ] = 'root';
$_DVWA[ 'db_port'] = '3306';

Modificar el /examen/DVWA/DVWA/config/config.inc.php.disk. 
db_server es el nombre de contenedor de mysql que hemos especificado en el archivo docker-compose.yml.
db_username es el nombre de usuario que quieres conectar. Tiene que ser el usuario root, sino no permite entrar en la base de datos.
db_paasword es la contraseña de usuario que quieres conectar.
db_name es el nombre de la base de datos que quieres conectar.  Poner dvwa.

version: '3.2'

services:

  dvwaweb:
	build:
  	context: './'
	networks:
   	- nbtnetx
	ports:
   	- 8080:80
	container_name: dvwaweb

  dvwams:
	build:
  	context: './mysql/'
	networks:
   	- nbtnetx
	container_name: dvwams
networks:
  nbtnetx:


/examen/DVWA/docker-compose.yml
Las funciones del docker compose son:
Construir una imagen dvwapweb con el nombre de contenedor dvwaweb, el puerto es 8080:80 u utiliza la red nbtnetx.
Construir una imagen dvwams con el nombre de contenedor dvwams u utiliza la red nbtnetx.

En el navegador poner la IP y el puerto. Para crear una base de datos, hay que ir al Setup/Reset DB.


# 2. bWAPP


Descomprimir el archivo bWAPP que hemos descargado en la página web https://sourceforge.net/projects/bwapp/files/bWAPP/
Guarda en el directorio /examen/dWAPP.

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
RUN chmod 777 /var/www/html/bWAPP/logs/
EXPOSE 80

examen/bWAPP
Crear un Dockerfile en el directorio examen/bWAPP. 
Las funciones de este Dockerfile son : 
Crear un apache de php7.4, además instala mysqli, pdo, libpng-dev, gd y actualizar los paquetes.  
Copiar el directorio bWAPP en el directorio de contenido, el que muestra la imagen en la página web.
Modificar los permisos de las carpetas de contenido para necesitar ejecutar el programa.
Exporté el puerto 80.

FROM mysql:5.7
LABEL mantainer=zxiang@iessacolomina.es
ENV MYSQL_ROOT_PASSWORD=root

examen/bWAPP/mysql
Crear un Dockerfile en el directorio examen/bWAPP/mysql.
Las funciones de este Dockerfile son:
Crear un mysql de la versión 5.7 para evitar el conflicto de autentificación.
Generar una contraseña del usuario root.
// Database connection settings
$db_server = "bwappms";
$db_username = "root";
$db_password = "root";
$db_name = "bWAPP";

Modificar el /examen/bWAPP/bWAPP/admin/settings.php. 
db_server es el nombre de contenedor de mysql que hemos especificado en el archivo docker-compose.yml.
db_username es el nombre de usuario que quieres conectar. Tiene que ser el usuario root, sino no permite entrar en la base de datos.
db_paasword es la contraseña de usuario que quieres conectar.
db_name es el nombre de la base de datos que quieres conectar. Tiene que ser bWAPP, no hay que modificar nada.

version: '3.2'

services:

  bwappweb:
	build:
  	context: './'
	networks:
   	- nbtnetx
	ports:
   	- 8081:80
	container_name: bwappweb

  bwappms:
	build:
  	context: './mysql/'
	networks:
   	- nbtnetx
	container_name: bwappms
networks:
  nbtnetx:


/examen/bWAPP/docker-compose.yml
Las funciones del docker compose son:
Construir una imagen bwappweb con el nombre de contenedor bwappweb, el puerto es 8080:80 u utiliza la red nbtnetx.
Construir una imagen bwappwms con el nombre de contenedor bwappms u utiliza la red nbtnetx.


Hay que instalar una base de datos automática.

Entrar el usuario bee y la contraseña bug. 

# 3. OWASP Multillidae II
Descomprimir el archivo OWASP que hemos descargado en la página web.
https://github.com/webpwnized/mutillidae
Guarda en el directorio /examen/OWASP.

#Web with php version 7.4
FROM php:7.4-apache
RUN docker-php-ext-install mysqli
RUN docker-php-ext-install pdo pdo_mysql
RUN apt-get update && apt-get -y install libpng-dev
RUN docker-php-ext-install gd
COPY ./mutillidae/ /var/www/html/mutillidae/

EXPOSE 80


/Examen/OWASP /Dockerfile
/Examen/OWASP /multillidae está toda la aplicación OWASP 
Las funciones de este Dockerfile son : 
Crear un apache de php7.4, además instala mysqli, pdo, libpng-dev, gd y actualizar los paquetes.  
Copiar el directorio OWASP en el directorio de contenido, el que muestra la imagen en la página web.
Modificar las carpetas de contenido para necesitar ejecutar el programa.
Exporté el puerto 80.


FROM mysql:5.7
LABEL mantainer=zxiang@iessacolomina.es
ENV MYSQL_ROOT_PASSWORD=root

/Examen/OWASP /mysql/Dockerfile
Crear un Dockerfile en el directorio examen/OWASP /mysql.
Las funciones de este Dockerfile son:
Crear un mysql de la versión 5.7 para evitar el conflicto de autentificación.
Generar una contraseña del usuario root.

define('DB_HOST', 'owaspms');
define('DB_USERNAME', 'root');
define('DB_PASSWORD', 'root');
define('DB_NAME', 'mutillidae');
define('DB_PORT', 3306);


Modificar el /examen/OWASP/mutilidae/incluedes/database-config.inc
db_server es el nombre de contenedor de mysql que hemos especificado en el archivo docker-compose.yml.
db_username es el nombre de usuario que quieres conectar. Tiene que ser el usuario root, sino no permite entrar en la base de datos.
db_paasword es la contraseña de usuario que quieres conectar.
db_name es el nombre de la base de datos que quieres conectar.  Poner mutillidae.

version: '3.2'

services:

  owaspweb:
	build:
  	context: './'
	networks:
   	- nbtnetx
	ports:
   	- 8082:80
	container_name: owaspweb

  owaspms:
	build:
  	context: './mysql/'
	networks:
   	- nbtnetx
	container_name: owaspms
networks:
  nbtnetx:




/examen/OWASP/docker-compose.yml
Las funciones del docker compose son:
Construir una imagen owaspweb con el nombre de contenedor owaspweb, el puerto es 8080:80 u utiliza la red nbtnetx.
Construir una imagen owspms con el nombre de contenedor owaspms u utiliza la red nbtnetx.

En el navegador poner la IP y el puerto. Para crear una base de datos, hay que ir al reset DB.


# 4. Reverse Proxy
sudo apt-get install apache2.
Instalar la aplicación apache.

sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod proxy_balancer
sudo a2enmod lbmethod_byrequests

Activar los modules.


Añadir proxypass y proxypassreverse en el archivo 000-default.conf o puede crear una configuración propia. 
Para activar la configuración con a2ensite ejemplo.conf. 
Para ver la configuración, ir al directorio sites-enable.

Recargar apache o reiniciar apache con el comando,
sudo service apache2 restart.

En la página web poner la IP y el nombre de la aplicación.
