---
icon: table-pivot
---

# Reshape et Pivot

Un même jeu de données peut être représenté sous différentes formes :

* en **format long** (tidy data), où chaque observation est une ligne,
* en **format large**, où certaines variables deviennent des colonnes.

Changer la forme d’un DataFrame est très courant : pour préparer des calculs, des agrégations ou encore des visualisations.\
Pandas propose plusieurs méthodes pour cela : `pivot`, `pivot_table`, `melt`, `stack` et `unstack`.

## Exemple de `pivot`

```python
import pandas as pd

df = pd.DataFrame({
    "jour": ["Lundi", "Lundi", "Mardi", "Mardi"],
    "ville": ["Paris", "Lyon", "Paris", "Lyon"],
    "valeur": [10, 12, 9, 11]
})
print(df)
>>>
    jour  ville  valeur
0  Lundi  Paris      10
1  Lundi   Lyon      12
2  Mardi  Paris       9
3  Mardi   Lyon      11

large = df.pivot(index="jour", columns="ville", values="valeur")
print(large)
>>>
ville   Lyon  Paris
jour                
Lundi     12     10
Mardi     11      9
```

👉 Ici, on est passé d’un format **long** (une ligne par observation) à un format **large** (colonnes par ville).

## Exemple de `pivot_table` (avec agrégation)

`pivot_table` est plus flexible que `pivot` :\
il permet d’agréger plusieurs lignes qui auraient les mêmes clés (`mean`, `sum`, etc.).

```python
df2 = pd.DataFrame({
    "ville": ["Paris", "Paris", "Lyon", "Lyon"],
    "jour": ["Lundi", "Lundi", "Lundi", "Lundi"],
    "valeur": [10, 12, 11, 15]
})

table = df2.pivot_table(index="jour", columns="ville", values="valeur", aggfunc="mean")
print(table)
>>>
ville  Lyon  Paris
jour              
Lundi  13.0   11.0
```

## Exemple de `melt` (large → long)

L’inverse de `pivot` : `melt` permet de repasser d’un format large à un format long.

```python
long = large.reset_index().melt(id_vars="jour", var_name="ville", value_name="valeur")
print(long)
>>>
   jour   ville  valeur
0  Lundi    Lyon      12
1  Mardi    Lyon      11
2  Lundi   Paris      10
3  Mardi   Paris       9
```

## Exemple de `stack` et `unstack`

Ces méthodes manipulent les index hiérarchiques :

* `stack()` compresse les colonnes en lignes (MultiIndex).
* `unstack()` fait l’opposé.

```python
stacked = large.stack()
print(stacked)
>>>
jour   ville
Lundi  Lyon     12
       Paris    10
Mardi  Lyon     11
       Paris     9
dtype: int64

unstacked = stacked.unstack()
print(unstacked)
>>>
ville  Lyon  Paris
jour              
Lundi    12     10
Mardi    11      9
```

## 👉 Retenir

* `pivot` → réorganise en large, mais suppose une seule valeur par combinaison.
* `pivot_table` → permet d’agréger en cas de doublons.
* `melt` → repasse en format long.
* `stack` / `unstack` → manipulent les index hiérarchiques.

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
