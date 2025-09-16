---
description: __main__
icon: house-blank
---

# Le rôle de \`\_\_main\_\_\`

Quand on regarde du code Python, on tombe très souvent sur la ligne suivante

```python
 ​if __name__ == "__main__":
    [...]
```

_Mais à quoi ça sert exactement ?_

***

## Comprendre `__name__` <a href="#comprendre-__name" id="comprendre-__name"></a>

En Python, chaque fichier `.py` est en réalité un **module**. Lorsqu’un fichier est exécuté, Python crée une variable spéciale appelée **`__name__`** :

* Si le fichier est exécuté **directement** (ex. `python mon_script.py`) → alors `__name__ == "__main__"`.
* Si le fichier est **importé** dans un autre script (ex. `import mon_script`) → alors `__name__ == "mon_script"`.

### Exemple simple <a href="#exemple-simple" id="exemple-simple"></a>

Imaginons un fichier `calculs.py`&#x20;

```python
def addition(a, b):
    return a + b

print("Ce message s’affiche toujours")

if __name__ == "__main__":
    # Ce code ne s'exécute QUE si on lance calculs.py directement
    print("Test :", addition(2, 3))
```

Si on exécute directement **`python calculs.py`** :

```python
Ce message s’affiche toujours
Test : 5
```

Si on importe `calculs` dans un autre script&#x20;

```python
import calculs
print(calculs.addition(10, 20))
```

Résultat&#x20;

```python
Ce message s’affiche toujours
30
```

On remarque que **la partie sous `if __name__ == "__main__":` n’a pas été exécutée** lors de l’import.&#x20;

C’est exactement son rôle : éviter que le “code de test” ou “code principal” ne s’exécute quand on utilise le fichier comme une librairie.

***

## Quand utiliser `__main__` ? <a href="#quand-utiliser-__main" id="quand-utiliser-__main"></a>

* ✅ Si ton fichier doit pouvoir être utilisé **à la fois comme script autonome** (exécuté directement) **et comme module importable** dans un autre projet.
* ✅ Pour écrire des **petits tests internes** (exécuter une fonction avec des exemples simples).
* ❌ Si ton fichier ne sera **jamais importé** ailleurs, ce n’est pas indispensable, mais c’est une **bonne habitude** à prendre.

#### Retenir <a href="#retenir" id="retenir"></a>

* `__name__` est une variable spéciale créée automatiquement par Python.
* `if __name__ == "__main__":` permet de séparer le **code exécutable** (tests, lancement du programme) du **code réutilisable** (fonctions, classes).
* C’est une bonne pratique, surtout quand on construit des projets plus gros ou qu’on veut partager son code.

***

## Exemple pratique : `__main__` et importation de modules <a href="#exemple-pratique-__main__-et-importation-de-modules" id="exemple-pratique-__main__-et-importation-de-modules"></a>

Imaginons que vous vouliez organiser votre code en **plusieurs fichiers**. C’est très courant en projet : on met les fonctions “utilitaires” dans un fichier séparé, et on les importe ensuite dans un script principal.

### Étape 1 : créer un fichier `outils.py` <a href="#etape-1-creer-un-fichier-outils.py" id="etape-1-creer-un-fichier-outils.py"></a>

```python
# outils.py

def addition(a, b):
    """Retourne la somme de deux nombres."""
    return a + b

def multiplication(a, b):
    """Retourne le produit de deux nombres."""
    return a * b

# Code de test (ne sera exécuté QUE si on lance directement ce fichier)
if __name__ == "__main__":
    print("Test des fonctions :")
    print("2 + 3 =", addition(2, 3))
    print("4 * 5 =", multiplication(4, 5))
```

Si vous exécutez **`python outils.py`**, le bloc `if __name__ == "__main__":` s’exécute et lance les tests. Mais si vous importez ce fichier depuis un autre, **ce bloc est ignoré** (il sert donc à ne pas polluer vos imports).

### Étape 2 : créer un fichier principal `main.py` <a href="#etape-2-creer-un-fichier-principal-main.py" id="etape-2-creer-un-fichier-principal-main.py"></a>

```python
# main.py

# On importe notre module "outils"
import outils

# Utilisation des fonctions définies dans outils.py
x = 7
y = 8

print("Somme :", outils.addition(x, y))
print("Produit :", outils.multiplication(x, y))
```

Exécution&#x20;

```
python main.py
```

Résultat :

```
Somme : 15
Produit : 56
```

#### Pourquoi séparer le code en modules ? <a href="#pourquoi-separer-le-code-en-modules" id="pourquoi-separer-le-code-en-modules"></a>

* Cela rend votre projet plus clair et mieux organisé.
* Vous pouvez réutiliser vos fonctions dans d’autres scripts simplement avec `import`.
* Les tests inclus sous `if __name__ == "__main__":` permettent de vérifier le module **sans perturber** les autres programmes qui l’utilisent.

***

## À Retenir <a href="#retenir-1" id="retenir-1"></a>

* Un fichier Python peut être utilisé **comme script principal** ou **comme module importable**.
* Le bloc `if __name__ == "__main__":` s’exécute seulement quand le fichier est lancé directement.
* Cette pratique est fortement conseillée pour organiser des projets un peu plus grands.

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
