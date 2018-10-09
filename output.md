---
title: "Python pour les économistes"
author: "Ewen Gallic"
date: "Octobre
2018"
knit: "bookdown::render_book"
documentclass: book
bibliography:
[biblio.bib]
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
      edit:
https://github.com/3wen/Python_pour_economistes/edit/master/%s
bookdown::pdf_book:
    highlight: tango
    keep_tex: yes
    includes:
in_header: styles/mystyle_books.tex
  bookdown::epub_book:
    stylesheet:
styles/style.css
---





# Propos liminaires {-}

<!-- ```{r, echo=F} -->
<!--
invisible(py_config()) -->
<!-- ``` -->





Ces notes de cours ont été
réalisées dans le cadre d'un enseignement d'introduction à Python adressé à des
étudiants du parcours Économétrie et Big Data de [l'École d'Economie d'Aix-
Marseille / Aix-Marseille School of Economics (AMSE)](https://www.amse-
aixmarseille.fr/) d'Aix-Marseille Université.


## Objectifs

Cet ouvrage a pour
but l'initiation au langage de programmation Python, afin d'être capable de s'en
servir de manière efficace et autonome. Le lecteur peut exécuter tous les
exemples fournis (et est vivement encouragé à le faire). Des exercices viennent
clore certains chapitres, pour mieux s'approprier les notions couvertes au fur
et à mesure de la lecture.


Bien évidemment, Python étant un langage très
vaste, ces notes ne sauraient et n'ont pas pour vocation à être exhaustives de
l'utilisation de ce langage informatique.




## À qui s'adressent ces notes ?
Dans un premier temps, cet ouvrage s'adresse aux débutants qui souhaientent
apprendre les bases en Python. Il est à destination des étudiants de l'AMSE mais
pourrait intéresser des individus ayant une approche de la donnée à travers la
discipline économique désirant découvrir Python.

# Introduction


Ce document
est construit principalement à l'aide de différentes références, parmi
lesquelles :

- des livres : @briggs_2013_python, @grus_2015_data,
@vanderplas2016python, @mckinney_2017_python ;
- des (excellents) notebooks :
@navaro_python.



## Historique


