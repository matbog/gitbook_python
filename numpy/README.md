---
icon: arrow-right-to-arc
---

# Introduction à NumPy

Avant de plonger dans [**Pandas**](https://matbog.gitbook.io/python/pandas), il est important de comprendre [**NumPy**](https://numpy.org/).\
NumPy est une bibliothèque fondamentale pour le calcul scientifique en Python.\
Elle permet de manipuler efficacement des **tableaux de nombres** (appelés **`ndarray`**) et de faire des calculs rapides.

### Pourquoi utiliser NumPy ?

* Les **listes Python** sont pratiques, mais lentes dès que l’on manipule de grands volumes de données.
* Avec NumPy, les calculs sont **vectorisés** : une opération s’applique à tout un tableau sans écrire de boucle.
* NumPy est utilisé partout en science des données : statistiques, machine learning, traitement du signal, génie énergétique…
* Pandas repose sur NumPy : chaque **colonne d’un DataFrame est en fait une `Series` qui encapsule un tableau NumPy**.

En résumé : si vous comprenez NumPy, vous comprendrez beaucoup mieux Pandas !

***

## 1. Installation et import

NumPy s’installe facilement (avec **pip** ou **conda**) :

```bash
pip install numpy
```

Puis, dans votre script :

```python
import numpy as np   # np est le “surnom” standard de numpy
```

## 2. Créer un array (tableau NumPy)

Un **array** ressemble à une liste, mais il est beaucoup plus puissant.

```python
import numpy as np

# Créer un tableau simple
a = np.array([2, 4, 6, 8])
print(a)
print("Type :", type(a))
```

Résultat :

```
[2 4 6 8]
Type : <class 'numpy.ndarray'>
```

## 3. Avantage : la vectorisation

Sans NumPy (avec une liste Python), il faudrait boucler :

```python
L = [2, 4, 6, 8]
L_doubles = [x * 2 for x in L]
print(L_doubles)
# [4, 8, 12, 16]
```

Avec NumPy, une seule ligne suffit :

```python
a = np.array([2, 4, 6, 8])
print(a * 2)     # [ 4  8 12 16]
print(a + 10)    # [12 14 16 18]
print(a ** 2)    # [ 4 16 36 64]
```

👉 Les calculs sont **beaucoup plus rapides** car NumPy utilise du code optimisé en C sous le capot.

## 4. Tableaux multidimensionnels

NumPy permet de manipuler facilement des matrices ou des grilles de données.

```python
M = np.array([[1, 2, 3],
              [4, 5, 6]])

print("M =")
print(M)
print("Dimensions :", M.ndim)   # 2
print("Taille :", M.shape)      # (2, 3)
print("Élément (ligne 0, colonne 2) :", M[0, 2])
```

Résultat :

```
M =
[[1 2 3]
 [4 5 6]]
Dimensions : 2
Taille : (2, 3)
Élément (ligne 0, colonne 2) : 3
```

## 5. Exemple pratique&#x20;

Imaginons que l’on ait les **consommations de chauffage** (en kWh/m²) pour 3 bâtiments, ainsi que leurs surfaces.\
On veut calculer la consommation totale de chaque bâtiment.

```python
# Surface en m²
surfaces = np.array([1200, 900, 1500])
# Consommation spécifique en kWh/m²
conso_m2 = np.array([15, 18, 12])

# Calcul de la consommation totale (vectorisé !)
conso_totale = surfaces * conso_m2
print("Consommations totales (kWh) :", conso_totale)

# Consommation moyenne
print("Consommation moyenne :", conso_totale.mean(), "kWh")
```

Résultat possible :

```
Consommations totales (kWh) : [18000 16200 18000]
Consommation moyenne : 17400.0 kWh
```

## 👉 **À retenir**

* **NumPy = base de Pandas et du calcul scientifique**.
* Les **arrays** sont plus rapides et plus pratiques que les listes.
* Grâce à la **vectorisation**, une seule opération peut s’appliquer à tout un tableau.
* Les `ndarray` peuvent être 1D, 2D (matrices) ou plus.
* On peut facilement combiner NumPy + Pandas pour analyser des données tabulaires.

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
