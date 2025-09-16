---
icon: border-none
---

# Création et manipulation de tableaux

Une fois NumPy installé et importé, l’outil principal que l’on utilise est le **tableau multidimensionnel** (`numpy.ndarray`).\
Cette page montre comment **créer** des tableaux et les manipuler (taille, forme, opérations simples).

## 1. Créer des tableaux

### À partir d’une liste Python

```python
import numpy as np

a = np.array([1, 2, 3, 4])
print(a)
# [1 2 3 4]
```

### Tableaux remplis automatiquement

```python
zeros = np.zeros(5)   # 5 zéros
ones = np.ones((2, 3))  # matrice 2x3 remplie de 1
plein = np.full((2, 2), 7)  # matrice 2x2 remplie de 7

print(zeros)
print(ones)
print(plein)
```

### Suites numériques rapides

```python
print(np.arange(0, 10, 2))   # [0 2 4 6 8]
print(np.linspace(0, 1, 5))  # [0.   0.25 0.5  0.75 1.  ]
```

## 2. Dimensions et formes

Chaque `ndarray` possède :

* **`.ndim`** → nombre de dimensions
* **`.shape`** → taille par dimension (tuple)
* **`.size`** → nombre total d’éléments

```python
M = np.array([[1, 2, 3],
              [4, 5, 6]])

print("Dimensions :", M.ndim)   # 2
print("Shape :", M.shape)       # (2, 3)
print("Taille :", M.size)       # 6
```

## 3. Reshape et flatten

On peut transformer la forme d’un tableau, tant que le **nombre total d’éléments** reste le même.

```python
a = np.arange(12)  # [0 1 2 3 4 5 6 7 8 9 10 11]

M = a.reshape(3, 4)   # tableau 3 lignes x 4 colonnes
print(M)

plat = M.flatten()    # revenir à un tableau 1D
print(plat)
```

Résultat :

```
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
[ 0  1  2  3  4  5  6  7  8  9 10 11]
```

## 4. Exemple pratique

Supposons qu’on mesure la consommation électrique de 2 bâtiments sur 4 jours :

```python
# Lignes = jours, colonnes = bâtiments
conso = np.array([
    [120, 135],
    [140, 150],
    [160, 170],
    [155, 165]
])

print("Consommations :")
print(conso)

# Consommation totale par bâtiment (somme par colonne)
print("Somme par bâtiment :", conso.sum(axis=0))

# Consommation quotidienne totale (somme par ligne)
print("Somme par jour :", conso.sum(axis=1))

# Moyenne globale
print("Moyenne totale :", conso.mean())
```

Résultat attendu :

```
Consommations :
[[120 135]
 [140 150]
 [160 170]
 [155 165]]
Somme par bâtiment : [575 620]
Somme par jour : [255 290 330 320]
Moyenne totale : 148.75
```

## **À retenir**

* `np.array([...])` pour transformer une liste en tableau.
* `zeros`, `ones`, `full`, `arange`, `linspace` pour générer des données rapidement.
* `.ndim`, `.shape`, `.size` pour explorer la structure d’un tableau.
* `reshape` change la **forme** sans modifier les données.
* Les `ndarray` sont la base du travail avec **Pandas** et la data science en général.

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
