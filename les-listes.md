---
description: Créer et manipuler des listes
icon: list
---

# Les listes

## Créer des listes&#x20;

Les listes sont les structures de bases de Python.

Les bases

```python
# Liste de int
liste = [1, 2, 3, 4, 5, 6] 
# Liste de str
liste_texte = ["aaa", "bbb", "ccc", "ddd"]
# Liste avec des float, du texte, un int, une autre liste...
liste_nimp = [0.0, "truc", 1, [1, 2, 3]]
```

On peut créer des liste de "tout", de nombres, de mots, de fontions, de graphiques, de `dataframes`, ... et mélanger "les choux et les carottes" !

On accède aux éléments d'une liste par leur index:

```python
liste_texte = ["aaa", "bbb", "ccc", "ddd"]
liste_texte[0]
>>>
"aaa"
#
liste_texte[2]
>>>
"ccc"
#
liste_texte[:2]
>>>
["aaa", "bbb"]
```

Quelques astuces sympa :

```python
5*["truc"]
>>> 
['truc', 'truc', 'truc', 'truc', 'truc']

5*[0]
>>>
[0, 0, 0, 0, 0]
# Créer une liste vide
a=[]
a
>>>
[]

```

#### `.zip()` pour accéder aux éléments de deux listes, typiquement dans une boucle&#x20;

```python
# zip()
a = ["a", "b", "c" ,"d", "e"]
b = [1, 2, 3, 4, 5]
# La boucle, en récpérant "facilement" les éléments des 2 listes, terme à terme. 
for x, y in zip(a, b):
    print(x, y)
>>>
a 1
b 2
c 3
d 4
e 5
```

## Ajouter des éléments à une liste existante

3 moyen principaux d'ajouter des éléments à une liste :&#x20;

* `append()` : Ajoute un _objet_ à la fin d'une liste
* `extend()` ou `+` ou  `+=` : Concatène une liste avec une autre, ou un autre élément
* `insert()` : Insère un objet à un index donnée

```python
# append() / Ajoute un object
liste = [1, 2, 3, 4, 5, 6]
liste.append(7)
liste
>>>
[1, 2, 3, 4, 5, 6, 7]
#
liste = [1, 2, 3, 4, 5, 6]
liste.append("chat")
liste
>>>
[1, 2, 3, 4, 5, 6, "chat"]
# /!\ Attention
liste = [1, 2, 3, 4, 5, 6]
liste.append([7, 8])
liste
>>> 
[1, 2, 3, 4, 5, 6, [7, 8]]
```

```python
# extend() / + met 2 listes bout à bout
liste = [1, 2, 3, 4, 5, 6]
liste.extend([7])
liste
>>>
[1, 2, 3, 4, 5, 6, 7]
# 
liste = [1, 2, 3, 4, 5, 6]
liste.extend([7, 8]) # on "extend" avec une autre liste ! 
liste
>>>
[1, 2, 3, 4, 5, 6, 7, 8]
# Ou plus simple à lire 
liste = [1, 2, 3, 4, 5, 6]
liste2 = [7, 8, "chat"]
liste+liste2
>>>
[1, 2, 3, 4, 5, 6, 7, 8, 'chat']
```

```python
# insert 
liste = [1, 2, 3, 4, 5, 6]
liste.insert(2,"chat") # On veut insérer "chat" à l'index 2
liste
>>>
[1, 2, 'chat', 3, 4, 5, 6]
```

## Retirer des éléments d'une liste

Deux méthodes et une fonction permettent de retirer des éléments d'une liste  :

* `.pop()` permet de retirer un élément via son index (ou le dernier élément si on ne précise pas) et retourne la valeur supprimée
* `.remove()` supprime la **première** occurrence de la valeur demandée.
* &#x20;`del` permet de retirer un élément via son index, ses index ou slices,

```python
# pop()
arr = [1, 2, 3]
arr.pop(1) # retire la valeur à l'index 1
arr
>>> 
[1,3]

# Si on ne précise pas d'index, retire la dernière valeur
arr = [1, 2, 3]
arr.pop() # Retire la dernière valeur en l'affichant
>>>
3
arr
>>>
arr = [1, 2]
```

```python
# remove()
a = [0, 2, 3, 2]
a.remove(2)
a 
>>>
[0, 3, 2] # La  *première* occurence de 2 est supprimée, pas la seconde. 
```

```python
# del
a = [9, 8, 7, 6]
del a[1]
a
>>> 
[9, 7, 6]
# Ou pour des slices
a = [9, 8, 7, 6, 5, 4, 3, 2, 1]
del a[2:-2] 
# Supprime à partir de la deuxième valeurs, jusqu'à l'avant dernière (non inclus)
a
>>> 
[9, 8, 2, 1]
```

Ou pour "tout" retirer : `.clear()`

## Assigner des variables à partir d'une liste&#x20;

```python
liste = [1, 2, 3]
a, b, c = liste
# a = 1 
# b = 2
# c = 3
```

### Utiliser les \* à bon escient !&#x20;

le `*x` peut servir à y mettre une liste de taille non définie à l'avance.

* Par exemple, prendre le premier élément, et laisser le reste dans une autre liste&#x20;

```python
data = [1, 2, 3, 4, 5, 6]
a, *b = data
# a = 1 
# b = [2,3,4,5,6]
```

* Autre exemple, prendre le premier et le dernier élément d'une liste, et garder le reste (le "milieu" dans une autre liste

```python
data = [1, 2, 3, 4, 5, 6]
a, *b, c = data
# a = 1 
# b = [2,3,4,5]
# c = 6
```

## Divers

### Liste à l'envers

```python
data = [1, 2, 3, 4, 5, 6]
data[::-1]
>>>
[6, 5, 4, 3, 2, 1]
```

### Compréhension de listes

Une **compréhension de liste** permet de créer une liste en une seule ligne, de manière compacte.

#### Exemple simple

```python
# Liste des carrés de 0 à 9
carres = [x**2 for x in range(10)]
print(carres)
>>>
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

#### Exemple avec condition

```python
# Les nombres pairs entre 0 et 9
pairs = [x for x in range(10) if x % 2 == 0]
print(pairs)
>>>
[0, 2, 4, 6, 8]
```

