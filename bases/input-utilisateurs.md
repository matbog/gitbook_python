---
description: Entrées utilisateur (input)
icon: input-text
---

# Input utilisateurs

Pour rendre un programme **interactif**, on peut demander une valeur à l’utilisateur avec la fonction `input()`.\
Par défaut, `input()` renvoie toujours une chaîne de caractères (`str`).

#### Exemple : demander un prénom

```python
nom = input("Quel est ton prénom ? ")
print("Bonjour", nom, "!")
```

Exécution possible :

```
Quel est ton prénom ? Alice
Bonjour Alice !
```

#### Exemple : demander un nombre

```python
age = input("Quel est ton âge ? ")
print("Type de la variable :", type(age))  # toujours <class 'str'>
```

Résultat :

```
Quel est ton âge ? 25
Type de la variable : <class 'str'>
```

👉 Comme `input()` renvoie du texte, il faut **convertir en nombre** si besoin :

```python
age = int(input("Quel est ton âge ? "))
print("Dans 5 ans, tu auras", age + 5, "ans.")
```

Exécution possible :

```
Quel est ton âge ? 25
Dans 5 ans, tu auras 30 ans.
```

***

✍️ Avec **input()**, vous pouvez commencer à écrire de petits programmes interactifs et tester vos premières idées en Python.
