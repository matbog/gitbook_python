---
icon: empty-set
---

# Valeurs manquantes

Dans les jeux de données réels, il y a presque toujours des **valeurs manquantes** (NA / NaN).\
Bien les identifier et savoir les traiter est indispensable pour éviter des erreurs de calcul ou des biais.

En Pandas, les valeurs manquantes sont représentées par **`NaN`** (Not a Number).

## Détecter les valeurs manquantes

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "ville": ["Paris", "Lyon", "Marseille", "Paris"],
    "PM10": [35, np.nan, 55, 28]
})

print(df)
>>>
       ville  PM10
0      Paris  35.0
1       Lyon   NaN
2  Marseille  55.0
3      Paris  28.0
```

On peut vérifier où sont les `NaN`&#x20;

```python
df.isna()              # tableau booléen
>>>
   ville   PM10
0  False  False
1  False   True
2  False  False
3  False  False

df.isna().sum()        # nombre de NaN par colonne
>>>
ville    0
PM10     1
dtype: int64         
```

## Supprimer les valeurs manquantes

```python
df_sans_na = df.dropna()
print(df_sans_na)
>>>
       ville  PM10
0      Paris  35.0
2  Marseille  55.0
3      Paris  28.0
```

⚠️ Attention : par défaut `dropna` supprime toute la **ligne** si au moins une colonne contient un NaN.

On peut aussi préciser les colonnes :

```python
df.dropna(subset=["PM10"])
```

## Remplacer les valeurs manquantes

### Insérer une valeur fixe

```python
df_filled = df.fillna(0)
print(df_filled)
>>>
       ville  PM10
0      Paris  35.0
1       Lyon   0.0
2  Marseille  55.0
3      Paris  28.0
```

Avec une valeur spécifique par colonne :

```python
df_filled = df.fillna({"PM10": df["PM10"].mean()})
```

Ici on remplace les NaN par la moyenne des autres valeurs de la colonne

### Propager les valeurs connues

* **Forward fill** (utiliser la dernière valeur connue) :

```python
df_ffill = df.fillna(method="ffill")
```

* **Backward fill** (utiliser la valeur suivante connue) :

```python
df_bfill = df.fillna(method="bfill")
```

### Interpolation

Pour les séries temporelles, on peut **estimer les valeurs manquantes** par interpolation.\
Par défaut, Pandas utilise une interpolation **linéaire**, mais il existe plusieurs méthodes (`linear`, `quadratic`, `cubic`, `time`, etc.).

```python
# interpolation linéaire (pas de prise en compte de l'index)
df_interp_lin = df.interpolate(method="linear")     

# interpolation basée sur l’index temporel
df_interp_time = df.interpolate(method="time")

# interpolation polynomiale (quadratique ici)
df_interp_poly = df.interpolate(method="polynomial", order=2)  # interpolation polynomiale (quadratique ici)
```

## À Retenir

* `isna()` / `notna()` pour détecter
* `dropna()` pour supprimer
* `fillna()` pour remplacer
* `interpolate()` pour estimer des valeurs manquantes en continue

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
