---
icon: chart-simple-horizontal
---

# Catégoriser des données

`pd.cut` / `pd.qcut`

Une tâche courante lors du traitement des données consiste à regrouper des « valeurs » en catégories, soit pour les compter, soit pour les classer.&#x20;

Ici, nous nous concentrerons sur le deuxième cas. Une fonction intégrée de pandas est là pour vous : pd.**cut**. Elle permet de regrouper des valeurs en catégories et de les attribuer à une nouvelle colonne. Personnellement, je l’utilise souvent pour classer les valeurs de température de l’air en niveaux de confort (par exemple, 18 < T° < 25 serait « Neutre »). Voyons quelques exemples.

_Documentation officielle :_ [_`pandas.cut`_](https://pandas.pydata.org/docs/reference/api/pandas.cut.html)



```python
# Create a dataframe
>>>> df = pd.DataFrame(np.random.randint(0,10,size=10),
                    columns=["some_data"],
                    index=pd.date_range("20180101", periods=10))
>>>> df
Out[1]: 
            some_data
2018-01-01          2
2018-01-02          8
2018-01-03          9
2018-01-04          2
2018-01-05          3
2018-01-06          6
2018-01-07          7
2018-01-08          7
2018-01-09          6
2018-01-10          6

# If we want to bin value between for example as follow : [0-5] / [5-10]
>>>> df['binned_values'] = pd.cut(df['some_data'],
                                  bins=[0,5,10])

# With default parameter, we will get a result like the following, where the new column is labelled automaticaly
>>>> df
Out[2]: 
            some_data binned_values
2018-01-01          2        (0, 5]
2018-01-02          8       (5, 10]
2018-01-03          9       (5, 10]
2018-01-04          2        (0, 5]
2018-01-05          3        (0, 5]
2018-01-06          6       (5, 10]
2018-01-07          7       (5, 10]
2018-01-08          7       (5, 10]
2018-01-09          6       (5, 10]
2018-01-10          6       (5, 10]

# And for a more comprehensive label, we could add 
>>>> df['binned_values'] = pd.cut(df['some_data'],
                                  bins = [0,5,10],
                                  labels = ["lower than 5","greater or equal to 5"],
                                  include_lowest = True,
                                  right = False)

>>>> df
Out[3]: 
            some_data          binned_values
2018-01-01          2           lower than 5
2018-01-02          8  greater or equal to 5
2018-01-03          9  greater or equal to 5
2018-01-04          2           lower than 5
2018-01-05          3           lower than 5
2018-01-06          6  greater or equal to 5
2018-01-07          7  greater or equal to 5
2018-01-08          7  greater or equal to 5
2018-01-09          6  greater or equal to 5
2018-01-10          6  greater or equal to 5
```

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
