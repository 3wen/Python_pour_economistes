---
title: "Python pour les économistes"
author: "Ewen Gallic"
date: "Octobre 2018"
knit: "bookdown::render_book"
documentclass: book
bibliography: [biblio.bib]
biblio-style: apalike
link-citations: yes
colorlinks: yes
lot: yes
lof: yes
fontsize: 12pt
monofont: "Source Code Pro"
monofontoptions: "Scale=0.7"
site: bookdown::bookdown_site
output:
  bookdown::gitbook:
    keep_md: true
    css: styles/style.css
    highlight: tango
    config:
      toc:
        collapse: subsection
        scroll_highlight: yes
        before: null
        after: null
      search: yes
      edit: https://github.com/3wen/Python_pour_economistes/edit/master/%s
  bookdown::pdf_book:
    highlight: tango
    keep_tex: yes
    includes:
      in_header: styles/mystyle_books.tex
  bookdown::epub_book:
    stylesheet: styles/style.css
---





# Propos liminaires {-}

<!-- ```{r, echo=F} -->
<!-- invisible(py_config()) -->
<!-- ``` -->





Ces notes de cours ont été réalisées dans le cadre d'un enseignement d'introduction à Python adressé à des étudiants du parcours Économétrie et Big Data de [l'École d'Economie d'Aix-Marseille / Aix-Marseille School of Economics (AMSE)](https://www.amse-aixmarseille.fr/) d'Aix-Marseille Université.


## Objectifs

Cet ouvrage a pour but l'initiation au langage de programmation Python, afin d'être capable de s'en servir de manière efficace et autonome. Le lecteur peut exécuter tous les exemples fournis (et est vivement encouragé à le faire). Des exercices viennent clore certains chapitres, pour mieux s'approprier les notions couvertes au fur et à mesure de la lecture.


Bien évidemment, Python étant un langage très vaste, ces notes ne sauraient et n'ont pas pour vocation à être exhaustives de l'utilisation de ce langage informatique.




## À qui s'adressent ces notes ?

Dans un premier temps, cet ouvrage s'adresse aux débutants qui souhaientent apprendre les bases en Python. Il est à destination des étudiants de l'AMSE mais pourrait intéresser des individus ayant une approche de la donnée à travers la discipline économique désirant découvrir Python.

# Introduction


Ce document est construit principalement à l'aide de différentes références, parmi lesquelles :

- des livres : @briggs_2013_python, @grus_2015_data, @vanderplas2016python, @mckinney_2017_python ;
- des (excellents) notebooks : @navaro_python.



## Historique


Python est un langage de programmation multi plates-formes, écrit en `C`, placé sous une licence libre. Il s'agit d'un langage interprété, c'est-à-dire qu'il nécessite un interprète pour exécuter les commandes, et n'a pas de phase de compilation. Sa première version publique date de 1991. L'auteur principal, [Guido van Rossum](https://en.wikipedia.org/wiki/Guido_van_Rossum) avait commencé à travailler sur ce langage de programmation durant la fin des années 1980. Le nom accordé au langage Python provient de l'intérêt de son créateur principal pour une série télévisée britannique diffusée sur la BBC intitulée "*Monty Python's Flying Circus*".

La popularité de Python a connu une croissance forte ces dernières années, comme le confirment les résultats de sondages proposés par [Stack Overflow](https://stackoverflow.com/) depuis 2011. Stack Overflow propose à ses utilisateurs de répondre à une enquête dans laquelle de nombreuses questions leur sont proposées, afin de décrire leur expérience en tant que développeur. [Les résultats de l'enquête de 2018](https://insights.stackoverflow.com/survey/2018#technology) montrent une nouvelle avancée de l'utilisation de Python par les développeurs. En effet, comme le montre la Figure\ \@ref(fig:intro-stack-langages), 38.8% des répondants indiquent développer en Python, soit 6.8 points de pourcentage de plus qu'un an auparavant, ce qui fait de ce langage de programmation celui dont la croissance a été la plus importante entre 2017 et 2018.

<div class="figure" style="text-align: center">
<img src="_main_files/figure-html/intro-stack-langages-1.png" alt="Langages de programmation, de scripting et de balisage."  />
<p class="caption">(\#fig:intro-stack-langages)Langages de programmation, de scripting et de balisage.</p>
</div>

## Versions

Ces notes de cours visent à fournir une introduction à Python, dans sa version 3.x. En ce sens, les exemples fournis corresponderont à cette version, non pas aux précédentes.

Comparativement à la version 2.7, la version 3.0 a apporté des modofications profondes. Il faut noter que Python 2.7 prendra "[sa retraite](https://pythonclock.org/)" le premier janvier 2020. Passée cette date, le support ne sera plus assuré.

## Espace de travail

Il existe de nombreux environnements dans lesquels programmer en Python. Nous allons en présenter succinctement quelques uns.

Il est supposé ici que vous vous avez installé [Anaconda](https://www.anaconda.com/) sur votre poste. Anaconda est une distribution gratuite et open source des langages de programmation Python et R pour les applications en *data science* et apprentissage automatique. Par ailleurs, lorsqu'il est fait mention du terminal dans les notes, il est supposé que le système d'exploitation de votre machine est soit Linux, soit Mac OS.

### Python dans un terminal

Il est possible d'appeler Python depuis un terminal, en exécutant la commande suivante (sous Windows : dans le menu démarrer, lancer le logiciel "Python 3.6") :

```shell
python
```

Ce qui donne le rendu visible sur la Figure\ \@ref(fig:intro-python-terminal) :

<div class="figure" style="text-align: center">
<img src="figs/python_terminal.png" alt="Python dans un terminal." width="70%" />
<p class="caption">(\#fig:intro-python-terminal)Python dans un terminal.</p>
</div>

On note la présence des caractères `>>>` (*prompt*), qui invitent l'utilisateur à inscrie une commande. Les expressions sont évaluées une fois qu'elle sont soumises (à l'aide de la touche `ENTREE`) et le résultat est donné, lorsqu'il n'y a pas d'erreur dans le code.

Par exemple, lorsque l'on évalue `2+1` :

```shell
>>> 2+1
3
>>>
```

On note la présence du *prompt* à la fin, indiquant que Python est prêt à recevoir de nouvelles instructions.


### IPython

Il existe un environnement un peu plus chaleureux que Python dans le terminal : IPython. Il s'agit également d'un terminal interactif, mais avec davantages de fonctionnalités, notamment la coloration syntaxique ou l'auto-complétion (en utilisant la touche de tabulation).

Pour lancer IPython, on peut ouvrir un terminal et taper (puis valider) :

```shell
ipython
```

On peut également lancer IPython depuis la fenêtre d'accueil d'Anaconda, en cliquant sur le bouton `Launch` de l'application `qtconsole`, visible sur la Figure\ \@ref(fig:intro-anaconda-navigator).


<div class="figure" style="text-align: center">
<img src="figs/anaconda_navigator.png" alt="Fenêtre d'accueil d'Anaconda." width="100%" />
<p class="caption">(\#fig:intro-anaconda-navigator)Fenêtre d'accueil d'Anaconda.</p>
</div>


La console IPython, une fois lancée, ressemble à ceci :
<div class="figure" style="text-align: center">
<img src="figs/ipython.png" alt="Console IPython." width="70%" />
<p class="caption">(\#fig:unnamed-chunk-4)Console IPython.</p>
</div>

Soumettons une instruction simple pour évaluation à Python :

```python
print("Hello World")
```


Le résultat donne :

```shell
In [1]: print("Hello World")
Hello World

In [2]:
```


Plusieurs choses sont à noter. Premièrement, on note qu'à la fin de l'exécution de l'instruction, IPython nous indique qu'il est prêt à recevoir de nouvelles instruction, par la présence du *prompt* `In [2]:`. Le numéro entre les crochets désigne le numéro de l'instruction. On note qu'il est passé de 1 à 2 après l'exécution. Ensuite, on note que le résultat de l'appel à la fonction `print()`, avec la chaîne de caractères (délimitée par des guillemets), affiche à l'écran ce qui était contenu entre les parenthèses.

### Spyder

Tandis que lorsqu'on utilise Python via un terminal, il est préférable d'avoir un éditeur de texte ouvert à côté (pour pouvoir sauvegarder les instructions), comme, par exemple, [Sublime Text](https://www.sublimetext.com/) sous Linux ou Mac OS, ou [notepad++](https://notepad-plus-plus.org/) sous Windows.

Une autre alternative consiste à utiliser un environnement de développement (IDE, pour *Integrated development environment*) unique proposant notamment, à la fois un éditeur et une console. C'est ce que propose [Spyder](https://www.spyder-ide.org/), avec en outre de nombreuses fonctionnalités supplémentaires, comme la gestion de projet, un explorateur de fichier, un historique des commandes, un débugger, etc.


Pour lancer Spyder, on peut passer par un terminal, en évaluant tout simplement `Spyder` (ou en lançant le logiciel depuis le menu démarrer sous Windows). Il est également possible de lancer Spyder depuis Anaconda.

L'environnement de développement, comme visible sur la Figure\ \@ref(fig:intro-spyder), se décompose en plusieurs fenêtres :

- à gauche : l'éditeur de script ;
- en haut à droite : une fenêtre permettant d'afficher l'aide de Python, l'arborescence du système ou encore les variables créées ;
- en bas à droite : une ou plusieurs consoles.


<div class="figure" style="text-align: center">
<img src="figs/spyder.png" alt="Spyder." width="100%" />
<p class="caption">(\#fig:intro-spyder)Spyder.</p>
</div>

### Jupyter

Il existe une interface graphique par navigateur d'IPython, appelée [Jupyter Notebook](http://jupyter.org/). Il s'agit d'une application en open-source permettant de créer et partager des documents qui contiennent du code, des équations, des représentations graphiques et du texte. Il est possible de faire figurer et exécuter des codes de langages différents dans les notebook Jupyter.


Pour lancer Jupyter, on peut passer par Anaconda. Après avoir cliqué sur le bouton `Launch`, de Jupyter Notebook, le navigateur web se lance et propose une arborescence, comme montré sur la Figure\ \@ref(fig:intro-jupyter). Sans que l'on s'en rendiez compte, un serveur local web a été lancé ainsi qu'un processus Python (un *kernel*).

Si le navigateur en se lance pas automatiquement, on peut accéder à la page qui aurait dû s'afficher, en se rendant à l'adresse suivante : http://localhost:8890/tree?.

<div class="figure" style="text-align: center">
<img src="figs/jupyter.png" alt="Jupyter." width="100%" />
<p class="caption">(\#fig:intro-jupyter)Jupyter.</p>
</div>


Pour aborder les principales fonctions de Jupyter, nous allons créer un dossier `jupyter` dans un répertoire de notre choix. Une fois ce dossier créé, y naviguer à travers l'arborescence de Jupyter, dans le navigateur web.


Une fois dans le dossier, créer un nouveau Notebook `Python 3` (en cliquant sur le bouton `New` en haut à gauche de la fenêtre, puis sur  Python 3`).


Un notebook intitulé `Untitled` vient d'être créé, la page affiche un document vide, comme visible sur la Figure\ \@ref(fig:intro-jupyter-notebook).


<div class="figure" style="text-align: center">
<img src="figs/jupyter_notebook.png" alt="Un notebook vide." width="100%" />
<p class="caption">(\#fig:intro-jupyter-notebook)Un notebook vide.</p>
</div>


Si on regarde dans notre explorateur de fichier, dans le dossier `jupyter` fraîchement créé, un nouveau fichier est apparu : `Untitled.ipynb`.





#### Évaluation d'une instruction

Retournons dans le navigateur web, sur la page affichant notre *notebook*.

En dessous de la barre des menus, on note la présence d'une zone encadrée, **une cellule**, commençant, à l'instar de ce que l'on voyait dans la console sur IPython, par `IN []:`. À droite, la zone grisée nous invite à soumettre des instructions en Python.

Inscrivons :

```python
2+1
```

Pour soumettre l'instruction à évaluation, il existe plusieurs manières (il s'assurer d'avoir cliqué à l'intérieur de la cellule) :

- dans la barre des menus : `Cell > Run Cells` ;
- dans la barre des raccourcis : bouton `Run` ;
- avec le clavier : maintenir la touche `CTRL`et presser sur `Entree`.

<div class="figure" style="text-align: center">
<img src="figs/jupyter_notebook_2.png" alt="Cellule évaluée." width="100%" />
<p class="caption">(\#fig:unnamed-chunk-8)Cellule évaluée.</p>
</div>

#### Cellules de texte

Un des intérêts des *notebooks* est qu'il est possible d'ajouter des cellules de texte.

Ajoutons une cellule en-dessous de la première. Pour ce faire, on peut procéder soit :

- par la barre de menu : `Insert > Insert Cell Below` (pour insérer une cellule en-dessous ; si on désire une insertion au-dessus, il suffit de choisir `Insert Cell Above`) ;
- en cliquant dans le cadre de la cellule à partir de laquelle on désire faire un ajout (n'importe où, sauf dans la zone grisée de code, de manière à passer en mode `commande`), puis en appuyant sur la touche `B` du clavier (`A` pour une insertion au-dessus).

La nouvelle cellule appelle à nouveau à inscrire une instruction en Python. Pour indiquer que le contenu doit être interprété comme du texte, il est nécessaire de le préciser. Encore une fois, plusieurs méthodes permettent de le faire :

- par la barre de menu : `Cell > Cell Type > Markdown` ;
- par la barre des raccourcis : dans le menu déroulant où est inscrit `Code`, en sélectionnant `Markdown` ;
- en mode commande (après avoir cliqué à l'intérieur du cadre de la cellule, mais pas dans la zone de code), en appuyant sur la touche `M` du clavier.

La cellule est alors prête à recevoir du texte, rédigé en markdown. Pour plus d'informations sur la rédaction en Markdown, se référer à cette [antisèche](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) par exemple.

Entrons quelques lignes de texte pour voir très rapidement le fonctionnement des cellules rédigées en Markdown.


```shell
# Un titre de niveau 1

Je vais écrire *du texte en italique* et aussi **en gras**.

## Un titre de niveau 2

Je peux faire des listes :

- avec un item ;
- un second ;
- et un troisième imbriquant une nouvelle liste :
    - avec un sous-item,
    - et un second ;
- un quatrième incluant une liste imbriquée numérotée :
    1. avec un sous-item,
    1. et un autre.

## Un autre titre de niveau 2


Je peux même faire figurer des équation $\LaTeX$.
Comme par exemple $X \sim \mathcal{N}(0,1)$.

Pour en savoir plus sur $\LaTeX$, on peut se référer à cette :
  [page Wikipédia](https://en.wikibooks.org/wiki/LaTeX/Mathematics).
```

Ce qui donne, dans Jupyter :

<div class="figure" style="text-align: center">
<img src="figs/jupyter_notebook_3.png" alt="Cellule textuelle non évaluée." width="100%" />
<p class="caption">(\#fig:unnamed-chunk-10)Cellule textuelle non évaluée.</p>
</div>

Reste alors à l'évaluer, comme s'il s'agissait d'une cellule contenant une instruction Python, pour basculer vers un affichage Markdown (`CTRL` et `ENTREE`).

Pour **éditer le texte** une fois que l'on a basculé en markdown, un simple double-clic dans la zone de texte de la cellule fait l'affaire.

Pour **changer le type de la cellule pour qu'elle devienne du code** :

- par la barre de menu : `Cell > Cell Type > Code` ;
- par la barre des raccourcis : dans le menu déroulant où est inscrit `Code`, en sélectionnant `Code` ;
- en mode commande, appuyer sur la touche du clavier `Y`.


#### Suppression d'une cellule

Pour supprimer une cellule :

- par la barre de menu : `Edit > Delete Cells` ;
- par la barre des raccourcis : icône en forme de ciseaux ;
- en mode commande, appuyer deux fois sur la touche du clavier `D`.


## Les variables

### Assignation et suppression

Lorsque nous avons évalué les instructions `2+1` précédemment, le résultat s'est affiché dans la console, mais il n'a pas été enregistré. Dans de nombreux cas, il est utile de conserver le contenu du résultat dans un objet, pour pouvoir le réutiliser par la suite. Pour ce faire, on utilise des *variables*. Pour créer une variable, on utilise le signe d'égalité (`=`), que l'on fait suivre par ce que l'on veut sauvegarder (du texte, un nombre, plusieurs nombres, etc.) et précéder par le nom que l'on utilisera pour désigner cette variable.

Par exemple, si on souhaite stocker le résultat du calcul `2+1` dans une variable que l'on nommera `x`, il faudra écrire :

```python
x = 2+1
```

Pour afficher la valeur de notre variable `x`, on fait appel à la fonction `print()` :

```python
print(x)
```

```
## 3
```


Pour changer la valeur de la variable, il suffit de faire une nouvelle assignation :

```python
x = 4
print(x)
```

```
## 4
```

Il est également possible de donner plus d'un nom à un même contenu (on réalise une copie de `x`) :

```python
x = 4;
y = x;
print(y)
```

```
## 4
```


Si on modifie la copie, l'original ne sera pas affecté :

```python
y = 0
print(y)
```

```
## 0
```


```python
print(x)
```

```
## 4
```

Pour **supprimer** une variable, on utilise l'instruction `del` :

```python
del y
```

L'affichage du contenu de `y` renvoit une erreur :

```python
print(y)
```

```
## NameError: name 'y' is not defined
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```

Mais on note que la variable `x` n'a pas été supprimée :

```python
print(x)
```

```
## 4
```

### Conventions de nommage

Le nom d'une variable peut être composé de caractères alphanumériques ainsi que du trait de soulignement (`_`) (il n'y a pas de limite sur la longueur du nom). Il est proscrit de faire commencer le nom de la variable par un nombre. Il est également interdit de faire figurer une espace dans le nom d'une variable.

Pour accroitre la lisibilité du nom des variables, plusieurs méthodes existes. Nous adopterons la suivante :

- toutes les lettres en minuscule ;
- la séparation des termes par un trait de soulignement.

Exemple, pour une variable contenant la valeur de l'identifiant d'un utilisateur : `id_utilisateur`.

Il faut noter que le nom des variables est **sensible à la casse** :

```python
x = "toto"
print(x)
```

```
## toto
```


```python
print(X)
```

```
## NameError: name 'X' is not defined
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```

## Les commentaires


Pour ajouter des commentaires en python, il existe plusieurs façons.


Une des manières de faire est d'utiliser le symbole dièse (`#`) pour effectuer un **commentaire sur une seule ligne**. Tout ce qui suit le dièse jusqu'à la fin de la ligne ne sera pas évalué par Python. En revanche, ce qui vient avant le dièse le sera.

```python
# Un commentaire print("Bonjour")
print("Hello") # Un autre commentaire
```

```
## Hello
```

L'introduction d'un **bloc de commentaires** (des commentaires sur plusieurs lignes) s'effectue quant à elle en entourant ce qui est ) commenter d'un délimiteur : trois guillemets simples ou doubles :

```python
"""
Un commentaire qui commencer sur une ligne
et qui continue sur une autre
et s'arrête à la troisième
"""
```

## Les modules et les packages


Certaines fonctions de base en Python sont chargées par défaut. D'autres, nécessitent de charger un **module**. Ces modules sont des fichiers qui contiennent des **définitions** ainsi que des **instructions**.

Lorsque plusieurs modules sont réunis pour offrir un ensemble de fonctions, on parle alors de _**package**_.

Parmi les *packages* qui seront utilisés dans ces notes, on peut citer :

- [NumPy](http://www.numpy.org/), un *package* fondamental pour effectuer des calculs scientifiques ;
- [pandas](https://pandas.pydata.org/), un *package* permettant de manipuler facilement les données et de les analyser ;
- [Matplotlib](https://matplotlib.org/), un *package* permettant de réaliser des graphiques.

Pour charger un module (ou un *package*), on utilise la commande `import`. Par exemple, pour charger le *package* `pandas` :

```python
import pandas
```

Ce qui permet de faire appel à des fonctions contenues dans le module ou le *package*. Par exemple, ici, on peut faire appel à la fonction `Series()`, contenue dans le *package* `pandas`, permettant de créer un tableau de données indexées à une dimension :


```python
x = pandas.Series([1, 5, 4])
print(x)
```

```
## 0    1
## 1    5
## 2    4
## dtype: int64
```

Il est possible de donner un alias au module ou au *package* que l'on importe, en le précisant à l'aide de la syntaxe suivante :

```python
import module as alias
```

Cette pratique est courante pour abréger les noms des modules que l'on va être amené à utiliser beaucoup. Par exemple, pour `pandas`, il est coutume d'écourter le nom en `pd` :


```python
import pandas as pd
x = pd.Series([1, 5, 4])
print(x)
```

```
## 0    1
## 1    5
## 2    4
## dtype: int64
```

On peut également importer une seule fonction d'un module, et lui attribuer (optionnellement) un alias. Par exemple, avec la fonction `pyplot` du *package* `matplotlib`, il est coutume de faire comme suit :


```python
import matplotlib
import matplotlib.pyplot  as plt
import numpy  as np
x = np.arange(0, 5, 0.1);
y = np.sin(x)
plt.plot(x, y)
```




<img src="figs/intro_pyplot.png" style="display: block; margin: auto;" />




## L'aide


Pour conclure cette introduction, il semble important de mentionner la présence de l'**aide** et de la **documentation** en Python.

Pour obtenir des informations sur des fonctions, il est possible de se référer à la [documentation en ligne](https://docs.python.org/3/). Il est également possible d'obtenir de l'aide à l'intérieur de l'environnement que l'on utilise, en utilisant le point d'interrogation (`?`).

Par exemple, lorsque l'on utilise IPython (ce qui, rappelons-le, est le cas dans Jupyter), on peut accéder à l'aide à travers différentes syntaxes :

- `?` : fournit une introduction et un aperçu des fonctionnalités offertes en Python (on la quitte avec la touche `ESC` par exemple);
- `object?` : fournit des détails au sujet de `'object'` (par exemple `x?` ou encore `plt.plot?`) ;
- `object??` : plus de détails à propos de `'object'` ;
- `%quickref` : référence courte sur les syntaxes en Python ;
- `help()` : accès à l'aide de Python.


*Note* : la touche de **tabulation** du clavier permet non seulement une **autocomplétion**, mais aussi une **exploration du contenu** d'un objet ou module.

Par ailleurs, lorsqu'il s'agit de trouver de l'aide sur un problème plus complèxe, le bon réflèxe à adopter est de ne pas hésiter à chercher sur un moteur de recherche, dans des mailing-lists et bien évidemment sur les nombreuses questions sur [Stack Overflow](https://stackoverflow.com).



# Types de données

Il existe quelques types de données intégrés dans Python. Nous allons dans cette partie évoquer les chaînes de caractères, les valeurs numériques, les bouléens (`TRUE`/`FALSE`), la valeur `null` et les dates et temps.


## Chaînes de caractères


Une chaîne de caractères, ou *string* en anglais, est une collection de caractères comme des lettres, des nombres, des espaces, des signes de ponctuation, etc.

Les chaînes de caractères sont repérées à l'aide de guillemets simples, doubles, ou triples.

Voici un exemple :


```python
x = "Hello World"
```

Pour afficher dans la console le contenu de notre variable `x` contenant la chaîne de caractères, on fait appel à la fonction `print()` :


```python
print(x)
```

```
## Hello World
```


Comme indiqué juste avant, des guillemets simples peuvent être utilisés pour créer une chaîne de caractères :

```python
y = 'How are you?'
print(y)
```

```
## How are you?
```


Pour faire figurer des apostrophes dans une chaîne de caractères créée à l'aide de guillemets simples, il est nécessaire d'utiliser un caracrère d'échappement : une barre oblique inversée (`\`) :

```python
z = 'I\'m fine'
print(z)
```

```
## I'm fine
```

On peut noter que si la chaîne de caractères est créée à l'aide de guillemets doubles, il n'est pas nécessaire d'avoir recours au caractère d'échappement :

```python
z = "I'm \"fine\""
print(z)
```

```
## I'm "fine"
```


Pour indiquer un retour à la ligne, on utilise la chaîne `\n` :


```python
x = "Hello, \nWorld"
print(x)
```

```
## Hello, 
## World
```

Dans le cas de chaînes de caractères sur **plusieurs lignes**, le fait d'utiliser des guillemets simples ou doubles renverra une erreur (*EOL while scanning trial literal*, *i.e.*, détection d'une erreur de syntaxe, Python s'attendait à quelque chose d'autre à la fin de la ligne). Pour écrire une chaîne de caractères sur plusieurs lignes, Python propose d'utiliser trois fois des guillemets (simples ou doubles) en début et fin de chaîne :

```python
x = """Hello,
World"""
print(x)
```

```
## Hello,
## World
```

\BeginKnitrBlock{remarque}<div class="remarque">Le caractère `\` (barre oblique inversée, ou *backslash*) est le caractère d'échappement. Il permet d'afficher certains caractères, comme les guillemets dans une chaîne elle-même définie à l'aide de guillemets, ou bien les caractères de contrôle, comme la tabulation, le saut de ligne, etc. Voici quelques exemples courants :

| Code  | Description | Code | Description |
| :---: |:-----------:| :---:|:-----------:|
| `\n` | Nouvelle ligne | `\r` | Retour à la ligne |
| `\t` | Tabulation | `\b` | Retour arrière |
| `\` | Barre oblique inversée | `\'` | Apostrophe |
| `\"` | Apostrophe double | `` \` `` | Accent grave |
</div>\EndKnitrBlock{remarque}


Pour récupérer la **longueur d'une chaîne de caractères**, Python propose la fonction `len()` :

```python
x = "Hello World !"
print(len(x))
```

```
## 13
```

```python
print(x, len(x))
```

```
## Hello World ! 13
```



### Concaténation de chaînes {#type-chaines-concatenation}

Pour concaténer des chaînes de caractères, c'est-à-dire les mettre bout à bout, Python propose d'utiliser l'opérateur `+` :


```python
print("Hello" + " World")
```

```
## Hello World
```

L'opérateur `*` permet quant à lui de répéter plusieurs fois une chaîne :


```python
print( 3 * "Go Habs Go! " + "Woo Hoo!")
```

```
## Go Habs Go! Go Habs Go! Go Habs Go! Woo Hoo!
```

Lorsque deux littéraux de chaînes sont côte à côte, Python les concatène :

```python
x = ('You shall ' 'not ' "pass!")
print(x)
```

```
## You shall not pass!
```



Il est également possible d'**ajouter à une chaîne de caractères le contenu d'une variable**, à l'aide du marqueur `%s` :

```python
x = "J'aime coder en %s"
langage_1 = "R"
langage_2 = "Python"
preference_1 = x % langage_1
print(preference_1)
```

```
## J'aime coder en R
```

```python
preference_2 = x % langage_2
print(preference_2)
```

```
## J'aime coder en Python
```

Il est tout à fait possible d'ajouter **plus d'un contenu de variable** dans une chaîne de caractères, toujours avec le marqueur `%s` :

```python
x = "J'aime coder en %s et en %s"
preference_3 = x % (langage_1, langage_2)
print(preference_3)
```

```
## J'aime coder en R et en Python
```


### Indexation et extraction


Les chaînes de caractères peuvent être indexées. Attention, **l'indice du premier caractère commence à 0*.

Pour obtenir le ie caractère d'une chaîne, on utilise des crochets. La syntaxe est la suivante :

```python
x[i-1]
```

Par exemple, pour afficher le premier caractère, puis le cinquième de la chaîne `Hello` :


```python
x = "Hello"
print(x[0])
```

```
## H
```

```python
print(x[4])
```

```
## o
```

L'extraction peut s'effectuer en partant par la fin de la chaîne, en faisant précéder la veleur de l'indice par le signe moins (`-`).

Par exemple, pour afficher l'avant-dernier caractère de notre chaîne `x` :

```python
print(x[-2])
```

```
## l
```


L'extraction d'une sous-chaîne en précisant sa position de début et de fin (implicitement ou non) s'effectue avec les crochets également. Il suffit de préciser les deux valeurs d'indices : `[debut:fin]`.


```python
x = "You shall not pass!"

# Du quatrième caractère (non inclus) au neuvième (inclus)
print(x[4:9])
```

```
## shall
```

Lorsque l'on ne précise pas la première valeur, le début de la chaîne est pris par défaut ; lorsque le second n'est pas précisé, la fin de la chaîne est prise par défaut.



```python
# Du 4e caractère (non inclus) à la fin de la chaîne
print(x[4:])
# Du début de la chaîne à l'avant dernier caractère (inclus)
print(x[:-1])
# Du 3e caractère avant la fin (inclus) jusqu'à la fin
print(x[-5:])
```


```
## shall not pass!
```

```
## You shall not pass
```

```
## pass!
```


Il est possible de rajouter un troisième indice dans les crochets : **le pas**.

```python
# Du 4e caractère (non inclus), jusqu'à la fin de la chaîne,
# par pas de 3.
print(x[4::3])
```

```
## sln s
```


Pour obtenir la chaîne en dans le sens opposé :

```python
print(x[::-1])
```

```
## !ssap ton llahs uoY
```


### Méthodes disponibles avec les chaînes de caractères


De nombreuses méthodes sont disponibles pour les chaînes de caractères. En ajoutant un point (`.`) après le nom d'un objet désignant une chaîne de caractères puis en appuyant sur la touche de tabulation, les méthodes disponibles s'affichent dans un menu déroulant.


Par exemple, la méthode `count()` permet de compter le nombre d'occurrences d'un motif dans la chaîne. Pour compter le nombre d'occurrence de `in` dans la chaîne suivante :

```python
x = "le train de tes injures roule sur le rail de mon indifférence"
print(x.count("in"))
```

```
## 3
```


\BeginKnitrBlock{remarque}<div class="remarque">Une fois l'appel à méthode écrit, en plaçant le curseur à la fin de la ligne et en appuyant sur les touches `Shift` et `Tabulation`, on peut afficher des explications.</div>\EndKnitrBlock{remarque}


#### Conversion en majuscules ou en minuscules


Les méthodes `lower()` et `upper()` permettent de passer une chaîne de caractères en caractères minuscules et majuscules, respectivement.

```python
x = "le train de tes injures roule sur le rail de mon indifférence"
print(x.lower())
print(x.upper())
```


```
## le train de tes injures roule sur le rail de mon indifférence
```

```
## LE TRAIN DE TES INJURES ROULE SUR LE RAIL DE MON INDIFFÉRENCE
```

#### Recherche de chaînes de caractères


Quand on souhaite **retrouver un motif** dans une chaîne de caractères, on peut utiliser la méthode `find()`. On fournit en paramètres un motif à rechercher. La méthode `find()` retourne le plus petit indice dans la chaîne où le motif est trouvé. Si le motif n'est pas retrouvé, la valeur retournée est `-1`.



```python
print(x.find("in"))
print(x.find("bonjour"))
```


```
## 6
```

```
## -1
```


Il est possible d'ajouter en option une indication permettant de **limiter la recherche sur une sous-chaîne**, en précisant l'indice de début et de fin :

```python
print(x.find("in", 7, 20))
```

```
## 16
```

Note : on peut omettre l'indice de fin ; en ce cas, la fin de la chaîne est utilisée :

```python
print(x.find("in", 20))
```

```
## 49
```

\BeginKnitrBlock{remarque}<div class="remarque">Si on ne désire pas connaître la position de la sous-chaîne, mais uniquement sa présence ou son absence, on peut utiliser l'opérateur `in` : `print("train" in x)`</div>\EndKnitrBlock{remarque}

Pour effectuer une recherche **sans prêter attention à la casse**, on peut utiliser la méthode `capitalize()` :


```python
x = "Mademoiselle Deray, il est interdit de manger de la choucroute ici."
print(x.find("deray"))
```

```
## -1
```

```python
print(x.capitalize().find("deray"))
```

```
## 13
```


#### Découpage en sous-chaînes

Pour **découper une chaîne de caractères en sous-chaînes**, en fonction d'un motif servant à la délimitation des sous-chaînes (par exemple une virgule, ou une espace), on utilise la méthode `split()` :

```python
print(x.split(" "))
```

```
## ['Mademoiselle', 'Deray,', 'il', 'est', 'interdit', 'de', 'manger', 'de', 'la', 'choucroute', 'ici.']
```

En indiquant en paramètres une valeur numérique, on peut limiter le nombre de sous-chaînes retournées :

```python
# Le nombre de sous-chaînes maximum sera de 3
print(x.split(" ", 3))
```

```
## ['Mademoiselle', 'Deray,', 'il', 'est interdit de manger de la choucroute ici.']
```

La méthode `splitlines()` permet également de séparer une chaîne de caractères en fonction d'un motif, ce motif étant un caractère de fin de ligne, comme un saut de ligne ou un retour chariot par exemple.


```python
x = '''"Luke, je suis ton pere !
- Non... ce n'est pas vrai ! C'est impossible !
- Lis dans ton coeur, tu sauras que c'est vrai.
- Noooooooon ! Noooon !"'''
print(x.splitlines())
```

```
## ['"Luke, je suis ton pere !', "- Non... ce n'est pas vrai ! C'est impossible !", "- Lis dans ton coeur, tu sauras que c'est vrai.", '- Noooooooon ! Noooon !"']
```



#### Nettoyage, complétion

Pour retirer des caractères blancs (*e.g.*, des espaces, sauts de ligne, quadratins, etc.) présents en début et fin de chaîne, on peut utiliser la méthode `strip()`, ce qui est parfois très utile pour nettoyer des chaînes.


```python
x = "\n\n    Pardon, du sucre ?     \n  \n"
print(x.strip())
```

```
## Pardon, du sucre ?
```

On peut préciser en paramètre quels caractères retirer en début et fin de chaîne :


```python
x = "www.egallic.fr"
print(x.strip("wrf."))
```

```
## egallic
```


Parfois, il est nécessaire de s'assurer d'obtenir une **chaîne d'une longueur donnée** (lorsque l'on doit fournir un fichier avec des largeurs fixes pour chaque colonne par exemple). La méthode `rjust()` est alors d'un grand secours. En lui renseignant une longueur de chaîne et un caractère de remplissage, elle retourne la chaîne de caractères avec une complétion éventuelle (si la longueur de la chaîne retournée n'est pas assez longue au regard de la valeur demandée), en répétant le caractère de remplissage autant de fois que nécessaire.

Par exemple, pour avoir une coordonnée de longitude, stockée dans une chaîne de caractères de longueur 7, en rajoutant des espaces si nécessaire :

```python
longitude = "48.11"
print(x.rjust(7," "))
```

```
## www.egallic.fr
```






#### Remplacements

La méthode `replace()` permet d'effectuer des **remplacements de motifs** dans une chaîne de caractères.


```python
x = "Criquette ! Vous, ici ? Dans votre propre salle de bain ? Quelle surprise !"
print(x.replace("Criquette", "Ridge"))
```

```
## Ridge ! Vous, ici ? Dans votre propre salle de bain ? Quelle surprise !
```

Cette méthode est très pratique pour **retirer des espaces** par exemple :


```python
print(x.replace(" ", ""))
```

```
## Criquette!Vous,ici?Dansvotrepropresalledebain?Quellesurprise!
```




Voici un tableau répertoriant quelques méthodes disponibles ([liste exhaustive dans la documentation](https://docs.python.org/3/library/stdtypes.html#string-methods)) :

| Méthode | Description |
|-------------:|-------------------------------------------------------------------------------:|
| `capitalize()` | Mise en majuscule du premier caractère et en minuscile du reste |
| `casefold()` | retire les distinctions de casse (utile pour la comparaison de chaînes sans faire attention à la casse) |
| `count()` | Compte le nombre d'occurrence (sans chevauchement) d'un motif |
| `encode()` | Encode une chaîne de caractères dans un encodage spécifique |
| `find()` | Retourne le plus petit indice où une sous-chaîne est trouvée |
| `lower()` | Retourne la chaîne en ayant passé chaque caractère alphabétique en minuscules |
| `replace()` | Remplace un motif par un autre |
| `split()` | Sépare la chaîne en sous-chaînes en fonction d'un motif |
| `title()` | Retourne la chaîne en ayant passé chaque première lettre de mot par une majuscule |
| `upper()` | Retourne la chaîne en ayant passé chaque caractère alphabétique en majuscules |


### Conversion en chaînes de caractères {#conversion-chaines-caracteres}

Lorsque l'on veut concaténer une chaîne de caractères avec un nombre, Python retourne une erreur.

```python
nb_followers = 0
message = "He has " + nb_followers + "followers."
```

```
## TypeError: must be str, not int
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```

```python
print(message)
```

```
## NameError: name 'message' is not defined
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```


Il est alors nécessaire de convertir au préalable l'objet n'étant pas une chaîne en une chaîne de caractères. Pour ce faire, Python propose la fonction `str()` :

```python
message = "He has " + str(nb_followers) + " followers."
print(message)
```

```
## He has 0 followers.
```


### Exercice


\BeginKnitrBlock{exframe}<div class="exframe">1. Créer deux variables nommées `a` et `b` afin qu'elles contiennent respectivement les chaînes de caractères suivantes : `23 à 0` et `C'est la piquette, Jack!`.
2. Afficher le nombre de caractères de `a`, puis de `b`.
3. Concaténer `a` et `b` dans une seule chaîne de caractères, en ajoutant une virgule comme caractère de séparation.
4. Même question en choisissant une séparation permettant un retour à la ligne entre les deux phrases.
5. À l'aide de la méthode appropriée, mettre en majuscules `a` et `b`.
6. À l'aide de la méthode appropriée, mettre en minuscules `a` et `b`.
7. Extraire le mot `la` et `Jack` de la chaîne `b`, en utilisant les indices.
8. Rechercher si la sous-chaîne `piqu` est présente dans `b`, puis faire de même avec la sous-chaîne `mauvais`.
9. Retourner la position (indice) du premier caractère `a` retrouvé dans la chaîne `b`, puis essayer avec le caractère `w`.
10. Remplacer les occurrences du motif `a` par le motif `Z` dans la sous-chaîne `b`.
11. Séparer la chaîne `b` en utilisant la virgule comme séparateur de sous-chaînes.
12. (Bonus) Retirer tous les caractères de ponctuation de la chaîne b, puis utiliser une méthode appropriée pour retirer les caractères blancs en début et fin de chaîne. (Utiliser la librairie `regex`).
</div>\EndKnitrBlock{exframe}



## Valeurs numériques

Il existe quatre catégories de nombres en Python : les entiers, les nombres à virgule flottante et les complèxes.


### Entiers

Les entiers (`ints`), en Python, sont des nombres entiers signés.

\BeginKnitrBlock{remarque}<div class="remarque">On accède au type d'un objet à l'aide de la fonction `type()` en Python.</div>\EndKnitrBlock{remarque}


```python
x = 2
y = -2
print(type(x))
```

```
## <class 'int'>
```

```python
print(type(y))
```

```
## <class 'int'>
```

### Nombre à virgule flottante

Les nombres à virgule flottante (`floats`) représentent les nombres réels. Ils sont écrits à l'aide d'un point permettant de distinguer la partie entière de la partie décimale du nombre.


```python
x = 2.0
y = 48.15162342
print(type(x))
```

```
## <class 'float'>
```

```python
print(type(y))
```

```
## <class 'float'>
```

Il est également possible d'avoir recours aux notations scientifiques, en utilisant `E` ou `e` pour indiquer une puissance de 10. Par exemple, pour écrire $3,2^12$, on procèdera comme suit :

```python
x = 3.2E12
y = 3.2e12
print(x)
```

```
## 3200000000000.0
```

```python
print(y)
```

```
## 3200000000000.0
```

### Nombres complèxes

Python permet nativement de manipuler des nombres complèxes, de la forme $z=a+ib$, où $a$ et $b$ sont des nombres à virgule flottante, et tel que $i^2=(-i)^2=1$. La partie réelle du nombre, $\mathfrak{R}(z)$, est $a$ tandis que sa partie imaginaire, $\mathfrak{I}(z)$, est $b$.

En python, l'unité imaginaire $i$ est dénotée par la lettre `j`.


```python
z = 1+3j
print(z)
```

```
## (1+3j)
```

```python
print(type(z))
```

```
## <class 'complex'>
```


Il est également possible d'utiliser la fonction `complex()`, qui demande deux paramètres (la partie réelle et la partie imaginaire) :

```python
z = complex(1, 3)
print(z)
```

```
## (1+3j)
```

```python
print(type(z))
```

```
## <class 'complex'>
```

Plusieurs méthodes sont disponibles avec les nombres complèxes. Par exemple, pour accéder au conjugué, Python fournit la méthode `conjugate()` :

```python
print(z.conjugate())
```

```
## (1-3j)
```

L'accès à la partie réelle d'un complèxe ou à sa partie imaginaire s'effectue à l'aide des méthodes `real()` et `imag()`, respectivement.

```python
z = complex(1, 3)
print(z.real())
```

```
## TypeError: 'float' object is not callable
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```

```python
print(z.imag())
```

```
## TypeError: 'float' object is not callable
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```

### Conversions

Pour convertir un nombre dans un autre format numérique, Python dispose de quelques fonctions.


#### Conversion en entier

La **conversion d'un nombre ou d'une chaîne de caractères en entier** s'effectue à l'aide de la fonction `int()` :

```python
x = "3"
x_int = int(x)
print(type(x))
```

```
## <class 'str'>
```

On note que la conversion d'un nombre à virgule flottante tronque le nombre pour ne garder que la partie entière :

```python
x = 3.6
x_int = int(x)
print(x_int)
```

```
## 3
```


#### Conversion en nombre à virgule flottante

Pour **convertir un nombre ou une chaîne de caractères en nombre à virgule flottante** (si possible), Python propose d'utiliser la fonction `float()`.


```python
x = "3.6"
x_float = float(x)
print(type(x_float))
```

```
## <class 'float'>
```

Avec un entier à l'origine :


```python
x = 3
x_float = float(x)
print(x_float)
```

```
## 3.0
```

#### Conversion en complèxe


La conversion d'un nombre ou d'une chaîne de caractères en nombre complèxe s'effectue avec la fonction `complex()` :


```python
x = "2"
x_complex = complex(x)
print(x_complex)
```

```
## (2+0j)
```

Avec un *float* :


```python
x = 2.4
x_complex = complex(x)
print(x_complex)
```

```
## (2.4+0j)
```


## Booléens

Les données de type logique peuvent prendre deux valeurs : `True` ou `False`. Elles répondent
à une condition logique. Il faut faire attention à bien respecter la casse.


```python
x = True
y = False
print(x, y)
```

```
## True False
```


`True` peut être converti automatiquement en 1 ;  `False` en 0. Cela peut s'avérer très pratique, pour faire des comptages de valeurs vraies ou fausses dans les colonnes d'un tableau de données, par exemple.


```python
res = True + True + False + True*True
print(res)
```

```
## 3
```


## Objet vide

L'objet vide, communément appelé `null`, possède un équivalent en Python : `None`. Pour l'assigner à une variable, il faut faire attention à la casse :

```python
x = None
print(x)
```

```
## None
```

```python
print(type(x))
```

```
## <class 'NoneType'>
```


L'objet `None` est une variable neutre, au comportement "null".

Pour tester si un objet est l'objet `None`, on procède comme suit (le résultat est un booléen) :

```python
x = 1
y = None
print(x is None)
```

```
## False
```

```python
print(y is None)
```

```
## True
```




## Dates et temps

Il existe plusieurs moduels pour gérer les dates et le temps en Python. Nous allons explorer une partie du module `datetime`.

### Module datetime

Python possède un module appelé `datetime` qui offre la possibilité de manipuler des dates et des durées (*dates* et *times*).

Il existe plusieurs types d'objets désignant des dates :

- `date` : une date suivant le calendrier grégorien, renseignant l'année, le mois et le jour ;
- `time` : un temp donné, sans prise en compte d'un jour particulier, renseignant l'heure, la minute, la seconde (possiblement la microseconde et le fuseau horaire également).
- `datetime` : une date combinant `date` et `time` ;
- `timedelta` : une durée entre deux objets de type `dates`, `time` ou `datetime` ;
- `tzinfo` : un type de base abstraite, renseignant au sujet des fuseaux horaires ;
- `timezone` : un type utilisant le type `tzinfo` comme un décalage fixe par rapport à l'UTC.


#### Date {#type-date}

Les objets de type `date` désignent des dates du calendrier grégorien, pour lesquelles sont mentionnées les caractéristiques suivantes : l'année, le mois et le jour.

Pour créer un objet `date`, la syntaxe est la suivante :

```python
date(year, month, day)
```

Par exemple, pour créer la date renseignant le 23 avril 2013 :

```python
from datetime import date
debut = date(year = 2013, month = 4, day = 23)
print(debut)
```

```
## 2013-04-23
```

```python
print(type(debut))
```

```
## <class 'datetime.date'>
```

\BeginKnitrBlock{remarque}<div class="remarque">Il n'est pas obligatoire de préciser le nom des paramètres dans l'appel à la fonction `date`. L'ordre à respecter devra toutefois être le suivant : année, mois, jour.</div>\EndKnitrBlock{remarque}

On peut ensuite accéder aux attributs de la date créée (ce sont des entiers) :


```python
print(debut.year) # Extraire l'année
```

```
## 2013
```

```python
print(debut.month) # Extraire le mois
```

```
## 4
```

```python
print(debut.day) # Extraire le jour
```

```
## 23
```


Les objets du type `date` possèdent quelques méthodes. Nous allons passer en revue quelques-unes d'entre-elles.

##### `ctime()`

La méthode `ctime()` retourne la date sous forme d'une chaîne de caractères.

```python
debut.ctime()
```

##### `weekday()`

La méthode `weekday()` retourne la position du jour de la semaine (lundi valant 0, dimanche 6)

```python
debut.weekday()
```

\BeginKnitrBlock{remarque}<div class="remarque">Cette méthode peut être très pratique lors d'une analyse des données, pour explorer les aspects de saisonnalité hebdomadaire.</div>\EndKnitrBlock{remarque}

##### `isoweekday()`

Dans la même veine que `weekday()`, la méthode `isoweekday()` retourne la position du jour de la semaine, en attribuant cette fois la valeur 1 au lundi et 7 au dimanche.

```python
debut.isoweekday()
```

##### `toordinal()`

La méthode `toordinal()` retourne le numéro du jour, en prenant comme référence la valeur 1 pour le premier jour de l'an 1.


```python
debut.toordinal()
```

##### `isoformat()`

La méthode `isoformat()` retourne la date en [numérotation ISO](https://fr.wikipedia.org/wiki/Num%C3%A9rotation_ISO_des_semaines), sous forme d'une chaîne de caractères.

```python
debut.isoformat()
```


##### `isocalendar()`

La méthode `isocalendar()` retourne un nuplet (c.f. Section\ \@ref(n-uplets-tuples)) comprenant trois éléments : l'année, le numéro de la semaine et le jour de la semaine (les trois en numérotation ISO).


```python
debut.isocalendar()
```


##### `replace()`

La méthode `replace()` retourne la date après avoir effectué une modification


```python
x = debut.replace(year=2014)
y = debut.replace(month=5)
z = debut.replace(day=24)
print(x, y, z)
```

```
## 2014-04-23 2013-05-23 2013-04-24
```

Cela n'a pas d'incidence sur l'objet d'origine :

```python
print(debut)
```

```
## 2013-04-23
```

Il est possible de modifier plusieurs éléments en même temps :

```python
x = debut.replace(day=24, month=5)
print(x)
```

```
## 2013-05-24
```


##### `strftime()`

La méthode `strftime()` retourne, sous la forme d'une chaîne de caractères, une représentation de la date, selon un masque utilisé.

Par exemple, pour que la date soit représentée sous la forme `DD-MM-YYYY` (jour sur deux chiffres, mois sur deux chiffres et année sur 4) :


```python
print(debut.strftime("%d-%m-%Y"))
```

```
## 23-04-2013
```

Dans l'exemple précédent, on note deux choses : la présence de directives de formatage (qui commencent par le symbole de pourcentage) et des caractères autres (ici, les tirets). On peut noter que les caractères peuvent être remplacés par d'autres, il s'agit ici d'un choix pour représenter la date en séparant ses éléments par ddes tirets. Il est tout à fait possible d'adopter une autre écriture, par exemple avec des barres obliques, ou même d'autres chaînes de caractères :

```python
print(debut.strftime("%d/%m/%Y"))
```

```
## 23/04/2013
```

```python
print(debut.strftime("Jour : %d, Mois : %m, Annee : %Y"))
```

```
## Jour : 23, Mois : 04, Annee : 2013
```

Concernant les directives de formatage, elles correspondent aux codes requis par le standard C (c.f. la [documentation de Python](https://docs.python.org/fr/3/library/datetime.html#strftime-strptime-behavior)). En voici quelques-uns :

| Code | Description | Exemple |
| -------: | -----------------------------------------------------: | ------------------: |
| `%a` | Abréviation du jour de la semaine (dépend du lieu) | `Tue` |
| `%A` | Jour de la semaine complet (dépend du lieu) | `Tuesday` |
| `%b` | Abréviation du mois (dépend du lieu) | `Apr` |
| `%B` | Nom du mois complet (dépend du lieu) octobre | `April` |
| `%c`| Date et heure (dépend du lieu) au format %a %e %b %H:%M:%S:%Y | `Tue Apr 23 00:00:00 2013` |
| `%C`| Siècle (00-99) -1 (partie entière de la division de l'année par 100) | `20` |
| `%d`| Jour du mois (01–31) | `23` |
| `%D`| Date au format %m/%d/%y | `04/23/13` |
| `%e`| Jour du mois en nombre décimal (1–31) | `23` |
| `%F`| Date au format %Y-%m-%d | `2013-04-23` |
| `%h`| Même chose que %b | `Apr` |
| `%H`| Heure (00–24) | `00` |
| `%I`| Heure (01–12) | `12` |
| `%j`| Jour de l'année (001–366) | `113` |
| `%m`| Mois (01–12)  | `04` |
| `%M`| Minute (00-59)  | `00` |
| `%n`| Retour à la ligne en output, caractère blanc en input | `\n` |
| `%p`| AM/PM PM | `AM` |
| `%r`| Heure au format 12 AM/PM | `12:00:00 AM` |
| `%R`| Même chose que %H:%M  | `00:00` |
| `%S`| Seconde (00-61)  | `00` |
| `%t`| Tabulation en output, caractère blanc en input | `\t` |
| `%T`| Même chose que %H:%M:%S | `00:00:00` |
| `%u`| Jour de la semaine (1–7), commence le lundi | `2` |
| `%U`| Semaine de l'anné (00–53), dimanche comme début de semaine, et le premier dimanche de l'année définit la semaine | `16` |
| `%V`| Semaine de l'année (00-53). Si la semaine (qui commence un lundi) qui contient le 1 er janvier a quatre jours ou plus dans la nouvelle année, alors elle est considérée comme la semaine 1. Sinon, elle est considérée comme la dernière de l'année précédente, et la semaine suivante est considérée comme semaine 1 (norme ISO 8601) | `17` |
| `%w`| Jour de la semaine (0–6), dimanche étant 0  | `2` |
| `%W`| Semaine de l'année (00–53), le lundi étant le premier jour de la semaine, et typiquement, le premier lundi de l'année définit la semaine 1 (conviention G.B.) | `16` |
| `%x`| Date (dépend du lieu) | `04/23/13` |
| `%X`| Heure (dépend du lieu) | `00:00:00'` |
| `%y`| Année sans le "siècle"" (00–99)  | `13` |
| `%Y`| Année (en input, uniquement de 0 à 9999)  | `2013` |
| `%z`| offset en heures et minutes par rapport au temps UTC  |  |
| `%Z`| Abréviation du fuseau horaire (en output seulement) CEST |  |

Table: (#tab:codes-formatage) Codes de formatages


#### Time {#type-time}


Les objets de type `time` désignent des temps précis sans prise en compte d'un jour particulier. Ils renseignant l'heure, la minute, la seconde (possiblement la microseconde et le fuseau horaire également).

Pour créer un objet `time`, la syntaxe est la suivante :

```python
time(hour, minute, second)
```

Par exemple, pour créer le moment 23:04:59 (vingt-trois heures, quatre minutes et cinquante-neuf secondes) :


```python
from datetime import time
moment = time(hour = 23, minute = 4, second = 59)
print(moment)
```

```
## 23:04:59
```

```python
print(type(moment))
```

```
## <class 'datetime.time'>
```


On peut rajouter des informations sur la microseconde. Sa valeur doit être comprise entre zéro et un million.

```python
moment = time(hour = 23, minute = 4, second = 59, microsecond = 230)
print(moment)
```

```
## 23:04:59.000230
```

```python
print(type(moment))
```

```
## <class 'datetime.time'>
```

On peut ensuite accéder aux attributs de la date créée (ce sont des entiers), parmi lesquels :


```python
print(moment.hour) # Extraire l'heure
```

```
## 23
```

```python
print(moment.minute) # Extraire la minute
```

```
## 4
```

```python
print(moment.second) # Extraire la seconde
```

```
## 59
```

```python
print(moment.microsecond) # Extraire la microseconde
```

```
## 230
```


Les objets du type `time` possèdent quelques méthodes, dont l'utilisation est similaire aux objets de classe `date` (se référer à la Section\ \@ref(type-date)).


#### Datetime



Les objets de type `datetime` combinent les éléments des objets de type `date` et `time`. Ils renseignant le jour dans le calendrier grégorien ainsi que l'heure, la minute, la seconde (possiblement la microseconde et le fuseau horaire).

Pour créer un objet `datetime`, la syntaxe est la suivante :

```python
datetime(year, month, day, hour, minute, second, microsecond)
```


Par exemple, pour créer la date 23-04-2013 à 17:10:00 :


```python
from datetime import datetime
x = datetime(year = 2013, month = 4, day = 23,
  hour = 23, minute = 4, second = 59)
print(x)
```

```
## 2013-04-23 23:04:59
```

```python
print(type(x))
```

```
## <class 'datetime.datetime'>
```

Les objets de type `datetime` disposent des attributs des objets de type `date` (c.f. Section\ \@ref(type-date)) et de type `time` (c.f. Section\ \@ref(type-time)).

Pour ce qui est des méthodes, davantage sont disponibles. Nous allons en commenter certaines.


##### `today()` et `now()`

Les méthodes `today()` et `now()` retournent le `datetime` courant, celui au moment où est évaluée l'instruction :

```python
print(x.today())
```

```
## 2018-10-09 15:56:24.220697
```

```python
print(datetime.today())
```

```
## 2018-10-09 15:56:24.228003
```

La distinction entre les deux réside dans le fuseau horaire. Avec `today()`, l'attribut `tzinfo` est mis à `None`, tandis qu'avec `now()`, l'attribut `tzinfo`, s'il est indiqué, est pris en compte.


##### `timestamp()`

La méthode `timestamp()` retourne, sous forme d'un nombre à virgule flottante, le *timestamp* POSIX correspondant à l'objet de type `datetime`. Le *timestamp* POSIX correspond à l'heure Posix, équivalent au nombre de secondes écoulées depuis le premier janvier 1970, à 00:00:00 UTC.

```python
print(x.timestamp())
```

```
## 1366751099.0
```


##### `date()`

La méthode `date()` retourne un objet de type `date` dont les attributs d'année, de mois et de jour sont identiques à ceux de l'objet :

```python
x_date = x.date()
print(x_date)
```

```
## 2013-04-23
```

```python
print(type(x_date))
```

```
## <class 'datetime.date'>
```


##### `time()`

La méthode `time()` retourne un objet de type `time` dont les attributs d'heure, minute, seconde, microseconde sont identiques à ceux de l'objet :

```python
x_time = x.time()
print(x_time)
```

```
## 23:04:59
```

```python
print(type(x_time))
```

```
## <class 'datetime.time'>
```




#### Timedelta

Les objets de type `timedelta` représentent des durées séparant deux dates ou heures.

Pour créer un objet de type `timedelta`, la syntaxe est la suivante :

```python
timedelta(days, hours, minutes, seconds, microseconds)
```

Il n'est pas obligatoire de fournir une valeur à chaque paramètre. Lorsque qu'un paramètre ne reçoit pas de valeur, celle qui lui est attribuée par défaut est 0.

Par exemple, pour créer un objet indiquant une durée de 1 jour et 30 secondes :

```python
from datetime import timedelta
duree = timedelta(days = 1, seconds = 30)
duree
```


```python
datetime.timedelta(1, 30)
```

On peut accéder ensuite aux attributs (ayant été définis). Par exemple, pour accéder au nombre de jours que représente la durée :


```python
duree.days
```

```python
1
```


La méthode `total_seconds()` permet d'obtenir la durée exprimée en secondes :


```python
duree = timedelta(days = 1, seconds = 30, hours = 20)
duree.total_seconds()
158430.0
```


##### Durée séparant deux objets `date` ou `datetime`

Lorsqu'on soustrait deux objets de type `date`, on obtient le nombre de jours séparant ces deux dates, sous la forme d'un objet de type `timedelta` :

```python
from datetime import timedelta
debut = date(2018, 1, 1)
fin = date(2018, 1, 2)
nb_jours = fin-debut
print(type(nb_jours))
```

```
## <class 'datetime.timedelta'>
```

```python
print(nb_jours)
```

```
## 1 day, 0:00:00
```



Lorsqu'on soustrait deux objets de type `datetime`, on obtient le nombre de jours, secondes (et microsecondes, si renseignées) séparant ces deux dates, sous la forme d'un objet de type `timedelta` :

```python
debut = datetime(2018, 1, 1, 12, 26, 30, 230)
fin = datetime(2018, 1, 2, 11, 14, 31)
duree = fin-debut
print(type(duree))
```

```
## <class 'datetime.timedelta'>
```

```python
print(duree)
```

```
## 22:48:00.999770
```



On peut noter que les durée données prennent en compte les années bissextiles. Regardons d'abord pour une année non-bissextile, le nombre de jours séparant le 28 février du premier mars :

```python
debut = date(2021, 2,28)
fin = date(2021, 3, 1)
duree = fin - debut
duree
```


```python
datetime.timedelta(1)
```

Regardons à présent la même chose, mais dans le cas d'une année bissextile :

```python
debut_biss = date(2020, 2,28)
fin_biss = date(2020, 3, 1)
duree_biss = fin_biss - debut_biss
duree_biss
```


```python
datetime.timedelta(2)
```



Il est également possible d'**ajouter des durées à une date** :

```python
debut = datetime(2018, 12, 31, 23, 59, 59)
print(debut + timedelta(seconds = 1))
```

```
## 2019-01-01 00:00:00
```

### Module `pytz`

Si la gestion des dates revêt une importance particulière, une librairie propose d'aller un peu plus loins, notamment en ce qui concerne la gestion des fuseaux horaires. Cette librarie s'appelle `pytz`. De nombreux exemples sont proposés sur [la page web du projet](https://pypi.org/project/pytz/).

### Exercices

\BeginKnitrBlock{exframe}<div class="exframe">1. En utilisant la fonction appropriée, stocker la date du 29 août 2019 dans un objet que l'on appellera
`d` puis afficher le type de l'objet.
2. À l'aide de la fonction appropriée, afficher la date du jour.
3. Stocker la date suivante dans un objet nommé `d2` : "2019-08-29 20:30:56". Puis, afficher dans la console avec la fonction `print()` les attributs d'année, de minute et de seconde de `d2`.
4. Ajouter 2 jours, 3 heures et 4 minutes à `d2`, et stocker le résultat dans un objet appelé `d3`.
5. Afficher la différence en secondes entre `d3` et `d2`.
6. À partir de l'objet `d2`, afficher sous forme de chaîne de caractères la date de `d2` de manière à ce qu'elle respecte la syntaxe suivante : "Mois Jour, Année", avec "Mois" le nom du mois (August), "Jour" le numéro du jour sur deux chiffres (29) et "Année" l'année de la date (2019).
</div>\EndKnitrBlock{exframe}


# Structures

Python dispose de plusieurs structures différentes intégrées de base. Nous allons aborder dans cette partie quelques unes d'entre-elles : les listes, les N-uplet (ou *tuples*), les ensembles et les dictionnaires.


## Listes {#structures-listes}

Une des structures les plus flexibles en Python est la liste. Il s'agit d'un regroupement de valeurs. La création d'une liste s'effectue en écrivant les valeurs en les séparant par une virgule et en entourant l'ensemble par des crochets (`[` et `]`).


```python
x = ["Pascaline", "Gauthier", "Xuan", "Jimmy"]
print(x)
```

```
## ['Pascaline', 'Gauthier', 'Xuan', 'Jimmy']
```


Le contenu d'une liste n'est pas forcément du texte :


```python
y = [1, 2, 3, 4, 5]
print(y)
```

```
## [1, 2, 3, 4, 5]
```

Il est même possible de faire figurer des éléments de type différent dans une liste :

```python
z = ["Piketty", "Thomas", 1971]
print(z)
```

```
## ['Piketty', 'Thomas', 1971]
```

Une liste peut contenir une autre liste :

```python
tweets = ["aaa", "bbb"]
followers = ["Anne", "Bob", "Irma", "John"]
compte = [tweets, followers]
print(compte)
```

```
## [['aaa', 'bbb'], ['Anne', 'Bob', 'Irma', 'John']]
```



### Extraction des éléments {#structure-liste-extraction}

L'accès aux éléments se fait grace à son indexation (attention, l'indice du premier élément est 0) :

```python
print(x[0]) # Le premier élément de x
```

```
## Pascaline
```

```python
print(x[1]) # Le second élément de x
```

```
## Gauthier
```

L'accès à un élément peut aussi se faire en parant de la fin, en faisant figurer le signe moins (`-`) devant l'indice :
L'accès aux éléments se fait grace à son indexation (attention, l'indice du premier élément est 0) :

```python
print(x[-1]) # Le dernier élément de x
```

```
## Jimmy
```

```python
print(x[-2]) # L'avant dernier élément de x
```

```
## Xuan
```

Le découpage d'une liste de manière à obtenir un sous-ensemble de la liste s'effectue avec les deux points (`:`) :


```python
print(x[1:2]) # Les premiers et seconds éléments de x
```

```
## ['Gauthier']
```

```python
print(x[2:]) # Du second (non inclus) à la fin de x
```

```
## ['Xuan', 'Jimmy']
```

```python
print(x[:-2]) # Du premier à l'avant dernier (non inclus)
```

```
## ['Pascaline', 'Gauthier']
```

\BeginKnitrBlock{remarque}<div class="remarque">Le découpage retourne également une liste.</div>\EndKnitrBlock{remarque}


Lors de l'extraction des éléments de la liste à l'aide des crochets, il est possible de rajouter un troisième paramètre, le pas :


```python
print(x[::2]) # Un élément sur deux
```

```
## ['Pascaline', 'Xuan']
```


L'accès à des listes imbriquées s'effectue en utilisant plusieurs fois les crochets :

```python
tweets = ["aaa", "bbb"]
followers = ["Anne", "Bob", "Irma", "John"]
compte = [tweets, followers]
res = compte[1][3] # Le 4e élément du 2e élément de la liste compte
```


Le **nombre d'éléments d'une liste** s'obtient avec la fonction `len()` :

```python
print(len(compte))
```

```
## 2
```

```python
print(len(compte[1]))
```

```
## 4
```


### Modification

Les listes sont mutables, c'est-à-dire que leur contenu peut être modifié une fois l'objet créé.

#### Remplacement

Pour **modifier** un élément dans une liste, on utilise l'indiçage :

```python
x = [1, 3, 5, 6, 9]
x[3] = 7 # Remplacement du 4e élément
print(x)
```

```
## [1, 3, 5, 7, 9]
```

#### Ajout d'éléments

Pour **ajouter des éléments à une liste**, on utilise la méthode `append()` :

```python
x.append(11) # Ajout de la valeur 11 en fin de liste
print(x)
```

```
## [1, 3, 5, 7, 9, 11]
```

Il est aussi possible d'utiliser la méthode `extend()`, pour concaténer des listes :

```python
y = [13, 15]
x.extend(y)
print(x)
```

```
## [1, 3, 5, 7, 9, 11, 13, 15]
```


#### Suppression d'éléments

Pour **retirer un élément d'une liste**, on utilise la méthode `remove()` :

```python
x.remove(3) # Retire le 4e élément
print(x)
```

```
## [1, 5, 7, 9, 11, 13, 15]
```

On peut aussi utiliser la commande `del` :

```python
x = [1, 3, 5, 6, 9]
del x[3] # Retire le 4e élément
print(x)
```

```
## [1, 3, 5, 9]
```


#### Affectations multiples

On peut modifier plusieurs valeurs en même temps :


```python
x = [1, 3, 5, 6, 10]
x[3:5] = [7, 9] # Remplace les 4e et 5e valeurs
print(x)
```

```
## [1, 3, 5, 7, 9]
```

La modification peut agrandir la taille de la liste :

```python
x = [1, 2, 3, 4, 5]
x[2:3] = ['a', 'b', 'c', 'd'] # Remplace la 3e valeur
print(x)
```

```
## [1, 2, 'a', 'b', 'c', 'd', 4, 5]
```


On peut supprimer plusieurs valeurs en même temps :

```python
x = [1, 2, 3, 4, 5]
x[3:5] = [] # Retire les 4e et 5e valeurs
print(x)
```

```
## [1, 2, 3]
```

### Test d'appartenance

En utilisant l'opérateur `in`, on peut tester l'appartenance d'un objet à une liste :


```python
x = [1, 2, 3, 4, 5]
print(1 in x)
```

```
## True
```


### Copie de liste {#copie-de-liste}

Attention, la copie d'une liste n'est pas triviale en Python. Prenons un exemple.

```python
x = [1, 2, 3]
y = x
```

Modifions le premier élément de `y`, et observons le contenu de `y` et de `x` :


```python
y[0] = 0
print(y)
```

```
## [0, 2, 3]
```

```python
print(x)
```

```
## [0, 2, 3]
```


Comme on peut le constater, le fait d'avoir utilisé le signe égal a simplement créé une référence et non pas une copie.

Pour effectuer une copie de liste, plusieurs façons existent. Parmi elles, l'utilisation de la fonction `list()` :

```python
x = [1, 2, 3]
y = list(x)
y[0] = 0
print("x : ", x)
```

```
## x :  [1, 2, 3]
```

```python
print("y : ", y)
```

```
## y :  [0, 2, 3]
```

On peut noter que lorsque l'on fait un découpement, un nouvel objet est créé, pas une référence :


```python
x = [1, 2, 3, 4]
y = x[:2]
y[0] = 0
print("x : ", x)
```

```
## x :  [1, 2, 3, 4]
```

```python
print("y : ", y)
```

```
## y :  [0, 2]
```

### Tri

Pour trier les objets de la liste (sans en créer une nouvelle), Python propose la méthode `sort()` :

```python
x = [2, 1, 4, 3]
x.sort()
print(x)
```

```
## [1, 2, 3, 4]
```

Cela fonctionne également avec des valeurs textuelles, en triant par ordre alphabétique :


```python
x = ["c", "b", "a", "a"]
x.sort()
print(x)
```

```
## ['a', 'a', 'b', 'c']
```

Il est possible de fournir à la méthode `sort()` des paramètres. Parmi ces paramètres, il en est un, `key`, qui permet de fournir une fonction pour effectuer le tri. Cette fonction doit retourner une valeur pour chaque objet de la liste, sur laquelle le tri sera effectué. Par exemple, avec la fonction `len()`, qui, lorsqu'appliquée à du texte, retourne le nombre de caractères  :



```python
x = ["aa", "a", "aaaaa", "aa"]
x.sort(key=len)
print(x)
```

```
## ['a', 'aa', 'aa', 'aaaaa']
```


## N-uplets (Tuples)

Les n-uplets, ou *tuples* sont des séquences d'objets Python.

Pour créer un n-uplet, on liste les valeurs, séparées par des virgules :

```python
x = 1, 4, 9, 16, 25
print(x)
```

```
## (1, 4, 9, 16, 25)
```

On note que les n-uplets sont repérés par une suite de valeurs, entourées dans deux parenthèses.

### Extraction des éléments

Les éléments d'un n-uplet s'extraient de la même manière que ceux des listes (c.f. Section\ \@ref(structure-liste-extraction)).


```python
print(x[0])
```

```
## 1
```

### Modification

Contrairement aux listes, les n-uplets sont **inaltérables** (c'est-à-dire ne pouvant pas être modifés après avoir été créés) :

```python
x[0] = 1
```

```
## TypeError: 'tuple' object does not support item assignment
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```


Il est possible d'**imbriquer des n-uplets** à l'intérieur d'un autre n-uplet. Pour ce faire, on a recours à l'utilisation de parenthèses :

```python
x = ((1, 4, 9, 16), (1, 8, 26, 64))
print(x)
```

```
## ((1, 4, 9, 16), (1, 8, 26, 64))
```


## Ensembles {#structure-ensembles}

Les ensembles (*sets*) sont des collections non ordonnée d'éléments uniques. Les ensembles sont inaltérables, et non indexés.

Pour créer un ensemble, Python fournit la fonction `set()`. On fournit un ou plusieurs éléments constituant l'ensemble, en les séparant par des virgules et en entourant l'ensemble d'accolades (`{}`) :

```python
ensemble = set({"Marseille", "Aix-en-Provence", "Nice", "Rennes"})
print(ensemble)
```

```
## {'Marseille', 'Rennes', 'Aix-en-Provence', 'Nice'}
```

De manière équivalent, on peut ne pas utiliser la fonction `set()` et définir l'ensemble uniquement à l'aide des crochets :

```python
ensemble = {"Marseille", "Aix-en-Provence", "Nice", "Rennes"}
print(ensemble)
```

```
## {'Marseille', 'Rennes', 'Aix-en-Provence', 'Nice'}
```

En revanche, si l'ensemble est vide, Python retourne un erreur si la fonction `set()` n'est pas utilisée :
il est nécessaire d'utiliser la fonction set :

```python
ensemble_vide = {}
type(ensemble_vide)
```

Le type de l'objet que l'on vient de créer n'est pas `set` mais `dict` (c.f. Section\ \@ref(type-dict)). Aussi, pour créer l'ensemble vide, on utilise `set()` :


```python
ensemble_vide = set()
type(ensemble_vide)
```


Lors de la création, s'il existe des doublons dans les valeurs fournies, ils seront supprimés pour ne garder qu'une seule valeur :


```python
ensemble = set({"Marseille", "Aix-en-Provence", "Nice", "Marseille", "Rennes"})
print(ensemble)
```

```
## {'Marseille', 'Rennes', 'Aix-en-Provence', 'Nice'}
```

La longueur d'un ensemble s'obtient à l'aide de la fonction `len()` :

```python
print(len(ensemble))
```

```
## 4
```

### Modifications

#### Ajout

Pour ajouter un élément à un ensemble, Python offre la méthode `add()` :

```python
ensemble.add("Toulon")
print(ensemble)
```

```
## {'Marseille', 'Aix-en-Provence', 'Nice', 'Toulon', 'Rennes'}
```

Si l'élément est déjà présent, il ne sera pas ajouté :

```python
ensemble.add("Toulon")
print(ensemble)
```

```
## {'Marseille', 'Aix-en-Provence', 'Nice', 'Toulon', 'Rennes'}
```


#### Suppression

Pour supprimer une valeur d'un ensemble, Python propose la méthode `remove()` :

```python
ensemble.remove("Toulon")
print(ensemble)
```

```
## {'Marseille', 'Aix-en-Provence', 'Nice', 'Rennes'}
```

Si la valeur n'est pas présente dans l'ensemble, Python retourne un message d'erreur :

```python
ensemble.remove("Toulon")
```

```
## KeyError: 'Toulon'
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```

```python
print(ensemble)
```

```
## {'Marseille', 'Aix-en-Provence', 'Nice', 'Rennes'}
```

### Test d'appartenance

Un des intérêts des ensembles est la recherche rapide de présence ou absence de valeurs (plus rapide que dans une liste). Comme pour les listes, les tests d'appartenance s'effectuent à l'aide de l'opérateur `in` :

```python
print("Marseille" in ensemble)
```

```
## True
```

```python
print("Paris" in ensemble)
```

```
## False
```


### Copie d'ensemble 


Pour copier un ensemble, comme pour les listes (c.f. Section\ \@ref(copie-de-liste)), il ne faut pas utiliser le signe d'égalité. La copie d'un ensemble se fait à l'aide de la méthode `copy()` :

```python
ensemble = set({"Marseille", "Aix-en-Provence", "Nice"})
y = ensemble.copy()
y.add("Toulon")
print("y : ", y)
```

```
## y :  {'Marseille', 'Toulon', 'Aix-en-Provence', 'Nice'}
```

```python
print("ensemble : ", ensemble)
```

```
## ensemble :  {'Marseille', 'Aix-en-Provence', 'Nice'}
```


### Conversion en liste

Un des intérêts des ensembles est est qu'ils contiennent des éléments uniques. Aussi, lorsque l'on souhaite obtenir les éléments distincts d'une liste, il est possible de la convertir en ensemble (avec la fonction `set()`), puis de convertir l'ensemble en liste (avec la fonction `list()`) :

```python
ma_liste = ["Marseille", "Aix-en-Provence", "Marseille", "Marseille"]
print(ma_liste)
```

```
## ['Marseille', 'Aix-en-Provence', 'Marseille', 'Marseille']
```

```python
mon_ensemble = set(ma_liste)
print(mon_ensemble)
```

```
## {'Marseille', 'Aix-en-Provence'}
```

```python
ma_nouvelle_liste = list(mon_ensemble)
print(ma_nouvelle_liste)
```

```
## ['Marseille', 'Aix-en-Provence']
```


## Dictionnaires {#type-dict}

Les dictionnaires en Python sont une implémentation d'objets clé-valeurs, les clés étant indexées.

Les clés sont souvent du texte, les valeurs peuvent être de différents types et différentes structures.


Pour créer un dictionnaire, on peut procéder en utilisant des accolades (`{}`). Comme rencontré dans la Section\ \@ref(structure-ensembles), si on évalue le code suivant, on obtient un dictionnaire :

```python
dict_vide = {}
print(type(dict_vide))
```

```
## <class 'dict'>
```

Pour créer un dictionnaire avec des entrée, on peut utiliser les accolades, on sépare chaque entrée par des virgules, et on distingue la clé de la valeur associée par deux points (`:`) :

```python
mon_dict = { "nom": "Kyrie",
  "prenom": "John",
  "naissance": 1992,
  "equipes": ["Cleveland", "Boston"]}
print(mon_dict)
```

```
## {'nom': 'Kyrie', 'prenom': 'John', 'naissance': 1992, 'equipes': ['Cleveland', 'Boston']}
```


Il est aussi possible de créer un dictionnaire à l'aide de la fonction `dict()`, en fournissant une séquence de clés-valeurs :

```python
x = dict([("Julien-Yacine", "Data-scientist"),
  ("Sonia", "Directrice")])
print(x)
```

```
## {'Julien-Yacine': 'Data-scientist', 'Sonia': 'Directrice'}
```


### Extraction des éléments

L'extraction dans les dictionnaires repose sur le même principe que pour les listes et les n-uplets (c.f. Section\ \@ref(#structure-liste-extraction)). Toutefois, l'extraction d'un élément d'un dictionnaire ne se fait pas en fonction de sa position dans le dictionnaire, mais par sa clé :

```python
print(mon_dict["prenom"])
```

```
## John
```

```python
print(mon_dict["equipes"])
```

```
## ['Cleveland', 'Boston']
```


Si l'extraction s'effectue par une clé non présente dans le dictionnaire, une erreur sera retournée :

```python
print(mon_dict["age"])
```

```
## KeyError: 'age'
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```


On peut tester la présence d'une clé avec l'opérateur `in` :

```python
print("prenom" in mon_dict)
```

```
## True
```

```python
print("age" in mon_dict)
```

```
## False
```

L'extraction de valeurs peut aussi se faire à l'aide de la méthode `get()`, qui retourne une valeur `None` si la clé n'est pas présente :

```python
print(mon_dict.get("prenom"))
```

```
## John
```

```python
print(mon_dict.get("age"))
```

```
## None
```



### Clés et valeurs

À l'aide de la méthode `key()`, on peut accéder aux clés du dictionnaire :

```python
les_cles = mon_dict.keys()
print(les_cles)
```

```
## dict_keys(['nom', 'prenom', 'naissance', 'equipes'])
```

```python
print(type(les_cles))
```

```
## <class 'dict_keys'>
```

Il est possible par la suite de transformer cette énumération de clés en liste :

```python
les_cles_liste = list(les_cles)
print(les_cles_liste)
```

```
## ['nom', 'prenom', 'naissance', 'equipes']
```


La méthode `values()` fournit quand à elle les valeurs du dictionnaire :

```python
les_valeurs = mon_dict.values()
print(les_valeurs)
```

```
## dict_values(['Kyrie', 'John', 1992, ['Cleveland', 'Boston']])
```

```python
print(type(les_valeurs))
```

```
## <class 'dict_values'>
```


La méthode `items()` fournit quand à elle les clés et valeurs sous forme de n-uplets :

```python
les_items = mon_dict.items()
print(les_items)
```

```
## dict_items([('nom', 'Kyrie'), ('prenom', 'John'), ('naissance', 1992), ('equipes', ['Cleveland', 'Boston'])])
```

```python
print(type(les_items))
```

```
## <class 'dict_items'>
```


### Recherche d'appartenance

Grâce aux méthodes `keys()`, `values()` et `items()`, il est aisé de rechercher la présence d'objets dans un dictionnaire.


```python
print("age" in les_cles)
```

```
## False
```

```python
print("nom" in les_cles)
```

```
## True
```

```python
print(['Cleveland', 'Boston'] in les_valeurs)
```

```
## True
```


### Modification

#### Remplacement

Pour remplacer la valeur associée à une clé, on peut utiliser les crochets (`[]`) et le signe d'égalité (`=`).

Par exemple, pour remplacer les valeurs associées à la clé `equipes` :

```python
mon_dict["equipes"] = ["Montclair Kimberley Academy",
  "Cleveland Cavaliers", "Boston Celtics"]
print(mon_dict)
```

```
## {'nom': 'Kyrie', 'prenom': 'John', 'naissance': 1992, 'equipes': ['Montclair Kimberley Academy', 'Cleveland Cavaliers', 'Boston Celtics']}
```


#### Ajout d'éléments

L'ajout d'un élément dans un dictionnaire peut s'effectuer avec les crochets (`[]`) et le signe d'égalité (`=`) :


```python
mon_dict["taille_cm"] = 191
print(mon_dict)
```

```
## {'nom': 'Kyrie', 'prenom': 'John', 'naissance': 1992, 'equipes': ['Montclair Kimberley Academy', 'Cleveland Cavaliers', 'Boston Celtics'], 'taille_cm': 191}
```


Pour ajouter le contenu d'un autre dictionnaire à un dictionnaire, Python propose la méthode `update()`.

Créons un second dictionnaire dans un premier temps :

```python
second_dict = {"masse_kg" : 88, "debut_nba" : 2011}
print(second_dict)
```

```
## {'masse_kg': 88, 'debut_nba': 2011}
```

Ajoutons le contenu de ce second dictionnaire au premier :

```python
mon_dict.update(second_dict)
print(mon_dict)
```

```
## {'nom': 'Kyrie', 'prenom': 'John', 'naissance': 1992, 'equipes': ['Montclair Kimberley Academy', 'Cleveland Cavaliers', 'Boston Celtics'], 'taille_cm': 191, 'masse_kg': 88, 'debut_nba': 2011}
```

Si on modifie par la suite le second dictionnaire, cela n'aura pas d'incidence sur le premier :

```python
second_dict["poste"] = "PG"
print(second_dict)
```

```
## {'masse_kg': 88, 'debut_nba': 2011, 'poste': 'PG'}
```

```python
print(mon_dict)
```

```
## {'nom': 'Kyrie', 'prenom': 'John', 'naissance': 1992, 'equipes': ['Montclair Kimberley Academy', 'Cleveland Cavaliers', 'Boston Celtics'], 'taille_cm': 191, 'masse_kg': 88, 'debut_nba': 2011}
```



#### Suppression d'éléments


La suppression d'un élément dans un dictionnaire peut s'effectuer de plusieurs manières. Par exemple, avec l'opérateur `del` :

```python
del mon_dict["debut_nba"]
print(mon_dict)
```

```
## {'nom': 'Kyrie', 'prenom': 'John', 'naissance': 1992, 'equipes': ['Montclair Kimberley Academy', 'Cleveland Cavaliers', 'Boston Celtics'], 'taille_cm': 191, 'masse_kg': 88}
```

Il est également possible d'utiliser la méthode `pop()` :


```python
res = mon_dict.pop("masse_kg")
print(mon_dict)
```

```
## {'nom': 'Kyrie', 'prenom': 'John', 'naissance': 1992, 'equipes': ['Montclair Kimberley Academy', 'Cleveland Cavaliers', 'Boston Celtics'], 'taille_cm': 191}
```

Dans l'instruction précédente, nous avons ajouté une assignation du résultat de l'appliation de la méthode `pop()` à une variable nommée `res`. Comme on peut le constater, la méthode `pop()`, en plus d'avoir supprimé la clé, a retourné la valeur associée :

```python
print(res)
```

```
## 88
```

### Copie de dictionnaire


Pour copier un dictionnaire, et non créer une référence (ce qui est le cas si on utilise le signe d'égalité), Python fournit comme pour les ensembles, une méthode `copy()` :


```python
d = {"Marseille": 13, "Rennes" : 35}
d2 = d.copy()
d2["Paris"] = 75
print("d: ", d)
```

```
## d:  {'Marseille': 13, 'Rennes': 35}
```

```python
print("d2: ", d2)
```

```
## d2:  {'Marseille': 13, 'Rennes': 35, 'Paris': 75}
```

### Exercice

\BeginKnitrBlock{exframe}<div class="exframe">1. Créer un dictionnaire nommé `photo`, comprenant les couples clés-valeurs suivants :
  1. clé : `id`, valeur : `1`,
  2. clé : `description`, valeur : `Une photo du Vieux-port de Marseille`,
  3. clé : `loc`, valeur : une liste dans laquelle sont données les coordonnées suivantes `5.3772133`, `43.302424`.
2.Ajouter le couple de clé-valeur suivant au dictionnaire `photo` : clé : `utilisateur`, valeur : `bob`.
3. Rechercher s'il existe une entrée dont la clé vaut `description` dans le dictionnaire `photo`. Si tel est le cas, afficher l'entrée correspondante (clé et valeur).
4. Supprimer l'entrée dans `photo` dont la clé vaut `utilisateur`.
5. Modifier la valeur de l'entrée `loc` dans le dictionnaire `photo`, pour proposer une nouvelle liste, dont les coordonnées sont les suivantes : `5.3692712` et `43.2949627`.
</div>\EndKnitrBlock{exframe}


# Opérateurs

Python comprend différents opérateurs, permettant d'effectuer des opérations entre les opérandes, c'est-à-dire entre des variables, des littéraux ou encore des expressions.

## Opérateurs arithmétiques {#operateurs-arithmetiques}

Les opérateurs arithmétiques de base sont intégrés dans Python.

Nous avons déjà utilisé dans les chapitres précédents certains d'entre eux, pour effectuer des opérations sur les entiers ou les nombres à virgule flotante (addition, soustraction, etc.). Faisons un tour rapide des opérateurs arithmétiques les plus courants permettant de réaliser des opérations sur des nombres.

### Addition

On effectue une addition entre deux nombres à l'aide du symbole `+` :


```python
print(1+1) # Addition
```

```
## 2
```


### Soustraction

On effectue une soustraction entre deux nombres à l'aide du symbole `-` :


```python
print(1+1) # Soustraction
```

```
## 2
```


### Multiplication

On effectue une multiplication entre deux nombres à l'aide du symbole `*` :


```python
print(2*2) # Multiplication
```

```
## 4
```


### Division

On effectue une division (réelle) entre deux nombres à l'aide du symbole `/` :


```python
print(3/2) # Division
```

```
## 1.5
```

Pour effectuer une division entière, on double la barre oblique :

```python
print(3//2) # Division entière
```

```
## 1
```

### Modulo

Le modulo (reste de la division euclidienne) s'obtient à l'aide du symbole `%` :


```python
print(12%10) # Modulo
```

```
## 2
```

### Puissance

Pour élever un nombre à une puissance données, on utilise deux étoiles (`**`) :

```python
print(2**3) # 2 élevé à la puissance 3
```

```
## 8
```


### Ordre

L'ordre des opérations suit la règle PEMDAS (*Parentheses*, *Exponents*, *Multiplication and Division*, *Addition and Subtraction*).

Par exemple, l'instruction suivante effectue d'abord le calcul $2\times 2$, puis ajoute $1$ :


```python
print(2*2+1) 
```

```
## 5
```


L'instruction suivante, grâce aux parenthèses, effectue d'abord le calcul $2+1$, puis la multiplication du résultat avec $2$ :

```python
print(2*(2+1)) 
```

```
## 6
```


### Opérateurs mathématiques sur des chaînes de caractères

Certains opérateurs mathématiques présentés dans la Section\ \@ref(operateurs-arithmetiques) peuvent-être appliquées à des chaînes de caractères.


Lorsque l'on utilise le symbole `+` entre deux chaînes de caractères, Python concatène ces deux chaînes (cf. Section\ \@ref(type-chaines-concatenation)) :

```python
a = "euro"
b = "dollar"
print(a+b)
```

```
## eurodollar
```


Lorsqu'on "multiplie" une chaîne par un scalaire $n$, Python répète la chaîne le nombre $n$ fois :

```python
2*a
```

### Opérateurs mathématiques sur des listes ou des n-uplets

Certains opérateurs mathématiques peuvent également être appliquées à des listes.

Lorsque l'on utilise le symble `+` entre deux listes, Python les concatène en une seule :

```python
l_1 = [1, "pomme", 5, 7]
l_2 = [9, 11]
print(l_1 + l_2)
```

```
## [1, 'pomme', 5, 7, 9, 11]
```

Idem avec des n-uplets =

```python
t_1 = (1, "pomme", 5, 7)
t_2 = (9, 11)
print(t_1 + t_2)
```

```
## (1, 'pomme', 5, 7, 9, 11)
```

En "multipliant" une liste par un scalaire $n$, Python répète $n$ fois cette liste :

```python
print(3*l_1)
```

```
## [1, 'pomme', 5, 7, 1, 'pomme', 5, 7, 1, 'pomme', 5, 7]
```

Idem avec des n-uplets :

```python
print(3*t_1)
```

```
## (1, 'pomme', 5, 7, 1, 'pomme', 5, 7, 1, 'pomme', 5, 7)
```

## Opérateurs de comparaison {#operateurs-comparaison}


Les opérateurs de comparaisons permettent de comparer entre eux des objets de tous les types de base. Le résultat d'un test de comparaison produit des valeurs booléennes.

| Opérateur | Opérateur en Python | Description |
| --------: | --------: | --------------------------------------: |
| $=$ | `==` |  Égal à |
| $\ne$ | `!=` (ou `<>`) |  Différent de |
| $>$ | `>` |  Supérieur à |
| $\geq$ | `>=` | & Supérieur ou égal à |
| $<$ | `<`  |Inférieur à |
| $\leq$ | `<=` | Inférieur ou égal à |
| $\in$ | `in` | Dans  |
| $\notin$ | `not in` | Exclu  |

Table: (#tab:operateurs-comparaison) Opérateurs de comparaison

### Égalité, inégalité

Pour tester l'égalité de contenu entre deux objets :

```python
a = "Hello"
b = "World"
c = "World"

print(a == c)
```

```
## False
```

```python
print(b == c)
```

```
## True
```

L'inégalité entre deux objets :

```python
x = [1,2,3]
y = [1,2,3]
z = [1,3,4]

print(x != y)
```

```
## False
```

```python
print(x != z)
```

```
## True
```



### Infériorité et supériorité, stricts ou larges

Pour savoir si un objet est inférieur (strictement ou non) ou inférieur (strictement ou non) à un autre :


```python
x = 1
y = 1
z = 2

print(x < y)
```

```
## False
```

```python
print(x <= y)
```

```
## True
```

```python
print(x > z)
```

```
## False
```

```python
print(x >= z)
```

```
## False
```


On peut également effectuer la comparaison entre deux chaînes de caractères. La comparaison s'effectue en fonction de l'ordre lexicographique :

```python
m_1 = "mange"
m_2 = "manger"
m_3 = "boire"
print(m_1 < m_2) # mange avant manger
```

```
## True
```

```python
print(m_3 > m_1) # boire avant manger
```

```
## False
```


Lorsque l'on compare deux listes entre-elles, Python fonctionne pas à pas. Regardons à travers un exemple comment cette comparaison est effectuée.

Créons deux listes :

```python
x = [1, 3, 5, 7]
y = [9, 11]
```

Python va commencer par comparer les premiers éléments de chaque liste (ici, c'est possible, les deux éléments sont comparables ; dans le cas contraire, une erreur serait retournée) :


```python
print(x < y)
```

```
## True
```

Comme `1<9`, Python retourne `True`.

Changeons `x` pour que le premier élément soit supérieur au premier de `y`

```python
x = [10, 3, 5, 7]
y = [9, 11]
print(x < y)
```

```
## False
```

Cette fois, comme $10>9$, Python retourne `False`.

Changeons à présent le premier élément de `x` pour qu'ils soit égal à celui de `y` :

```python
x = [10, 3, 5, 7]
y = [10, 11]
print(x < y)
```

```
## True
```

Cette fois, Python compare le premier élement de `x` avec celui de `y`, comme les deux sont identiques, les seconds éléments sont comparés. On peut s'en convaincre en évaluant le code suivant :


```python
x = [10, 12, 5, 7]
y = [10, 11]
print(x < y)
```

```
## False
```



### Inclusion et exclusion

Comme rencontré plusieurs fois dans le Chapitre\ \@ref(structures), les tests d'inclusions s'effectuent à l'aide de l'opérateur `in`.


```python
print(3 in [1,2, 3])
```

```
## True
```


Pour tester si un élément est exclu d'une liste, d'un n-uplet, dictionnaire, etc., on utilise `not in` :


```python
print(4 not in [1,2, 3])
```

```
## True
```

```python
print(4 not in [1,2, 3, 4])
```

```
## False
```

Avec un dictionnaire :

```python
dictionnaire = {"nom": "Rockwell", "prenom": "Criquette"}
"age" not in dictionnaire.keys()
```


## Opérateurs logiques

Les opérateurs logiques opèrent sur un ou plusieurs objets de type logique (des booléens).

### Et logique

L'opérateur `and` permet d'effectuer des comparaisons "ET" logiques. On compare deux objets, `x` et `y` (ces objets peuvent résulter d'une comparaison préalable, il suffit juste que tous deux soient des booléens).

Si l'un des deux objets `x` et `y` est vrai, la comparaison "ET" logique retourne vrai :


```python
x = True
y = True
print(x and y)
```

```
## True
```

Si au moins l'un des deux est faux, la comparaison "ET" logique retourne faux :


```python
x = True
y = False

print(x and y)
```

```
## False
```

```python
print(y and y)
```

```
## False
```

Si un des deux objets comparés vaut la valeur vide (`None`), alors la comparaison "ET" logique retourne :

- la valeur `None` si l'autre objet vaut `True` ou `None` ;
- la valeur `False` si l'autre objet vaut `False`

```python
x = True
y = False
z = None
print(x and z)
```

```
## None
```

```python
print(y and z)
```

```
## False
```

```python
print(z and z)
```

```
## None
```



### Ou logique


L'opérateur `or` permet d'effectuer des comparaisons "OU" logiques. À nouveau, on compare deux booléens, `x` et `y`.

Si au moins un des deux objets `x` et `y` est vrai, la comparaison "OU" logique retourne vrai :


```python
x = True
y = False
print(x or y)
```

```
## True
```

Si les deux sont faux, la comparaison "OU" logique retourne faux :


```python
x = False
y = False
print(x or y)
```

```
## False
```

Si l'un des deux objets vaut `None`, la comparaison "OU" logique retourne :

- `True` si l'autre objet vaut `True` ;
- `None` si l'autre objet vaut `False` ou `None`


```python
x = True
y = False
z = None
print(x or z)
```

```
## True
```

```python
print(y or z)
```

```
## None
```

```python
print(z or z)
```

```
## None
```



### Non logique


L'opérateur `not`, lorsqu'appliqué à un booléen, évalue ce dernier à sa valeur opposée :



```python
x = True
y = False
print(not x)
```

```
## False
```

```python
print(not y)
```

```
## True
```


Lorsque l'on utilise l'opérateur `not` sur une valeur vide (`None`), Python retourne `True` :

```python
x = None
not x
```



## Quelques fonctions


Python dispose de nombreuses fonctions utiles pour manipuler les structures et données. Le tableau suivant en répertorie quelques-unes. Certaines nécessitent le chargement de la librairie `math`, d'autres la librairie `statistics`. Nous verrsons d'autres fonctions propres à la librairie `NumPy` au Chapitre\ \@ref(numpy).

| Fonction | Description |
| --------------: | --------------------------------------------: |
| `math.ceil(x)` | Plus petits entier supérieur ou égal à `x` |
| `math.copysign(x, y)` | Valeur absolue de `x` mais avec le signe de `y` |
| `math.floor(x)` | Plus petits entier inférieur ou égal à `x` |
| `math.round(x, ndigits)` | Arrondi de `x` à `ndigits` décimales près |
| `math.fabs(x)` | Valeur absolue de `x` |
| `math.exp(x)` | Exponentielle de `x` |
| `math.log(x)` | Logarithme naturel de `x` (en base e) |
| `math.log(x, b)` | Logarithme en base `b`  de `x` |
| `math.log10(x)` | Logarithme en base 10  de `x` |
| `math.pow(x,y)` | `x` élevé à la puissance `y` |
| `math.sqrt(x)` | Racine carrée de `x` |
| `math.fsum()` | Somme des valeurs de `x` |
| `math.sin(x)` | Sinus de `x` |
| `math.cos(x)` | Cosinus de `x` |
| `math.tan(x)` | Tangente de `x` |
| `math.asin(x)` | Arc-sinus de `x` |
| `math.acos(x)` | Arc-cosinus de `x` |
| `math.atan(x)` | Arc-tangente de `x` |
| `math.sinh(x)` | Sinus hyperbolique de `x` |
| `math.cosh(x)` | Cosinus hyperbolique de `x` |
| `math.tanh(x)` | Tangente hyperbolique de `x` |
| `math.asinh(x)` | Arc-sinus hyperbolique de `x` |
| `math.acosh(x)` | Arc-cosinus hyperbolique de `x` |
| `math.atanh(x)` | Arc-tangente hyperbolique de `x` |
| `math.degree(x)` | Conversion de `x` de radians en degrés |
| `math.radians(x)` | Conversion de `x` de degrés en radians |
| `math.factorial()` | Factorielle de `x` |
| `math.gcd(x, y)` | Plus grand commun diviseur de `x` et `y` |
| `math.isclose(x, y, rel_tol=1e-09, abs_tol=0.0)` | Compare `x` et `y` et retourne s'ils sont proches au reard de la tolérance `rel_tol` (`abs_tol` est la tolérance minimum absolue) |
| `math.isfinite(x)` | Retourne `True` si `x` est soit l'infini, soir `NaN`  |
| `math.isinf(x)` | Retourne `True` si `x` est l'infini, `False` sinon |
| `math.isnan(x)` | Retourne `True` si `x` est `NaN`, `False` sinon |
| `statistics.mean(x)` | Moyenne de x |
| `statistics.median(x)` | Médiane de x |
| `statistics.mode(x)` | Mode de x |
| `statistics.stdev(x)` | Écart-type de x |
| `statistics.variance(x)` | Variance de x |


Table: (#tab:fonctions-numeriques) Quelques fonctions numériques

## Quelques constantes

La librairie `math` propose quelques constantes :

| Fonction | Description |
| -----------: | --------------------------------------------: |
| `math.pi` | Le nombre Pi ($\pi$) |
| `math.e` | La constante $e$  |
| `math.tau` | La constante $\tau$, égale à $2\pi$ |
| `math.inf` | L'infini ($\infty$) |
| `-math.inf` | Moins l'infini ($-\infty$) |
| `math.nan` | Nombre à virgule flotante *not a number* |

Table: (#tab:constantes-base) Quelques constantes intégrées dans Python

## Exercice

\BeginKnitrBlock{exframe}<div class="exframe">1. Calculer le reste de la division euclidienne de 10 par 3.
2. Afficher le plus grand commun diviseur entre 6209 et 4435.
3. Soient deux objets : `a = 18` et `b = -4`. Tester si: 
  
  - `a` est inférieur à `b` strictement,
  - `a` est supérieur ou égal à `b`,
  - `a` est différent de `b`.
4. Soit la liste `x = [1, 1, 2, 3, 5, 8]`. Regarder si :
  
  - `1` est dans `x` ;
  - `0` est dans `x` ;
  - `1` et `0` sont dans `x` ;
  - `1` ou `0` sont dans `x` ;
  - `1` ou `0` n'est pas présent dans `x`.
</div>\EndKnitrBlock{exframe}


# Chargement et sauvegarde de données

Pour explorer des données et/ou réaliser des analyses statistiques ou économétriques, il est important de savoir importer et exporter des données.

Avant toute chose, il convient d'évoquer la notion de répertoire courant (*working directory*). En informatique, le répertroire courant d'un processus désigne un répertoire du système de fichier associé à ce processus.

Lorsqu'on lance Jupyter, une arborescence nous est proposée, et nous navigons à l'interieur de celle-ci pour créer ou ouvrir un *notebook*. Le répertoire contenant le *notebook* est le répertoire courant. Lorsqu'on indiquera à Python d'importer des données (ou d'exporter des objets), l'origine (ou la destination) sera indiquée **relativement** au répertoire courant, à moins d'avoir recours à des chemins absolus (c'est-à-dire un chemin d'accès à partir de la racine `/`).

Si on lance un programme Python depuis un terminal, le répertoire courant est le répertoire dans lequel on se trouve dans le terminal au moment de lancer le programme.

Pour afficher dans Python le répertoire courant, on peut utiliser le code suivant :

```python
import os
cwd = os.getcwd()
print(cwd)
```

```
## /Users/ewengallic/Dropbox/Universite_Aix_Marseille/Magistere_2_Programming_for_big_data/Cours/chapters/python/Python_pour_economistes
```


\BeginKnitrBlock{remarque}<div class="remarque">La fonction `listdir()` de la librairie `os` est très pratique : elle permet de lister tous les documents et répertoires contenus dans le répertoire couant, ou dans n'importe quel répertoire si le
paramètre `path` renseigne le chemin (absolu ou relatif). Après avoir importé la fonction (`from os import getcwd`), on peut l'appeler : `os.listdir()`.
</div>\EndKnitrBlock{remarque}


## Charger des données {#charger-donnees}


En fonction du format d'enregistrement des données, les techniques d'importation de données diffèrent.


\BeginKnitrBlock{remarque}<div class="remarque">Le Chapitre\ \@ref(pandas) propose d'autres manières d'importer les données, avec la libraririe `pandas`.</div>\EndKnitrBlock{remarque}


### Fichiers textes {#import-fichiers-texte}

Lorsque les données sont présentes dans un fichier texte (ASCII), Python propose d'utiliser la fonction `open()`.

La syntaxe (simplifiée) de la fonction `open()` est la suivante :

```python
open(file, mode='r', buffering=-1,
  encoding=None, errors=None, newline=None)
```

Voici à quoi correspondent les paramètres (il en existe d'autres) :

- `file` : une chaîne de caractères indiquant le chemin et le nom du fichier à ouvrir ;
- `mode` : spécifie la manière par laquelle le fichier est ouvert (c.f. juste après pour les valeurs possibles) ;
- `buffering` : spécifie à l'aide d'un entier le comportement à adopter pour la mise en mémoire tampon (1 pour mettre en mémoire par ligne ; un entier $>1$ pour indiquer la taille en octets des morceaux à charger en mémoire tampon) ;
- `encoding` : spécifie l'encodage du fichier ;
- `errors` : spécifie la manière de gérer les erreurs d'encodage et de décodage (*e.g.*, `strict` retourne une erreur d'exception, `ignore` permet d'ignorer les erreurs, `replace` de les remplacer, `backslashreplace` de remplacer les données mal formées par des séquences d'échappement) ;
- `newline` : contrôle la fin des lignes (`\n`, `\r`, etc.).

| Valeur | Description |
| -------: | ---------------------------------------------------: |
| `r` |	Ouverture pour lire (défaut) |
| `w` |	Ouverture pour écrire |
| `x` |	Ouverture pour créer un document, échoue si le fichier existe déjà |
| `a` |	Ouverture pour écrire, en venant ajouter à la fin du fichier si celui-ci existe déjà |
| `+` |	Ouverture pour mise à jour (lecture et écriture) |
| `b` | À ajouter à un mode d'ouverture pour les fichiers binaires (`rb` ou `wb`) |
| `t` | Mode texte (décodage automatique des octets en Unicode). Par défaut si non spécifié (s'ajoute au mode, comme `b`) |

Table: (#tab:open-mode-ouverture) Valeurs principales pour la manière d'ouvrir les fichiers.


Il est important de bien penser à **fermer le fichier** une fois qu'on a terminé de l'utiliser. Pour ce faire, on utilise la méthode `close()`.


Dans le dossier `fichiers_exemples` se trouve un fichier appelé `fichier_texte.txt` qui contient trois lignes de texte. Ouvrons ce fichier, et utilisons la méthode `.read()` pour afficher son contenu :

```python
path = "./fichiers_exemples/fichier_texte.txt"
# Ouverture en mode lecture (par défaut)
mon_fichier = open(path, mode = "r")
print(mon_fichier.read())
```

```
## Bonjour, je suis un fichier au format txt.
## Je contiens plusieurs lignes, l'idée étant de montrer comment fonctionne l'importation d'un tel fichier dans Python.
## Trois lignes devraient suffir.
```

```python
mon_fichier.close()
```

Une pratique courante en Python est d'ouvrir un fichier dans un bloc `with`. La raison de ce choix est qu'un fichier ouvert dans un tel bloc est automatiquement refermé à la fin du bloc.

La syntaxe est la suivante :

```python
# Ouverture en mode lecture (par défaut)
with open(path, "r") as mon_fichier:
  donnees = fonction_pour_recuperer_donnees_depuis_mon_fichier()
```

Par exemple, pour récupérer chaque ligne comme un élément d'une liste, on peut utiliser une boucle parcourant chaque ligne du fichier. À chaque itération, on récupère la ligne :

```python
# Ouverture en mode lecture (par défaut)
with open(path, "r") as mon_fichier:
  donnees = [x for x in mon_fichier]
print(donnees)
```

```
## ['Bonjour, je suis un fichier au format txt.\n', "Je contiens plusieurs lignes, l'idée étant de montrer comment fonctionne l'importation d'un tel fichier dans Python.\n", 'Trois lignes devraient suffir.']
```

Note : à chaque itération, on peut appliquer la méthode `strip()`, qui retourne la chaîne de caractère de la ligne, en retirant les éventuels caractères blancs en début de chaîne :

```python
# Ouverture en mode lecture (par défaut)
with open(path, "r") as mon_fichier:
  donnees = [x.strip() for x in mon_fichier]
print(donnees)
```

```
## ['Bonjour, je suis un fichier au format txt.', "Je contiens plusieurs lignes, l'idée étant de montrer comment fonctionne l'importation d'un tel fichier dans Python.", 'Trois lignes devraient suffir.']
```


On peut également utiliser la méthode `readlines()` pour importer les lignes dans une liste :

```python
with open(path, "r") as mon_fichier:
    donnees = mon_fichier.readlines()
print(donnees)
```

```
## ['Bonjour, je suis un fichier au format txt.\n', "Je contiens plusieurs lignes, l'idée étant de montrer comment fonctionne l'importation d'un tel fichier dans Python.\n", 'Trois lignes devraient suffir.']
```


Il se peut parfois que l'encodage des caractères pose problème lors de l'importation. Dans ce cas, il peut être une bonne idée de changer la valeur du paramètre `encoding` de la fonction `open()`. Les encodages disponibles sont fonction de la locale. Les valeurs disponibles s'obtiennent à l'aide de la méthode suivante (code non exécuté dans ces notes) :

```python
import locale
locale.locale_alias
```



#### Importation depuis internet

Pour importer un fichier texte depuis Internet, on peut utiliser des méthodes de la librairie `urllib` :


```python
import urllib
from urllib.request import urlopen
url = "http://egallic.fr/Enseignement/Python/fichiers_exemples/fichier_texte.txt"
with urllib.request.urlopen(url) as mon_fichier:
   donnees = mon_fichier.read()
print(donnees)
```

```
## b"Bonjour, je suis un fichier au format txt.\nJe contiens plusieurs lignes, l'id\xc3\xa9e \xc3\xa9tant de montrer comment fonctionne l'importation d'un tel fichier dans Python.\nTrois lignes devraient suffir."
```

Comme on peut le constater, l'encodage des caractères pose souci ici. On peut appliquer la méthode `decode()` :


```python
print(donnees.decode())
```

```
## Bonjour, je suis un fichier au format txt.
## Je contiens plusieurs lignes, l'idée étant de montrer comment fonctionne l'importation d'un tel fichier dans Python.
## Trois lignes devraient suffir.
```

### Fichiers CSV {#importation-fichiers-csv}

Les fichier CSV (*comma separated value*) sont très répandus. De nombreuses bases de données exportent leurs données en CSV (*e.g.*, Banque Mondiale, FAO, Eurostat, etc.). Pour les importer dans Python, on peut uiliser le module `csv`.

À nouveau, on utilise la fonction `open()`, avec les paramètres décrits dans la Section\ \@ref(import-fichiers-texte). Ensuite, on fait appel à la méthode `reader()` du module `csv` :


```python
import csv
with open('./fichiers_exemples/fichier_csv.csv') as mon_fichier:
  mon_fichier_reader = csv.reader(mon_fichier, delimiter=',', quotechar='"')
  donnees = [x for x in mon_fichier_reader]

print(donnees)
```

```
## [['nom', 'prénom', 'équipe'], ['Irving', ' "Kyrie"', ' "Celtics"'], ['James', ' "Lebron"', ' "Lakers"', ''], ['Curry', ' "Stephen"', ' "Golden State Warriors"']]
```

La méthode `reader()` peut prendre plusieurs paramètres, décrits dans le Tableau\ \@ref(tab:parametres-reader-csv).

| Paramètre | Description |
| ------------------: | ---------------------------------------------: |
| `csvfile` | L'objet ouvert avec `open()` |
| `dialect` | Paramètre spécifiant le 'dialect' du fichier CSV (e.g., `excel`, `excel-tab`, `unix`) |
| `delimiter` | Le caractère délimitant les champs (*i.e.*, les valeurs des variables) |
| `quotechar` | Caractère utilisé pour entourer les champs contenant des caractères spéciaux |
| `escapechar` | Caractère d'échappement |
| `doublequote` | Contrôle comment les *quotechar* apparaissent à l'intérieur d'un champ : quand `True`, le caractère est doublé, ; quand `False`, le caractère d'échappement est utilisé en préfixe au *quotechar* |
| `lineterminator` | Chaîne de caractères utilisée pour terminer une ligne |
| `skipinitialspace` | Quand `True`, le caractère blanc situé juste après le caractère de séparation des champs est ignoré |
| `strict` | Quand `True`, retourne une erreur d'exception en cas de mauvais `input` de CSV |

Table: (#tab:parametres-reader-csv) Paramètres de la fonction `reader()`


On peut aussi importer un fichier CSV en tant que dictionnaire, à l'aide de la méthode `csv.DictReader()` du module CSV :


```python
import csv
chemin = "./fichiers_exemples/fichier_csv.csv"
with open(chemin) as mon_fichier:
    mon_fichier_csv = csv.DictReader(mon_fichier)
    donnees = [ligne for ligne in mon_fichier_csv]
print(donnees)
```

```
## [OrderedDict([('nom', 'Irving'), ('prénom', ' "Kyrie"'), ('équipe', ' "Celtics"')]), OrderedDict([('nom', 'James'), ('prénom', ' "Lebron"'), ('équipe', ' "Lakers"'), (None, [''])]), OrderedDict([('nom', 'Curry'), ('prénom', ' "Stephen"'), ('équipe', ' "Golden State Warriors"')])]
```



#### Importation depuis internet

Comme pour les fichiers `txt`, on peut charger un fichier CSV hébergé sur Internet :


```python
import csv
import urllib.request
import codecs

url = "http://egallic.fr/Enseignement/Python/fichiers_exemples/fichier_csv.csv"
with urllib.request.urlopen(url) as mon_fichier:
    mon_fochier_csv = csv.reader(codecs.iterdecode(mon_fichier, 'utf-8'))
    donnees = [ligne for ligne in mon_fochier_csv]
print(donnees)
```

```
## [['nom', 'prénom', 'équipe'], ['Irving', ' "Kyrie"', ' "Celtics"'], ['James', ' "Lebron"', ' "Lakers"', ''], ['Curry', ' "Stephen"', ' "Golden State Warriors"']]
```

### Fichier JSON

Pour importer des fichiers au format JSON (*JavaScript Object Notation*), qui sont très utilisés dès lors qu'on communique avec une API, on peut utiliser la librairie `json`, et sa méthode `load()` :


```python
import json
lien = './fichiers_exemples/tweets.json'

with open(lien) as mon_fichier_json:
    data = json.load(mon_fichier_json)
```

Ensuite, on peut afficher le contenu importé à l'aide de la fonction `pprint()` :


```python
from pprint import pprint
pprint(data)
```

```
## {'created_at': 'Wed Sep 26 07:38:05 +0000 2018',
##  'id': 11,
##  'loc': [{'long': 5.3698}, {'lat': 43.2965}],
##  'text': 'Un tweet !',
##  'user_mentions': [{'id': 111, 'screen_name': 'nom_twittos1'},
##                    {'id': 112, 'screen_name': 'nom_twittos2'}]}
```

#### Importation depuis Internet

Encore une fois, il est possible d'importer des fichiers JSON depuis Internet :


```python
import urllib
from urllib.request import urlopen
url = "http://egallic.fr/Enseignement/Python/fichiers_exemples/tweets.json"
with urllib.request.urlopen(url) as mon_fichier:
   donnees = json.load(mon_fichier)
pprint(donnees)
```

```
## {'created_at': 'Wed Sep 26 07:38:05 +0000 2018',
##  'id': 11,
##  'loc': [{'long': 5.3698}, {'lat': 43.2965}],
##  'text': 'Un tweet !',
##  'user_mentions': [{'id': 111, 'screen_name': 'nom_twittos1'},
##                    {'id': 112, 'screen_name': 'nom_twittos2'}]}
```


### Fichiers Excel

Les fichiers Excel (`xls` ou `xlsx`) sont aussi très largement répandus en économie. Le lecteur est prié de se référer à la Section\ \@ref(pandas-importation-excel) pour une méthode d'importation des données Excel avec la librairie `pandas`.


## Exporter des données

Il n'est pas rare de devoir exporter ses données, ne serait-ce que pour les partager. À nouveau, la fonction `open()` est mise à contribution, en jouant avec la valeur du paramètre `mode` (c.f. Tableau\ \@ref(tab:open-mode-ouverture)).

### Fichiers textes

Admettons que nous ayons besoin d'exporter des lignes de texte dans un fichier. Avant de donner un exemple avec la fonction `open()`, regardons deux fonctions importantes pour convertir les contenus de certains objets en texte.

La première, `str()`, retourne une version en chaînes de caractères d'un objet. Nous l'avons déjà appliquée à des nombres que l'on désirait concaténer en Section\ \@ref(conversion-chaines-caracteres).


```python
x = ["pomme", 1, 3]
str(x)
```

Le résultat de cette instruction retourne la liste sous la forme d'une chaîne de caractères : `"['pomme', 1, 3]"`.


La seconde fonction qu'il semble important d'aborder est `repr()`. Cette fonction retourne une chaîne contenant une représentation imprimable à l'écran d'un objet. De plus, cette chaîne peut être lue par l'interprète.


```python
y = "Fromage, tu veux du fromage ?\n"
repr(y)
```

Le résultat donne : `"'Fromage, tu veux du fromage ?\\n'"`.


Admettons que nous souhaitons exporter deux lignes :

- la première, un texte qui indique un titre ("Caractéristiques de Kyrie Irving") ;
- la seconde, un dictionnaire contenant des informations sur Kyrie Irving (c.f. ci-dessous).


Définissions ce dictionnaire :


```python
z = { "nom": "Kyrie",
  "prenom": "John",
  "naissance": 1992,
  "equipes": ["Cleveland", "Boston"]}
```

Une des syntaxes pour exporter les données au format `txt` est :

```python
# Ouverture en mode lecture (par défaut)
chemin = "chemin/vers/fichier.txt"
with open(chemin, "w") as mon_fichier:
  fonction_pour_exporter()
```

On créé une variable indiquant le chemin vers le fichier. On ouvre ensuite le fichier en mode écriture en précisant le paramètre `mode = "w"`. Puis, il reste à écrire nos lignes dans le fichier.


```python
chemin = "./fichiers_exemples/Irving.txt"
with open(chemin, mode = "w") as mon_fichier:
  mon_fichier.write("Caractéristiques de Kyrie Irving\n")
  mon_fichier.writelines(repr(z))
```

Si le fichier est déjà existant, en ayant utilisé `mode="w"`, l'ancien fichier sera écrasé par le nouveau. Si on souhaite ajouter des lignes au fichier existant, on utilisera `mode="a"` par exemple :

```python
with open(chemin, mode = "a") as mon_fichier:
  mon_fichier.writelines("\nUne autre ligne\n")
```


Si on souhaite être prévenu si le fichier est déjà existant, et faire échouer l'écriture si tel est le cas, on peut utiliser `mode="x"` :

```python
with open(chemin, mode = "x") as mon_fichier:
  mon_fichier.writelines("Une nouvelle ligne qui ne sera pas ajoutée\n")
```

```
## FileExistsError: [Errno 17] File exists: './fichiers_exemples/Irving.txt'
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```


### Fichiers CSV


En tant qu'économiste, il est plus fréquent d'avoir à exporter les données au format CSV plutôt que texte, du fait de la structure en rectangle des données que l'on manipule. Comme pour l'importation de CSV (c.f. Section\ \@ref(importation-fichiers-csv)), on utilise le module `csv`. Pour écrire dans le fichier, on utilise la méthode `writer()`. Les paramètres de formatage de cette fonction sont les mêmes que ceux de la fonction `reader()` (c.f. Tableau\ \@ref(tab:parametres-reader-csv)).


Exemple de création d'un fichier CSV :


```python
import csv
chemin = "./fichiers_exemples/fichier_export.csv"

with open(chemin, mode='w') as mon_fichier:
    mon_fichier_ecrire = csv.writer(mon_fichier, delimiter=',',
                                    quotechar='"',
                                    quoting=csv.QUOTE_MINIMAL)

    mon_fichier_ecrire.writerow(['Pays', 'Année', 'Trimestre', 'TC_PIB'])
    mon_fichier_ecrire.writerow(['France', '2017', 'Q4', 0.7])
    mon_fichier_ecrire.writerow(['France', '2018', 'Q1', 0.2])
```


Bien évidemment, la plupart du temps, nous n'écrivons pas à la main chaque entrée. Nous exportons les données contenues dans une structure. La Section\ \@ref(pandas-importation-excel) donne des exemples de ce type d'export, lorsque les données sont contenues dans des tableaux à deux dimension créés avec la librairie `Pandas`.


### Fichier JSON

Il peut être nécessaire de sauvegarder des données structurées au format JSON, par exemple lorsqu'on a fait appel à une API (*e.g.*, l'API de Twitter) qui retourne des objets au format JSON.

Pour ce faire, nous allons utiliser la librairire `json`, et sa méthode `dump()`. Cette méthode permet de sérialiser un objet (par exemple une liste, comme ce que l'on obtient avec l'API Twitter interrogée avec la libraririe `twitter-python`) en JSON.



```python
import json
x = [1, "pomme", ["pépins", "rouge"]]
y = { "nom": "Kyrie",
  "prenom": "John",
  "naissance": 1992,
  "equipes": ["Cleveland", "Boston"]}
x_json = json.dumps(x)
y_json = json.dumps(y)

print("x_json: ", x_json)
```

```
## x_json:  [1, "pomme", ["p\u00e9pins", "rouge"]]
```

```python
print("y_json: ", y_json)
```

```
## y_json:  {"nom": "Kyrie", "prenom": "John", "naissance": 1992, "equipes": ["Cleveland", "Boston"]}
```


Comme on peut le constater, on rencontre quelques petite problèmes d'affichage des caractères accentués. On peut préciser, à l'aide du paramètre `ensure_ascii` évalué à `False` que l'on ne désire pas s'assurer que les caractères non-ascii soient échappés par des séquences de type `\uXXXX`.

```python
x_json = json.dumps(x, ensure_ascii=False)
y_json = json.dumps(y, ensure_ascii=False)

print("x_json: ", x_json)
```

```
## x_json:  [1, "pomme", ["pépins", "rouge"]]
```

```python
print("y_json: ", y_json)
```

```
## y_json:  {"nom": "Kyrie", "prenom": "John", "naissance": 1992, "equipes": ["Cleveland", "Boston"]}
```



```python
chemin = "./fichiers_exemples/export_json.json"

with open(chemin, 'w') as f:
    json.dump(json.dumps(x, ensure_ascii=False), f)
    f.write('\n')
    json.dump(json.dumps(y, ensure_ascii=False), f)
```


Si on souhaite réimporter dans Python le contenu du fichier `export_json.json` :

```python
chemin = "./fichiers_exemples/export_json.json"
with open(chemin, "r") as f:
    data = []
    for line in f:
        data.append(json.loads(line, encoding="utf-8"))

print(data)
```

```
## ['[1, "pomme", ["pépins", "rouge"]]', '{"nom": "Kyrie", "prenom": "John", "naissance": 1992, "equipes": ["Cleveland", "Boston"]}']
```



### Exercice

\BeginKnitrBlock{exframe}<div class="exframe">1. Créer une liste nommée `a` contenant des informations sur le taux de chômage en France au deuxième trimestre 2018. Cette liste doit contenir trois éléments :
    - l'année ;
    - le trimestre ;
    - la valeur du taux de chômage ($9.1\%$).
2. Exporter au format CSV le contenu de la liste `a`, en le faisant précéder d'une ligne précisant les noms des champs. Utiliser le point virgule comme séparateur de champs.
3. Importer le fichier créé dans la question précédente dans Python.
</div>\EndKnitrBlock{exframe}





# Conditions {#conditions}

Souvent, en fonction de l'évaluation d'une expression, on désire réaliser une opération plutôt qu'une autre. Par exemple, lorsqu'on créé une nouvelle variable dans une analyse statistique, et que cette variable prend ses valeurs en fonction d'une autre, on peut être amené à utiliser des **instructions conditionnelles** : "si la valeur est inférieur à $x$, alors... sinon, ...".

Dans ce court chapitre, nous regardons comment rédiger les instructions conditionnelles.

## Les instructions conditionnelles `if`

L'instruction conditionnelle la plus simple que l'on peut rencontrer est `if`. Si et seulement si une expression est évaluée à `True`, alors une instruction sera évaluée. 


La syntaxe est la suivante :

```python
if expression:
  instruction
```

Les lignes après les deux points (`:`) doivent être placées dans un bloc, en utilisant un taquet de tabulation.

\BeginKnitrBlock{remarque}<div class="remarque">Un bloc de code est un regroupement d'instructions. Des codes imbriqués indentés à la même position font partie du même bloc :

    ligne du bloc 1
    ligne du bloc 1
      ligne du bloc2
      ligne du bloc2
    ligne du bloc1
</div>\EndKnitrBlock{remarque}




Dans le code ci-dessous, nous définissons une variable `x` contenant l'entier $2$. L'instruction suivante évalue l'expression `x == 2` (cf. Section\ \@red(#operateurs-comparaison) pour des rappels sur les opérateurs de comparaison). Si le résultat de cette expression est `Vrai`, alors le contenu du bloc est évalué.

```python
x = 2
if x == 2:
  print("Hello")
```

```
## Hello
```

Si on change la valeur de `x` de manière à ce que l'expression `x == 2` retourne `False` :

```python
x = 3
if x == 2:
  print("Hello")
```


À l'intérieur du bloc, on peut écrire plusieurs instructions qui seront évaluées si l'expression est `True` :

```python
x = 2
if x == 2:
  y = "Hello"
  print(y + ", x vaut : " + str(x))
```

```
## Hello, x vaut : 2
```



\BeginKnitrBlock{remarque}<div class="remarque">Lorsqu'on rédige son code, il peut-être pratique d'utiliser des instructions conditionnelles `if` pour évaluer ou non certaines parties du code. Par exemple, quand on régide un script, il arrive des moments où nous devons réévaluer le début, mais que certaines parties ne nécessitent pas d'être réévaluées à chaque fois, comme des sorties graphiques (ce qui prend du temps). Il est possible de commenter ces parties de codes ne nécessitant pas une nouvelle évaluation, ou alors on peut les placer dans un bloc conditionnel :

- au début du script, on créé une variable `graph = False` ;
- avant de créer un graphique, on le place dans un bloc `if graphe:`

Au moment de l'exécution du script, on peut choisir de créer et exporter les graphiques des blocs `if graphe:` en modifiant à sa guise la variable `graph`.</div>\EndKnitrBlock{remarque}

## Les instructions conditionnelles `if-else`


Si la condition n'est pas vérifiée, on peut proposer des instructions à effectuer, à l'aide des instructions `if-else`.


La syntaxe est la suivante :

```python
if expression:
  instructions
else:
  autres_instruction
```


Par exemple, admettons qu'on veuille créer une variable de chaleur prenant la valeur `chaud` si la valeur de la variable `temperature` dépasse 28 degrés C, `froid` sinon. Admettons que la température est de 26 degrés C :


```python
temperature = 26
chaleur = ""

if temperature > 28:
  chaleur = "chaud"
else:
  chaleur = "froid"

print("Il fait " + chaleur)
```

```
## Il fait froid
```

Si la température est à présent de 32 degrés C :

```python
temperature = 32
chaleur = ""

if temperature > 28:
  chaleur = "chaud"
else:
  chaleur = "froid"

print("Il fait " + chaleur)
```

```
## Il fait chaud
```


## Les instructions conditionnelles `if-elif`


Si la condition n'est pas vérifiée, on peut en tester une autre et alors évaluer d'autres instructions si cette seconde est vérifiée. Sinon, on peut en tester encore une autre, et ainsi de suite. On peut aussi proposer des instructions si aucune des conditions n'a été évaluée à `True`. Pour ce faire, on peut utiliser des instructions conditionnelles `if-elif`.


La syntaxe est la suivante :


```python
if expression:
  instructions
elif expression_2:
  instructions_2
elif expression_3:
  instructions_3
else:
  autres_instruction
```


L'exemple précédent manque un peu de sens commun. Peut-on dire que lordqu'il fait 28 degrés C ou moins il fait froid ? Ajoutons quelques nuances :



```python
temperature = -4
chaleur = ""

if temperature > 28:
  chaleur = "chaude"
elif temperature <= 28 and temperature > 15:
  chaleur = "tempérée"
elif temperature <= 15 and temperature > 0:
  chaleur = "froide"
else:
  chaleur = "très froide"

print("La température est " + chaleur)
```

```
## La température est très froide
```



\BeginKnitrBlock{remarque}<div class="remarque">L'avantage d'utiliser des instructions conditionnelles `if-elif` par rapport à écrire plusieurs instructions conditionnelles `if` à la suite est qu'avec la première manière de faire, les comparaisons s'arrêtent dès qu'une est remplie, ce qui est plus efficace.</div>\EndKnitrBlock{remarque}


## Exercice

\BeginKnitrBlock{exframe}<div class="exframe">Soit une liste nommée `europe` contenant les valeurs suivantes, sous forme de chaînes de caractères : "Allemagne", "France" et "Espagne".

Soit une seconde liste, nommée `asie`, contenant sous forme de chaînes de caractères : "Vietnam", "Chine" et "Inde".

L'objectif va être de créer une variable `continent` qui va indiquer soit `Europe`, `Asie` ou autre à l'issue de l'exécution du code.

À l'aide d'instructions conditionnelles de type `if-elif`, rédiger un code qui vérifie la valeur d'une variable `pays`, et définit la valeur d'une autre variable nommée `continent` en fonction du contenu observé dans `pays` tel que :

- si la valeur de pays est présente dans la liste `europe`, `pays` vaudra `Europe` ;
- si la valeur de pays est présente dans la liste `asie`, `pays` vaudra `Asie` ;
- si la valeur de pays n'est présente ni dans `europe` ni dans `asie`, la variable `pays` vaudra `Autre`.
  

Pour ce faire :

1. Créer les deux listes `europe` et `asie` ainsi que la variable `pays` (valant "Espagne") et la variable `continent` (initiée avec une chaîne de caractères vide).
2. Rédiger le code permettant de réaliser l'objectif expliqué, et afficher le contenu de la variable `continent` à l'issue de l'exécution.
3. Changer la valeur de `pays` à `Chine` puis à `Brésil` et dans chacun des cas, exécuter le code rédigé dans la question précédente.
</div>\EndKnitrBlock{exframe}


# Boucles {#boucles}

Quand on doit répéter plusieurs fois la même opération, pour un nombre déterminé de fois ou tant qu'une condition est vérifiée (ou tant qu'elle n'est pas vérifiée), on peut utiliser des boucles, ce qui est bien moins pénible que d'évaluer à la main ou à coups de copier/coller la même instruction.

Nous allons aborder deux types de boucles dans ce chapitre :

- celles pour lesquelles nous ne savons pas `a priori` le nombre d'itérations (le nombre de répétitions) à effectuer : les boucles `while()`
- celles pour lesquelles nous savons `a priori` combien d'itérations sont nécessaires : les boucles `for()`


\BeginKnitrBlock{remarque}<div class="remarque">Il est possible d'arrêter une boucle `for()` avant un nombre d'itérations prédéfini ; dans le même esprit, il est possible d'utiliser une boucle `while()` en sachant d'avance le nombre d'itérations à effectuer.
</div>\EndKnitrBlock{remarque}


## Boucles avec `while()`

Le principe d'une boucle `while()` est que les instructions à l'intérieur de la boucle seront répétées tant qu'une condition est respectée. L'idée est de faire dépendre cette condition d'un ou plusieurs objets qui seront modifiés au cours des itérations (sans cela, la boucle tournerait à l'infini).

La syntaxe est la suivante :

```python
while condition:
  instructions
```

Comme pour les instructions conditionnelles (c.f. Section\ \@ref(conditions)), les instructions sont placées à l'intérieur d'un bloc.

Regardons un exemple de boucle `while()` :

```python
x = 100
while x/3 > 1:
  print(x/3)
  x = x/3
```

```
## 33.333333333333336
## 11.111111111111112
## 3.703703703703704
## 1.234567901234568
```

```python
print(x/3>1)
```

```
## False
```

```python
print(x/3)
```

```
## 0.41152263374485604
```

Dans cette boucle, à chaque itération, la valeur de `x` divisé par 3 est affichée, puis la valeur de `x` est remplacée par le tiers de sa valeur courante. Cette opération est répétée tant que l'expression `x/3 > 1` retourne `True`.





## Boucles avec `for()`


Quand on connaît le nombre d'itérations à l'avance, on pourra utiliser une boucle `for()`. La syntaxe est la suivante :

```python
for objet in valeurs_possibles:
  instructions
```

avec `objet` le nom d'une variable locale à la fonction `for()`, `valeurs_possibles` un objet comprenant $n$ éléments définissant les valeurs que prendra `objet` pour chacun des $n$ tours, et `instructions` les instructions qui seront exécutées à chaque itération.

Nous allons, dans l'exemple qui suit, calculer le carré des $n$ premiers entiers. Les valeurs que vont prendre notre variable `objet` (que nous allons appeler `i`) seront les entiers de 1 à $n$. Pour obtenir une séquence d'entiers en Python, on peut utiliser la fonction `range()`, qui prend les paramètres suivants :

- `start` : (optionnel, par défaut, 0) valeur de début pour la séquence (inclue) ;
- `stop` : valeur de fin de la séquence (non inclue) ;
- `step` : (optionnel, par défaut 1) le pas.

Avant de calculer la suite des $n$ premiers carrés, regardons un exemple de fonctionnement de la fonction `range()` :

```python
print(list(range(0, 4))) # Les entiers de 0 à 3
```

```
## [0, 1, 2, 3]
```

```python
print(list(range(4))) # Les entiers de 0 à 3
```

```
## [0, 1, 2, 3]
```

```python
print(list(range(2, 10))) # Les entiers de 2 à 9
```

```
## [2, 3, 4, 5, 6, 7, 8, 9]
```

```python
print(list(range(2, 10, 3))) # Les entiers de 2 à 9 par pas de 3
```

```
## [2, 5, 8]
```

Aussi, pour afficher la suite des $10$ premiers carrés :


```python
n=10
for i in range(0, n+1):
  print("Le carré de %s est %s" % (i,i**2))
```

```
## Le carré de 0 est 0
## Le carré de 1 est 1
## Le carré de 2 est 4
## Le carré de 3 est 9
## Le carré de 4 est 16
## Le carré de 5 est 25
## Le carré de 6 est 36
## Le carré de 7 est 49
## Le carré de 8 est 64
## Le carré de 9 est 81
## Le carré de 10 est 100
```

Lors de la première itération, `i` vaut 0. Lors de la seconde, `i` vaut 1. Lors de la troisième, `i` vaut 2, etc.


Si on veut stocker le résultat dans une liste :

```python
n=10
n_entiers_carres = []
for i in range(0, n+1):
  n_entiers_carres.append(i**2)
  
print(n_entiers_carres)
```

```
## [0, 1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```


Il n'est pas obligatoire d'utiliser la fonction `range()` dans une boucle `for()`, on peut définir les valeurs "à la main" :


```python
for i in [0, 1, 2, 8, 9, 10]:
  print("Le carré de %s est %s" % (i,i**2))
```

```
## Le carré de 0 est 0
## Le carré de 1 est 1
## Le carré de 2 est 4
## Le carré de 8 est 64
## Le carré de 9 est 81
## Le carré de 10 est 100
```


Dans le même esprit, il n'est pas obligatoire d'itérer sur des valeurs numériques :

```python
for prenom in ["Pascaline", "Gauthier", "Xuan", "Jimmy"]:
  print("Il y a %s lettre(s) dans le prénom %s" % (len(prenom), prenom))
```

```
## Il y a 9 lettre(s) dans le prénom Pascaline
## Il y a 8 lettre(s) dans le prénom Gauthier
## Il y a 4 lettre(s) dans le prénom Xuan
## Il y a 5 lettre(s) dans le prénom Jimmy
```



Rien n'empêche de faire des boucles à l'intérieur de boucles :

```python
for i in range(0,3):
    for j in range(0,3):
        print("i vaut %s et j vaut %s" % (i, j))
```

```
## i vaut 0 et j vaut 0
## i vaut 0 et j vaut 1
## i vaut 0 et j vaut 2
## i vaut 1 et j vaut 0
## i vaut 1 et j vaut 1
## i vaut 1 et j vaut 2
## i vaut 2 et j vaut 0
## i vaut 2 et j vaut 1
## i vaut 2 et j vaut 2
```

Comme on peut le constater, l'itération se fait pour chaque valeur de `i`, et pour chacune de ces valeurs, une seconde itération est effectuée sur les valeurs de `j`.


\BeginKnitrBlock{remarque}<div class="remarque">On utilise souvent les lettres `i` et `j` pour désigner un compteur dans une boucle `for()`, mais ce n'est évidemment pas une obligation.
</div>\EndKnitrBlock{remarque}

Dans une boucle, si on désire incrémenter un comteur, on peut utiliser le symbole `+=` plutôt que d'écrire `compteur = compteur + ...` :



```python
j = 10
for i in range(0, 4):
  j += 5
  print("Nouvelle valeur pour j : %s" % j)
  
```

```
## Nouvelle valeur pour j : 15
## Nouvelle valeur pour j : 20
## Nouvelle valeur pour j : 25
## Nouvelle valeur pour j : 30
```

```python
print(j)
```

```
## 30
```




## Exercice

\BeginKnitrBlock{exframe}<div class="exframe">1. Rédiger un programme très naïf visant à déterminer si un nombre est premier ou non. Pour ce faire : 

    1. définir une variable `nombre` contenant un entier naturel de votre choix (pas trop grand),
    2. à l'aide d'une boucle, vérifier si chaque entier jusqu'à la racine carrée de votre nombre, est un diviseur de votre nombre (s'arrêter si jamais c'est le cas)
    3. en sortie de boucle, écrire une instruction conditionnelle indiquant si le nombre est premier ou non.
2. Choisir un nombre mystère entre 1 et 100, et le stocker dans un objet que l'on nommera `nombre_mystere`. Ensuite, créer une boucle qui à chaque itération effectue un tirage aléatoire d'un entier compris entre 1 et 100. Tant que le nombre tiré est différent du nombre mystère, la boucle doit continuer. À la sortie de la boucle, une variable que l'on appellera `nb_tirages` contiendra le nombre de tirages réalisés pour obtenir le nombre mystère.

*Note : pour tirer un nombre aléatoirement entre 1 et 100, on peut utiliser la méthode `randint()` du module `random`).*

3. Parcourir les entiers de 1 à 20 à l'aide d'une boucle for en affichant dans la console à chaque itération si le nombre courant est pair.
4. Utiliser une boucle `for()` pour reprouire la suite de Fibonacci jusqu'à son dixième terme (la séquence $F_n$ est définie par la relation de récurrence suivante : $F_n = F_{n-1} + F_{n-2}$ ; les valeurs initiales sont $F_0 = 0$ et $F_1 = 1$).
</div>\EndKnitrBlock{exframe}



# Fonctions

La plupart du temps, on utilise les fonctions de base ou contenues dans des modules. Cela dit, lorsque l'on récupère des données en ligne ou qu'on doit mettre en forme des données importées depuis diverses sources, il arrive qu'il soit nécessaire de créer ses propres fonctions. L'avantage de créer ses fonctions se révèle dès lors qu'on doit effectuer une suite d'instruction de manière répétée, avec quelques légères différences (on peut alors appliquer les fonctions au sein d'une boucle, comme nous l'avons abordé dans le Chapitre\ \@ref(boucles)).


## Définition

Une fonction est déclarée à l'aide du mot clé `keyword`. Ce qu'elle renvoie est retourné à l'aide du mot clé `return`.

La syntaxe est la suivante :

```python
def nom_fonction(parametres):
  corps_de_la_fonction
```

Une fois que la fonction est définie, on l'appelle en faisant référence à son nom :

```python
nom_fonction()
```


Il suffit donc de rajouter des parenthèses au nom de la fonction pour l'appeler. En effet, `nom_fonction` désigne l'objet qui contient la fonction qui est appelée à l'aide de l'expression `nom_fonction()`.
Par exemple, si on souhaite définir la fonction qui calcule le carré d'un nombre, voici ce que l'on peut écrire :


```python
def carre(x):
  return x**2
```

On peut ensuite l'appeler :

```python
print(carre(2))
```

```
## 4
```

```python
print(carre(-3))
```

```
## 9
```

### Ajout d'une description

Il est possible (et fortement recommandé) d'ajouter une description de ce que la fonction fait :

```python
def carre(x):
  """retourne le carré de x"""
  return x**2
```

De fait, quand on évalue ensuite l'instruction suivante, la description de la fonction s'affiche :

```r
?carre
```

Dans Jupyter Notebook, après avoir écrit le nom de la fonction, on peut aussi afficher la description en appuyant sur les touches du clavier `Shift` et `Tabulation`.

### Paramètres d'une fonction

Dans l'exemple de la fonction `carre()` que nous avons créée, nous avons renseigné un seul paramètre, appelé `x`. Si la fonction que l'on souhaite créer nécessite plusieurs paramètres, il faut les séparer par une virgule.

Considérons par exemple le problème suivant. Nous disposons d'une fonction de production $Y(L, K, M)$, qui dépend du nombre de travailleurs $L$ et de la quantité de capital $K$, et du matériel $M$, telle que $Y(L, K, M) = L^{0.3} K^{0.5}M^2$. Cette fonction pourra s'écrire en Python de la manière suivante :


```python
def production(l, k, m):
  """
  @param l (float) travail
  @param k (float) capital
  @param m (float) matériel
  @desc Retourne la valeur de la production en fonction
    du travail, du capital et du matériel.
  """
  return l**0.3 * k**0.5 * m**(0.2)
```

#### Appel sans noms de paramètres

En reprenant l'exemple précédent, si on nous donne $L = 60$ et $K = 42$ et $M = 40$, on peut en déduire la production :


```python
prod_val = production(60, 42, 40)
print(prod_val)
```

```
## 46.289449781254994
```

On peut noter que le nom des paramètres n'a pas été mentionné ici. Lors de l'appel de la fonction, la valeur du premier paramètre a été attribué au paramètre défini en premier (`l`), celle du second au second paramètre (`k`) et enfin celle du troisième au troisième paramètre (`m`).


#### Paramètres positionnels paramètres par mots-clés

Il existe deux types de paramètres que l'on peut donner à une fonction en Python : 

- les paramètres positionnels ;
- les paramètres par mots-clés.


Contrairement aux paramètres positionnels, les paramètres par mot clé ont une valeur attribuée par défaut. On parle de paramètre formel pour désigner les paramètres de la fonction (les variables utilisées dans le corps de la fonction) et de paramètre effectif pour désigner la valeur que l'on souhaite donner au paramètre formel. Pour définir la valeur à donner à un paramètre formel, on utilise le symbol d'égalité. Lors de l'appel de la fonction, si l'utilisateur ne définit pas explicitement une valeur, celle par défaut sera affectée. Ainsi, il n'est pas forcément nécessaire de préciser les paramètres par mots-clés lors de l'appel de la fonction.

Il est important de noter que les arguments positionnels (ceux qui n'ont pas de valeur par défaut) doivent apparaître en premier dans la liste des paramètres.

Prenons un exemple avec deux paramètres positionnels (`l` et `m`) et un paramètre par mot-clé (`k`) :


```python
def production_2(l, m, k=42):
  """
  @param l (float) travail
  @param m (float) matériel
  @param k (float) capital (defaut : 42)
  @desc Retourne la valeur de la production en fonction
    du travail, du capital et du matériel.
  """
  return l**0.3 * k**0.5 * m**(0.2)
```

La fonction `production_2()` peut s'appeler, pour donner le même résultat, des trois manières suivantes :


```python
# En nommant tous les paramètres, en ommettant k
prod_val_1 = production_2(l = 42, m = 40)
# En nommant tous les paramètres et en précisant k
prod_val_2 = production_2(l = 42, m = 40, k = 42)
# En nommant uniquement le paramètre mot-clé k
prod_val_3 = production_2(42, 40, k = 42)
# En ne nommant aucun paramètre
prod_val_4 = production_2(42, 40, 42)

res = [prod_val_1, prod_val_2, prod_val_3, prod_val_4]
print(res)
```

```
## [41.59215573604822, 41.59215573604822, 41.59215573604822, 41.59215573604822]
```

\BeginKnitrBlock{remarque}<div class="remarque">Si la fonction contient plusieurs paramètres positionnels ; lors de l'appel :

- soit on nomme tous les paramètres positonnels par leur nom ;
- soit aucun ;
- il n'y a pas d'entre deux.
</div>\EndKnitrBlock{remarque}


Du moment que tous les paramètres positionnels sont nommés lors de l'appel, on peut les faire figurer dans des ordres différents :

```python
def production_3(a, l, m = 40, k=42):
  """
  @param a (float) productivité totale des facteurs
  @param l (float) travail
  @param m (float) matériel (défaut : 40)
  @param k (float) capital (défaut : 42)
  @desc Retourne la valeur de la production en fonction
    du travail, du capital et du matériel.
  """
  return a * l**0.3 * k**0.5 * m**(0.2)
  
prod_val_1 = production_3(1, 42, m = 38)
prod_val_2 = production_3(a = 1, l = 42)
prod_val_3 = production_3(l = 42, a = 1)
prod_val_4 = production_3(m = 40, l = 42, a = 1)

res = [prod_val_1, prod_val_2, prod_val_3, prod_val_4]
print(res)
```

```
## [41.16765711449734, 41.59215573604822, 41.59215573604822, 41.59215573604822]
```

#### Fonction comme paramètre

Une fonction peut être fournie en paramètre à une autre fonction.


```python
def carre(x):
  """Retourne le carré de x"""
  return x**2
  
def appliquer_carre_4(fun):
  """Applique la fonction `fun` à 4"""
  return fun(4)

print(appliquer_carre_4(carre))
```

```
## 16
```


## Portée

Lorsque une fonction est appelée, le corps de cette fonction est interprété. Les variables ayant été définies dans le corps de la fonction sont assignées à un *namespace* local. C'est-à-dire qu'elles ne vivent qu'à l'intérieur ce cet espace local, qui est créé au moment de l'appel de la fonction et détruit à la fin de celui ci. On parle alors de portée des variables. Ainsi, une variable ayant une portée locale (assignée dans l'espace local) peut avoir le même nom qu'une variable globale (définie dans l'espace de travail global), sans pour autant désigner le même objet, ou écraser cet objet.

Regardons cela à travers un exemple.


```python
# Définition d'une variable globale :
valeur = 1

# Définition d'une variable locale à la fonction f
def f(x):
  valeur = 2
  nouvelle_valeur = 3
  print("valeur vaut :", valeur)
  print("nouvelle_valeur vaut :", nouvelle_valeur)
  return x + valeur
```

Appelons la fonction `f()`, puis regardons la valeur de `valeur` et celle de `nouvelle_valeur` après l'exécution de la fonction.


```python
res = f(3)
```

```
## valeur vaut : 2
## nouvelle_valeur vaut : 3
```

```python
print("valeur vaut :", valeur)
```

```
## valeur vaut : 1
```

```python
print("nouvelle_valeur vaut :", nouvelle_valeur)
```

```
## NameError: name 'nouvelle_valeur' is not defined
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```

Comme on peut le constater, durant l'appel, la variable locale du nom `valeur` valait 2. Cette variable ne faisait pas référence à la variable du même nom définie dans l'environnement global. À l'issue de l'exécution de la fonction `f()`, cette variable `valeur` locale est supprimée, et il en est de même pour la variable locale `nouvelle_valeur`, qui n'existe pas dans l'environnement gloabl (d'où l'erreur retournée).


Sans trop rentrer trop dans les détails, il semble important de connaître quelques principes à propos de la portée des variables. Les variables sont définies dans des environnements, qui sont embriqués les uns dans les autres. Si une variable n'est pas définie dans le corps d'une fonction, Python ira chercher dans un environnement parent.


```python
valeur = 1
def f(x):
  return x + valeur
  
print(f(2))
```

```
## 3
```

Si on définit une fonction à l'intérieur d'une autre fonction, et qu'on appelle une variable non définie dans le corps de cette fonction, Python ira chercher dans l'environnement directement supérieur. S'il ne trouve pas, il ira chercher dans l'environnement encore supérieur, et ainsi de suite jusqu'à l'environnement global.



```python
# La variable valeur n'est pas définie dans
# l'environnement local de g().
# Python va alors chercher dans f().
valeur = 1
def f():
  valeur = 2
  def g(x):
    return x + valeur

  return g(2)

print(f())
```

```
## 4
```



```python
# La variable valeur n'est définie ni dans g() ni dans f()
# mais dans l'environnement supérieur (ici, global)
valeur = 1
def f():
  def g(x):
    return x + valeur

  return g(2)

print(f())
```

```
## 3
```

Si on définit une variable dans le corps d'une fonction et que l'on souhaite qu'elle soit accessible dans l'environnement global, on peut utiliser le mot-clé `global` :


```python
def f(x):
  global y
  y = x+1

f(3)
print(y)
```

```
## 4
```

\BeginKnitrBlock{remarque}<div class="remarque">La variable que l'on souhaite définir de manière globale depuis un espace local de la fonction ne doit pas avoir le même nom d'un des paramètres.
</div>\EndKnitrBlock{remarque}


## Fonctions lambda

Python propose ce que l'on appelle des fonctions lambdas, ou encore des fonctions anonymes. Une fonction lambda ne possède qu'une seule instruction dont le résultat est celui de la fonction.

On les définit à l'aide du mot-clé `lambda`. La syntaxe est la suivante :

```python
nom_fonction = lambda parametres : retour
```

Les paramètres sont à séparer par des virugles.

Reprenons la fonction `carre()` créée précédemment :

```python
def carre(x):
  return x**2
```

La fonction lambda équivalent s'écrit :


```python
carre_2 = lambda x: x**2
print(carre_2(4))
```

```
## 16
```

Avec plusieurs paramètres, regardons la fonction lambda équivalente à la fonction `produduction()` :


```python
def production(l, k, m):
  """
  @param l (float) travail
  @param k (float) capital
  @param m (float) matériel
  @desc Retourne la valeur de la production en fonction
    du travail, du capital et du matériel.
  """
  return l**0.3 * k**0.5 * m**(0.2)
```



```python
production_2 = lambda l,k,m : l**0.3 * k**0.5 * m**(0.2)
print(production(42, 40, 42))
```

```
## 40.987803063838406
```

```python
print(production_2(42, 40, 42))
```

```
## 40.987803063838406
```


## Retour de plusieurs valeurs

Il peut parfois être pratique de retourner plusieurs éléments en retour d'une fonction. Bien que la liste se porte candidate à cette fonctionnalité, il peut-être plus avisé d'utiliser un dictionnaire, pour pouvoir accéder aux valeurs grâce à leur clé !


```python
import statistics
def stat_des(x):
  """Retourne la moyenne et l'écart-type de `x`"""
  return {"moyenne": statistics.mean(x),
  "ecart_type": statistics.stdev(x)}

x = [1,3,2,6,4,1,8,9,3,2]
res = stat_des(x)
print(res)
```

```
## {'moyenne': 3.9, 'ecart_type': 2.8460498941515415}
```

```python
print("La moyenne vaut %s et l'écart-type vaut %s" % 
      (res["moyenne"], res["ecart_type"]))
```

```
## La moyenne vaut 3.9 et l'écart-type vaut 2.8460498941515415
```


## Exercice

\BeginKnitrBlock{exframe}<div class="exframe">1. Créer une fonction nommée `somme_n_entiers` qui retourne la somme des $n$ premiers entiers. Son seul paramètre sera `n`.
2. À l'aide d'une boucle, afficher la somme des 2 premiers entiers, puis 3 premiers entiers, puis 4 premiers entiers, etc. jusqu'à 10.
3. Créer une fonction qui à partir de deux points représentés par des couples de coordonnées ($x_1$, $y_1$) et ($x_2$, $y_2$) retourne la distance euclidienne entre ces deux points. Proposer une seconde solution à l'aide d'une fonction lambda.
</div>\EndKnitrBlock{exframe}



# Introduction à Numpy {#numpy}

Ce chapitre est consacré à une librairie importante pour les calculs numérique : `NumPy` (abréviation de *Numerical Python*).

Il est coutume d'importer `NumPy` en lui attribuant l'alias `np` :


```python
import numpy as np
```


## Tableaux

NumPy propose une structure de données populaire, les tableaux (de type *array*), sur lesquels il est possible d'effectuer de manière efficace des calculs. Les tableaux sont une structure notamment utile pour effectuer des opérations statistiques basiques ainsi que de la génération pseudo-aléatoire de nombres.

La stucture des tableaux ressemble à celle des listes, mais ces dernières sont moins rapides à être traitées et utilisent davantage de mémoire. Le gain de vitesse de traitement des tableaux en `NumPy` vient du fait que les données sont stockées dans des blocs contigus de mémoire, facilitant ainsi les accès en lecture.

Pour s'en convaincre, on peut reprendre l'exemple de Pierre Navaro [donné dans son *notebook* sur `NumPy`](https://github.com/pnavaro/python-notebooks/blob/master/13.Numpy.ipynb). Créons deux listes de longueur 1000 chacune, avec des nombres tirés aléatoirement à l'aide de la fonction `random()` du module `random`. Divisons chaque élément de la première liste par l'élément à la même position dans la seconde ligne, puis calculons la somme de ces 1000 divisions. Regardons ensuite le temps d'exécution à l'aide de la fonction magique `%timeit` :

```python
from random import random
from operator import truediv
l1 = [random() for i in range(1000)]
l2 = [random() for i in range(1000)]
# %timeit s = sum(map(truediv,l1,l2))
```

(décommenter la dernière ligne et tester sur un Jupyter Notebook)

À présent, transformons les deux listes en tableaux `NumPy` avec la méthode `array()`, et effectuons le même calcul à l'aide d'une méthode `NumPy` :

```python
a1 = np.array(l1)
a2 = np.array(l2)
# %timeit s = np.sum(a1/a2)
```

Comme on peut le constater en exécutant ces codes dans un environnement IPython, le temps d'exécution est bien plus rapide avec les méthodes de `NumPy` pour ce calcul.

### Création

La création d'un tableau peut s'effectuer avec la méthode `array()`, à partir d'une liste, comme nous venon de le faire :

```python
liste = [1,2,4]
tableau = np.array(liste)
print(tableau)
```

```
## [1 2 4]
```

```python
print(type(tableau))
```

```
## <class 'numpy.ndarray'>
```

Si on fournit à `array()` une liste de listes imbriquées de même longueur, un tableau multidimensionnel sera créé :

```python
liste_2 = [ [1,2,3], [4,5,6] ]
tableau_2 = np.array(liste_2)
print(tableau_2)
```

```
## [[1 2 3]
##  [4 5 6]]
```

```python
print(type(tableau_2))
```

```
## <class 'numpy.ndarray'>
```


Les tableaux peuvent aussi être créés à partir de n-uplets :

```python
nuplet = (1, 2, 3)
tableau = np.array(nuplet)
print(tableau)
```

```
## [1 2 3]
```

```python
print(type(tableau))
```

```
## <class 'numpy.ndarray'>
```


Un tableau en dimension 1 peut être changé en tableau en dimension 2 (si possible), en modifiant son attribut `shape` :

```python
tableau = np.array([3, 2, 5, 1, 6, 5])
tableau.shape = (3,2)
print(tableau)
```

```
## [[3 2]
##  [5 1]
##  [6 5]]
```



#### Quelques fonctions générant des `array`

Certaines fonctions de `NumPy` produisent des tableaux pré-remplis. C'est le cas de la fonction `zeros()`. Quand on lui fournit une valeur entière $n$, la fonction `zeros()` créé un tableau à une dimension, avec $n$ 0 :

```python
print( np.zeros(4) )
```

```
## [0. 0. 0. 0.]
```

On peut préciser le type des zéros (par exemple `int`, `int32`, `int64`, `float`, `float32`, `float64`, etc.), à l'aide du paramètre `dtype` :

```python
print( np.zeros(4, dtype = "int") )
```

```
## [0 0 0 0]
```

D'avantage d'explications sur les types de données avec `NumPy` sont disponibles [sur la documentation en ligne](https://docs.scipy.org/doc/numpy-1.15.1/reference/arrays.dtypes.html).


Le type des éléments d'un tableau est indiqué dans l'attribut `dtype` :

```python
x = np.zeros(4, dtype = "int")
print(x, x.dtype)
```

```
## [0 0 0 0] int64
```

Il est par ailleurs possible de convertir le type des éléments dans un un autre type, à l'aide de la méthode `astype()` :

```python
y = x.astype("float")
print(x, x.dtype)
```

```
## [0 0 0 0] int64
```

```python
print(y, y.dtype)
```

```
## [0. 0. 0. 0.] float64
```


Quand on lui fournit un n-uplet de longueur supérieure à 1, `zeros()` créé un tableau à plusieurs dimensions : 

```python
print( np.zeros((2, 3)) )
```

```
## [[0. 0. 0.]
##  [0. 0. 0.]]
```

```python
print( np.zeros((2, 3, 4)) )
```

```
## [[[0. 0. 0. 0.]
##   [0. 0. 0. 0.]
##   [0. 0. 0. 0.]]
## 
##  [[0. 0. 0. 0.]
##   [0. 0. 0. 0.]
##   [0. 0. 0. 0.]]]
```


La fonction `empty()` de `Numpy` retourne également un tableau sur le même principe que `zeros()`, mais sans initialiser les valeurs à l'intérieur.

```python
print( np.empty((2, 3), dtype = "int") )
```

```
## [[0 0 0]
##  [0 0 0]]
```

La fonction `ones()` de `Numpy` retourne le même genre de tableaux, avec des 1 en valeurs initialisées :

```python
print( np.ones((2, 3), dtype = "float") )
```

```
## [[1. 1. 1.]
##  [1. 1. 1.]]
```

Pour choisir une valeur spécifique pour l'initialisation, on peut utiliser la fonction `full()` de `Numpy` :

```python
print( np.full((2, 3), 10, dtype = "float") )
```

```
## [[10. 10. 10.]
##  [10. 10. 10.]]
```

```python
print( np.full((2, 3), np.inf) )
```

```
## [[inf inf inf]
##  [inf inf inf]]
```

La fonction `eye()` de `Numpy` créé un tableau à deux dimensions dans laquelle tous les éléments sont initalisés à zéro, sauf ceux de la diagonale initialisés à 1 :

```python
print( np.eye(2, dtype="int64") )
```

```
## [[1 0]
##  [0 1]]
```

En modifiant le paramètre mot-clé `k`, on peut décaler la diagonale :

```python
print( np.eye(3, k=-1) )
```

```
## [[0. 0. 0.]
##  [1. 0. 0.]
##  [0. 1. 0.]]
```

La fonction `identity()` de `Numpy` créé quant à elle une matrice identité sous la forme d'un tableau :

```python
print( np.identity(3, dtype = "int") )
```

```
## [[1 0 0]
##  [0 1 0]
##  [0 0 1]]
```


La fonction `arange()` de `Numpy` permet de générer une séquence de nombres séparés par un interval fixe, le tout stocké dans un tableau. La syntaxe est la suivante :

```python
np.arange( start, stop, step, dtype )
```

avec `start` la valeur de départ, `stop` celle d'arrivée, `step` le pas, l'espacement entre les nombres de la séquence et `dtype` le type des nombres :

```python
print( np.arange(5) )
```

```
## [0 1 2 3 4]
```

```python
print( np.arange(2, 5) )
```

```
## [2 3 4]
```

```python
print( np.arange(2, 10, 2) )
```

```
## [2 4 6 8]
```


### Dimensions

Pour connaître la dimension d'un tableau, on peut afficher la valeur de l'attribut `ndim` :

```python
print("ndim tableau : ", tableau.ndim)
```

```
## ndim tableau :  2
```

```python
print("ndim tableau_2 : ", tableau_2.ndim)
```

```
## ndim tableau_2 :  2
```

Le nombre d'éléments dans le tableau peut s'obtenir par l'attribut `size` ou par la fonction `size()` de `Numpy` :

```python
print("size tableau : ", tableau.size)
```

```
## size tableau :  6
```

```python
print("size tableau_2 : ", tableau_2.size)
```

```
## size tableau_2 :  6
```

```python
print("np.size(tableau) :", np.size(tableau))
```

```
## np.size(tableau) : 6
```

L'attribut `shape` retourne un n-uplet indiquant la longueur pour chaque dimension du tableau :

```python
print("size tableau : ", tableau.shape)
```

```
## size tableau :  (3, 2)
```

```python
print("size tableau_2 : ", tableau_2.shape)
```

```
## size tableau_2 :  (2, 3)
```



### Extraction des éléments d'un tableau

L'accès aux éléments d'un tableau se fait de la même manière que pour les listes  (c.f. Section\ \@ref(stucture-liste-extraction)), grâce à l'indiçage. La syntaxe est la suivante :

```python
tableau[lower:upper:step]
```

avec `lower` la borne inférieur de la plage d'indices, `upper` la plage supérieur, et `step` l'espacement entre les valeurs.

- Lorsque `lower` n'est pas précisé, le premier élément (indicé 0) est considéré comme la valeur attribuée à `lower`. 
- Lorsque `upper` n'est pas précisé, le dernier élément est considéré comme la valeur attribuée à `upper`. 
- Lorsque `step` n'est pas précisé, un pas de 1 est attribué par défaut.

Reprenons rapidement quelques exemples, en s'appuyant sur deux objets : un tableau de dimension 1, et un second de dimension 2.


```python
tableau_1 = np.arange(1,13)
tableau_2 = [ [1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]]
tableau_2 = np.array(tableau_2)
```

L'accès au premier élément :

```python
print("tableau_1[0] : %s (type : %s)" %
      (tableau_1[0], type(tableau_1[0])))
```

```
## tableau_1[0] : 1 (type : <class 'numpy.int64'>)
```

```python
print("tableau_2[0] : %s (type : %s)" %
      (tableau_2[0], type(tableau_2[0])))
```

```
## tableau_2[0] : [1 2 3] (type : <class 'numpy.ndarray'>)
```


L'accès aux éléments peut se faire en partant par la fin :

```python
print("tableau_1[-1] : ", tableau_1[-1]) # dernier élément
```

```
## tableau_1[-1] :  12
```

```python
print("tableau_2[-1] : ", tableau_2[-1]) # dernier élément
```

```
## tableau_2[-1] :  [10 11 12]
```


Le découpage est possible :


```python
# les éléments du 2e (non inclus) au 4e
print("Slice Tableau 1 : \n", tableau_1[2:4])
```

```
## Slice Tableau 1 : 
##  [3 4]
```

```python
print("Sclie Tableau 2 : \n", tableau_2[2:4])
```

```
## Sclie Tableau 2 : 
##  [[ 7  8  9]
##  [10 11 12]]
```

Pour les tableaux à deux dimensions, on peut accéder aux éléments de la manière suivante, de manière équivalente :

```python
# Dans le 3e élément, accéder au 1er élément
print(tableau_2[2][0])
```

```
## 7
```

```python
print(tableau_2[2,0])
```

```
## 7
```


#### Extraction à l'aide de booléens


Pour extraire ou non des éléments d'un tableu, on peut utiliser des tableaux de booléens en tant que masques. L'idée est de fournir un tableau de booléens (un masque) de même dimension que celui pour lequel on désire extraire des éléments sous certaines conditions. Lorsque la valeur du booléen dans le masque vaut `True`, l'élément correspondant du tableau est retourné ; sinon, il ne l'est pas.


```python
tableau = np.array([0, 3, 2, 5, 1, 4])
res = tableau[[True, False, True, False, True, True]]
print(res)
```

```
## [0 2 1 4]
```

Seuls les éléments en position 1, 3, 5 et 6 on été retournés.

En pratique, le masque n'est que très rarement créé par l'utilisateur, il est plutôt issu d'une instruction logique appliquée au tableau d'intérêt. Par exemple, dans notre tableau, nous pouvons dans un premier temps créer un masque de manière à identifier les éléments pairs :


```python
masque = tableau % 2 == 0
print(masque)
```

```
## [ True False  True False False  True]
```

```python
print(type(masque))
```

```
## <class 'numpy.ndarray'>
```

Une fois ce masque créé, on peut l'appliquer au tableau pour extraire uniquement les éléments pour lesquels la valeur correspondante dans le masque vaut `True` :

```python
print(tableau[masque])
```

```
## [0 2 4]
```



### Modification

Pour remplacer les valeurs d'un tableau, on utilise le signe égal (`=`) :

```python
tableau = np.array([ [1, 2, 3], [4, 5, 6], [7, 8, 9], [10, 11, 12]])
tableau[0] = [11, 22, 33]
print(tableau)
```

```
## [[11 22 33]
##  [ 4  5  6]
##  [ 7  8  9]
##  [10 11 12]]
```


Si on fournit un scalaire lors du remplacement, la valeur sera répétée pour tous les éléments de la dimension :

```python
tableau[0] = 100
print(tableau)
```

```
## [[100 100 100]
##  [  4   5   6]
##  [  7   8   9]
##  [ 10  11  12]]
```

Idem avec un découpage :


```python
tableau[0:2] = 100
print(tableau)
```

```
## [[100 100 100]
##  [100 100 100]
##  [  7   8   9]
##  [ 10  11  12]]
```

D'ailleurs, un découpage avec juste les deux points sans préciser les paramètres de début et de fin du découpage suivi d'un signe égal et d'un nombre remplace toutes les valeurs du tableau par ce nombre :

```python
tableau[:] = 0
print(tableau)
```

```
## [[0 0 0]
##  [0 0 0]
##  [0 0 0]
##  [0 0 0]]
```

### Copie de tableau

La copie d'un tableau, comme pour les listes (c.f. Section\ \@ref(copie-de-liste)), ne doit pas se faire avec le symbole égal (`=`).


```python
tableau_1 = np.array([1, 2, 3])
tableau_2 = tableau_1
```

Modifions le premier élément de `tableau_2`, et observons le contenu de `tableau_2` et de `tableau_1` :


```python
tableau_2[0] = 0
print("Tableau 1 : \n", tableau_1)
```

```
## Tableau 1 : 
##  [0 2 3]
```

```python
print("Tableau 2 : \n", tableau_2)
```

```
## Tableau 2 : 
##  [0 2 3]
```


Comme on peut le constater, le fait d'avoir utilisé le signe égal a simplement créé une référence et non pas une copie.

Pour effectuer une copie de tableaux, plusieurs façons existent. Parmi elles, l'utilisation de la fonction `np.array()` :

```python
tableau_1 = np.array([1, 2, 3])
tableau_2 = np.array(tableau_1)
tableau_2[0] = 0
print("tableau_1 : ", tableau_1)
```

```
## tableau_1 :  [1 2 3]
```

```python
print("tableau_2 : ", tableau_2)
```

```
## tableau_2 :  [0 2 3]
```

On peut également utiliser la méthode `copy()` :

```python
tableau_1 = np.array([1, 2, 3])
tableau_2 = tableau_1.copy()
tableau_2[0] = 0
print("tableau_1 : ", tableau_1)
```

```
## tableau_1 :  [1 2 3]
```

```python
print("tableau_2 : ", tableau_2)
```

```
## tableau_2 :  [0 2 3]
```

On peut noter que lorsque l'on fait un découpement, un nouvel objet est créé, pas une référence :


```python
tableau_1 = np.array([1, 2, 3, 4])
tableau_2 = tableau_1[:2]
tableau_2[0] = 0
print("tableau_1 : ", tableau_1)
```

```
## tableau_1 :  [0 2 3 4]
```

```python
print("tableau_2 : ", tableau_2)
```

```
## tableau_2 :  [0 2]
```


### Tri

La librairie `NumPy` fournit une fonction pour trier les tableaux : `sort()`.

```python
tableau = np.array([3, 2, 5, 1, 6, 5])
print("Tableau trié : ", np.sort(tableau))
```

```
## Tableau trié :  [1 2 3 5 5 6]
```

```python
print("Tableau : ", tableau)
```

```
## Tableau :  [3 2 5 1 6 5]
```

Comme on peut le constater, la fonction `sort()` de `NumPy` propose une vue : le tableau n'est pas modifié, ce qui n'est  pas le cas si on utilise la méthode `sort()` :

```python
tableau = np.array([3, 2, 5, 1, 6, 5])
tableau.sort()
print("Le tableau a été modifié : ", tableau)
```

```
## Le tableau a été modifié :  [1 2 3 5 5 6]
```

### Transposition {#transposition-tableau}

Pour obtenir la transposée d'un tableau, on fait appel à l'attribut `T`. Il faut noter que l'on obtient une vue de l'objet, que cela ne le modifie pas.


```python
tableau = np.array([3, 2, 5, 1, 6, 5])
tableau.shape = (3,2)
print("Tableau : \n", tableau)
```

```
## Tableau : 
##  [[3 2]
##  [5 1]
##  [6 5]]
```

```python
print("Tableau transposé : \n", tableau.T)
```

```
## Tableau transposé : 
##  [[3 5 6]
##  [2 1 5]]
```

On peut également utiliser la fonction `transpose()` de `NumPy` :

```python
print(np.transpose(tableau))
```

```
## [[3 5 6]
##  [2 1 5]]
```

Attention, si on assigne un nom à la transposée, que ce soit en utilisant l'attribut `T` ou la méthode `np.transpose()`, cela créé une référence, pas une copie d'élément...

```python
tableau_transpose = np.transpose(tableau)
tableau_transpose[0,0] = 99
print("tableau : \n", tableau)
```

```
## tableau : 
##  [[99  2]
##  [ 5  1]
##  [ 6  5]]
```

```python
print("tableau_transpose : \n", tableau_transpose)
```

```
## tableau_transpose : 
##  [[99  5  6]
##  [ 2  1  5]]
```

Pour savoir si un tableau est une vue ou non, on peut afficher l'attribut `base`, qui retourne `None` si ce n'est pas le cas :

```python
print("tableau : ", tableau.base)
```

```
## tableau :  None
```

```python
print("tableau_transpose : ", tableau_transpose.base)
```

```
## tableau_transpose :  [[99  2]
##  [ 5  1]
##  [ 6  5]]
```


### Opérations sur les tableaux

Il est possible d'utiliser des opérateurs sur les tableaux. Leur effet nécessite quelques explications.

#### Opérateurs `+` et `-`

Lorsque l'opérateur `+` (`-`) est utilisé entre deux tableaux de même dimension, une addition (soustraction) terme à terme est effectuée :

```python
t_1 = np.array([1, 2, 3, 4])
t_2 = np.array([5, 6, 7, 8])
t_3 = np.array([[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]])
t_4 = np.array([[13, 14, 15, 16], [17, 18, 19, 20], [21, 22, 23, 24]])
t_1 + t_2
```


```python
t_3 + t_4
```


```python
t_1 - t_2
```

Lorsque l'opérateur `+` (`-`) est utilisé entre un scalaire et un tableau, le scalaire est ajouté (soustrait) à tous les éléments du tableau :

```python
print("t_1 + 3 : \n", t_1 + 3)
```

```
## t_1 + 3 : 
##  [4 5 6 7]
```

```python
print("t_1 + 3. : \n", t_1 + 3.)
```

```
## t_1 + 3. : 
##  [4. 5. 6. 7.]
```

```python
print("t_3 + 3 : \n", t_3 + 3)
```

```
## t_3 + 3 : 
##  [[ 4  5  6  7]
##  [ 8  9 10 11]
##  [12 13 14 15]]
```

```python
print("t_3 - 3 : \n", t_3 - 3)
```

```
## t_3 - 3 : 
##  [[-2 -1  0  1]
##  [ 2  3  4  5]
##  [ 6  7  8  9]]
```

#### Opérateurs `*` et `/`

Lorsque l'opérateur `*` (`/`) est utilisé entre deux tableaux de même dimension, une multiplication (division) terme à terme est effectuée :

```python
t_1 * t_2
```


```python
t_3 * t_4
```


```python
t_3 / t_4
```


Lorsque l'opérateur `*` (`/`) est utilisé entre un scalaire et un tableau, tous les éléments du tableau sont multipliés (divisés) par ce scalaire :

```python
print("t_1 * 3 : \n", t_1 * 3)
```

```
## t_1 * 3 : 
##  [ 3  6  9 12]
```

```python
print("t_1 / 3 : \n", t_1 / 3)
```

```
## t_1 / 3 : 
##  [0.33333333 0.66666667 1.         1.33333333]
```


#### Puissance

Il est également possible d'élever chaque nombre d'un tableau à une puissance donnée :

```python
print("t_1 ** 3 : \n", t_1 ** 3)
```

```
## t_1 ** 3 : 
##  [ 1  8 27 64]
```


#### Opérations sur des matrices

En plus des opérations/soustraction/multiplication/division terme à terme ou par un scalaire, il est possible d'effectuer certains calculs sur des tableaux à deux dimension.

Nous avons déjà vu la tranposée en Section\ \@ref(transposition-tableau).

Pour effectuer un produit matriciel, `NumPy` fournit la fonction `dot()` :

```python
np.dot(t_3, t_4.T)
```

Il faut bien s'assurer d'avoir des matrices compatibles, sinon, une erreur sera retournée :

```python
np.dot(t_3, t_4)
```

```
## ValueError: shapes (3,4) and (3,4) not aligned: 4 (dim 1) != 3 (dim 0)
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```

Le produit matriciel peut également s'obtenir à l'aide de l'opérateur `@` :


```python
t_3 @ t_4.T
```

Le produit d'un vecteur avec une matrice est également possible :

```python
np.dot(t_1, t_3.T)
```


### Quelques constantes


`NumPy` propose quelques constantes, dont certaines sont reportées dans le Tableau\ \@ref(tab:constantes-numpy).

| Code | Description |
| ------------: | ----------------------------------------------------: |
| `np.inf` | Infini (on obtient $-\infty$ en écrivant `-np.inf` ou `np.NINF`) |
| `np.nan` | Représentation en tant que nombre à virgule flottante de Not a Number |
| `np.e` | Constante d'Euler ($e$) |
| `np.euler_gamma` | Constante d'Euler-Mascheroni ($\gamma$) |
| `np.pi` | Nombre Pi ($\pi$) |

Table: (#tab:constantes-numpy) Codes de formatages


## Statistiques descriptives


`NumP` propose des fonctions et méthodes pour effectuer des statistiques descriptives (moyenne, )


### Génération de nombres aléatoires



# Manipulation de données avec Pandas {#pandas}

## Importation et exportation de données

### Fichiers Excel {#pandas-importation-excel}

## Sélection

## Filtrage

## Retrait des valeurs dupliquées

## Modification des colonnes

## Tri

## Jointures

## Agrégation

## Stacking et unstacking






# Visualisation de données

# Programmation parallèle

# References







<!--chapter:end:python_for_economists.Rmd-->

