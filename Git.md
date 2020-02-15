
GIT :                                                                      
-------------------------------------------------------------------------------------------------------
###### [README](/README.md)
### Installation :
Linux : <http://git-scm.com/downloads>  
Windows :  <http://msysgit.github.io>
 
    git config --global user.name "name"
    git config --global user.email "email"

Pour activer un dossier comme repository Git, il suffit de se placer dans ce dossier avec le Terminal :

    git init
    git add checklist-vacances.md # ajoute un fichier
    git add . # ajoute tous les fichiers
     
Créez le fichier **.gitignore** pour y lister les fichiers que vous ne voulez pas versionner dans Git 
(les fichiers comprenant les variables de configuration, les clés d'APIs et autres clés secrètes, les mots de passe, etc.). 
Listez ces fichiers ligne par ligne dans .gitignore en indiquant leurs chemins complets.

### Remote :
1. Interne :

2. Externe
    Services de remote :
    1. [GitHub](https://github.com/)
    2. [BitBucket](https://bitbucket.org/)

### Commandes :

Annuler tous les changements que je n'ai pas encore commités :

    git reset --hard‌

Vous pouvez "revert" un commit, c'est-à-dire créer un nouveau commit qui fait l'inverse du précédent, avec la commande suivante :

    git log # affiche la liste de tous les commits
    git revert SHADuCommit

Si vous voulez simplement modifier le message de votre dernier commit, vous pouvez utiliser la commande suivante :

    git commit --amend -m "Votre nouveau message"

Pour vous positionner sur un commit donné de votre historique :

    git checkout SHADuCommit
    git checkout master # pour revenir sur la branche principale
    
#### Récupérez du code d'un autre repository :

    git clone lienFourniParGitHub 

#### Create a new repository on the command line :

    echo "# crepes_bretonnes" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/geo1310/crepes_bretonnes.git
    git push -u origin master

Pushez! Envoyez ces modifications sur votre repo GitHub :

    git push origin master
    
La branche **master** est la branche qui contient le code courant de votre repo GitHub.  
Le remote sur lequel vous envoyez votre code est appelé **origin** par défaut.

Pour récupérer en local les dernières modifications du repo GitHub :

    git pull origin master
    
Créez des branches :

    git branch nouvelle-branche
    git checkout nouvelle-branche
    git checkout -b ma-branche # cree la branche et se positionne dessus
    
    git checkout brancheA
    git merge brancheB # Fusionne B avec A
    
### Résoudre un Conflit :

Il existe aussi des outils proposant des interfaces graphiques pour comparer les différences de versions d'un fichier.  
 *vimdiff, meld, opendiff, kdiff3, tkdiff, xxdiff, tortoisemerge, gvimdiff, diffuse, ecmerge, p4merge, araxis, emerge*

    git mergetool vimdiff 
    git commit # Git va détecter que vous avez résolu le conflit et vous proposer un message de commit par défaut
    
 Retrouver qui a fait une modification particulière dans un fichier :

    git blame nomdufichier.extension # liste toutes les modifications qui ont été faites sur le fichier
    git log
    git show 05b1233
    
Mettre de côté vos modifications en cours :

    git stash # mets de coté les modifications encours
    git stash pop # récupère les modifications mises de coté
    
Attention, pop vide votre stash des modifications que vous aviez rangées dedans.   
Donc une fois que vous avez récupéré ces modifications dans votre branche, il vous faut finir votre tâche et les committer !   
(ou bien les remettre de côté en exécutant à nouveau la commande git stash).

Si vous voulez garder les modifications dans votre stash, vous pouvez utiliser apply à la place de pop :

     git stash apply
     
### Pull Request :
Un **FORK** : faire une copie du repo en question sur votre compte GitHub. Pour cela, rendez-vous sur le repo GitHub

