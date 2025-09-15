---
icon: chart-scatter
---

# La base : Matplotlib

La visualisation est l’une des forces de Python. Avec seulement quelques lignes de code, on peut créer des graphiques clairs et esthétiques.\
La bibliothèque la plus utilisée est [**Matplotlib**](https://matplotlib.org/stable/users/getting_started/) (bas niveau, très flexible)

## Les bases

Matplotlib est très flexible mais parfois verbeux.

Créons un petit jeu de données simple (évolution d’une température mesurée sur une journée), avec les imports minimum

```python
import numpy as np
import matplotlib.pyplot as plt

heures = np.arange(0, 24, 3)        # heures de 0h à 21h
temperature = [5, 6, 9, 14, 18, 17, 12, 8]
```

***



### Courbe simple (line plot)

```python
plt.plot(heures, temperature)
plt.xlabel("Heure")
plt.ylabel("Température (°C)")
plt.title("Évolution de la température sur 24h")
plt.show()
```

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

***

### Personnaliser le style de la courbe

```python
plt.plot(heures, temperature, 'o--r', label="Température")
plt.xlabel("Heure")
plt.ylabel("Température (°C)")
plt.title("Courbe personnalisée")
plt.legend()
plt.grid(True)
plt.show()
```

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

* `'o--r'` = points + ligne pointillée rouge
* `plt.grid(True)` pour afficher une grille

### Tracer plusieurs courbes

Imaginons une deuxième série (humidités mesurées aux mêmes heures) :



```python
humidite = [80, 78, 70, 60, 55, 65, 75, 85]

plt.plot(heures, temperature, '-r', label="Température (°C)")
plt.plot(heures, humidite, '-b', label="Humidité (%)")
plt.xlabel("Heure")
plt.title("Température et humidité")
plt.legend()
plt.show()
```

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

## Types de graphiques

### Diagramme en barres (bar plot)

Comparons les températures moyennes par ville :

```python
villes = ["Paris", "Lyon", "Marseille"]
moyennes = [15.2, 17.5, 20.1]

plt.bar(villes, moyennes, color="skyblue")
plt.ylabel("Température moyenne (°C)")
plt.title("Température moyenne par ville")
plt.show()
```

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### Histogramme

Un histogramme permet de visualiser la distribution d’un ensemble de données.

```python
donnees = np.random.normal(loc=20, scale=5, size=200)  # 200 valeurs simulées

plt.hist(donnees, bins=15, color="green", alpha=0.7, edgecolor="black")
plt.xlabel("Valeur")
plt.ylabel("Fréquence")
plt.title("Histogramme d'une distribution de températures")
plt.show()
```

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

### Nuage de points (scatter plot)

Pour visualiser la relation entre deux variables (par ex. température vs humidité) :

```python
plt.scatter(temperature, humidite, c="purple", s=80)
plt.xlabel("Température (°C)")
plt.ylabel("Humidité (%)")
plt.title("Relation Température / Humidité")
plt.show()
```

<figure><img src=".gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

👉 Avec ces bases, tu peux déjà réaliser la plupart des graphiques “classiques” (courbes, barres, histogrammes, nuages de points).

### Et tous les autres...

:astonished: Il existe de nombreux autres types de graphiques !&#x20;

#### 📈 Plots de base

* `plot()` → courbes (line plots)
* `scatter()` → nuages de points
* `bar()` et `barh()` → barres verticales et horizontales
* `hist()` → histogrammes
* `pie()` → diagrammes circulaires

***

#### 📊 Graphiques statistiques

* `boxplot()` → boîte à moustaches (distribution, outliers)
* `violinplot()` → distribution lissée (similaire à boxplot, mais avec densité)
* `stem()` → stem plots (bâtons verticaux pour valeurs discrètes)
* `stackplot()` → courbes empilées (aires cumulées)

***

#### 🌍 Graphiques avancés / spécialisés

* `imshow()` → afficher une image ou une matrice (ex : heatmap simple)
* `pcolor()` / `pcolormesh()` → cartes de couleurs (heatmaps sur grilles)
* `contour()` et `contourf()` → tracés de courbes de niveau (2D/3D)
* `quiver()` → champs de vecteurs (flèches directionnelles)
* `streamplot()` → champs de flux (trajectoires continues de vecteurs)

***

#### 🧭 3D (via `Axes3D` de `mpl_toolkits.mplot3d`)

* `plot3D()` → courbes 3D
* `scatter3D()` → nuages de points 3D
* `bar3D()` → barres 3D
* `contour3D()` → contours 3D
* `surface` plots (`ax.plot_surface`) → surfaces 3D continues
* `wireframe` plots (`ax.plot_wireframe`) → maillages 3D

***

#### 🖼️ Autres utilitaires

* `errorbar()` → courbes avec barres d’erreur
* `fill_between()` → zones colorées entre courbes
* `polar()` → graphiques polaires (rayon-angle)
* `hexbin()` → diagrammes hexagonaux (densité 2D)

***

👉 Pour t’y retrouver facilement :

* La [**Matplotlib Gallery**](https://matplotlib.org/stable/gallery/index.html) montre un exemple pour chaque type de tracé.
* La [**cheat sheet officielle** (PDF)](https://github.com/matplotlib/cheatsheets) est très pratique comme aide-mémoire visuel.

\
Ensuite, on peut passer à **Seaborn** pour des graphiques plus esthétiques et rapides à configurer.

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
