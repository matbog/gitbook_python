---
icon: bolt-lightning
---

# Accélérer son code

Quand on commence en Python, on remarque parfois que certains programmes sont plus **lents** que prévu, surtout pour des calculs lourds ou des boucles sur de gros volumes de données.

Cela vient du fait que **Python est un langage interprété** (le code est traduit et exécuté ligne par ligne), et qu’il utilise un mécanisme interne appelé **GIL (Global Interpreter Lock)** qui limite l’exécution de code Python pur à un seul cœur à la fois.

Heureusement, il existe plusieurs techniques pour améliorer les performances !

## 1. Optimiser le code avant tout

Avant de “multithreader” ton programme, il est crucial d’écrire du code efficace :

### **Utilise les bonnes structures de données**

Exemple : préférez un `set` pour tester l’appartenance plutôt qu’une liste.

```python
# Peu efficace
nums = [1, 2, 3, 4, 5]
print(999999 in nums)  # doit parcourir toute la liste
>>>
False

# Plus efficace avec un set
nums_set = {1, 2, 3, 4, 5}
print(999999 in nums_set)  # vérification quasi instantanée
>>>
False
```

_Si vous testez ce code, vous ne verrez pas de différences, mais avec plusieurs million de valeurs, il y en aura une !_&#x20;

### **Préférence pour la vectorisation (NumPy, pandas)**

Éviter les boucles Python et utiliser des opérations sur des tableaux complets.

```python
import numpy as np

# Calcul du carré de 1 million de nombres
data = np.arange(1_000_000)

# Lenteur : boucle Python
squares = [x**2 for x in data]

# Rapide : vectorisation NumPy
squares_fast = data**2
```

## 2. Threads et tâches concurrentes (I/O-bound)

Le **multithreading** en Python est utile pour exécuter plusieurs tâches d’**entrée/sortie** en parallèle (téléchargements, requêtes API, lecture de fichiers), car ces tâches passent beaucoup de temps à attendre.

Exemple : télécharger plusieurs pages web en parallèle avec `concurrent.futures` :

```python
import requests
from concurrent.futures import ThreadPoolExecutor

urls = [
    "https://example.com",
    "https://www.python.org",
    "https://www.wikipedia.org"
]

def fetch(url):
    r = requests.get(url)
    return url, len(r.text)

with ThreadPoolExecutor(max_workers=3) as executor:
    results = executor.map(fetch, urls)

for url, size in results:
    print(f"{url}: {size} caractères téléchargés")
```

## 3. Parallélisme (CPU-bound)

Pour des calculs lourds (simulations physiques, traitement de données, calculs numériques), les threads Python ne suffisent pas à cause du **GIL**.\
Il vaut mieux utiliser plusieurs **processus indépendants** grâce au module `multiprocessing`, ou des outils comme **joblib**.

Exemple avec `multiprocessing` :

```python
from multiprocessing import Pool
import math

# Une fonction coûteuse
def is_prime(n: int) -> bool:
    if n < 2:
        return False
    for i in range(2, int(math.sqrt(n)) + 1):
        if n % i == 0:
            return False
    return True

numbers = [1234567, 1234577, 1234587, 1234597, 1234607]

with Pool(processes=4) as pool:  # utilise 4 cœurs
    results = pool.map(is_prime, numbers)

print(results)  # [False, True, True, True, False]
```

Des bons exemples d'utilisatoin en ingénieire sont disponibles ici : [https://eddes.github.io/#go-parallel](https://eddes.github.io/#go-parallel)

## 4. Accélération avec **Numba**

Numba est une librairie qui **compile ton code Python en code machine optimisé** grâce à LLVM.\
Elle est particulièrement efficace pour les boucles lourdes sur des tableaux numériques, sans devoir réécrire le code en C ou C++.

#### Exemple : calcul rapide de factorielle avec Numba

```python
from numba import njit

@njit # C'est tout ce qu'on a à ajouter !!! 
def factorielle(n):
    res = 1
    for i in range(1, n+1):
        res *= i
    return res

# Sans Numba
import math, time
t0 = time.time()
for i in range(1_000_000):
    math.factorial(10)
print("Temps sans Numba :", time.time() - t0, "s")

# Avec Numba
t0 = time.time()
for i in range(1_000_000):
    factorielle(10)
print("Temps avec Numba :", time.time() - t0, "s")
```

Apprès une première execution de la fonction, sur mon ordinateur portable de travail, j'ai les résultats suivants :rocket: :

```
Temps sans Numba : 4.801123857498169 s
Temps avec Numba : 0.1369612216949463 s
```

💡 **Astuce** : la première exécution d’une fonction `@njit` peut être plus lente (car Numba compile le code), mais les appels suivants sont beaucoup plus rapides.

## 5. Quand utiliser quoi ?

* **Optimisation simple** : revoir l’algorithme, éviter les boucles inutiles.
* **Vectorisation (NumPy / pandas)** : idéal pour les calculs sur des tableaux ou des colonnes.
* **Threads (`threading`, `ThreadPoolExecutor`)** : utiles pour l’I/O (lecture/écriture, API, téléchargements).
* **Multiprocessing (`multiprocessing`, `ProcessPoolExecutor`)** : utile pour paralléliser des calculs lourds.
* **Numba** : parfait pour accélérer du code Python pur, en particulier les boucles numériques.

