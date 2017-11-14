=====================================================================
	INSTALLATION DES IMAGES ET LANCEMENT DES CONTAINERS	     
=====================================================================

// r�cup�re l'image officiel php
docker pull php:7.0-apache

// r�cup�re l'image officiel mysql
docker pull mysql

// cr�e le container-mysql avec le mdp "admin"
docker run --name container-mysql -e MYSQL_ROOT_PASSWORD=admin -d mysql

// cr�e le container-php et le lie � container-mysql, ouvre le port 80:80 et cr�e un dossier de partage
docker run --name container-php --link container-mysql:mysql -d -p 80:80 -v c:/www/php:/var/www/html php:7.0-apache

// cr�e le container container-wordpress et le lie � container-mysql, ouvre le port 8080:80
docker run --name container-wordpress --link container-mysql:mysql -p 8080:80 -d wordpress

=====================================================================
	ACC�S ET INSTALLATION DU DRIVER PDO	     
=====================================================================

// connexion en ligne de commande au serveur mysql
docker exec -ti container-mysql bash

// connexion au bash mysql
mysql -u root -p

// r�cupere l'IP du container mysql pour s'y connecter avec PDO
docker inspect container-mysql | grep IPAddress

// installe PDO sur le container-php
docker-php-ext-install pdo pdo_mysql