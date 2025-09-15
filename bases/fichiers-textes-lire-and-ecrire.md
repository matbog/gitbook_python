---
description: Lire et écrire des fichiers texte
icon: text-size
---

# Fichiers textes : lire & ecrire

En Python, on peut facilement travailler avec des fichiers texte : lire leur contenu, ou écrire dedans.\
C’est très utile pour enregistrer des résultats de calculs ou pour lire des données avant de les analyser avec **Pandas**.

### 1. Ouvrir un fichier

La fonction principale est **`open()`**.\
On doit préciser :

* le **nom du fichier**
* le **mode** :
  * `"r"` → lecture (read)
  * `"w"` → écriture (write, efface le contenu existant)
  * `"a"` → ajout (append, écrit à la fin du fichier)

***

### 2. Lire un fichier

#### Lire tout le contenu

```python
with open("exemple.txt", "r", encoding="utf-8") as f:
    contenu = f.read()
    print(contenu)
```

#### Lire ligne par ligne

```python
with open("exemple.txt", "r", encoding="utf-8") as f:
    for ligne in f:
        print("Ligne :", ligne.strip())
```

### 3. Écrire dans un fichier

#### Écraser le contenu existant

```python
with open("resultats.txt", "w", encoding="utf-8") as f:
    f.write("Première ligne\n")
    f.write("Deuxième ligne\n")
```

Après exécution, le fichier **resultats.txt** contiendra :

```
Première ligne
Deuxième ligne
```

#### Ajouter à la fin du fichier

```python
with open("resultats.txt", "a", encoding="utf-8") as f:
    f.write("Troisième ligne\n")
```

Le fichier contient maintenant :

```
Première ligne
Deuxième ligne
Troisième ligne
```

### 4. Lire un fichier ligne par ligne dans une liste

```python
with open("resultats.txt", "r", encoding="utf-8") as f:
    lignes = f.readlines()

print(lignes)
# ['Première ligne\n', 'Deuxième ligne\n', 'Troisième ligne\n'
```

## 👉 Retenir

* Toujours utiliser `with open(...)` pour que le fichier se ferme automatiquement.
* Modes utiles : `"r"` (lecture), `"w"` (écriture, écrase), `"a"` (ajout).
* `.read()`, `.readline()`, `.readlines()` permettent de lire un fichier de différentes façons.
