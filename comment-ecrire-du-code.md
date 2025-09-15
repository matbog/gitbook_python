---
description: Commentaires et indentation
icon: pen-line
---

# Comment ecrire du code

## Commentaires et indentation

En Python, l’**indentation** (les espaces en début de ligne) n’est pas qu’une question de style : elle sert à définir la structure du programme.\
Les **commentaires** permettent, eux, d’expliquer le code pour toi-même et pour les autres.

***

### 1. Les commentaires

Un commentaire commence par `#` et n’est **pas exécuté** par Python.\
On les utilise pour documenter le code, rappeler une idée, ou désactiver une ligne.

```python
# Ceci est un commentaire
x = 5   # Ici, on crée une variable
print(x)  # On affiche la valeur de x
>>>
5
```

### 2. L’importance de l’indentation

En Python, on **indente avec 4 espaces** (évitez les tabulations, cela peut créer des erreurs).\
Chaque bloc (après un `if`, une[ boucle,](https://matbog.gitbook.io/python/basics/les-boucles) une [fonction](https://matbog.gitbook.io/python/basics/les-fonctions)…) doit être indenté.

```python
# Exemple correct
for i in range(3):
    print("Tour :", i)   # ligne indentée
print("Fin")             # retour au niveau 0
```

Si on oublie d’indenter :

```python
for i in range(3):
print("Tour :", i)   # ❌ erreur
```

Résultat :

```
IndentationError: expected an indented block
```

### 3. Bonnes pratiques de style

* Utiliser **4 espaces** pour chaque niveau d’indentation.
* Garder le code lisible (éviter les lignes trop longues).
* Nommer clairement les variables et fonctions.
* Ajouter des **commentaires utiles** (mais pas trop !) pour expliquer les parties complexes.

## 👉 Retenir

* Les **commentaires** servent à expliquer ton code, mais ne sont jamais exécutés.
* L’**indentation** est obligatoire en Python, elle structure ton programme.
* Un code bien indenté et commenté est plus facile à lire et à maintenir.
