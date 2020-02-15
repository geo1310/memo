
MARKDOWN
------------------------------------------------------------------------------------------------------------------
###### [README](/README.md)
C'est un petit langage très simple qui permet d'écrire du HTML de façon raccourcie.  
<https://michelf.ca/projets/php-markdown/syntaxe/>

Emphase faible (italique)  
Voici un mot *important*  
Voici un mot _important_ 

Emphase forte (gras)  
Voici des mots **très importants**  
Voici des mots __très importants__

Voici un mot ~~barré~~ !!!

* Une puce
* Une autre puce
    * Une sous-puce
    * Une autre sous-puce
* Et encore une autre puce !

1. Et de un
2. Et de deux
3. Et de trois

**Sous-Listes numérotées:**
   1. Numbered sub-list
      1. Numbered sub-sub-list
      1. Numbered sub-sub-list
         1. Numbered sub-sub-list
         1. Numbered sub-sub-list
         
> Ceci est un texte cité. Vous pouvez répondre

> Une citation
>
> > Une réponse à la citation
> >
> > Réponse qui contient une liste à puces :
> >
> > * Puce
> > * Autre puce

# Titre 1
Titre 1
=======
## Titre 2
Titre 2
-------
### Titre 3
#### Titre 4
##### Titre 5
###### Titre 6

-----
Faire une barre de séparation.

-----

| Les tableaux | sont | intéressants |
| ------------- |:-------------:| -----:|
| la colonne 3 | est alignée à droite | 1600 $ |
| la colonne 2 | est centrée | 12 $ |
| les rayures | sont élégantes | 1 $ |

### Liens :

[Google](https://www.google.com)  
Google : <https://www.google.com>

Les images s'insèrent de la même façon que les liens.  
Vous devez simplement mettre un point d'exclamation devant les premiers crochets :  

![Zozor](http://uploads.siteduzero.com/files/420001_421000/420263.png)

Logo de Markdown : ![logo de Markdown Here](http://adam-p.github.io/markdown-here/img/icon24.png)

### Bloc de code :

```javascript
function colorationSyntaxique() {
  var n = 33;
  var t = "bonjour";
  console.log(t);
}
```

```
bloc de code
sans coloration syntaxique
```

    var n = 33;
    var t = "bonjour";
    console.log(t);

Code à l'interieur `d'une ligne de texte`