---
description: Sauvegarder des graphiques avec Matplotlib
icon: floppy-disks
---

# Export des figures

Jusqu’ici, nous avons affiché les graphiques à l’écran avec `plt.show()`.\
Mais il est souvent utile de **sauvegarder vos figures** pour les insérer dans un rapport, une présentation ou un article.

Pour cela, on utilise la fonction **`plt.savefig()`**.

## 1. Sauvegarder en PNG

```python
import matplotlib.pyplot as plt
import numpy as np

# Données
x = np.linspace(0, 10, 100)
y = np.sin(x)

# Tracé
plt.plot(x, y, label="sinus")
plt.title("Exemple de sinusoïde")
plt.xlabel("x")
plt.ylabel("sin(x)")
plt.legend()

# Sauvegarde en image PNG
plt.savefig("sinus.png", dpi=150, bbox_inches="tight")
```

* `dpi=150` : qualité de l’image (dots per inch). Plus la valeur est élevée, plus l’image est nette.
* `bbox_inches="tight"` : permet de réduire les marges inutiles autour du graphique.

## 2. Sauvegarder en PDF

Vous pouvez aussi enregistrer vos figures en **PDF vectoriel**, pratique pour l’intégrer dans un rapport scientifique ou une présentation.

```python
plt.savefig("sinus.pdf", bbox_inches="tight")
```

Le PDF garde la **qualité vectorielle** (aucune perte si on zoome).

## 3. Autres formats disponibles

Matplotlib peut exporter dans de nombreux formats, par exemple :

* `"png"` → image classique pour le web
* `"jpg"` → image compressée
* `"svg"` → vectoriel pour le web
* `"pdf"` → vectoriel, parfait pour un rapport ou une présentation

## 👉 Retenir

* `plt.show()` affiche le graphique à l’écran.
* `plt.savefig("nom_fichier.format")` enregistre le graphique.
* Avec `dpi` et `bbox_inches="tight"`, vous contrôlez la qualité et la mise en pag

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
