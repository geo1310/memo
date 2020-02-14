

PYTHON :
--------------------------------------------------------------------------------------------------------

PyPI (de l'anglais « Python Package Index ») est le dépôt tiers officiel du langage de programmation Python.  
Son objectif est de doter la communauté des développeurs Python d'un catalogue complet recensant tous  
les paquets Python libres1. Il est analogue au dépôt CPAN pour Perl

#### pip:

A partir des versions 2.7.9 et et 3.4, pip est fournit automatiquement avec Python.

    sudo apt install python3-pip

    pip install --user bottle
    pip uninstall bottle
    pip install bottle==0.9 # installer une version
    pip install bottle --upgrade # mise a jour
    pip install bottle==0.9 --upgrade # downgrade

    pip freeze > requirements.txt # liste toutes les librairies installées et leurs versions.
    pip install -r requirements.txt # On peut ensuite les réinstaller sur une autre machine facilement


    pip bundle nom_du_projet.pybundle -r requirements.txt # création d un bundle
    pip install nom_du_projet.pybundle

    pip install git+git://github.com/sametmax/0bin.git # pourvu que le code source vienne avec un fichier setup.py


#### Python mysqlclient :

    sudo apt-get install libssl-dev # Unable to install mysqlclient using pip (Ubuntu 18.04 LTS)
            ou
    apt-get install default-libmysqlclient-
            et
    pip install mysqlclient


#### Environnement Virtuel :

    pip install --user virtualenv

## DJANGO :

    sudo pip install django-debug-toolbar
    sudo pip install dj-database-url
    sudo pip install whitenoise

    sudo apt install liapache2-mod-wgsi
    
<http://packages.debian.org/wheezy/libapache2-mod-wsgi>

Création d'un projet ou d'une Application :

    django-admin startproject NameProject
    django-admin startapp NameApp
    
Pour que Django crée la table SQL associée au modèle :

    python manage.py makemigrations 
    python manage.py migrate
    
Django propose un interpréteur interactif Python synchronisé avec votre configuration du framework.

    python manage.py shell
    
    >>> from blog.models import Article
    >>> article = Article(titre="Salut", auteur="Eric", contenu="Nouveau sur le Blog")
    >>> article.save()
    
    >>> article.delete()












