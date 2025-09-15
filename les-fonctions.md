---
description: Les fonctions en python
icon: gear-complex
---

# Les fonctions

## Les bases&#x20;

Les **fonctions** permettent de regrouper du code réutilisable.\
On leur donne un **nom**, éventuellement des **arguments**, et elles peuvent **renvoyer un résultat** avec `return`.

Ici les indentations on un sens, il faut absolument les respecter pour que les fonctions soient bien définies !&#x20;

### Exemple 1 : fonction sans argument

```python
def dire_bonjour():
    print("Bonjour à tous !")

dire_bonjour()
>>>
Bonjour à tous !
```

### Exemple 2 : fonction avec argument

```python
def saluer(prenom):
    print(f"Bonjour {prenom} !")

saluer("Alice")
>>> 
Alice

saluer("Mehdi")
>>> 
Mehdi
```

### Exemple 3 : fonction qui renvoie un résultat

```python
def aire_rectangle(longueur, largeur):
    return longueur * largeur

print(aire_rectangle(2, 5))
>>>
10
```

## Fonctions : notions avancées

On peut rendre les fonctions plus puissantes grâce à :

* des **arguments par défaut**,
* des **arguments multiples** (`*args`, `**kwargs`),
* des **fonctions anonymes** (`lambda`).

### Exemple : argument par défaut

```python
def saluer(prenom="inconnu"):
    print(f"Bonjour {prenom} !")

saluer()         
>>> 
Bonjour inconnu !

saluer("Léa")
>>>
Bonjour Léa !
```

### Exemple : fonction anonyme (lambda)

```python
carre = lambda x: x**2
print(carre(4))
>>>
16
```

### Exemple : fonction avec un nombre indéfini d'arguments

```python
def additionner(*nombres):
    return sum(nombres)

print(additionner(1, 2, 3))
>>> 
6
```

### Exemple : \*args et \*\*kwargs

* `*args` permet de passer un nombre **variable** d’arguments positionnels.
* `**kwargs` permet de passer un nombre **variable** d’arguments nommés (sous forme de dictionnaire).

**Exemple avec \*args**

<pre class="language-python"><code class="lang-python">def moyenne(*nombres):
    return sum(nombres) / len(nombres)

print(moyenne(10, 20, 30))
>>>
20.0

print(moyenne(5, 15, 25, 35))
>>>
20.0
<strong>
</strong></code></pre>

**Exemple avec \*\*kwargs**

```python
def infos_etudiant(**kwargs):
    for cle, valeur in kwargs.items():
        print(f"{cle} : {valeur}")

infos_etudiant(nom="Alice", age=22, formation="Génie civil")
>>>
nom : Alice
age : 22
formation : Génie civil
```

👉 On utilise souvent `**kwargs` pour écrire des fonctions génériques qui acceptent beaucoup de paramètres optionnels.

### La récursivité

Une fonction peut s’appeler **elle-même**.\
C’est utile pour certains calculs, par exemple le **factoriel** :

```python
def factorielle(n):
    """Calcule le factoriel d’un entier n (n!)."""
    if n == 0:
        return 1
    else:
        return n * factorielle(n - 1)

print(factorielle(5))
>>>
120
```

Autre exemple : la suite de **Fibonacci**.

```python
def fibonacci(n):
    """Renvoie le n-ième terme de la suite de Fibonacci."""
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

print(fibonacci(6))
>>>
8
```

## Documenter les fonctions

Pour commencer, on peut simplement ajouter des commentaires dans son code pour documenter les variables et le modalités d'une fonction, mais Python intègre un standard dédié ; les Docstring !&#x20;

Les **docstrings** sont des commentaires spéciaux (entre triples guillemets `""" ... """`) placés juste après la définition d’une fonction.\
Ils servent de documentation intégrée et peuvent être affichés avec `help()`.

```python
def aire_rectangle(longueur, largeur):
    """
    Calcule l’aire d’un rectangle.
    
    Paramètres
    ----------
    longueur : float
        Longueur du rectangle
    largeur : float
        Largeur du rectangle

    Retourne
    --------
    float
        Aire du rectangle (longueur × largeur)
    """
    return longueur * largeur

print(aire_rectangle(4, 2))
>>>
8

help(aire_rectangle)
>>>
Help on function aire_rectangle in module __main__:

aire_rectangle(longueur, largeur)
    Calcule l’aire d’un rectangle.

    Paramètres
    ----------
    longueur : float
        Longueur du rectangle
    largeur : float
        Largeur du rectangle

    Retourne
    --------
    float
        Aire du rectangle (longueur × largeur)
```

