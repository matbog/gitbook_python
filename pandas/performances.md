---
icon: medal
---

# Performances

## Performance avancée avec Pandas

### Pourquoi s'intéresser aux performances ?

Quand on travaille avec des datasets de quelques milliers de lignes, les performances ne sont pas un enjeu. Mais dès qu'on dépasse les 100 000 lignes, ou qu'on manipule des données répétitivement (dans une boucle d'analyse par exemple), chaque optimisation compte.

Les deux leviers principaux sont :

1. **La mémoire** : moins on en utilise, plus c'est rapide
2. **Les opérations vectorisées** : éviter les boucles Python

## Optimiser les types de données (`dtypes`)

### Le problème des types par défaut

Pandas choisit des [types](https://matbog.gitbook.io/python/bases/les-types-en-python) "sûrs" par défaut, mais souvent surdimensionnés :

* Les entiers deviennent `int64` (même pour stocker des valeurs < 1000)
* Les chaînes deviennent `object` (très gourmand en mémoire)
* Les `floats` sont en `float64` (alors que `float32` suffit souvent)

```python
import pandas as pd
import numpy as np

# Créons un DataFrame "typique" d'analyse de données
df = pd.DataFrame({
    'user_id': range(1000000),              # IDs utilisateur (max ~1M)
    'category': ['Electronics', 'Books', 'Clothing'] * 333334,  # 3 catégories répétées
    'rating': np.random.uniform(1, 5, 1000000),  # Notes de 1 à 5
    'is_premium': [True, False] * 500000,    # Statut premium
    'age_group': ['18-25', '26-35', '36-50', '50+'] * 250000  # Tranches d'âge
})

print("Types par défaut :")
print(df.dtypes)
print(f"\nMémoire utilisée : {df.memory_usage(deep=True).sum() / 1024**2:.1f} MB")

# Résultat typique :
>>>
Types par défaut :
user_id         int64
category       object
rating        float64
is_premium       bool
age_group      object
dtype: object

Mémoire utilisée : 136.8 MB
```

#### La solution : types adaptés aux données

```python
# Analysons nos données pour choisir les bons types
print("Analyse des valeurs :")
print(f"user_id max : {df['user_id'].max()}")  # 999999 → int32 suffit (max 2.1 milliards)
print(f"Catégories uniques : {df['category'].nunique()}")  # 3 valeurs → category parfait
print(f"Rating min/max : {df['rating'].min():.2f} / {df['rating'].max():.2f}")  # float32 suffisant
>>>
Analyse des valeurs :
user_id max : 999999
Catégories uniques : 3
Rating min/max : 1.00 / 5.00


# Optimisation ciblée
df_optimized = df.astype({
    'user_id': 'int32',     # Divise par 2 la mémoire vs int64
    'category': 'category', # Stocke une seule fois chaque valeur unique
    'rating': 'float32',    # Divise par 2 la mémoire vs float64
    'age_group': 'category' # Pareil que category
})

print(f"\nMémoire optimisée : {df_optimized.memory_usage(deep=True).sum() / 1024**2:.1f} MB")
print(f"Gain : {(1 - df_optimized.memory_usage(deep=True).sum() / df.memory_usage(deep=True).sum()) * 100:.0f}%")

# Résultat typique : 
>>>
Mémoire optimisée : 10.5 MB
Gain : 92%
```

Les optimisations de "mémoire" permettent dans ce cas plus de 90% de gains !!!&#x20;

#### Le type `category` : un super-pouvoir méconnu

Le type `category` est idéal quand on a peu de valeurs uniques répétées beaucoup de fois :

```python
# Comparaison concrète
cities = ['Paris', 'Lyon', 'Marseille'] * 100000  # 300k répétitions de 3 villes

# Version object (classique)
series_object = pd.Series(cities, dtype='object')
print(f"En 'object' : {series_object.memory_usage(deep=True) / 1024**2:.1f} MB")

# Version category
series_category = pd.Series(cities, dtype='category')
print(f"En 'category' : {series_category.memory_usage(deep=True) / 1024**2:.1f} MB")

# Résultat typique : 
>>>
En 'object' : 18.0 MB
En 'category' : 0.3 MB

# Bonus : les opérations sur categories sont souvent plus rapides
%timeit series_object.value_counts()   # ~10ms
%timeit series_category.value_counts() # ~2ms
>>>
7.21 ms ± 149 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
2.52 ms ± 943 µs per loop (mean ± std. dev. of 7 runs, 1,000 loops each)
```

**Principe du type `category` :**

* Stocke une seule fois chaque valeur unique dans un "dictionnaire"
* Chaque ligne ne contient qu'un index vers ce dictionnaire
* Plus il y a de répétitions, plus c'est efficace

### Types nullable modernes : fini les NaN parasites

Le problème des NaN "forcés"

```python
# Situation classique frustrante
df_ages = pd.DataFrame({
    'name': ['Alice', 'Bob', 'Charlie', 'Diana'],
    'age': [25, 30, None, 35]  # Une seule valeur manquante
})

print("Types avec NaN classique :")
print(df_ages.dtypes)
print(df_ages)
>>>
Types avec NaN classique :

name     object
age     float64
dtype: object

      name   age
0    Alice  25.0
1      Bob  30.0
2  Charlie   NaN
3    Diana  35.0

```

Problème : la colonne `age` devient `float64` à cause du `None`.&#x20;

On perd l'information que ce sont des entiers...

#### La solution : types "nullable" pandas.&#x20;

Tout se joue dans la majuscule du type !!

```python
# Types nullable modernes (depuis pandas 1.0)
df_modern = pd.DataFrame({
    'name': pd.array(['Alice', 'Bob', 'Charlie', 'Diana'], dtype='string'),
    'age': pd.array([25, 30, None, 35], dtype='Int64'),  # Majuscule = nullable
    'is_student': pd.array([True, False, None, True], dtype='boolean'),
    'salary': pd.array([45000.0, 55000.0, None, 48000.0], dtype='Float64')
})

print("Types nullable modernes :")
print(df_modern.dtypes)
print(df_modern)
>>> 
Types nullable modernes :

name          string[python]
age                    Int64
is_student           boolean
salary               Float64
dtype: object

      name   age  is_student   salary
0    Alice    25        True  45000.0
1      Bob    30       False  55000.0
2  Charlie  <NA>        <NA>     <NA>
3    Diana    35        True  48000.0
```

Avantages :&#x20;

1. Les types restent cohérents malgré les valeurs manquantes
2. Distinction claire entre `0`,  `False` et valeurs manquantes
3. Meilleure interopérabilité (export Excel, base de données, ...)



## `map`/`apply` vs vectorisation : la bataille des performances

#### Le problème

Python est un langage interprété, ce qui signifie que les boucles sont lentes.&#x20;

`Pandas`/`NumPy` utilisent du code C compilé → les opérations vectorisées sont ultra-rapides. On va donc voir comment en tirer profit !&#x20;

<pre class="language-python"><code class="lang-python"># Cas d'usage réaliste : classification de température
temperatures = np.random.uniform(10, 40, 100000)  # 100k mesures
df_temp = pd.DataFrame({'temperature': temperatures})

def classify_comfort_python(temp):
    """Classification 'naïve' en Python pur"""
    if temp &#x3C; 16:
        return 'Too Cold'
    elif temp &#x3C; 20:
        return 'Cool'
    elif temp &#x3C; 24:
        return 'Comfortable'
    elif temp &#x3C; 28:
        return 'Warm'
    else:
        return 'Too Hot'

# Méthode lente : apply appelle la fonction Python pour chaque ligne
%timeit df_temp['comfort_slow'] = df_temp['temperature'].apply(classify_comfort_python)
>>>
146 ms ± 6.74 ms per loop (mean ± std. dev. of 7 runs, 10 loops each) 

# Méthode plus rapide : vectorisation avec np.select
conditions = [
    df_temp['temperature'] &#x3C; 16,
    df_temp['temperature'] &#x3C; 20, 
    df_temp['temperature'] &#x3C; 24,
    df_temp['temperature'] &#x3C; 28
]
choices = ['Too Cold', 'Cool', 'Comfortable', 'Warm']

%timeit df_temp['comfort_fast'] = np.select(conditions, choices, default='Too Hot')
<strong>>>>
</strong><strong>103 ms ± 1.97 ms per loop (mean ± std. dev. of 7 runs, 10 loops each) 
</strong></code></pre>

On vient de gagner 30% de temps d'exécution.&#x20;

Pour info, avec cet exemple, il y aurait même encore plus rapide, avec la catégorisation et la fonction `cut` décrite [ici](https://matbog.gitbook.io/python/pandas/categoriser-des-donnees). &#x20;

```python
bins = [-np.inf, 16, 20, 24, 28, np.inf]
labels = ['Too Cold', 'Cool', 'Comfortable', 'Warm', 'Too Hot']

%timeit df_temp['comfort_cut'] = pd.cut(df_temp['temperature'], bins=bins, labels=labels)
>>>
22 ms ± 651 µs per loop (mean ± std. dev. of 7 runs, 10 loops each)
```

Guyide de décision :&#x20;

```python
## En prenant des exemples différents (dfs non fournies)

# 1. MAP : dictionnaire de correspondance simple
status_mapping = {1: 'Active', 2: 'Inactive', 3: 'Suspended'}
df['status_name'] = df['status_code'].map(status_mapping)  # ✅ Très rapide

# 2. VECTORISATION : conditions mathématiques/logiques (voir "masks")
df['is_adult'] = df['age'] >= 18  # ✅ Ultra rapide
df['bmi_category'] = np.where(df['bmi'] > 25, 'Overweight', 'Normal')  # ✅ Rapide

# 3. APPLY : logique complexe non-vectorisable
def complex_business_rule(row):
    """Exemple : règle métier complexe avec plusieurs colonnes"""
    if row['department'] == 'Sales' and row['experience'] > 5:
        bonus_rate = 0.15
    elif row['department'] == 'Tech' and row['certifications'] > 2:
        bonus_rate = 0.12
    else:
        bonus_rate = 0.05
    
    return row['salary'] * bonus_rate * (1 + row['performance_score'] / 100)

df['bonus'] = df.apply(complex_business_rule, axis=1)  # ⚠️ Plus lent mais nécessaire
```

