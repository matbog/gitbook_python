---
icon: kerning
---

# Les "types" en python

## Les types de base en Python

Chaque valeur en Python appartient à un **type**.\
Connaître les types est essentiel pour comprendre ce que l’on peut faire avec une variable (et éviter certaines erreurs).

### 1. Nombres

* **Entiers (`int`)** : nombres sans virgule.

```python
a = 5
print(a, type(a))
>>>
5 <class 'int'>
```

* Flottants (`float`) : noobre à virgules

```python
b = 3.14
print(b, type(b))
>>>
3.14 <class 'float'>
```

### 2. Chaînes de caractères (`str`)

Du texte, entre guillemets simples `' '` ou doubles `" "`.

```python
nom = "Alice"
message = 'Bonjour'
print(nom, type(nom))
>>>
Alice <class 'str'>

print(message, type(message))
>>>
Bonjour <class 'str'>
```

### 3. Booléens (`bool`)

Seulement deux valeurs possibles : `True` ou `False`.\
Souvent le résultat de comparaisons.

```python
x = 10
print(x > 5)
>>>
True

print(x == 3)
>>>
False

print(type(x > 5))
>>>
<class 'bool'>
```

#### 4. Conversion entre types

On peut convertir un type en un autre avec des fonctions comme `int()`, `float()`, `str()`.

```python
# Transformer un texte en nombre
age_txt = "25"
age = int(age_txt)
print(age + 5)
>>>
30

# Transformer un nombre en texte
n = 3.5
texte = str(n)
print("La valeur est " + texte)
>>>
La valeur est 3.5

```

### 👉 Retenir

* `int` → entiers
* `float` → réels (nombres à virgule)
* `str` → chaînes de caractères (texte)
* `bool` → True / False

Ces 4 types de base reviennent tout le temps dans la programmation Python.

## Notions avancées sur les types

### 1. Le type `None`

* Représente “rien”, l’absence de valeur.
* Utilisé souvent comme valeur par défaut dans une fonction ou pour indiquer qu’une variable n’a pas encore de contenu.

```python
resultat = None
print(resultat, type(resultat))
>>>
None <class 'NoneType'>
```

### **2. La fonction `type()` et `isinstance()`**

* `type(obj)` → renvoie le type exact d’un objet.
* `isinstance(obj, type)` → permet de tester si une variable est d’un certain type (et accepte les sous-classes).

```python
x = 42
print(type(x))
>>> 
<class 'int'>

print(isinstance(x, int))
>>>
True

print(isinstance(x, float))
>>>
False
```

### **3. Conversion implicite (type casting automatique)**

* Quand on mélange un `int` et un `float` dans une opération, Python “penche” automatiquement vers le type le plus général.

```python
a = 3       # int
b = 2.5     # float
c = a + b
print(c, type(c))
>>> 
5.5 <class 'float'>
```
