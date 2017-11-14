=====================================================================
	INSTALLATION DES IMAGES ET LANCEMENT DES CONTAINERS	     
=====================================================================

// récupère l'image officiel php
docker pull php:7.0-apache

// récupère l'image officiel mysql
docker pull mysql

// crée le container some-mysql avec le mdp "admin"
docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=admin -d mysql

// crée le container my-apache-php-app et le lie au container some-mysql, ouvre le port 80:80 et cré un dossier de partage
docker run --name my-apache-php-app --link some-mysql:mysql -d -p 80:80 -v c:/www/php:/var/www/html php:7.0-apache

=====================================================================
	ACCÈS ET INSTALLATION DU DRIVER PDO	     
=====================================================================

// connexion en ligne de commande au serveur mysql
docker exec -ti some-mysql bash

// connexion au bash mysql
mysql -u root -p

// récupere l'IP du container mysql pour s'y connecter avec PDO
docker inspect some-mysql | grep IPAddress

// installe PDO sur le container php:7.0-apache
docker-php-ext-install pdo pdo_mysql