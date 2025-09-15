---
description: Boucles itératives, avec des conditions
icon: rotate-left
---

# Les boucles

## FOR

### `for` avec un liste

```python
trucs = ["aaa", "bbb", "ccc", "ddd"]
for bidule in trucs: 
    print(bidule)
>>>
aaa
bbb
ccc
ddd
```

### `for` avec `range`

`range()` : créer une "liste" avec des nombres

`range(start, end, step)`

```python
for i in range(5):
    print(i)
>>>
0
1
2
3
4
#
for i in range(2, 5): # Si on précise 2 éléments, c'est debut-fin /avec step= 1
    print(i)
>>> 
2
3
4
#
for i in range(0, 10, 2): #
    print(i)
>>>
0
2
4
6
8

```

### `for`avec `enumerate`

Permet d'itérer sur un objet, une liste par exemple, et d'avoir en même temps un "index".

```python
trucs = ["aaa", "bbb", "ccc", "ddd"]
for idx, text in enumerate(trucs): 
    print(idx, text)
    
>>>
0 aaa
1 bbb
2 ccc
3 ddd
```

## WHILE

```python
i=0
i_max=100

while i < i_max:
    i=i+10
    print(i)
>>> 
10
20
30
40
50
60
70
80
90
100

```

## Contrôler le flux d’une boucle : `pass`, `continue`, `break`

Dans une boucle `for` ou `while`, on peut utiliser des mots-clés spéciaux pour contrôler l’exécution.

***

### `pass` : ne rien faire (placeholder)

Parfois, on doit écrire une boucle ou une condition, mais on n’a pas encore décidé du contenu.\
`pass` sert alors de **bouchon** : il ne fait rien, mais évite une erreur de syntaxe.

```python
for i in range(5):
    if i < 3:
        pass  # pour l'instant, on ne fait rien
    else:
        print("i vaut", i)
>>>
i vaut 3
i vaut 4
```

### `continue` : sauter à l’itération suivante

`continue` interrompt **l’itération en cours**, puis passe directement à la suivante.\
Exemple : afficher seulement les nombres pairs de 0 à 6.

```python
for i in range(7):
    if i % 2 != 0:
        continue  # on ignore les nombres impairs
    print("Pair :", i)
>>>
Pair : 0
Pair : 2
Pair : 4
Pair : 6
```

### `break` : arrêter complètement la boucle

`break` stoppe la boucle **dès qu’il est exécuté**, même s’il restait des itérations.

```python
for i in range(10):
    if i == 5:
        print("On s'arrête à", i)
        break
    print("i =", i)
>>>
i = 0
i = 1
i = 2
i = 3
i = 4
On s'arrête à 5
```

### 👉 Résumé

* **`pass`** : ne fait rien (utile comme “brouillon”).
* **`continue`** : saute le reste de l’itération et passe à la suivante.
* **`break`** : arrête totalement la boucle.

