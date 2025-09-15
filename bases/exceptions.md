---
icon: triangle-exclamation
---

# Exceptions

## Exceptions : les bases

En Python, lorsqu’une erreur survient, le programme s’arrête et génère une **exception**.\
Exemple : diviser par zéro produit une exception de type `ZeroDivisionError`.

On peut intercepter ces erreurs avec un bloc `try ... except`.\
👉 Le mot-clé après `except` correspond au **type précis de l’exception** que l’on veut gérer.

### Exemple : division par zéro

```python
try:
    x = 10 / 0
except ZeroDivisionError:   # on intercepte uniquement les divisions par zéro
    print("On ne peut pas diviser par zéro !")
```

Sans l’`except`, Python aurait affiché un message d’erreur et interrompu le programme.\
Ici, on « attrape » l’erreur et on choisit quoi faire à la place.

## Exceptions : notions avancées

### Intercepter plusieurs types d’erreurs

On peut écrire plusieurs `except` différents selon les cas :

```python
try:
    with open("data.csv") as f:
        contenu = f.read()
except FileNotFoundError:   # si le fichier n’existe pas
    print("Fichier introuvable.")
except PermissionError:     # si on n’a pas le droit de l’ouvrir
    print("Pas la permission d’ouvrir ce fichier.")
```

👉 Ici, après `except` on a mis `FileNotFoundError` ou `PermissionError`, qui sont deux classes d’exception intégrées à Python.\
Il en existe des dizaines (ex : `ValueError`, `TypeError`, `KeyError`…), chacune correspondant à un type d’erreur bien précis.

### Intercepter plusieurs exceptions en même temps

On peut regrouper plusieurs types d’erreurs dans le même bloc :

```python
try:
    num = int("abc")   # conversion impossible
except (ValueError, TypeError):
    print("Erreur de type ou de valeur.")
```

### else et finally

* `else` : s’exécute seulement si **aucune exception** n’a eu lieu.
* `finally` : s’exécute **toujours**, qu’il y ait eu une exception ou non (pratique pour fermer un fichier, libérer une ressource, etc.).

```python
try:
    nombre = int("42")
except ValueError:
    print("Impossible de convertir en entier.")
else:
    print("Conversion réussie :", nombre)
finally:
    print("Fin de l’opération.")
>>> 
Conversion réussie : 42
Fin de l’opération.
```

👉 Retenir :

* après `except`, on met **le nom de l’exception à gérer** ;
* ce nom correspond en réalité à une **classe d’exception Python** ;
* on peut définir plusieurs `except`, ou les combiner, selon les besoins.

## Exceptions les plus courantes&#x20;

Voici un **aperçu des plus courantes et utiles** pour l’enseignement ou la pratique courante :

***

### 🌍 Exceptions générales

* **`Exception`** : classe de base pour la plupart des erreurs (à éviter seule, car elle capture “trop large”).
* **`BaseException`** : classe racine de toutes les exceptions (rarement utilisée directement).

***

### 🔢 Erreurs de type et de valeur

* **`TypeError`** : mauvais type d’objet (ex: addition entre une chaîne et un entier).
* **`ValueError`** : valeur invalide (ex: convertir `"abc"` en entier avec `int("abc")`).
* **`IndexError`** : index de liste ou tuple hors limite.
* **`KeyError`** : clé inexistante dans un dictionnaire.
* **`AttributeError`** : attribut ou méthode inexistante pour un objet.

***

### 📂 Fichiers et entrées-sorties

* **`FileNotFoundError`** : fichier introuvable.
* **`PermissionError`** : pas les droits d’accès.
* **`IsADirectoryError`** / **`NotADirectoryError`** : confusion fichier ↔ répertoire.
* **`IOError`** : problème générique d’entrée-sortie (souvent remplacé par plus spécifique).

***

### ➗ Nombres et maths

* **`ZeroDivisionError`** : division par zéro.
* **`OverflowError`** : résultat numérique trop grand.
* **`FloatingPointError`** : erreur dans un calcul flottant.

***

### 🧵 Logique et programmation

* **`AssertionError`** : déclenchée par un `assert` qui échoue.
* **`ImportError`** / **`ModuleNotFoundError`** : problème d’importation de module.
* **`IndentationError`** : indentation incorrecte (sous-type de `SyntaxError`).
* **`SyntaxError`** : code Python invalide.
* **`NameError`** : variable non définie.
* **`UnboundLocalError`** : variable locale utilisée avant affectation.

***

### 🧵 Concurrence et exécution

* **`TimeoutError`** : dépassement de délai.
* **`RuntimeError`** : erreur d’exécution générique.
* **`RecursionError`** : récursion trop profonde.

***

### 🛑 Exceptions spéciales du noyau Python

* **`KeyboardInterrupt`** : déclenchée quand l’utilisateur interrompt (Ctrl+C).
* **`SystemExit`** : levée par `sys.exit()`.
* **`GeneratorExit`** : levée quand un générateur est fermé.

***

👉 En pratique, vous allez rencontrer surtout :

* `ZeroDivisionError`, `ValueError`, `TypeError`, `IndexError`, `KeyError`, `FileNotFoundError`.
