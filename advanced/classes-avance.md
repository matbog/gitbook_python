---
description: Pour aller plus loin !
icon: graduation-cap
---

# Classes / Avancé

Dans cette page, on pousse plus loin la POO en Python :

* **Héritage** : réutiliser et spécialiser du code.
* **Polymorphisme** : un même nom de méthode, des comportements adaptés.
* **Dataclasses** : créer des classes “porte-données” sans boilerplate.

***

## 1. Héritage : réutiliser et spécialiser

L’héritage permet de créer une classe **enfant** à partir d’une classe **parent**.\
La classe enfant récupère attributs et méthodes du parent, et peut **ajouter** ou **surcharger** (redéfinir) des méthodes.

```python
class Vehicule:
    def __init__(self, nom):
        self.nom = nom

    def demarrer(self):
        print(f"{self.nom} démarre.")

class Voiture(Vehicule):
    def __init__(self, nom, conso_l_100km):
        super().__init__(nom)                 # appel au constructeur parent
        self.conso_l_100km = conso_l_100km

    def consommation(self, distance_km):
        litres = distance_km * self.conso_l_100km / 100
        return f"{self.nom} consomme ~{litres:.1f} L sur {distance_km} km."

v = Voiture("Renault", 5.2)
v.demarrer()                         # hérité
>>>
Renault démarre.

print(v.consommation(150))           # surchargé/ajouté
>>>
Renault consomme ~7.8 L sur 150 km.
```

**À retenir**

* `super()` permet de réutiliser proprement le code du parent (ex. initialisation).
* On peut surcharger une méthode du parent pour un comportement spécifique.

***

## 2. Polymorphisme : même interface, comportements adaptés

Le polymorphisme consiste à définir la **même méthode** sur plusieurs classes, et laisser chaque classe fournir **sa propre implémentation**.

```python
class Vehicule:
    def autonomie(self):
        raise NotImplementedError("À implémenter dans les sous-classes")

class VoitureThermique(Vehicule):
    def __init__(self, reservoir_l, conso_l_100km):
        self.reservoir_l = reservoir_l
        self.conso_l_100km = conso_l_100km
    def autonomie(self):
        return 100 * self.reservoir_l / self.conso_l_100km

class VoitureElectrique(Vehicule):
    def __init__(self, batterie_kwh, conso_kwh_100km):
        self.batterie_kwh = batterie_kwh
        self.conso_kwh_100km = conso_kwh_100km
    def autonomie(self):
        return 100 * self.batterie_kwh / self.conso_kwh_100km

flotte = [
    VoitureThermique(50, 5.0),
    VoitureElectrique(60, 15.0)
]

for car in flotte:
    print(f"Autonomie ≈ {car.autonomie():.0f} km")
>>>
Autonomie ≈ 1000 km
Autonomie ≈ 400 km
```

Ici, `autonomie()` existe dans les deux classes, mais son **calcul dépend du type** de véhicule.\
Le code client (la boucle) n’a pas besoin de savoir **quel** type précis il manipule → c’est le **principe clé** du polymorphisme.

***

## 3. Dataclasses : classes “porte-données” sans boilerplate

Les **dataclasses** (Python 3.7+) génèrent automatiquement des méthodes “standard” (`__init__`, `__repr__`, `__eq__`, …) selon les **annotations de types**.\
Parfait pour stocker des données simples.

```python
from dataclasses import dataclass

@dataclass
class Batiment:
    nom: str
    surface_m2: float
    conso_kwh_m2: float

    @property
    def conso_totale(self) -> float:
        return self.surface_m2 * self.conso_kwh_m2

b = Batiment("Bibliothèque", 1200, 15.2)
print(b)
>>> 
Batiment(nom='Bibliothèque', surface_m2=1200, conso_kwh_m2=15.2)

print(b.conso_totale)
>>>
18240.0
```

#### Options utiles

* `frozen=True` → rend l’objet **immuable** (comme un tuple)
* `slots=True` → réduit la mémoire / accélère l’accès aux attributs
* `order=True` → compare/ordonne les instances selon les champs

```python
from dataclasses import dataclass

@dataclass(frozen=True, slots=True)
class Capteur:
    id: str
    type: str
    localisation: str

c = Capteur("S01", "PM10", "Quai A")
print(c)
# c.localisation = "Quai B"  # ❌ Erreur si frozen=True (objet immuable)
```

***

## 4. Bonus

### Propriétés, méthodes de classe et méthodes statiques

#### `@property` : attribut calculé (interface propre)

<pre class="language-python"><code class="lang-python"><strong>class Rectangle:
</strong>    def __init__(self, L, l):
        self.L = L
        self.l = l

    @property
    def aire(self):
        return self.L * self.l

r = Rectangle(4, 3)
print(r.aire)
>>>
12 
#(sans parenthèses → comme un attribut)
</code></pre>

#### `@classmethod` : méthode liée à la **classe**

Utile pour des **constructeurs alternatifs**.

```python
class Batiment:
    def __init__(self, nom, surface_m2):
        self.nom = nom
        self.surface_m2 = surface_m2

    @classmethod
    def depuis_pieds_carres(cls, nom, surface_ft2):
        return cls(nom, surface_ft2 * 0.092903)

b = Batiment.depuis_pieds_carres("Hall", 10000)
print(b.surface_m2)
>>>
929.03
```

#### `@staticmethod` : utilitaire **sans `self` ni `cls`**

```python
class Energie:
    @staticmethod
    def kwh_to_mwh(kwh):
        return kwh / 1000

print(Energie.kwh_to_mwh(18500))
>>>
18.5
```

### Classes abstraites (contrat d’interface)

Les **classes abstraites** définissent un contrat (méthodes à implémenter).\
Elles évitent d’instancier par erreur une classe incomplète.

```python
from abc import ABC, abstractmethod

class ModeleQualiteAir(ABC):
    @abstractmethod
    def predire_pm10(self, features):
        pass

class ModeleLineaire(ModeleQualiteAir):
    def predire_pm10(self, features):
        # implémentation simplifiée
        return 0.5*features["trafic"] + 0.2*features["vent"] - 0.1*features["pluie"]

m = ModeleLineaire()
print(m.predire_pm10({"trafic": 80, "vent": 10, "pluie": 2}))
>>> 
41.8
```

### Méthodes spéciales (dunder)

Elles rendent vos objets “naturels” à utiliser.

```python
class Vecteur2D:
    def __init__(self, x, y): self.x, self.y = x, y
    def __repr__(self): return f"Vecteur2D({self.x}, {self.y})"
    def __add__(self, other): return Vecteur2D(self.x + other.x, self.y + other.y)
    def __len__(self): return int((self.x**2 + self.y**2) ** 0.5)

v1, v2 = Vecteur2D(2, 3), Vecteur2D(1, -1)
print(v1 + v2)
>>>
Vecteur2D(3, 2)

print(len(v1))
>>>
3
```

***

## À retenir

* **Héritage** : partage et spécialisation du comportement (penser à `super()`).
* **Polymorphisme** : même “interface”, implémentations spécifiques par classe.
* **Dataclasses** : classes porte-données rapides, lisibles, avec moins de code.
* (Bonus) **property / classmethod / staticmethod** : interfaces plus propres.
* (Bonus) **ABC** et **méthodes spéciales** : designer des contrats et rendre vos objets “pythoniques”.

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
