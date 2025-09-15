---
description: Dataframes et Series
icon: file-plus
---

# Créer  un Dataframe

Le cœur de Pandas est la **DataFrame** : un tableau à 2 dimensions avec des lignes et colonnes, un peu comme une feuille Excel.\
Avant de travailler sur des données (filtrer, grouper, tracer…), il faut savoir comment créer une DataFrame.

## 1. À partir d’un dictionnaire

C’est la méthode la plus simple pour de petits exemples.\
Chaque clé du dictionnaire devient une **colonne**, et les listes associées contiennent les valeurs.

```python
import pandas as pd

data = {
    "Nom": ["Alice", "Bob", "Charlie"],
    "Âge": [25, 30, 35],
    "Ville": ["Paris", "Lyon", "Marseille"]
}

df = pd.DataFrame(data)
print(df)
>>>
       Nom  Âge      Ville
0    Alice   25      Paris
1      Bob   30       Lyon
2  Charlie   35  Marseille
```

## 2. À partir d’une liste de dictionnaires

Chaque dictionnaire correspond à une ligne.\
Pratique quand les données viennent d’un JSON ou d’une API.

```python
data = [
    {"Nom": "Alice", "Âge": 25, "Ville": "Paris"},
    {"Nom": "Bob", "Âge": 30, "Ville": "Lyon"},
    {"Nom": "Charlie", "Âge": 35, "Ville": "Marseille"}
]

df = pd.DataFrame(data)
```

## 3. À partir d’une liste de listes

On peut fournir une liste de lignes + une liste de noms de colonnes.

```python
data = [
    ["Alice", 25, "Paris"],
    ["Bob", 30, "Lyon"],
    ["Charlie", 35, "Marseille"]
]

df = pd.DataFrame(data, columns=["Nom", "Âge", "Ville"])

```

## 4. Créer une DataFrame vide

Parfois utile comme point de départ.

```python
df = pd.DataFrame(columns=["Nom", "Âge", "Ville"])
print(df)
```

## 5. Series vs DataFrame

En Pandas, il existe deux structures principales :

* **Series** : tableau **1D** (une seule colonne de données, avec un index).
* **DataFrame** : tableau **2D** (plusieurs colonnes, chaque colonne étant en fait une Series).

#### Exemple : créer une Series

```python
import pandas as pd

ages = pd.Series([25, 30, 35], name="Âge")
print(ages)
>>>
0    25
1    30
2    35
Name: Âge, dtype: int64
```

👉 Ici, on a **une seule colonne** avec un index automatique (0, 1, 2).

#### Exemple : créer une DataFrame

```python
data = {
    "Nom": ["Alice", "Bob", "Charlie"],
    "Âge": [25, 30, 35]
}

df = pd.DataFrame(data)
print(df)
```

Résultat :

```
       Nom  Âge
0    Alice   25
1      Bob   30
2  Charlie   35
```

👉 Ici, on a un tableau **2D**, avec plusieurs colonnes.

#### Passer de l’un à l’autre

* Extraire une colonne d’une DataFrame → renvoie une **Series** :

```python
print(df["Âge"])
```

* Extraire plusieurs colonnes → renvoie un **DataFrame** :

```python
print(df[["Nom", "Âge"]])
```

👉 Retenir :

* Une **Series** est une seule colonne de données.
* Une **DataFrame** est un tableau complet (plusieurs Series mises ensemble).
* Chaque fois que vous manipulez une DataFrame, souvenez-vous qu’en interne, ce n’est qu’un ensemble de Series alignées sur le même index.

## 👉 Retenir

* On peut créer une DataFrame “à la main” avec des dictionnaires ou listes.
* Une DataFrame est **la structure centrale de Pandas**, que l’on manipulera ensuite avec toutes les fonctions vues dans les chapitres suivants.
* Mais très souvent vous pourrez charger directement un **fichier CSV / Excel / SQL** pour les cas réels.\
  Voir dans le prochain chapitre !&#x20;

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
