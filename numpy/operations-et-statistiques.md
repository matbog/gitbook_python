---
icon: percent
---

# Opérations et statistiques

Un des gros avantages de NumPy est de pouvoir effectuer des **opérations mathématiques directement sur des tableaux entiers**, sans écrire de boucles.\
Cela rend le code plus **rapide** et plus **lisible** qu’avec des listes classiques.

## 1. Opérations arithmétiques de base

Avec NumPy, les opérations s’appliquent **élément par élément.** Donc une seule instruction agit sur tout un tableau par exmple : on parle de **vectorisation.**

```python
import numpy as np

x = np.array([1, 2, 3, 4])
y = np.array([10, 20, 30, 40])

print(x + y)   # [11 22 33 44]
print(x - y)   # [ -9 -18 -27 -36]
print(x * y)   # [10 40 90 160]
print(y / x)   # [10. 10. 10. 10.]
```

## 2. Fonctions mathématiques

NumPy contient déjà de nombreuses fonctions utiles :

```python
a = np.array([2, 4, 6, 8])

print(np.mean(a))   # moyenne → 5.0
print(np.median(a)) # médiane → 5.0
print(np.std(a))    # écart-type → 2.236
print(np.sum(a))    # somme → 20
print(np.min(a))    # minimum → 2
print(np.max(a))    # maximum → 8
```

## 3. Opérations par axe

Sur les tableaux multidimensionnels (`ndarray` à 2D ou plus), on peut calculer par **ligne** ou par **colonne** grâce au paramètre `axis`.

```python
M = np.array([[1, 2, 3],
              [4, 5, 6]])

print(M.sum())        # somme de tous les éléments → 21
print(M.sum(axis=0))  # somme par colonne → [5 7 9]
print(M.sum(axis=1))  # somme par ligne   → [6 15]
```

## 4. Produit matriciel et algèbre linéaire

NumPy fournit aussi un module dédié : **`np.linalg`**.

```python
# Deux matrices
A = np.array([[1, 2],
              [3, 4]])

B = np.array([[2, 0],
              [1, 2]])

# Produit matriciel
print(A @ B)
# [[ 4  4]
#  [10  8]]

# Transposée
print(A.T)
# [[1 3]
#  [2 4]]

# Inverse de A
print(np.linalg.inv(A))
# [[-2.   1. ]
#  [ 1.5 -0.5]]
```

## 5. Exemple pratique&#x20;

Imaginons que l’on ait les **consommations spécifiques** (kWh/m²) de 3 bâtiments\
et leurs **surfaces** (en m²). On veut calculer le **bilan total** et la **consommation par habitant**.

```python
import numpy as np

# Surface (m²) et conso spécifique (kWh/m²)
surfaces = np.array([1200, 900, 1500])
conso_m2 = np.array([15, 18, 12])

# Consommation totale (kWh)
conso_totale = surfaces * conso_m2
print("Consommation totale de chaque bâtiment :", conso_totale)

# Nombre d’habitants par bâtiment
habitants = np.array([80, 60, 120])

# Consommation par habitant (kWh/hab)
conso_par_habitant = conso_totale / habitants
print("Consommation moyenne par habitant :", conso_par_habitant)
```

Résultat possible :

```
Consommation totale de chaque bâtiment : [18000 16200 18000]
Consommation moyenne par habitant : [225. 270. 150.]
```

## 👉 À retenir

* Les opérations NumPy sont **vectorisées** (rapides, pas besoin de boucles).
* On peut appliquer des fonctions mathématiques directement sur tout un tableau.
* Les paramètres `axis=0` (par colonnes) et `axis=1` (par lignes) sont très fréquents.
* Le module **`np.linalg`** offre des outils puissants pour l’algèbre linéaire.

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
