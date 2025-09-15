---
icon: play-pause
---

# Bases

_Les bases de la base !_&#x20;

Avant d’aller plus loin, commençons par quelques bases très simples de Python :

## Affectation et affichage de variables

```python
temperature = 18.6
print("Température mesurée :", temperature)
>>>
Température mesurée : 18.6
```

👉 Le signe `#` sert à écrire un **commentaire**. Python l’ignore à l’exécution.

```python
# Ceci est un commentaire : il ne s'affiche pas
print("Cette ligne, en revanche, s'affiche bien.")
```

## Les opérations mathématiques

### Les opérateurs arithmétiques

Exécutons quelques instructions pour voir l’évolution d’une variable :

```python
# Addition
x = 5
print("Valeur initiale :", x)
>>>
Valeur initiale :  5

# Soustraction
x = x - 2
print("Après soustraction :", x)
>>>
Après soustraction :  3

# Multiplication
x *= 4
print("Après multiplication :", x)
>>>
Après multiplication :  12

# Division entière
x //= 3
print("Division entière :", x)
>>>
Division entière :  4

# Modulo
x = x % 2
print("Reste de la division par 2 :", x)
>>>
Reste de la division par 2 :  0

# Puissance
a = 3
print("a =", a)
>>>
a = 3

a = a**2
print("Carré :", a)
>>>
Carré : 9


b = 9**0.5
print("Racine carrée de 9 =", b)
>>>
Racine carrée de 9 = 3.0
```

### Opérateurs de comparaison

Ces opérateurs renvoient un **booléen** (`True` ou `False`).\
Ils sont très utilisés dans les [conditions](https://matbog.gitbook.io/python/basics/les-conditions) (`if`, `while`).

| Opérateur | Exemple (`x=10`, `y=3`) | Résultat | Signification     |
| --------- | ----------------------- | -------- | ----------------- |
| `==`      | `x == y`                | False    | Égal à            |
| `!=`      | `x != y`                | True     | Différent de      |
| `<`       | `x < y`                 | False    | Inférieur à       |
| `>`       | `x > y`                 | True     | Supérieur à       |
| `<=`      | `x <= 10`               | True     | Inférieur ou égal |
| `>=`      | `y >= 5`                | False    | Supérieur ou égal |

