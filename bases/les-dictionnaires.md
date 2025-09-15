---
description: Créer et manipuler les dictionnaires
icon: spell-check
---

# Les dictionnaires

Les dictionnaires, c'est un peu comme les listes, mais en mieux ! \
Au lieu d'utiliser des `index`, on peut nommer les choses, avec des `keys` (clés)

On peut voir les "clés" comme des noms de colonnes, et mettre ce qu'on veut ensuite dans les colonnes.&#x20;

## Créer des `dict`

Trois façon&#x20;

1. Avec des accolades :&#x20;

```python
# Create a dict with curly brackets :
mon_dict = {
    "Nom": "Bob",
    "Age": 25, 
    "Ville": "Paris"
}
```

2. Avec le "constructeur" `dict`

```python
# Create a dict using the dict() constructor :
mon_dict = dict(
    Nom = "Bob",
    Age = 25, 
    Ville = "Paris"
)
```

3. Avec des listes de paires (`tuple`):

```renpy
# Creating a dictionary from a list of tuples
mon_dict = dict([
    ("Nom", "Bob"),
    ("Age", 25), 
    ("Ville", "Paris")
])
```

Ces trois `dict` sont identiques

On voit qu'après un clé, on peut mettre "ce qu'on veut", un nombre, une chaine de caractère, ça pourrait être une liste, ou n'importe quel "objet".&#x20;

### Accéder aux données

* Pour accéder à un item, on utilise la "clé" (`key`)

```python
mon_dict["Nom"]
>>>>>
"Bob"
```

* Pour connaitre toutes les "clés" d'un dict, on peut le demander :&#x20;

```python
mon_dict.keys()
>>>>>
dict_keys(['Nom', 'Age', 'Ville'])
```

### Ajouter une nouvelle "colonne",  ou un nouvel item

Le plus simple :&#x20;

```python
mon_dict["Nouvelle données"] = "bidule"
print(mon dict)
>>>>>
{'Nom': 'Bob', 'Age': 25, 'Ville': 'Paris', 'Nouvelle données': 'bidule'}
```

Ou la façon `update` : c'est un peu comme si on assemblait 2 dictionnaires&#x20;

```python
mon_dict.update({"encore un truc": [1,2,3,4]})
print(mon_dict)
>>>>>
{
'Nom': 'Bob',
'Age': 25,
'Ville': 'Paris',
'Nouvelle données': 'bidule',
'encore un truc': [1, 2, 3, 4]
}
```

### Enlever un élément

```python
mon_dict.pop("Nouvelle données")
>>>>>
"bidule"

print(mon_dict)
>>>>>
{'Nom': 'Bob', 'Age': 25, 'Ville': 'Paris', 'encore un truc': [1, 2, 3, 4]}
```

## Itérer sur d'un dict&#x20;

#### Itérer sur les clés :&#x20;

```python
for x in mon_dict:
    print(x)
>>>>>
Nom
Age
Ville
Nouvelle données
encore un truc
```

#### Itérer sur les valeurs :&#x20;

```python
for x in mon_dict:
    print(mon_dict[x])
>>>>>
Bob
25
Paris
bidule
[1, 2, 3, 4]
```

ou&#x20;

```python
for x in mon_dict.values():
    print(x)
>>>>>
Bob
25
Paris
bidule
[1, 2, 3, 4]
```

#### Itérer sur les 2 :&#x20;

```python
for x, y in mon_dict.items():
  print(x, y)
>>>>>
Nom Bob
Age 25
Ville Paris
Nouvelle données bidule
encore un truc [1, 2, 3, 4]
```
