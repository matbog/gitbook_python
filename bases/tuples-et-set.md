---
icon: boxes-stacked
---

# Tuples et Set

Après les **listes** et les **dictionnaires**, découvrons deux autres types de collections en Python :\
les **tuples** et les **sets**.

***

## 1. Les Tuples

Un **tuple** est une séquence ordonnée d’éléments, **mais immuable** :\
👉 une fois créé, on ne peut plus modifier son contenu.

### Création

On les écrit entre **parenthèses** `()`.

```python
coord = (2, 5)
print(coord)
>>> 
(2, 5)

print(type(coord))
>>>
<class 'tuple'>
```

### Accéder aux éléments

Comme pour une liste, on utilise les indices (en commençant à 0).

```python
print(coord[0])
>>>
2

print(coord[1])
>>>
5
```

### Déstructurer un tuple

Très pratique pour affecter plusieurs variables en une seule ligne :

```python
x, y = coord
print("x =", x, "y =", y)
>>>
x = 2 y = 5
```

### Pourquoi utiliser un tuple ?

* Pour stocker des données **qui ne doivent pas changer** (ex. coordonnées, dates, clés fixes).
* Comme **clé dans un dictionnaire** (contrairement aux listes, les tuples peuvent être utilisés comme clés).

```python
d = { (0,0): "origine", (1,2): "point A" }
print(d[(1,2)])
>>> 
point A
```

## 2. Les sets (ensembles)

Un **set** est une collection **non ordonnée** et **sans doublons**.

### Création

On les écrit entre accolades `{ }`.

```python
s = {1, 2, 2, 3}
print(s)   # {1, 2, 3}
```

### Opérations ensemblistes

```python
A = {1, 2, 3}
B = {3, 4, 5}

print(A | B)   # union 
>>>
{1, 2, 3, 4, 5}

print(A & B)   # intersection
>>>
{3}

print(A - B)   # différence
>>>
{1, 2}
```

## 👉 Retenir

* **Tuple** = comme une liste, mais figé (utile pour des coordonnées, clés de dictionnaire, etc.).
  * souvent utilisés pour représenter des données fixes (coordonnées `(x, y)`, valeurs qui ne doivent pas être modifiées).
  * très différents des listes car ils sont **immutables** → on ne peut pas changer leur contenu.
  * utilisés aussi pour **déstructurer** plusieurs valeurs en une seule affectation.
* **Set** = ensemble sans doublons, idéal pour tester l’appartenance ou faire des unions/intersections.
  * très utiles pour enlever des doublons automatiquement.
  * permettent de faire des **opérations ensemblistes** : union, intersection, différence.
  * souvent pratiques dans les traitements de données (par exemple pour savoir quelles valeurs uniques apparaissent dans une colonne).
