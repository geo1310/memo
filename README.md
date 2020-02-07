

# WINDOWS POWERSHELL :

PowerShell ISE -> éditeur de script intégré ( alternative à PowerGUI )

Windows PowerShell est la nouvelle interface système de Microsoft
le lancer en admin
CMD est l’un des derniers vestiges du système d’exploitation MS-DOS

Get-ExecutionPolicy -> connaitre le mode utilisé
Set-ExecutionPolicy Unrestricted

Restricted : aucun script ne peut être exécuté. PowerShell est utilisable uniquement en mode interactif.

AllSigned : seuls les scripts signés peuvent être exécutés.

RemoteSigned : les scripts téléchargés depuis Internet doivent être signés pour être exécutés.
Les scripts présents sur votre poste de travail ne sont pas concernés et peuvent être exécutés.

Unrestricted : pas de restrictions. Les scripts peuvent être exécutés.

C:\Windows\system32> Send-MailMessage -From "geo1310@hotmail.fr" -To "gbriche59@yahoo.fr" -Subject "votre objet" -SmtpServer "smtp.mail.yahoo.fr" -Body "Le corps du mail" -Attachments "le chemin d’accès à votre fichier"

Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
curl.exe -L -o ubuntu-1604.appx https://aka.ms/wsl-ubuntu-1604
Add-AppxPackage .\app_name.appx



# GIT :

    git config --global user.name "name"
    git config --global user.email "email"

    git clone lienFourniParGitHub

### create a new repository on the command line

    echo "# crepes_bretonnes" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/geo1310/crepes_bretonnes.git
    git push -u origin master



# VIRTUAL BOX :

### Additions invitees

    Open your terminal.
    sudo apt-get install build-essential gcc make perl dkms
    reboot
    Open your terminal
    Go to the installation disk
    sudo sh VBoxLinuxAdditions.run
    reboot


# LINUX :

### SSH SERVER :

    sudo apt-get install openssh-server
    sudo /etc/init.d/ssh start, stop, status, reload

    /etc/ssh/ssh_config # fichier de config

    ssh login@ip # ouvrir une connection

### CONFIG RESEAU :

    hostname
    hostname -I
    ifconfig

### Liste des Ports ouverts :

    netstat -tlnpu # t=tcp, u=udp, p=programs/PID, l=listening, n=numeric  
    ps auxw | grep runserver # liste des serveurs
    kill -9 process

### ENVIRONNEMENT VIRTUEL :

    sudo pip3 install virtualenv
    virtualenv --version
    virtualenv --python=python3 envname
    source . envname/bin/activate

### PAQUETS :

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

### LAMP ( Linux Apache MySql Php )

apache2 : # Serveur Web

    sudo apt-get install apache2 apache2-doc
    sudo service apache2 status
    sudo service apache2 start ( stop)
    sudo service apache2 restart

php:

    sudo apt-get install php-common libapache2-mod-php php-cli
    
Pour tester l’installation, dans le répertoire /var/www/html, créez le fichier info.php 

avec le contenu suivant

<?php phpinfo(); ?>, redemarrer apache et verifier  http://IP_du_serveur/info.php  

mysql :

    sudo apt-get install mysql-server
    sudo /etc/init.d/mysql start

# personnaliser la sécurisation
sudo mysql_secure_installation utility
# changement de mot de passe root
sudo mysql -u root -p
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'le_mot_de_pass_choisi';

PHPMYADMIN :

sudo apt-get install phpmyadmin

Afin d’accéder à l’interface de gestion de phpMyAdmin, vous devrez finaliser la configuration
de votre serveur Apache. Pour cela, éditez le fichier /etc/apache2/apache2.conf
Ajouter à la fin :
# Include phpMyAdmin
Include /etc/phpmyadmin/apache.conf
sudo service apache2 restart

# erreur count dans phpmyadmin

 sudo vim /usr/share/phpmyadmin/libraries/sql.lib.php
 # erreur de parentheses '(count($analyzed_sql_results['select_expr']) == 1)'
sudo service apache2 restart






PYTHON :
--------

PyPI (de l'anglais « Python Package Index ») est le dépôt tiers officiel du langage de programmation Python.
Son objectif est de doter la communauté des développeurs Python d'un catalogue complet recensant tous
les paquets Python libres1. Il est analogue au dépôt CPAN pour Perl

* pip:

A partir des versions 2.7.9 et et 3.4, pip est fournit automatiquement avec Python.

sudo apt install python3-pip

pip install --user bottle
pip uninstall bottle
pip install bottle==0.9 # installer une version
pip install bottle --upgrade # mise a jour
pip install bottle==0.9 --upgrade # downgrade

pip freeze > requirements.txt # liste toutes les librairies installées et leurs versions.
On peut ensuite les réinstaller sur une autre machine facilement:

pip install -r requirements.txt

pip bundle nom_du_projet.pybundle -r requirements.txt # création d un bundle
pip install nom_du_projet.pybundle

pip install git+git://github.com/sametmax/0bin.git # pourvu que le code source vienne avec un fichier setup.py




* Python mysqlclient :

sudo apt-get install libssl-dev # Unable to install mysqlclient using pip (Ubuntu 18.04 LTS)
            ou
apt-get install default-libmysqlclient-
            et
pip install mysqlclient

lsb_release _a # afficher version linux

Environnement Virtuel :

pip install --user virtualenv

DJANGO :
--------

sudo pip3 install django-debug-toolbar
sudo pip3 install dj-database-url

sudo apt install liapache2-mod-wgsi
http://packages.debian.org/wheezy/libapache2-mod-wsgi

TEST DE DEPLOIEMENT :
---------------------
django-admin startproject idreammicro # dans le dossier django_apps
django-admin startapp helloword










