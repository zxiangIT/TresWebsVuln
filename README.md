# Tree_Vul_Webs
# Aviso: En la carpeta DVWA no tiene la carpeta de la aplicación DVWA, hay que instalar en https://github.com/digininja/DVWA. Modificar el DVWA/DVWA/config/config.inc.php.disk.

# 1. DVWA

Descomprimir el archivo bWAPP que hemos descargado en la página web.
https://github.com/digininja/DVWA
Guarda en el directorio /DVWA.

	FROM mysql:5.7
	LABEL mantainer=zxiang@iessacolomina.es
	ENV MYSQL_ROOT_PASSWORD=root

/DVWA/mysql/Dockerfile
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

Modificar el /DVWA/DVWA/config/config.inc.php.disk. 
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


/DVWA/docker-compose.yml
Las funciones del docker compose son:
	Construir una imagen dvwapweb con el nombre de contenedor dvwaweb, el puerto es 8080:80 u utiliza la red nbtnetx.
	Construir una imagen dvwams con el nombre de contenedor dvwams u utiliza la red nbtnetx.

En el navegador poner la IP y el puerto. Para crear una base de datos, hay que ir al Setup/Reset DB.


# 2. bWAPP


Descomprimir el archivo bWAPP que hemos descargado en la página web https://sourceforge.net/projects/bwapp/files/bWAPP/
Guarda en el directorio /dWAPP.

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

Modificar el /bWAPP/bWAPP/admin/settings.php. 
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


/bWAPP/docker-compose.yml
Las funciones del docker compose son:
	Construir una imagen bwappweb con el nombre de contenedor bwappweb, el puerto es 8080:80 u utiliza la red nbtnetx.
	Construir una imagen bwappwms con el nombre de contenedor bwappms u utiliza la red nbtnetx.

En la página pone install.php para generar una base de datos automática.

Entrar el usuario bee y la contraseña bug. 

# 3. OWASP Multillidae II
Descomprimir el archivo OWASP que hemos descargado en la página web.
https://github.com/webpwnized/mutillidae
Guarda en el directorio /OWASP.

	#Web with php version 7.4
	FROM php:7.4-apache
	RUN docker-php-ext-install mysqli
	RUN docker-php-ext-install pdo pdo_mysql
	RUN apt-get update && apt-get -y install libpng-dev
	RUN docker-php-ext-install gd
	COPY ./mutillidae/ /var/www/html/mutillidae/
	EXPOSE 80

/OWASP /Dockerfile
/OWASP /multillidae está toda la aplicación OWASP 
Las funciones de este Dockerfile son : 
	Crear un apache de php7.4, además instala mysqli, pdo, libpng-dev, gd y actualizar los paquetes.  
	Copiar el directorio OWASP en el directorio de contenido, el que muestra la imagen en la página web.
	Modificar las carpetas de contenido para necesitar ejecutar el programa.
	Exporté el puerto 80.

	FROM mysql:5.7
	LABEL mantainer=zxiang@iessacolomina.es
	ENV MYSQL_ROOT_PASSWORD=root

/OWASP /mysql/Dockerfile
Crear un Dockerfile en el directorio examen/OWASP /mysql.
Las funciones de este Dockerfile son:
Crear un mysql de la versión 5.7 para evitar el conflicto de autentificación.
Generar una contraseña del usuario root.

	define('DB_HOST', 'owaspms');
	define('DB_USERNAME', 'root');
	define('DB_PASSWORD', 'root');
	define('DB_NAME', 'mutillidae');
	define('DB_PORT', 3306);


Modificar el /OWASP/mutilidae/incluedes/database-config.inc
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

/OWASP/docker-compose.yml
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
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html
        ProxyPass /dvwa  http://192.168.3.251:8080/DVWA/
        ProxyPassReverse /dvwa  http://192.168.3.251:8080/DVWA/
        ProxyPass /bwapp  http://192.168.3.251:8081/bWAPP
        ProxyPassReverse /bwapp  http://192.168.3.251:8081/bWAPP
        ProxyPass /mutillidae  http://192.168.3.251:8082/mutillidae
        ProxyPassReverse /mutillidae  http://192.168.3.251:8082/mutillidae


        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>

Añadir proxypass y proxypassreverse en el archivo 000-default.conf o puede crear una configuración propia. 
Para activar la configuración con a2ensite ejemplo.conf. 
Para ver la configuración, ir al directorio sites-enable.

Recargar apache
sudo service apache2 reload

Reiniciar apache con el comando
sudo service apache2 restart.

En la página web poner la IP y el nombre de la aplicación.
