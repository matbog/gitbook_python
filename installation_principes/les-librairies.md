---
icon: books
---

# Les Librairies

En programmation, on ne repart (heureusement !) pas toujours de zéro.

\
Des milliers de développeurs ont déjà écrit du code pour résoudre des problèmes courants, et ils partagent ces morceaux de code sous forme de **librairies** (ou _packages,_ ou encore _modules_).

Utiliser une librairie, c’est réutiliser ces briques toutes faites au lieu de réinventer la roue.\
Exemple : pourquoi écrire soi-même un calcul de moyenne alors que NumPy le fait en une ligne ?

***

## 1. Pourquoi utiliser des librairies ?

* **Gagner du temps** : pas besoin de tout recoder.
* **Fiabilité** : ces codes sont souvent testés et maintenus par de grandes communautés.
* **Performance** : certaines librairies (comme NumPy) sont optimisées en C/C++.
* **Partage** : tu peux réutiliser et combiner des outils existants pour ton projet.

***

## 2. Installer une librairie

Deux méthodes principales :

#### Avec `pip` (gestionnaire standard Python)

```bash
pip install numpy
```

#### Avec **Anaconda** (recommandé pour la data science)

```
conda install numpy
```

👉 Selon ton environnement (Python “pur” ou Anaconda), tu utiliseras l’une ou l’autre commande.

## 3. Importer une librairie

En Python, on utilise le mot-clé **`import`**.

```python
import math
print(math.sqrt(16))  # -> 4.0
```

#### Importer avec un alias

Cela permet de donner un nom "court" à la librairie importée, et ensuite d'aller chercher ses fonctions.&#x20;

```python
import numpy as np
print(np.array([1, 2, 3]) * 2)
```

#### Importer seulement une fonction précise

```python
from math import sqrt
print(sqrt(25))  # -> 5.0
```

#### Importer tout (déconseillé)

```python
from math import *
print(sqrt(9))
```

⚠️ Déconseillé, car cela peut créer des conflits de noms (deux fonctions avec le même nom mais de librairies différentes).

## 4. Quelques librairies populaires

### Pour débuter en Python

**Liste non-exhaustive !**&#x20;

* **NumPy** → calcul numérique (vecteurs, matrices)
* **Pandas** → manipulation de données tabulaires (CSV, Excel, bases de données)
* **Matplotlib** → graphiques simples (lignes, barres, nuages de points)
* **Seaborn** → graphiques statistiques, plus esthétiques et plus simples à utiliser

### Pour l'ingénierie et le traitement de données

* **pvlib** → outils pour la **modélisation et l’analyse des systèmes photovoltaïques** (irradiation, production solaire, suivi de panneaux).
* **meteostat** → accès facile aux **données météorologiques** historiques et récentes (température, vent, ensoleillement). Très utile pour les études énergétiques.
* **pyvista** → bibliothèque de **visualisation 3D** (cartes, volumes, champs de température ou de vitesse). Idéal pour représenter des simulations ou des modèles 3D de bâtiments.

## 👉 **À retenir**

* Une **librairie** est un ensemble de fonctions réutilisables.
* On les installe via `pip install ...` ou `conda install ...`.
* Certaines sont **génériques** (NumPy, Pandas, Matplotlib), d’autres sont plus spécialisées pour l’**ingénierie et l’énergie** (pvlib, meteostat, pyvista).
