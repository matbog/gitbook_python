---
description: (merge, join, concat)
icon: object-exclude
---

# Joindre des Dataframes

Quand on travaille avec plusieurs sources de données, il est fréquent de vouloir les **combiner**.\
En Pandas, il existe trois grandes approches complémentaires :

1. **`merge`** → fusionner deux DataFrames **selon une ou plusieurs colonnes communes** (clé(s) de jointure).\
   👉 C’est l’équivalent des jointures en SQL.
2. **`join`** → similaire à `merge`, mais basé sur **l’index** des DataFrames.\
   👉 Pratique si vos DataFrames sont déjà indexés de manière cohérente.
3. **`concat`** → empiler ou juxtaposer plusieurs DataFrames (sans clé commune, juste les aligner par colonnes ou par lignes).\
   👉 Pratique pour rassembler plusieurs fichiers de structure identique.



## Exemple avec `merge`

```python
import pandas as pd

df_mesures = pd.DataFrame({
    "capteur_id": [1, 2, 3],
    "valeur": [10.0, 12.5, 9.8]
})

df_meta = pd.DataFrame({
    "capteur_id": [1, 2, 4],
    "nom_capteur": ["Cap1", "Cap2", "Cap4"]
})

df_inner = pd.merge(df_mesures, df_meta, on="capteur_id", how="inner")
print(df_inner)
>>>
   capteur_id  valeur nom_capteur
0           1    10.0        Cap1
1           2    12.5        Cap2
```

### Types de jointures avec `merge`

| `how`     | Description                                                       |
| --------- | ----------------------------------------------------------------- |
| `"inner"` | garde seulement les lignes présentes dans **les deux** DataFrames |
| `"left"`  | garde tout de gauche (ici `df_mesures`)                           |
| `"right"` | garde tout de droite (`df_meta`)                                  |
| `"outer"` | garde tout, complète avec NaN si pas de correspondance            |

## Exemple avec `join`

Si les clés de jointure sont déjà dans l’index :

```python
df1 = df_mesures.set_index("capteur_id")
df2 = df_meta.set_index("capteur_id")

df_join = df1.join(df2, how="left")
print(df_join)
>>>
            valeur nom_capteur
capteur_id                    
1             10.0        Cap1
2             12.5        Cap2
3              9.8         NaN
```

***

## Exemple avec `concat`

Pour **empiler** deux DataFrames avec les mêmes colonnes :

```python
df_stack = pd.concat([df_mesures, df_mesures], ignore_index=True)
print(df_stack)
>>>
   capteur_id  valeur
0           1    10.0
1           2    12.5
2           3     9.8
3           1    10.0
4           2    12.5
5           3     9.8
```

***

## 👉 Retenir

* Utiliser `merge` quand on a une ou plusieurs colonnes en commun.
* Utiliser `join` quand les index sont déjà définis et cohérents.
* Utiliser `concat` pour empiler ou juxtaposer des DataFrames entiers (mêmes colonnes).

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
