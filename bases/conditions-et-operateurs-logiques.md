---
description: if / elif / else
icon: square-check
---

# Conditions et Opérateurs logiques

## Les Condition : if / elif / else

`if` peut être utiliser seul, ou avec le `else`, et / ou avec le `elif` (: `else` `if`)

```python
a=1
if a<0: 
    print("négatif")
else:
    print("positif")

>>>
positif


a = 0.5
if a<0:
    print("negatif")
elif (a>=0 and a<1) :
    print("entre 0 et 1")
else:
    print("plus grand que 1")
>>>
entre 0 et 1
```

Ces conditions peuvent "d'additioner" et / ou s'imbriquer :

## Opérateurs logiques (`and`, `or`, `not`)

En plus des comparaisons (`==`, `<`, `>`, `!=`…), on peut combiner plusieurs conditions avec des **opérateurs logiques** :

| Opérateur | Exemple (`x=5`, `y=10`) | Résultat | Signification                                 |
| --------- | ----------------------- | -------- | --------------------------------------------- |
| `and`     | `(x > 2) and (y < 20)`  | True     | Vrai si **toutes** les conditions sont vraies |
| `or`      | `(x < 2) or (y < 20)`   | True     | Vrai si **au moins une** condition est vraie  |
| `not`     | `not (x > 2)`           | False    | Inverse le résultat (négation logique)        |

Exemple concret :

```python
temperature = 22
ensoleille = True

if temperature > 20 and ensoleille:
    print("On peut aller se promener !")
>>>
On peut aller se promener !
```

Ces opérateurs servent à écrire des conditions plus complexes et précises.
