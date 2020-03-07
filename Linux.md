
LINUX :
----------------------------------------------------------------------------------------------------
   ###### [README](/README.md) 
   
#### VERSION :
    cat /proc/version # version du noyau Linux utilisé, son nom, la version du compilateur utilisé
    uname -mr # version du noyau Linux utilisé
   
    # liste des noyaux installés
    dpkg -l | awk '/^rc/{next} ; / linux-(c|g|h|i|lo|m|si|t)/{print $1,$2,$3,$4 | "sort -k3 | column -t"}'  
    
    # mise à jour
    sudo apt-get update &&  apt-get upgrade && apt-get dist-upgrade
---    
#### LISTE COMMANDES :
        

---    
###FICHIERS :

#####STRUCTURE :

* **bin :** contient des programmes (exécutables) susceptibles d'être utilisés par tous les utilisateurs de la machine.
* **boot :** fichiers permettant le démarrage de Linux.
* **dev :** fichiers contenant les périphériques.Ce dossier contient des sous-dossiers qui « représentent » chacun un périphérique.  
* **etc :** fichiers de configuration.
* **home :** répertoires personnels des utilisateurs.A la manière du dossier Mes documents de Windows.
* **lib :** dossier contenant les bibliothèques partagées (généralement des fichiers.so) utilisées par les programmes. C'est en fait là qu'on trouve l'équivalent des.dll de Windows.
* **media :** lorsqu'un périphérique amovible (comme une carte mémoire SD ou une clé USB) est inséré dans votre ordinateur, Linux vous permet d'y accéder à partir d'un sous-dossier de media. On parle de montage.
* **mnt :** c'est un peu pareil que media, mais pour un usage plus temporaire.
* **opt :** répertoire utilisé pour les add-ons de programmes.
* **proc :** contient des informations système.
* **root :** c'est le dossier personnel de l'utilisateur « root ». Normalement, les dossiers personnels sont placés dans home, mais celui de « root » fait exception. En effet, comme je vous l'ai dit dans le chapitre précédent, « root » est le superutilisateur, le « chef » de la machine en quelque sorte. Il a droit à un espace spécial.
* **sbin :** contient des programmes système importants.
* **tmp :** dossier temporaire utilisé par les programmes pour stocker des fichiers.
* **usr :** c'est un des plus gros dossiers, dans lequel vont s'installer la plupart des programmes demandés par l'utilisateur.
* **var :** ce dossier contient des données « variables », souvent des logs (traces écrites de ce qui s'est passé récemment sur l'ordinateur).

##### FICHIERS UTILES :
    /usr/share/vim/vimrc # Configuration vim
    ~/.vimrc # Configuration vim local
    /etc/apt/sources.list # liste des dépots
    ~/.bashrc # liste des alias  
 
##### COMMANDES UTILES :
        du # disk usage
        ls -larthF # liste détaillée
        ls -i # liste avec no inode
        cat ou less # affichage de fichiers
        head file -n 2 # affiche les 2 premieres lignes d'un fichier
        tail file -n 2 -f -s 3 # affiche les 2 dernieres lignes d'un fichier ( -f:follow -s 3 : toutes les 3s)
        
        touch file # crée un fichier ou modifie sa date s'il existe
        
        mkdir -p x/y/z # -p crée les sous-dossiers également
        cp file copyfile # copie de fichier
        cp -R # copie un dossier
        mv # deplacer ou renommer un fichier ou un dossier
        rm -r # suppression d'un dossier
        rm -rf /* # la commande qui tue 
        ln # creer un lien physique ( partage le meme contenu entre plusieurs nom de fichiers )
        ln -s # creer un lien symbolique ( raccourci entre plusieurs fichiers ou dossiers)
        
        
        
        
        
        
 ---
#### CLAVIER ( azerty - qwerty ):

    setxkbmap fr # ponctuel
    setxkbmap us
    sudo dpkg-reconfigure keyboard-configuration

    sudo loadkeys fr
    sudo loadkeys us
---
#### SSH SERVER :

    sudo apt-get install openssh-server
    sudo /etc/init.d/ssh start, stop, status, reload

    /etc/ssh/ssh_config # fichier de config

    ssh login@ip # ouvrir une connection
    
    # Reconfigurer clé SSH
    cd /etc/ssh
    sudo dpkg-reconfigure openssh-server # modifie la clé 
---    
#### CONFIG MATERIEL :

    lspci # liste materiel pci
    lsusb # liste materiel usb
    
    lsmod # ???
---
#### CONFIG RESEAU :
    # identifier les cartes réseau :
    lspci -nn | grep -i network
    lspci -nnd ::0280 # chercher une carte wifi
    
    hostname
    hostname -I
    ifconfig
    ip addr # debian 9
    
    iwconfig # sans-fil
    sudo iwlist scan # ???

##### Liste des Ports ouverts :

    netstat -tlnpu # t=tcp, u=udp, p=programs/PID, l=listening, n=numeric  
    ps auxw | grep runserver # liste des serveurs
    kill -9 process
---    
#### ENVIRONNEMENT VIRTUEL :

    sudo pip3 install virtualenv
    virtualenv --version
    virtualenv --python=python3 envname
    source . envname/bin/activate
---
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

    synaptic # gestionnaire de paquets avec interface 

##### INSTALLER UNE ARCHIVE :

1. Extraire l'archive dans mes documents
2. Afficher les fichiers
3. Copier le lien du dossier dans mes documents ( clic droit proprietes...)

        sudo mv /home/geo1310/Documents/sublime_text_3 /opt
        sudo ln -s /opt/sublime_text_3 usr/local/sublime_text_3
        sudo ln -s /usr/local/sublime_text_3/sublime_text /usr/local/bin/st3
---        
#### COMMANDES PERSONNALISABLES :

    vim ~/.bash_aliases

* Exemple -> alias int='sudo nano /etc/network/interfaces'
* Relancer la console
    
---
###UTILISATEURS ET DROITS :

 sudo : super-user do  
 groups ou id # verification de groupes d un utilisateur
    
    addgroup # cree un groupe 
    adduser newuser # nouvel utilisateur (useradd et userdel pour autres distributions )
    usermod -aG sudo newuser #ajout au groupe sudo
    adduser mnewuser sudo
    deluser --remove-home user # supprimer un utilisateur

    su - newuser # connexion ( le - permet d'atterir dans le home du newuser )
    sudo su # connexion root ( ctrl+d ou exit pour sortir de root )
    
    sudo passwd user # changement mot de passe pour user
---
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
    