Python est un langage de programmation multi
plates-formes, écrit en `C`, placé sous une licence libre. Il s'agit d'un
langage interprété, c'est-à-dire qu'il nécessite un interprète pour exécuter les
commandes, et n'a pas de phase de compilation. Sa première version publique date
de 1991. L'auteur principal, [Guido van
Rossum](https://en.wikipedia.org/wiki/Guido_van_Rossum) avait commencé à
travailler sur ce langage de programmation durant la fin des années 1980. Le nom
accordé au langage Python provient de l'intérêt de son créateur principal pour
une série télévisée britannique diffusée sur la BBC intitulée "*Monty Python's
Flying Circus*".

La popularité de Python a connu une croissance forte ces
dernières années, comme le confirment les résultats de sondages proposés par
[Stack Overflow](https://stackoverflow.com/) depuis 2011. Stack Overflow propose
à ses utilisateurs de répondre à une enquête dans laquelle de nombreuses
questions leur sont proposées, afin de décrire leur expérience en tant que
développeur. [Les résultats de l'enquête de
2018](https://insights.stackoverflow.com/survey/2018#technology) montrent une
nouvelle avancée de l'utilisation de Python par les développeurs. En effet,
comme le montre la Figure\ \@ref(fig:intro-stack-langages), 38.8% des répondants
indiquent développer en Python, soit 6.8 points de pourcentage de plus qu'un an
auparavant, ce qui fait de ce langage de programmation celui dont la croissance
a été la plus importante entre 2017 et 2018.



## Versions

Ces notes de cours
visent à fournir une introduction à Python, dans sa version 3.x. En ce sens, les
exemples fournis corresponderont à cette version, non pas aux précédentes.
Comparativement à la version 2.7, la version 3.0 a apporté des modofications
profondes. Il faut noter que Python 2.7 prendra "[sa
retraite](https://pythonclock.org/)" le premier janvier 2020. Passée cette date,
le support ne sera plus assuré.

## Espace de travail

Il existe de nombreux
environnements dans lesquels programmer en Python. Nous allons en présenter
succinctement quelques uns.

Il est supposé ici que vous vous avez installé
[Anaconda](https://www.anaconda.com/) sur votre poste. Anaconda est une
distribution gratuite et open source des langages de programmation Python et R
pour les applications en *data science* et apprentissage automatique. Par
ailleurs, lorsqu'il est fait mention du terminal dans les notes, il est supposé
que le système d'exploitation de votre machine est soit Linux, soit Mac OS.

###
Python dans un terminal

Il est possible d'appeler Python depuis un terminal, en
exécutant la commande suivante (sous Windows : dans le menu démarrer, lancer le
logiciel "Python 3.6") :

```python
python
```

Ce qui donne le rendu visible sur la Figure\ \@ref(fig:intro-python-terminal) :
On note la présence des caractères `>>>` (*prompt*), qui invitent l'utilisateur
à inscrie une commande. Les expressions sont évaluées une fois qu'elle sont
soumises (à l'aide de la touche `ENTREE`) et le résultat est donné, lorsqu'il
n'y a pas d'erreur dans le code.

Par exemple, lorsque l'on évalue `2+1` :

```python
>>> 2+1
3
>>>
```

On note la présence du *prompt* à la fin, indiquant que Python est prêt à
recevoir de nouvelles instructions.


### IPython

Il existe un environnement un
peu plus chaleureux que Python dans le terminal : IPython. Il s'agit également
d'un terminal interactif, mais avec davantages de fonctionnalités, notamment la
coloration syntaxique ou l'auto-complétion (en utilisant la touche de
tabulation).

Pour lancer IPython, on peut ouvrir un terminal et taper (puis
valider) :

```python
ipython
```

On peut également lancer IPython depuis la fenêtre d'accueil d'Anaconda, en
cliquant sur le bouton `Launch` de l'application `qtconsole`, visible sur la
Figure\ \@ref(fig:intro-anaconda-navigator).





La console IPython, une fois
lancée, ressemble à ceci :


Soumettons une instruction simple pour évaluation à
Python :

```python
print("Hello World")
```

Le résultat donne :

```python
In [1]: print("Hello World")
Hello World

In [2]:
```

Plusieurs choses sont à noter. Premièrement, on note qu'à la fin de l'exécution
de l'instruction, IPython nous indique qu'il est prêt à recevoir de nouvelles
instruction, par la présence du *prompt* `In [2]:`. Le numéro entre les crochets
désigne le numéro de l'instruction. On note qu'il est passé de 1 à 2 après
l'exécution. Ensuite, on note que le résultat de l'appel à la fonction
`print()`, avec la chaîne de caractères (délimitée par des guillemets), affiche
à l'écran ce qui était contenu entre les parenthèses.

### Spyder

Tandis que
lorsqu'on utilise Python via un terminal, il est préférable d'avoir un éditeur
de texte ouvert à côté (pour pouvoir sauvegarder les instructions), comme, par
exemple, [Sublime Text](https://www.sublimetext.com/) sous Linux ou Mac OS, ou
[notepad++](https://notepad-plus-plus.org/) sous Windows.

Une autre alternative
consiste à utiliser un environnement de développement (IDE, pour *Integrated
development environment*) unique proposant notamment, à la fois un éditeur et
une console. C'est ce que propose [Spyder](https://www.spyder-ide.org/), avec en
outre de nombreuses fonctionnalités supplémentaires, comme la gestion de projet,
un explorateur de fichier, un historique des commandes, un débugger, etc.


Pour
lancer Spyder, on peut passer par un terminal, en évaluant tout simplement
`Spyder` (ou en lançant le logiciel depuis le menu démarrer sous Windows). Il
est également possible de lancer Spyder depuis Anaconda.

L'environnement de
développement, comme visible sur la Figure\ \@ref(fig:intro-spyder), se
décompose en plusieurs fenêtres :

- à gauche : l'éditeur de script ;
- en haut
à droite : une fenêtre permettant d'afficher l'aide de Python, l'arborescence du
système ou encore les variables créées ;
- en bas à droite : une ou plusieurs
consoles.




### Jupyter

Il existe une interface graphique par navigateur
d'IPython, appelée [Jupyter Notebook](http://jupyter.org/). Il s'agit d'une
application en open-source permettant de créer et partager des documents qui
contiennent du code, des équations, des représentations graphiques et du texte.
Il est possible de faire figurer et exécuter des codes de langages différents
dans les notebook Jupyter.


Pour lancer Jupyter, on peut passer par Anaconda.
Après avoir cliqué sur le bouton `Launch`, de Jupyter Notebook, le navigateur
web se lance et propose une arborescence, comme montré sur la Figure\
\@ref(fig:intro-jupyter). Sans que l'on s'en rendiez compte, un serveur local
web a été lancé ainsi qu'un processus Python (un *kernel*).

Si le navigateur en
se lance pas automatiquement, on peut accéder à la page qui aurait dû
s'afficher, en se rendant à l'adresse suivante : http://localhost:8890/tree?.
Pour aborder les principales fonctions de Jupyter, nous allons créer un dossier
`jupyter` dans un répertoire de notre choix. Une fois ce dossier créé, y
naviguer à travers l'arborescence de Jupyter, dans le navigateur web.


Une fois
dans le dossier, créer un nouveau Notebook `Python 3` (en cliquant sur le bouton
`New` en haut à gauche de la fenêtre, puis sur  Python 3`).


Un notebook
intitulé `Untitled` vient d'être créé, la page affiche un document vide, comme
visible sur la Figure\ \@ref(fig:intro-jupyter-notebook).





Si on regarde
dans notre explorateur de fichier, dans le dossier `jupyter` fraîchement créé,
un nouveau fichier est apparu : `Untitled.ipynb`.





#### Évaluation d'une
instruction

Retournons dans le navigateur web, sur la page affichant notre
*notebook*.

En dessous de la barre des menus, on note la présence d'une zone
encadrée, **une cellule**, commençant, à l'instar de ce que l'on voyait dans la
console sur IPython, par `IN []:`. À droite, la zone grisée nous invite à
soumettre des instructions en Python.

Inscrivons :

```python
2+1
```

Pour soumettre l'instruction à évaluation, il existe plusieurs manières (il
s'assurer d'avoir cliqué à l'intérieur de la cellule) :

- dans la barre des
menus : `Cell > Run Cells` ;
- dans la barre des raccourcis : bouton `Run` ;
-
avec le clavier : maintenir la touche `CTRL`et presser sur `Entree`.



####
Cellules de texte

Un des intérêts des *notebooks* est qu'il est possible
d'ajouter des cellules de texte.

Ajoutons une cellule en-dessous de la
première. Pour ce faire, on peut procéder soit :

- par la barre de menu :
`Insert > Insert Cell Below` (pour insérer une cellule en-dessous ; si on désire
une insertion au-dessus, il suffit de choisir `Insert Cell Above`) ;
- en
cliquant dans le cadre de la cellule à partir de laquelle on désire faire un
ajout (n'importe où, sauf dans la zone grisée de code, de manière à passer en
mode `commande`), puis en appuyant sur la touche `B` du clavier (`A` pour une
insertion au-dessus).

La nouvelle cellule appelle à nouveau à inscrire une
instruction en Python. Pour indiquer que le contenu doit être interprété comme
du texte, il est nécessaire de le préciser. Encore une fois, plusieurs méthodes
permettent de le faire :

- par la barre de menu : `Cell > Cell Type > Markdown`
;
- par la barre des raccourcis : dans le menu déroulant où est inscrit `Code`,
en sélectionnant `Markdown` ;
- en mode commande (après avoir cliqué à
l'intérieur du cadre de la cellule, mais pas dans la zone de code), en appuyant
sur la touche `M` du clavier.

La cellule est alors prête à recevoir du texte,
rédigé en markdown. Pour plus d'informations sur la rédaction en Markdown, se
référer à cette [antisèche](https://github.com/adam-p/markdown-
here/wiki/Markdown-Cheatsheet) par exemple.

Entrons quelques lignes de texte
pour voir très rapidement le fonctionnement des cellules rédigées en Markdown.

```python
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



Reste alors à l'évaluer, comme s'il s'agissait
d'une cellule contenant une instruction Python, pour basculer vers un affichage
Markdown (`CTRL` et `ENTREE`).

Pour **éditer le texte** une fois que l'on a
basculé en markdown, un simple double-clic dans la zone de texte de la cellule
fait l'affaire.

Pour **changer le type de la cellule pour qu'elle devienne du
code** :

- par la barre de menu : `Cell > Cell Type > Code` ;
- par la barre
des raccourcis : dans le menu déroulant où est inscrit `Code`, en sélectionnant
`Code` ;
- en mode commande, appuyer sur la touche du clavier `Y`.


####
Suppression d'une cellule

Pour supprimer une cellule :

- par la barre de menu
: `Edit > Delete Cells` ;
- par la barre des raccourcis : icône en forme de
ciseaux ;
- en mode commande, appuyer deux fois sur la touche du clavier `D`.
## Les variables

### Assignation et suppression

Lorsque nous avons évalué les
instructions `2+1` précédemment, le résultat s'est affiché dans la console, mais
il n'a pas été enregistré. Dans de nombreux cas, il est utile de conserver le
contenu du résultat dans un objet, pour pouvoir le réutiliser par la suite. Pour
ce faire, on utilise des *variables*. Pour créer une variable, on utilise le
signe d'égalité (`=`), que l'on fait suivre par ce que l'on veut sauvegarder (du
texte, un nombre, plusieurs nombres, etc.) et précéder par le nom que l'on
utilisera pour désigner cette variable.

Par exemple, si on souhaite stocker le
résultat du calcul `2+1` dans une variable que l'on nommera `x`, il faudra
écrire :

```python
x = 2+1
```

Pour afficher la valeur de notre variable `x`, on fait appel à la fonction
`print()` :

```python
print(x)
```

```python
## 3
```

Pour changer la valeur de la variable, il suffit de faire une nouvelle
assignation :

```python
x = 4
print(x)
```

```python
## 4
```

Il est également possible de donner plus d'un nom à un même contenu (on réalise
une copie de `x`) :

```python
x = 4;
y = x;
print(y)
```

```python
## 4
```

Si on modifie la copie, l'original ne sera pas affecté :

```python
y = 0
print(y)
```

```python
## 0
```

```python
print(x)
```

```python
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

```python
## NameError: name 'y' is not defined
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```

Mais on note que la variable `x` n'a pas été supprimée :

```python
print(x)
```

```python
## 4
```

### Conventions de nommage

Le nom d'une variable peut être composé de
caractères alphanumériques ainsi que du trait de soulignement (`_`) (il n'y a
pas de limite sur la longueur du nom). Il est proscrit de faire commencer le nom
de la variable par un nombre. Il est également interdit de faire figurer une
espace dans le nom d'une variable.

Pour accroitre la lisibilité du nom des
variables, plusieurs méthodes existes. Nous adopterons la suivante :

- toutes
les lettres en minuscule ;
- la séparation des termes par un trait de
soulignement.

Exemple, pour une variable contenant la valeur de l'identifiant
d'un utilisateur : `id_utilisateur`.

Il faut noter que le nom des variables est
**sensible à la casse** :

```python
x = "toto"
print(x)
```

```python
## toto
```

```python
print(X)
```

```python
## NameError: name 'X' is not defined
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
```

## Les commentaires


Pour ajouter des commentaires en python, il existe
plusieurs façons.


Une des manières de faire est d'utiliser le symbole dièse
(`#`) pour effectuer un **commentaire sur une seule ligne**. Tout ce qui suit le
dièse jusqu'à la fin de la ligne ne sera pas évalué par Python. En revanche, ce
qui vient avant le dièse le sera.

```python
# Un commentaire print("Bonjour")
print("Hello") # Un autre commentaire
```

```python
## Hello
```

L'introduction d'un **bloc de commentaires** (des commentaires sur plusieurs
lignes) s'effectue quant à elle en entourant ce qui est ) commenter d'un
délimiteur : trois guillemets simples ou doubles :

```python
"""
Un commentaire qui commencer sur une ligne
et qui continue sur une autre
et s'arrête à la troisième
"""
```

## Les modules et les packages


Certaines fonctions de base en Python sont
chargées par défaut. D'autres, nécessitent de charger un **module**. Ces modules
sont des fichiers qui contiennent des **définitions** ainsi que des
**instructions**.

Lorsque plusieurs modules sont réunis pour offrir un ensemble
de fonctions, on parle alors de _**package**_.

Parmi les *packages* qui seront
utilisés dans ces notes, on peut citer :

- [NumPy](http://www.numpy.org/), un
*package* fondamental pour effectuer des calculs scientifiques ;
-
[pandas](https://pandas.pydata.org/), un *package* permettant de manipuler
facilement les données et de les analyser ;
-
[Matplotlib](https://matplotlib.org/), un *package* permettant de réaliser des
graphiques.

Pour charger un module (ou un *package*), on utilise la commande
`import`. Par exemple, pour charger le *package* `pandas` :

```python
import pandas
```

Ce qui permet de faire appel à des fonctions contenues dans le module ou le
*package*. Par exemple, ici, on peut faire appel à la fonction `Series()`,
contenue dans le *package* `pandas`, permettant de créer un tableau de données
indexées à une dimension :

```python
x = pandas.Series([1, 5, 4])
print(x)
```

```python
## 0    1
## 1    5
## 2    4
## dtype: int64
```

Il est possible de donner un alias au module ou au *package* que l'on importe,
en le précisant à l'aide de la syntaxe suivante :

```python
import module as alias
```

Cette pratique est courante pour abréger les noms des modules que l'on va être
amené à utiliser beaucoup. Par exemple, pour `pandas`, il est coutume d'écourter
le nom en `pd` :

```python
import pandas as pd
x = pd.Series([1, 5, 4])
print(x)
```

```python
## 0    1
## 1    5
## 2    4
## dtype: int64
```

On peut également importer une seule fonction d'un module, et lui attribuer
(optionnellement) un alias. Par exemple, avec la fonction `pyplot` du *package*
`matplotlib`, il est coutume de faire comme suit :

```python
import matplotlib
import matplotlib.pyplot  as plt
import numpy  as np
x = np.arange(0, 5, 0.1);
y = np.sin(x)
plt.plot(x, y)
```

```python
## FileNotFoundError: [Errno 2] No such file or directory: 'figs/intro_pyplot.png'
## 
## Detailed traceback: 
##   File "<string>", line 1, in <module>
##   File "/anaconda3/lib/python3.6/site-packages/matplotlib/figure.py", line 2035, in savefig
##     self.canvas.print_figure(fname, **kwargs)
##   File "/anaconda3/lib/python3.6/site-packages/matplotlib/backend_bases.py", line 2263, in print_figure
##     **kwargs)
##   File "/anaconda3/lib/python3.6/site-packages/matplotlib/backends/backend_agg.py", line 526, in print_png
##     with cbook.open_file_cm(filename_or_obj, "wb") as fh:
##   File "/anaconda3/lib/python3.6/contextlib.py", line 81, in __enter__
##     return next(self.gen)
##   File "/anaconda3/lib/python3.6/site-packages/matplotlib/cbook/__init__.py", line 624, in open_file_cm
##     fh, opened = to_filehandle(path_or_file, mode, True, encoding)
##   File "/anaconda3/lib/python3.6/site-packages/matplotlib/cbook/__init__.py", line 609, in to_filehandle
##     fh = io.open(fname, flag, encoding=encoding)
```

## L'aide


Pour conclure cette introduction, il semble important de mentionner
la présence de l'**aide** et de la **documentation** en Python.

Pour obtenir
des informations sur des fonctions, il est possible de se référer à la
[documentation en ligne](https://docs.python.org/3/). Il est également possible
d'obtenir de l'aide à l'intérieur de l'environnement que l'on utilise, en
utilisant le point d'interrogation (`?`).

Par exemple, lorsque l'on utilise
IPython (ce qui, rappelons-le, est le cas dans Jupyter), on peut accéder à
l'aide à travers différentes syntaxes :

- `?` : fournit une introduction et un
aperçu des fonctionnalités offertes en Python (on la quitte avec la touche `ESC`
par exemple);
- `object?` : fournit des détails au sujet de `'object'` (par
exemple `x?` ou encore `plt.plot?`) ;
- `object??` : plus de détails à propos de
`'object'` ;
- `%quickref` : référence courte sur les syntaxes en Python ;
-
`help()` : accès à l'aide de Python.


*Note* : la touche de **tabulation** du
clavier permet non seulement une **autocomplétion**, mais aussi une
**exploration du contenu** d'un objet ou module.

Par ailleurs, lorsqu'il s'agit
de trouver de l'aide sur un problème plus complèxe, le bon réflèxe à adopter est
de ne pas hésiter à chercher sur un moteur de recherche, dans des mailing-lists
et bien évidemment sur les nombreuses questions sur [Stack
Overflow](https://stackoverflow.com).



# Types de données

Il existe quelques
types de données intégrés dans Python. Nous allons dans cette partie évoquer les
chaînes de caractères, les valeurs numériques, les bouléens (`TRUE`/`FALSE`), la
valeur `null` et les dates et temps.


## Chaînes de caractères


Une chaîne de
caractères, ou *string* en anglais, est une collection de caractères comme des
lettres, des nombres, des espaces, des signes de ponctuation, etc.

Les chaînes
de caractères sont repérées à l'aide de guillemets simples, doubles, ou triples.
Voici un exemple :

```python
x = "Hello World"
```

Pour afficher dans la console le contenu de notre variable `x` contenant la
chaîne de caractères, on fait appel à la fonction `print()` :

```python
print(x)
```

```python
## Hello World
```

Comme indiqué juste avant, des guillemets simples peuvent être utilisés pour
créer une chaîne de caractères :

```python
y = 'How are you?'
print(y)
```

```python
## How are you?
```

Pour faire figurer des apostrophes dans une chaîne de caractères créée à l'aide
de guillemets simples, il est nécessaire d'utiliser un caracrère d'échappement :
une barre oblique inversée (`\`) :

```python
z = 'I\'m fine'
print(z)
```

```python
## I'm fine
```

On peut noter que si la chaîne de caractères est créée à l'aide de guillemets
doubles, il n'est pas nécessaire d'avoir recours au caractère d'échappement :

```python
z = "I'm \"fine\""
print(z)
```

```python
## I'm "fine"
```

Pour indiquer un retour à la ligne, on utilise la chaîne `\n` :

```python
x = "Hello, \nWorld"
print(x)
```

```python
## Hello, 
## World
```

Dans le cas de chaînes de caractères sur **plusieurs lignes**, le fait
d'utiliser des guillemets simples ou doubles renverra une erreur (*EOL while
scanning trial literal*, *i.e.*, détection d'une erreur de syntaxe, Python
s'attendait à quelque chose d'autre à la fin de la ligne). Pour écrire une
chaîne de caractères sur plusieurs lignes, Python propose d'utiliser trois fois
des guillemets (simples ou doubles) en début et fin de chaîne :

```python
x = """Hello,
World"""
print(x)
```

```python
## Hello,
## World
```
