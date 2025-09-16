---
icon: chart-mixed
---

# Seaborn : graphiques haut niveau

[Seaborn ](https://seaborn.pydata.org/)est construit au-dessus de Matplotlib.\
Il permet de créer rapidement des graphiques plus esthétiques, avec moins de code, surtout quand les données sont sous forme de **DataFrame Pandas**.

## Bases

Créons un petit jeu de données fictif (pollution PM10 mesurée dans 3 villes, sur 2 jours) :

<pre class="language-python"><code class="lang-python">import seaborn as sns
import pandas as pd
<strong>df = pd.DataFrame({
</strong>    "Ville": ["Paris", "Paris", "Lyon", "Lyon", "Marseille", "Marseille"]*2,
    "Jour": ["Lundi"]*6 + ["Mardi"]*6,
    "PM10": [35, 28, 42, 30, 55, 40, 38, 25, 45, 32, 60, 43]
})

print(df.head())
>>>
       Ville   Jour  PM10
0      Paris  Lundi    35
1      Paris  Lundi    28
2       Lyon  Lundi    42
3       Lyon  Lundi    30
4  Marseille  Lundi    55
</code></pre>

### Lineplot (courbes)

Tracer l’évolution de la pollution par ville, avec couleurs et légende automatiques.

```python
sns.lineplot(data=df, x="Jour", y="PM10", hue="Ville", marker="o")
plt.title("Évolution quotidienne de la pollution (PM10)")
plt.ylabel("PM10 (µg/m³)")
plt.show()
```

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

***

### Barplot (diagrammes en barres)

Comparer les moyennes par ville.\
Par défaut, Seaborn calcule automatiquement la moyenne et un intervalle de confiance.

```python
sns.barplot(data=df, x="Ville", y="PM10", ci=None, palette="pastel")
plt.title("Pollution moyenne par ville")
plt.ylabel("PM10 (µg/m³)")
plt.show()
```

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

***

### Scatterplot (nuages de points)

Afficher les valeurs individuelles selon la ville et le jour.

```python
sns.scatterplot(data=df, x="Ville", y="PM10", hue="Jour", style="Jour", s=120)
plt.title("Pollution par ville et par jour")
plt.ylabel("PM10 (µg/m³)")
plt.show()
```

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

***

### Boxplot (distribution)

Comparer la distribution des valeurs par ville (très utile pour voir la variabilité).

```python
sns.boxplot(data=df, x="Ville", y="PM10", palette="Set2")
plt.title("Distribution des PM10 par ville")
plt.show()
```

<figure><img src=".gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

***

### Heatmap (tableau de couleurs)

On peut transformer les données et afficher une **matrice de valeurs**.

```python
table = df.pivot_table(index="Jour", columns="Ville", values="PM10", aggfunc="mean")
sns.heatmap(table, annot=True, cmap="Reds")
plt.title("Pollution moyenne par jour et par ville")
plt.show()
```

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

***

### Points clés

* **Seaborn** simplifie beaucoup la création de graphiques à partir de DataFrames.
* Les couleurs, légendes et styles sont automatiques (et plus esthétiques que Matplotlib par défaut).
* Tu peux rapidement passer d’une vision **par valeur individuelle** (scatter), à des **résumés statistiques** (barplot, boxplot), ou à des **cartes de chaleur** (heatmap).

## Pour aller plus loin : Les principaux plots Seaborn

### Données continues (courbes, distributions)

* `lineplot()` → courbes (évolution temporelle, séries chronologiques)
* `scatterplot()` → nuages de points
* `regplot()` → nuage de points + droite de régression (optionnelle)
* `lmplot()` → similaire à `regplot`, mais plus flexible (gère plusieurs facettes et variables de regroupement).

***

### Données catégorielles

* `barplot()` → barres (moyenne + intervalle de confiance)
* `countplot()` → histogramme de comptage (effectifs par catégorie)
* `boxplot()` → boîtes à moustaches (distribution + outliers)
* `violinplot()` → distribution lissée (mélange boîte + densité)
* `stripplot()` → valeurs individuelles (points “jitterés”)
* `swarmplot()` → valeurs individuelles réparties sans chevauchement (plus lisible qu’un stripplot).

***

### Distribution & densité

* `histplot()` → histogrammes (remplace l’ancien `distplot`)
* `kdeplot()` → densité (courbe lissée)
* `ecdfplot()` → fonction de répartition empirique (ECDF).

***

### Relations multivariées

* `pairplot()` → matrice de nuages de points + histogrammes diagonaux (exploration rapide)
* `jointplot()` → nuage de points avec histogrammes sur les marges (2 variables).
* `heatmap()` → matrice colorée (corrélations, pivot tables, etc.)
* `clustermap()` → heatmap avec clustering hiérarchique automatique.

***

### Facettes & organisation

* `FacetGrid()` → base pour tracer plusieurs sous-graphiques selon des variables.
* `catplot()` → fonction générique pour combiner barplot, boxplot, etc., avec facettes.
* `relplot()` → fonction générique pour lineplot et scatterplot avec facettes.

## Ressources complémentaires&#x20;

Ressources utiles :

* [Seaborn Gallery](https://seaborn.pydata.org/examples/index.html) (beaucoup d’exemples concrets)

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
