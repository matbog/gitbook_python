---
icon: font-case
---

# Les chaînes de caractères (strings)

En Python, le texte est représenté par le type **`str`**.\
On écrit une chaîne de caractères entre guillemets simples `'...'` ou doubles `"..."`.

```python
nom = "Alice"
ville = 'Paris'
print(nom, ville)
>>>
Alice Paris
```

## 1. Les bases

### Longueur d’une chaîne

```python
mot = "Python"
print(len(mot))
>>>
6
```

### Indexation et slicing

On peut accéder aux caractères un par un (l’index commence à 0) :

```python
mot = "Python"
print(mot[0])   # (premier caractère)
>>>
P 

print(mot[-1])  # (dernier caractère)
>>>
n

print(mot[0:3]) # (caractères d’indice 0 à 2)
>>>
Pyt
```

## 2. Transformations courantes

<pre class="language-python"><code class="lang-python">texte = "  Bonjour le Monde  "

print(texte.upper())   # (majuscules)
>>>
  BONJOUR LE MONDE

print(texte.lower())   # (minuscules)
>>>
<strong>  bonjour le monde
</strong>
print(texte.strip())   # (supprime espaces au début et à la fin)
>>>
Bonjour le Monde

print(texte.replace("Bonjour", "Salut") 
>>>
  Salut le Monde  
</code></pre>

## 3. Concaténation et formatage

### Concaténer avec `+`

```python
prenom = "Alice"
age = 25
message = "Je m'appelle " + prenom + " et j'ai " + str(age) + " ans."
print(message)
>>>
Je m'appelle Alice et j'ai 25 ans.
```

## 4. Utiliser les **f-strings** (recommandé)

Les **f-strings** (introduites en Python 3.6) ne servent pas seulement à insérer des variables dans une chaîne.\
On peut aussi **contrôler l’affichage** : nombre de décimales, alignement, pourcentages, etc.

```python
prenom = "Alice"
age = 25
print(f"Bonjour, je suis {prenom} et j’ai {age} ans.")
>>>
Bonjour, je suis Alice et j'ai 25 ans.
```

#### 4.1. Formater des nombres

```python
pi = 3.14159265
pourcentage = 0.8734

print(f"Pi ≈ {pi:.2f}")       # 3.14 (2 décimales)
print(f"Pi ≈ {pi:8.3f}")      # '   3.142' (aligné sur 8 caractères)
print(f"Taux : {pourcentage:.1%}")  # 87.3%
```

#### 4.2. Aligner du texte

On peut aussi définir la largeur et l’alignement du texte.

```python
nom = "Alice"
print(f"|{nom:<10}|")  # aligné à gauche
print(f"|{nom:^10}|")  # centré
print(f"|{nom:>10}|")  # aligné à droite
```

Résultat :

```
|Alice     |
|  Alice   |
|     Alice|
```

#### 4.3. Afficher des [dictionnaires](https://matbog.gitbook.io/python/basics/les-dictionnaires) ou objets

On peut accéder directement aux clés ou attributs dans une f-string :

```python
personne = {"nom": "Dupont", "age": 30}

print(f"Nom : {personne['nom']}, Âge : {personne['age']} ans")

class Batiment:
    def __init__(self, nom, surface):
        self.nom = nom
        self.surface = surface

gare = Batiment("Gare de Lyon", 1200)
print(f"Bâtiment : {gare.nom}, surface = {gare.surface} m²")
```

## 5. Initiation aux expressions régulières (regex)

Les **regex** permettent de rechercher ou transformer du texte selon des motifs.\
En Python, on utilise le module `re`.

### Exemples simples

#### Exemple : vérifier si une chaîne contient un chiffre

```python
import re

texte = "Station A - Ligne 14"
motif = r"\d+"  # motif = une ou plusieurs chiffres

resultat = re.findall(motif, texte)
print(resultat)
>>>
['14']
```

#### Exemple : extraire un mot commençant par "St"

```python
texte = "Station A - Ligne 14"
motif = r"St\w+"

resultat = re.findall(motif, texte)
print(resultat)
>>>
['Station']
```

### Exemples un peu plus avancés

#### Exemple 1 : Vérifier un format (e-mail)

Avec les regex, on peut contrôler si une chaîne respecte un certain **format**.\
Ici : vérifier si un texte ressemble à une adresse e-mail simple.

```python
import re

emails = ["contact@exemple.com", "hello.world", "test123@mail.fr"]

motif = r"^[\w\.-]+@[\w\.-]+\.\w+$"

for e in emails:
    if re.match(motif, e):
        print(e, "✅ est une adresse valide")
    else:
        print(e, "❌ n'est pas valide")

>>>
contact@exemple.com ✅ est une adresse valide
hello.world ❌ n'est pas valide
test123@mail.fr ✅ est une adresse valide
```

#### Exemple 2 : Extraire des nombres d’un texte

Dans des données de capteurs, on rencontre souvent des mesures cachées dans une chaîne de caractères.

```python
texte = "Température = 21.7°C, Humidité = 45%"
motif = r"[-+]?\d*\.?\d+"  # nombres entiers ou décimaux

nombres = re.findall(motif, texte)
print(nombres)
>>>
['21.7', '45']
```

On peut ensuite convertir en nombres réels :

```python
nombres = [float(x) for x in nombres]
print(nombres)
>>> 
[21.7, 45.0]
```

Ces exemples montrent comment utiliser les chaînes et les regex pour :

* **valider** un format (utile pour vérifier des mails, numéros, codes),
* **extraire** des informations d’un texte (logs, capteurs, fichiers

## 6. Construire des motifs (regex)

Une **expression régulière** (regex) est une petite “langue” qui décrit un motif dans un texte.\
Elles sont très utilisées pour **chercher, filtrer ou extraire** des chaînes de caractères complexes (mails, codes, dates, etc.).

### Symboles de base

<table><thead><tr><th width="131">Symbole</th><th>Signification</th><th>Exemple</th><th>Correspondance</th></tr></thead><tbody><tr><td><code>.</code></td><td>n’importe quel caractère</td><td><code>a.c</code></td><td><code>"abc"</code>, <code>"a2c"</code>, …</td></tr><tr><td><code>\d</code></td><td>un chiffre (0–9)</td><td><code>\d\d</code></td><td><code>"42"</code></td></tr><tr><td><code>\w</code></td><td>une lettre ou chiffre (<code>a-z</code>, <code>A-Z</code>, <code>0-9</code>, <code>_</code>)</td><td><code>\w+</code></td><td><code>"Python3"</code></td></tr><tr><td><code>\s</code></td><td>un espace (ou tabulation)</td><td><code>\s+</code></td><td><code>" "</code></td></tr><tr><td><code>^</code></td><td>début de chaîne</td><td><code>^Hello</code></td><td><code>"Hello world"</code></td></tr><tr><td><code>$</code></td><td>fin de chaîne</td><td><code>world$</code></td><td><code>"Hello world"</code></td></tr><tr><td><code>[]</code></td><td>une liste de caractères possibles</td><td><code>[abc]</code> → <code>"a"</code>, <code>"b"</code>, ou <code>"c"</code></td><td></td></tr><tr><td><code>[^ ]</code></td><td>tout sauf…</td><td><code>[^0-9]</code> → tout sauf un chiffre</td><td></td></tr><tr><td><code>*</code></td><td>0 ou plusieurs répétitions</td><td><code>ha*</code> → <code>"h"</code>, <code>"ha"</code>, <code>"haa"</code>, …</td><td></td></tr><tr><td><code>+</code></td><td>1 ou plusieurs répétitions</td><td><code>ha+</code> → <code>"ha"</code>, <code>"haa"</code>, mais pas <code>"h"</code></td><td></td></tr><tr><td><code>?</code></td><td>0 ou 1 répétition</td><td><code>colou?r</code> → <code>"color"</code> ou <code>"colour"</code></td><td></td></tr></tbody></table>

### Exemple 1 : extraire tous les numéros de téléphone simples

```python
import re

texte = "Appelle-moi au 01-45-67-89-00 ou au 06-12-34-56-78."
motif = r"\d{2}-\d{2}-\d{2}-\d{2}-\d{2}"

print(re.findall(motif, texte))
>>>
['01-45-67-89-00', '06-12-34-56-78']
```

### Exemple 2 : filtrer des mots spécifiques

```python
texte = "Le train arrive à Paris, puis continue vers Lyon et Marseille."
motif = r"(Paris|Lyon)"  # correspond à "Paris" OU "Lyon"

print(re.findall(motif, texte))
>>>
['Paris', 'Lyon']
```

#### Exemple 3 : extraire les majuscules

```python
texte = "Le TGV part de Paris Gare de Lyon"
motif = r"[A-Z]"

print(re.findall(motif, texte))
>>>
['L', 'T', 'G', 'V', 'P', 'G', 'L']
```

#### **Astuce**

vous pouvez tester vos regex en ligne avec des outils comme [regex101.com](https://regex101.com/), très pratique pour comprendre ce qui est reconnu.

## 👉 Retenir

* Une **string** est un texte entre `'` ou `"`.
* On peut la manipuler facilement avec les méthodes `.upper()`, `.lower()`, `.strip()`, `.replace()`.
* La **concaténation** peut se faire avec `+`, mais les **f-strings** sont plus simples et lisibles.
* Les **regex (`re`)** permettent d’aller beaucoup plus loin : rechercher des motifs complexes, extraire ou transformer des morceaux de texte.
