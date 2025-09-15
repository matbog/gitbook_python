---
icon: glasses
---

# Lire des fichiers (xlsx / csv / pkl)

## Lire des fichiers `CSV`

Quelques options de base utiles&#x20;

{% embed url="https://pandas.pydata.org/docs/reference/api/pandas.read_csv.html" %}

```python
import pandas as pd
data = pd.read_csv(
        '/path/to/file.csv',   # Path to the file
        delimiter=',',         # delimiter for the CSV encoding ! UTILE EN FRANCE
        decimal='.',           # decimal separator / Usefull for french files where the coma ',' is often used
        header='infer',        # Usefull if there is a clean header
        skiprows=1,            # Skip N rows
        nrows=1000             # Number of rows to read
        # if the csvc index is already a "time"
        parse_dates=True,
        infer_datetime_format=True,
       )     
```

## Lire des fichiers `Excel`

{% embed url="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_excel.html" %}

```python
import pandas as pd
data = pd.read_excel_csv(
        '/path/to/file.xlsx',   # Path to the Excel file
        #Options utiles
        sheet_name=0, # le nom de la "feuille" excel
        index_col = 0, # le numero de la colonne qui servira d'index
        dtype={'Name': str, 'Value': float} # type de colonnes {le nom de la colonne: le type de données}
       )   
```

## Lire des fichiers `PICKLE`

{% embed url="https://pandas.pydata.org/pandas-docs/version/2.1/reference/api/pandas.read_pickle.html" %}

Si vous utilisez des `pickle` (format de données python assez compressé) très utiles pour les "grosses" `dataframes` .

Si on lit une `dataframe` qui a été enregistré en `pickle`, à la lecture on la retrouve formatée de la même façon !&#x20;

```python
data = pd.read_pickle("./dummy.pkl")  
```

***

_<mark style="color:$info;">Auteur :</mark>_ [_<mark style="color:$info;">Mateusz Bogdan</mark>_](https://matbog.github.io/)\
&#xNAN;_<mark style="color:$info;">Contenu texte et illustrations :</mark>_ [_<mark style="color:$info;">CC BY 4.0</mark>_](https://creativecommons.org/licenses/by/4.0/)\
&#xNAN;_<mark style="color:$info;">Exemples de code :</mark>_ [_<mark style="color:$info;">MIT License</mark>_](https://opensource.org/licenses/MIT)
