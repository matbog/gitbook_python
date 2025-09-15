---
icon: globe
---

# Les Environnements

Quand on débute en Python, on installe souvent tout “en vrac” sur son ordinateur. _C'est ce que j'ai fait pendant des années!_&#x20;

Mais plus on avance, plus on installe de librairies différentes, et il devient vite difficile de garder tout propre et compatible. C’est là qu’entrent en jeu les **environnements Python**.

## 1. Qu’est-ce qu’un environnement Python ?

Un **environnement Python** est comme une petite “bulle” isolée qui contient sa propre version de Python et ses propres librairies.\
Ainsi, chaque projet peut avoir ses dépendances spécifiques, sans interférer avec les autres.

📌 Exemple :

* Projet A a besoin de **NumPy 1.21**.
* Projet B a besoin de **NumPy 2.0** (une version plus récente).\
  Sans environnements virtuels, ces deux projets se mélangeraient et créeraient des erreurs. Avec un environnement séparé pour chaque projet, chacun a sa bonne version.

## 2. Comment créer et utiliser un environnement virtuel ?

### Avec **conda** (si tu utilises Anaconda/Miniconda)

```bash
# Créer un environnement nommé "projet_data" avec une version précise de Python
conda create -n projet_data python=3.11

# Activer l’environnement
conda activate projet_data

# Pour quitter l’environnement :
conda deactivate
```

### Avec `venv` (inclus dans Python)

```bash
# Créer un nouvel environnement dans un dossier nommé "env_projet"
python -m venv env_projet
```

Activer l’environnement

#### Sur macOS / Linux :

```
source env_projet/bin/activate
```

#### Sur Windows (PowerShell) :

```
.\env_projet\Scripts\Activate
```

#### Pour quitter l’environnement :

```
deactivate
```

👉 Tu peux choisir un autre nom de dossier (par ex. `.venv`, `venv_test`, `env_ml`, etc.).\
Il suffit ensuite de toujours activer l’environnement correspondant avant de travailler.

## 3. Installer une version spécifique de Python

Selon ton projet, tu peux avoir besoin d’une version particulière de Python (par exemple pour être compatible avec une librairie).

#### Avec `venv` (Python officiel)

Tu dois d’abord avoir la version de Python souhaitée installée sur ton système, puis créer l’environnement en précisant le binaire :

```bash
python3.10 -m venv env_projet
```

Ici, on crée un environnement qui utilise **Python 3.10**.

#### Avec **conda**

Avec conda, on peut directement préciser la version de Python lors de la création :

```bash
conda create -n projet_climat python=3.9
```



## 4. Le fichier `requirements.txt`

Quand ton projet commence à utiliser plusieurs **librairies externes**, il devient vite compliqué de se souvenir de toutes leurs versions exactes.\
C’est là qu’intervient le fichier **`requirements.txt`** :

* C’est un simple fichier texte qui liste toutes les dépendances de ton projet, avec leurs versions.
* Exemple de contenu :

```txt
numpy==1.26.4
pandas==2.2.2
matplotlib==3.9.0
```

*   Pour **générer automatiquement** ce fichier (dans un environnement virtuel activé) :

    ```bash
    pip freeze > requirements.txt
    ```
*   Pour **recréer le même environnement** sur un autre ordinateur :

    ```bash
    python -m venv .venv
    source .venv/bin/activate   # ou .\venv\Scripts\Activate sous Windows
    pip install -r requirements.txt
    ```

Ainsi, tu assures que tout le monde travaille avec **les mêmes versions** de bibliothèques, ce qui évite beaucoup de problèmes de compatibilité.

## 👉 **À retenir**

* Un environnement virtuel = un espace isolé avec ses propres versions de Python et des packages.
* Donne un **nom clair** à ton environnement (ex. `projet_data`) pour t’y retrouver.
* Utilise **`requirements.txt`** pour partager et reproduire facilement ton environnement sur un autre poste.
