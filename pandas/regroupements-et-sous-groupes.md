---
icon: layer-group
---

# Regroupements et Sous-groupes

## `.groupby()`

Si on veut regrouper des données (pas forcément temporelles) via un index, ou les valeurs d'une colonne, pour faire des opération dessus.&#x20;

Le mot-clé `groupby` permet de regrouper un DataFrame selon une ou plusieurs colonnes, puis d’appliquer des calculs (moyenne, somme, comptage…).\
C’est très pratique pour analyser des sous-ensembles de données.

> 🧪 **Exercices interactifs — Pandas**
>
> Pour manipuler des données tabulaires, filtrer, agréger, gérer les dates et les valeurs manquantes, ouvre le notebook :
>
> **`03_pandas.ipynb`**
>
> 👉 [Ouvrir Python Lab](https://matbog.github.io/python-lab/lab/index.html)

Créons un petit DataFrame factice :

```python
import pandas as pd

data = {
    "Ville": ["Paris", "Paris", "Lyon", "Lyon", "Marseille", "Marseille"],
    "Jour":  ["Lundi", "Mardi", "Lundi", "Mardi", "Lundi", "Mardi"],
    "PM10":  [35, 28, 42, 30, 55, 40]
}

df = pd.DataFrame(data)
print(df)
>>>
        Ville    Jour  PM10
0       Paris   Lundi    35
1       Paris   Mardi    28
2        Lyon   Lundi    42
3        Lyon   Mardi    30
4   Marseille   Lundi    55
5   Marseille   Mardi    40
```

#### Calculer une statistique par groupe

Par exemple, la concentration moyenne de PM10 par ville&#x20;

`df.groupby("Ville")["PM10"].mean()`

```python
df.groupby("Ville")["PM10"].mean()
>>>
Ville
Lyon         36.0
Marseille    47.5
Paris        31.5
Name: PM10, dtype: float64
```

Par défaut, la colonne de regroupement devient l’index.

#### Garder la colonne de regroupement

On peut garder la colonne `Ville` comme colonne classique avec `as_index=False` :

```python
df.groupby("Ville", as_index=False)["PM10"].mean()
>>>
        Ville  PM10
0        Lyon  36.0
1   Marseille  47.5
2       Paris  31.5
```

#### Plusieurs agrégations avec `.agg()`

On peut calculer plusieurs statistiques d’un coup :

```python
df.groupby("Ville", as_index=False).agg(
    moyenne_PM10=("PM10", "mean"),
    max_PM10=("PM10", "max"),
    nb_mesures=("PM10", "size")
)
>>>
       Ville  moyenne_PM10  max_PM10  nb_mesures
0       Lyon          36.0        42           2
1  Marseille          47.5        55           2
2      Paris          31.5        35           2
```

#### Transformation avec `.transform()`

`transform` applique une fonction à chaque groupe **mais renvoie une série de la même longueur que l’original** (pratique pour créer de nouvelles colonnes).

Exemple : centrer chaque valeur par rapport à la moyenne de sa ville :

```python
df["PM10_centre"] = df.groupby("Ville")["PM10"].transform(
    lambda s: s - s.mean()
)
print(df)
>>>
        Ville    Jour  PM10  PM10_centre
0       Paris   Lundi    35          3.5
1       Paris   Mardi    28         -3.5
...
```

🔗 Pour aller plus loin : voir la documentation officielle de `groupby`, `agg` et `transform`.

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
