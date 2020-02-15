
LINUX :
----------------------------------------------------------------------------------------------------
   ###### [README](/README.md) 
#### SSH SERVER :

    sudo apt-get install openssh-server
    sudo /etc/init.d/ssh start, stop, status, reload

    /etc/ssh/ssh_config # fichier de config

    ssh login@ip # ouvrir une connection

#### CONFIG RESEAU :

    hostname
    hostname -I
    ifconfig

#### Liste des Ports ouverts :

    netstat -tlnpu # t=tcp, u=udp, p=programs/PID, l=listening, n=numeric  
    ps auxw | grep runserver # liste des serveurs
    kill -9 process

#### ENVIRONNEMENT VIRTUEL :

    sudo pip3 install virtualenv
    virtualenv --version
    virtualenv --python=python3 envname
    source . envname/bin/activate

#### PAQUETS :

dpkg (pour Debian package) est l'outil de bas niveau gérant les paquets
des distributions basées sur Debian

    sudo apt update # mise à jour de l’index de paquet du serveur

    sudo apt autoremove paquet # desinstallation

    dpkg -l # liste des paquets avec description
    dpkg --get-selections # liste des paquets sans description

    /var/lib/dpkg/status # fichier liste paquets

liste des paquets installés

    dpkg --get-selections | grep -v deinstall
    dpkg --get-selections > liste-des-paquets_`hostname`_`date +%H:%M-%d-%m-%Y`

réinstallation

    sudo apt-get update
    sudo apt-get dist-upgrade
    dpkg –set-selections < ubuntu-files

    synaptic # gestionnaire de paquets avec interface graphique

Utilisateurs :

 sudo : super-user do  
 groups ou id # verification de groupes d un utilisateur

    adduser mynewuser # nouvel utilisateur
    usermod -aG sudo mynewuser #ajout au groupe sudo
    adduser mynewuser sudo

    su - mynewuser # connexion

#### LAMP ( Linux Apache MySql Php )

apache2 : # Serveur Web

    sudo apt-get install apache2 apache2-doc
    sudo service apache2 status
    sudo service apache2 start ( stop)
    sudo service apache2 restart

php:

    sudo apt-get install php-common libapache2-mod-php php-cli
    
Pour tester l’installation, dans le répertoire /var/www/html, créez le fichier info.php, 
avec le contenu suivant:  \<?php phpinfo();  ?>  
Redemarrer apache et verifier  <http://IP_du_serveur/info.php> 

mysql :

    sudo apt-get install mysql-server
    sudo /etc/init.d/mysql start

personnaliser la sécurisation

    sudo mysql_secure_installation utility

changement de mot de passe root

    sudo mysql -u root -p
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'le_mot_de_pass_choisi';

#### PHPMYADMIN :

    sudo apt-get install phpmyadmin

Afin d’accéder à l’interface de gestion de phpMyAdmin, vous devrez finaliser la configuration
de votre serveur Apache.  

Pour cela, éditez le fichier /etc/apache2/apache2.conf
Ajouter à la fin :

\# Include phpMyAdmin  
Include /etc/phpmyadmin/apache.conf  

    sudo service apache2 restart

Erreur count dans phpmyadmin

    sudo vim /usr/share/phpmyadmin/libraries/sql.lib.php
    
*erreur de parentheses (count($analyzed_sql_results['select_expr']) == 1)*

    sudo service apache2 restart
    












