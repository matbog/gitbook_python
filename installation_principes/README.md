---
icon: desktop-arrow-down
---

# Installation et premières utilisations

Avant de commencer à programmer, il est utile de comprendre quelques notions pratiques autour de Python :

* comment installer Python,
* où écrire son code (IDE / éditeur),
* comment exécuter un script (`script.py`),
* comment importer et utiliser des librairies.

## Installation de Python

* Sur Windows / Mac / Linux, la manière la plus simple est d’installer [Anaconda](https://www.anaconda.com/) :
  * il contient Python, Jupyter, **Spyder**, et de nombreuses librairies utiles pour la data science.
* Une alternative plus légère est [Miniconda](https://docs.conda.io/en/latest/miniconda.html).
* Sinon, vous pouvez télécharger directement Python sur le site officiel : [python.org](https://www.python.org/).

***

## L’IDE (environnement de développement)

Un **IDE** (_Integrated Development Environment_) est un logiciel qui facilite l’écriture de code : coloration syntaxique, exécution, débogage, ...

* [**Spyder**](https://www.spyder-ide.org/) : inclus dans Anaconda, interface proche de **Matlab**, très apprécié des étudiants en sciences et ingénierie.
* [**VS Code**](https://code.visualstudio.com/) : léger, moderne et très extensible (plugins pour Python, Git, Jupyter…).
* [**PyCharm**](https://www.jetbrains.com/fr-fr/pycharm/) : IDE complet (version Community gratuite), utile pour de gros projets.
* [**Thonny**](https://thonny.org/) : **super léger et très simple**, parfait pour débuter si on ne veut pas installer un gros IDE.
* [**Jupyter Notebook**](https://jupyter.org/) **/ JupyterLab** : idéal pour tester du code interactif, faire des cours ou des analyses de données étape par étape.

Les interfaces varient d'un IDE à l'autre, mais vous aurez toujours les éléments suivants :&#x20;

* Une zone pour <mark style="color:red;">éditer</mark> vos fichier \*.py
* Une zone avec une <mark style="color:green;">console</mark>, pour lancer votre script, ou exécuter des partie de celui-ci,&#x20;
* Une zone pour <mark style="color:yellow;">explorer les variables, voir les graphiques, l'arborescence de vos fichiers, etc.</mark>&#x20;

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

_<mark style="color:$info;">Interface de l'IDE</mark>_ [_<mark style="color:$info;">Spyder</mark>_](https://www.spyder-ide.org/)

***

## Le terminal

Le **terminal** (ou “invite de commandes”) permet de lancer Python ou vos scripts sans ouvrir l'IDE.\
Exemple : exécuter un fichier `mon_script.py` dans le dossier courant :

* Ouvrez l'invite de commande ( `cmd.exe` sous Windows),&#x20;
* Naviguez jusqu'à votre dossier,&#x20;
* Exécuter :

```bash
python mon_script.py
```

## Les fichiers `.py`

* Un fichier Python porte l’extension `.py`
* Exemple : `mon_script.py` avec ce contenu :

```python
print("C'est pas faux !")
```

Exécution dans le terminal :

```bash
python mon_script.py
```

Résultat :

```
C'est pas faux !
```

&#x20;Avec ces bases en place, vous êtes prêt à passer aux [_**Bases**_](https://matbog.gitbook.io/python/bases) de la programmation en Python !



***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
