---
icon: indent
---

# Indexation, masques et broadcasting

Un des points forts de NumPy est la **manipulation efficace des données** :\
on peut accéder rapidement aux éléments d’un tableau, extraire des sous-ensembles, ou appliquer des opérations sans boucle explicite.

## 1. Indexation simple

Un tableau NumPy peut avoir une ou plusieurs dimensions.\
On utilise des **indices entre crochets** :

```python
import numpy as np

a = np.array([10, 20, 30, 40])
print(a[0])   # premier élément → 10
print(a[-1])  # dernier élément → 40

M = np.array([[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]])

print(M[0, 2])  # ligne 0, colonne 2 → 3
print(M[2, 1])  # ligne 2, colonne 1 → 8
```

### 2. Slicing (tranches)

On peut sélectionner plusieurs valeurs à la fois grâce à la **notation `:`**.\
La syntaxe est : `array[start:stop:step]`.

```python
x = np.arange(10)  # [0 1 2 3 4 5 6 7 8 9]

print(x[2:6])    # [2 3 4 5]
print(x[:4])     # [0 1 2 3]   (du début jusqu’à l’indice 3)
print(x[5:])     # [5 6 7 8 9] (de l’indice 5 à la fin)
print(x[::2])    # [0 2 4 6 8] (un élément sur deux)
```

## 3. Indexation avec une liste d’indices

On peut demander directement les éléments d’un tableau en donnant une **liste d’indices**.

```python
x = np.array([10, 20, 30, 40, 50])

print(x[[0, 2, 4]])  # [10 30 50]
```

## 4. Indexation booléenne (masques)

On peut filtrer un tableau en créant un **masque de valeurs True/False**.\
Seules les positions avec `True` sont conservées.

```python
x = np.array([5, 12, 18, 7, 3, 25])

mask = x > 10
print(mask)       # [False  True  True False False  True]

print(x[mask])    # [12 18 25]
```

On peut combiner plusieurs conditions :

```python
print(x[(x > 5) & (x < 20)])  # [12 18 7]
```

## 5. Broadcasting

Le **broadcasting** permet d’appliquer des opérations entre des tableaux de **formes différentes**, tant que leurs dimensions sont compatibles.\
C’est une des grandes forces de NumPy !

#### Exemple : ajouter un vecteur à chaque ligne d’une matrice

```python
M = np.array([[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]])

v = np.array([10, 20, 30])

print(M + v)
```

Résultat :

```
[[11 22 33]
 [14 25 36]
 [17 28 39]]
```

Ici, NumPy **“étire” (broadcast)** le vecteur `v` sur chaque ligne de `M`. Pas besoin d’écrire de boucle !

## 6. Exemple pratique (capteurs d’air)

Imaginons que nous avons mesuré la concentration en CO₂ dans deux salles pendant 5 jours :

```python
import numpy as np

jours = np.array(["Lun","Mar","Mer","Jeu","Ven"])
salle_A = np.array([420, 450, 500, 480, 460])
salle_B = np.array([390, 400, 420, 410, 405])

# On empile les deux séries dans une matrice
mesures = np.vstack([salle_A, salle_B])
print(mesures)
```

```
[[420 450 500 480 460]
 [390 400 420 410 405]]
```

#### Calculer la moyenne par jour (sur les deux salles) :

```python
moyenne_jour = mesures.mean(axis=0)
print("CO₂ moyen par jour :", moyenne_jour)
```

Résultat :

```
CO₂ moyen par jour : [405. 425. 460. 445. 432.5]
```

## **À retenir**

* **Slicing** permet d’extraire des sous-parties d’un tableau.
* **Indexation booléenne** est idéale pour filtrer avec des conditions.
* **Broadcasting** évite d’écrire des boucles et accélère les calculs.
* NumPy est une brique essentielle pour manipuler des données scientifiques et préparer les DataFrames avec Pandas.

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
