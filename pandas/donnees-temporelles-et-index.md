---
description: Manipuler les index ou les colonnes avec des données temporelles
icon: clock
---

# Données temporelles et index

* Une `dataframe` exemple :

```python
import pandas as pd
# Create a random time indexed dataframe
df = pd.DataFrame(np.random.randint(0,10,size=10),
                  columns=["Random"],
                  index=pd.date_range("20180101", periods=10))
>>>> df

            Random
2018-01-01       5
2018-01-02       3
2018-01-03       5
2018-01-04       5
2018-01-05       3
2018-01-06       6
2018-01-07       0
2018-01-08       0
2018-01-09       3
2018-01-10       3

```

L'index est bien un temps, grâce à la commande `.date_range()` , et on a une donnée "journalière".&#x20;

### `.resample()`

Si maintenant on voulait travailler sur des données horaires, en interpolant les valeurs présentes dans la colonne `random`&#x20;

```python
# Obtenir une df avec un pas de temps horaire 
resampledDf =  df.resample('h')
# Remplissage des "nouveaux" index avec une interpolation linéaire
resampledDf.interpolate(method='linear') 
>>>
2018-01-01 00:00:00  5.000000
2018-01-01 01:00:00  4.916667
2018-01-01 02:00:00  4.833333
2018-01-01 03:00:00  4.750000
2018-01-01 04:00:00  4.666667
                      ...
2018-01-09 20:00:00  3.000000
2018-01-09 21:00:00  3.000000
2018-01-09 22:00:00  3.000000
2018-01-09 23:00:00  3.000000
2018-01-10 00:00:00  3.000000

[217 rows x 1 columns]
```

:warning: L'interpolation linéaire ne prends pas en compte le temps, mais rempli les "trous" comme s'ils étaient également espacées.&#x20;



### `.between_times()`

Permet de sélectionner des données entre des heures, sur la longueur de la `dataframe`. Exemple avec 48 de donénes, et on ne électionne que les données entre 10h et 14h :&#x20;



<pre class="language-python"><code class="lang-python"><strong>import pandas as pd
</strong><strong>import numpy as np
</strong># Création d'un index temporel horaire sur 2 jours
<strong>i = pd.date_range('2018-04-09', periods=48, freq='h')
</strong><strong># Création de la dataframe avec des valeurs aléatoires
</strong>df = pd.DataFrame({'A': np.random.randint(0,10,size=48)}, index=i)
print(df)
>>>
                     A
2018-04-09 00:00:00  3
2018-04-09 01:00:00  1
2018-04-09 02:00:00  5
...
2018-04-10 22:00:00  6
2018-04-10 23:00:00  6

df.between_time("10:00", "14:00") #  .between_times(start, end)
>>>
                     A
2018-04-09 10:00:00  4
2018-04-09 11:00:00  1
2018-04-09 12:00:00  4
2018-04-09 13:00:00  2
2018-04-09 14:00:00  0
2018-04-10 10:00:00  3
2018-04-10 11:00:00  6
2018-04-10 12:00:00  5
2018-04-10 13:00:00  3
2018-04-10 14:00:00  7


</code></pre>

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
