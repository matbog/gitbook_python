---
icon: filter
---

# Filtrer des données

Filtrer les données d'une `pd.dataframe` avec une ou plusieurs conditions

* Création d'une `dataframe` pour les exemples :

```python
import pandas as pd
col = [
        "colonne_A",
        "colonne_B",
        "colonne_C"
]
idx = range(0,10,1)
df = pd.DataFrame(
        index=idx,
        columns=col
     )
df["colonne_A"] = [28.8, 28.1, 27, 26.7, 25, 29, 29.9, 32, 25, 21]
df["colonne_B"] = 6*["jour"] + 4*["nuit"]
df["colonne_C"] = [125, 126, 124, 123.5, 127, 102, 87, 89, 75, 78]

df
>>>
        colonne_A colonne_B colonne_C
0       28.8      jour      125.0
1       28.1      jour      126.0
2       27.0      jour      124.0
3       26.7      jour      123.5
4       25.0      jour      127.0
5       29.0      jour      102.0
6       29.9      nuit       87.0
7       32.0      nuit       89.0
8       25.0      nuit       75.0
9       21.0      nuit       78.0
```

## Méthode 1 : les "mask"

**L'idée** : _utiliser une "liste" de `True` / `False`, que l'on va appliquer à notre donnée pour ne garder que les lignes avec `True`._

**Par exemple** : _On souhaite obtenir toutes les lignes de `df` où la `colonne_A` est supérieure à 28_

* On créé le "mask" :

```python
mask = df["colonne_A"] > 28
mask
>>>
0     True
1     True
2    False
3    False
4    False
5     True
6     True
7     True
8    False
9    False
Name: colonne_A, dtype: bool
```

* On applique ce "mask" à la `dataframe` :&#x20;

Soit on obtient une nouvelle `dataframe`, soit on utilise directement les valeurs :

```python
df2 = df[mask]
df2
>>>
   colonne_A colonne_B  colonne_C
0       28.8      jour      125.0
1       28.1      jour      126.0
5       29.0      jour      102.0
6       29.9      nuit       87.0
7       32.0      nuit       89.0
```

Après on peut aller chercher dans cette _nouvelle_ donnée que la `colonne_B`, de trois façons équivalentes :

```python
df2["colonne_B"]
# ou 
df[mask]["colonne_B"]
# ou, le tout en une ligne : 
df[ df["colonne_A"] > 28 ]["colonne_B"]
>>> 
0    jour
1    jour
5    jour
6    nuit
7    nuit
Name: colonne_B, dtype: object
```

Un des points fort est que l'on peut combiner les conditions, sur une ou plusieurs colonnes ou sur l'index, avec de ET  `&` / OU `|` (les différentes conditions doivent être entre parenthèses).

Par exemple : _Sortir les valeurs de la `colonne_C` lorsque les valeurs de la `colonne_A > 28` et `colonne_B == "jour"`_

```python
df[ (df["colonne_A"] > 28) & (df["colonne_B"] == "jour")]["colonne_C"]
>>>
0    125.0
1    126.0
5    102.0
Name: colonne_C, dtype: float64
```

On utilise ici `&` et `|` au lieu de `and` et `or` car on veut qu'il fasse l'opération ligne par ligne.&#x20;

## Méthode 2 : fonction `df.loc`

#### 1. Sortir les valeur correspondantes à une ou plusieurs conditions:

```python
df.loc[ df["colonne_A"] > 28 ]
>>>
   colonne_A colonne_B  colonne_C
0       28.8      jour      125.0
1       28.1      jour      126.0
5       29.0      jour      102.0
6       29.9      nuit       87.0
7       32.0      nuit       89.0
```

#### 2. Ne sortir qu'une des colonnes

```python
df.loc[df["colonne_A"] > 28, "colonne_C"]
>>>
0    125.0
1    126.0
5    102.0
6     87.0
7     89.0
Name: colonne_C, dtype: float64
```

#### 3. Remplacer les valeurs d'une colonne à partir d'une condition sur cette colonne, OU SUR UNE AUTRE

**Par exemple :** _on veut prendre les lignes avec `colonne_A > 28`, et sur cette ligne, mettre `50` dans la `colonne_C`_

```python
df.loc[df["colonne_A"] > 28, "colonne_C"] = 50
>>>
   colonne_A colonne_B  colonne_C
0       28.8      jour       50.0
1       28.1      jour       50.0
2       27.0      jour      124.0
3       26.7      jour      123.5
4       25.0      jour      127.0
5       29.0      jour       50.0
6       29.9      nuit       50.0
7       32.0      nuit       50.0
8       25.0      nuit       75.0
9       21.0      nuit       78.0
```

:warning:  Les données sont modifiées en place, on ne peut plus revenir en arrière !!!

:warning:  Si on ne précise pas qu'on veut remplacer la valeur de la `colonne_C` il va remplacer toute la ligne qui a satisfait à la condition demandée !

:thumbsup:  Avantages :

* On peut, comme avant, utiliser plusieurs conditions en les combinant
* On peut remplacer les valeurs de plusieurs colonnes en même temps

```python
df.loc[df["colonne_A"] > 28, ["colonne_C", "colonne_B"]] = [50, "soleil"]
>>>
   colonne_A colonne_B  colonne_C
0       28.8    soleil       50.0
1       28.1    soleil       50.0
2       27.0      jour      124.0
3       26.7      jour      123.5
4       25.0      jour      127.0
5       29.0    soleil       50.0
6       29.9    soleil       50.0
7       32.0    soleil       50.0
8       25.0      nuit       75.0
9       21.0      nuit       78.0
```

## :rocket: Pour aller plus loin&#x20;

D'autres fonctions incluses dans `pandas`:

Pour gagner en vitesse, avec les logiques assez proches :

* `df.mask(condition, valeur si vrai)`
* `df.where(condition, valeur si faux)`
  * &#x20;sympa si on a une modif à faire selon les "2 sens" de la condition : _si `true` modifie la valeur par truc, et si `False` alors modifie en machin_
    * `df['col'] = (value_if_false).where(condition, value_if_true)`
    * `df['A'] = (df['A'] / 2).where(df['A'] < 20, df['A'] * 2)`
* Et sûrement d'autres !&#x20;

### Encore plus loin ?

Pour des plus grandes données, plus lourdes, ce types de filtres peut être "vectorisé" pour être appliqué de façon plus optimisé à vos données. En 2022-2023, il était encore pertinent des passer par `numpy`, notamment avec le `np.where`, qui fait sensiblement la même chose que plus haut, mais plus vite...&#x20;

:clock1: Petit comparatif :&#x20;

```python
np.random.seed(0)
n = 10000000
df = pd.DataFrame(np.random.random(n))

%timeit df.loc[df[0] > 0.5, 0] = df[0]*2       # 217 ms ± 10 ms
%timeit df[0].mask(df[0] > 0.5, df[0]*2)       # 60.7 ms ± 2.32 ms
%timeit np.where(df[0] > 0.5, df[0]*2, df[0])  # 46.7 ms ± 2.22 ms
```



## Références / Documentation

{% embed url="https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.loc.html" %}

{% embed url="https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.where.html" %}

{% embed url="https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.mask.html" %}

{% embed url="https://numpy.org/doc/stable/reference/generated/numpy.where.html" %}

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
