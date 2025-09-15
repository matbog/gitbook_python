---
icon: chalkboard-user
---

# Les classes

Jusqu’ici, nous avons utilisé des **variables**, des **listes**, des **dictionnaires** et des **fonctions**.\
Mais dans des projets plus grands, il devient vite utile de **structurer** les données et les fonctions qui leur sont associées.\
C’est exactement ce que permettent les **classes** en Python.

## 1. Qu’est-ce qu’une classe ?

* Une **classe** est un plan ou un “moule” qui décrit un objet.
* Un **objet** est une “instance” de cette classe, avec ses **données** (attributs) et ses **méthodes** (fonctions qui lui sont propres).
* C'est pour ces fameuse classes et ces objet qu'on parle parfois de [Programmation Orientée Objet](https://fr.wikipedia.org/wiki/Programmation_orient%C3%A9e_objet), ou **POO.**

On définit une classe avec le mot-clé `class`.

***

#### Exemple simple : une voiture

```python
class Voiture:
    def __init__(self, marque, vitesse):
        # __init__ est le constructeur : il initialise l’objet
        self.marque = marque
        self.vitesse = vitesse

    def accelerer(self, ajout):
        """Augmente la vitesse de la voiture."""
        self.vitesse += ajout
        print(f"La vitesse de la {self.marque} est maintenant {self.vitesse} km/h.")

# On crée un objet de type Voiture
ma_voiture = Voiture("Renault", 50)

# On peut accéder aux attributs
print(ma_voiture.marque)   # Renault
print(ma_voiture.vitesse)  # 50

# On appelle une méthode
ma_voiture.accelerer(20)   # La vitesse de la Renault est maintenant 70 km/h.
```

## 2. L’attribut spécial `self`

* `self` représente **l’objet lui-même**.
* Il doit toujours apparaître en premier paramètre des méthodes définies dans la classe.
*   Quand on appelle `ma_voiture.accelerer(20)`, Python traduit en réalité par :

    ```python
    Voiture.accelerer(ma_voiture, 20)
    ```

## 3. Ajouter des méthodes utiles

Une classe peut contenir plusieurs méthodes qui manipulent ses données.

```python
class Rectangle:
    def __init__(self, largeur, hauteur):
        self.largeur = largeur
        self.hauteur = hauteur

    def aire(self):
        return self.largeur * self.hauteur

    def perimetre(self):
        return 2 * (self.largeur + self.hauteur)

rect = new = Rectangle(4, 3)
print("Aire :", rect.aire())         # 12
print("Périmètre :", rect.perimetre())  # 14
```

## 4. Héritage

Une classe peut **hériter** d’une autre pour réutiliser et spécialiser son comportement.

```python
class Vehicule:
    def __init__(self, marque):
        self.marque = marque

    def demarrer(self):
        print(f"{self.marque} démarre.")

class Moto(Vehicule):
    def cabrer(self):
        print(f"La moto {self.marque} fait un wheeling !")

m = Moto("Yamaha")
m.demarrer()  # Yamaha démarre.
m.cabrer()    # La moto Yamaha fait un wheeling !
```

## 5. Les méthodes spéciales

Les classes peuvent définir des **méthodes magiques** (commençant et finissant par `__`) :

* `__init__` : constructeur (appelé à la création de l’objet).
* `__str__` : texte affiché quand on fait `print(mon_objet)`.
* `__len__` : permet d’utiliser `len(mon_objet)`.
* `__add__` : définit ce que veut dire `objet1 + objet2`.

Exemple :

```python
class Vecteur:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __str__(self):
        return f"({self.x}, {self.y})"
    
    def __add__(self, autre):
        return Vecteur(self.x + autre.x, self.y + autre.y)

v1 = Vecteur(2, 3)
v2 = Vecteur(1, -1)

print(v1)         # (2, 3)
print(v1 + v2)    # (3, 2)
```

## En résumé

* Une **classe** = un plan qui regroupe données (**attributs**) et comportements (**méthodes**).
* Le mot-clé **`self`** désigne l’objet lui-même.
* On peut créer ses propres types adaptés à un problème d’ingénierie (ex : un “Cercle”, une “Station”, un “Capteur”).
* L’**héritage** permet de réutiliser et spécialiser du code.
* Les **méthodes spéciales** (`__init__`, `__str__`, `__len__`, …) permettent d’intégrer vos objets au langage Python de manière naturelle.

## Exemple concret : une classe `Batiment`

Imaginons qu’on veuille représenter un bâtiment, avec sa surface et sa consommation énergétique.\
On peut créer une classe dédiée pour regrouper ces informations et les fonctions associées.

### Défintion d'une classe "Batiment"

```python
class Batiment:
    def __init__(self, nom, surface, conso_m2):
        """
        Représente un bâtiment.

        Paramètres
        ----------
        nom : str
            Nom du bâtiment
        surface : float
            Surface utile en m²
        conso_m2 : float
            Consommation énergétique par m² (en kWh/m²)
        """
        self.nom = nom
        self.surface = surface
        self.conso_m2 = conso_m2

    def conso_totale(self):
        """Calcule la consommation totale du bâtiment (kWh)."""
        return self.surface * self.conso_m2

    def changer_surface(self, nouvelle_surface):
        """Met à jour la surface du bâtiment."""
        self.surface = nouvelle_surface

    def __str__(self):
        """Représentation lisible de l’objet."""
        return f"Bâtiment {self.nom} ({self.surface} m², {self.conso_m2} kWh/m²)"
```

### Utilisation

```python
# On crée un bâtiment de 1000 m² qui consomme 20 kWh/m²
gare = Batiment("Gare de Lyon", 1000, 20)

print(gare)  
# Bâtiment Gare de Lyon (1000 m², 20 kWh/m²)

print("Consommation totale :", gare.conso_totale(), "kWh")
# Consommation totale : 20000 kWh

# On change la surface (par ex. après rénovation)
gare.changer_surface(1200)
print("Nouvelle consommation :", gare.conso_totale(), "kWh")
# Nouvelle consommation : 24000 kWh
```

👉 Cet exemple illustre bien comment une classe permet de **structurer des données** (nom, surface, consommation spécifique) et d’ajouter des **méthodes métiers** (calcul de consommation totale, mise à jour des caractéristiques).\
C’est exactement le genre d’outil qui devient utile quand on manipule des bâtiments, des capteurs ou des simulations complexes.

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
