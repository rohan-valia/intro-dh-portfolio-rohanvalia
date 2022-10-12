---
layout: page
title: Crowdsourced-Data Normalization with Python and Pandas
description: This lesson uses crowdsourcing as a form of data creation and explains how pandas can be used to prepare a crowdsourced dataset to be analyzed.
---
## Source
[Halle Burns, "Crowdsourced-Data Normalization with Python and Pandas," Programming Historian (2021)](programminghistorian.org/en/lessons/crowdsourced-data-normalization-with-pandas.

## Reflection
Crowdsourcing is the practice of collecting data or information from an outsourced group of people through an online platform. In this example from the Programming Historian, crowdsourcing is used to determine whether longer menus were more popular during certain times of the year using the New York Public Library Historical Menu Dataset.

The code in this example was logical and made sense in terms of how it was applied in the data cleaning and data normalization process. The deletion of null columns and rows made sense in getting rid of any excess space in our dataset and cleaning our data. When removing data from this dataset, I learned that it presents the possibility of altering the autenticity and historical value of the dataset. With these challenges that came with cleaning our dataset, I was able to understand how although crowdsourcing can be efficient, it presents a difficulty in data normalization that can often offsets its advantages. This was most apparant when trying to convert the dates to datetime datatypes, which caused an error in our program that required us to manually find and replace each date.

## Code

```python
import pandas as pd

df = pd.read_csv("Menu.csv")
print(df.head())
```

          id name                     sponsor                 event       venue  \
    0  12463  NaN               HOTEL EASTMAN             BREAKFAST  COMMERCIAL   
    1  12464  NaN            REPUBLICAN HOUSE              [DINNER]  COMMERCIAL   
    2  12465  NaN  NORDDEUTSCHER LLOYD BREMEN  FRUHSTUCK/BREAKFAST;  COMMERCIAL   
    3  12466  NaN  NORDDEUTSCHER LLOYD BREMEN                LUNCH;  COMMERCIAL   
    4  12467  NaN  NORDDEUTSCHER LLOYD BREMEN               DINNER;  COMMERCIAL   
    
                                    place         physical_description occasion  \
    0                     HOT SPRINGS, AR              CARD; 4.75X7.5;  EASTER;   
    1                    MILWAUKEE, [WI];   CARD; ILLUS; COL; 7.0X9.0;  EASTER;   
    2  DAMPFER KAISER WILHELM DER GROSSE;    CARD; ILLU; COL; 5.5X8.0;      NaN   
    3  DAMPFER KAISER WILHELM DER GROSSE;    CARD; ILLU; COL; 5.5X8.0;      NaN   
    4  DAMPFER KAISER WILHELM DER GROSSE;  FOLDER; ILLU; COL; 5.5X7.5;      NaN   
    
                                                   notes call_number  keywords  \
    0                                                NaN   1900-2822       NaN   
    1  WEDGEWOOD BLUE CARD; WHITE EMBOSSED GREEK KEY ...   1900-2825       NaN   
    2  MENU IN GERMAN AND ENGLISH; ILLUS, STEAMSHIP A...   1900-2827       NaN   
    3  MENU IN GERMAN AND ENGLISH; ILLUS, HARBOR SCEN...   1900-2828       NaN   
    4  MENU IN GERMAN AND ENGLISH; ILLUS, HARBOR SCEN...   1900-2829       NaN   
    
       language       date                    location  location_type currency  \
    0       NaN  4/15/1900               Hotel Eastman            NaN      NaN   
    1       NaN  4/15/1900            Republican House            NaN      NaN   
    2       NaN  4/16/1900  Norddeutscher Lloyd Bremen            NaN      NaN   
    3       NaN  4/16/1900  Norddeutscher Lloyd Bremen            NaN      NaN   
    4       NaN  4/16/1900  Norddeutscher Lloyd Bremen            NaN      NaN   
    
      currency_symbol    status  page_count  dish_count  
    0             NaN  complete           2          67  
    1             NaN  complete           2          34  
    2             NaN  complete           2          84  
    3             NaN  complete           2          63  
    4             NaN  complete           4          33  



```python
print(df.columns)
```

    Index(['id', 'name', 'sponsor', 'event', 'venue', 'place',
           'physical_description', 'occasion', 'notes', 'call_number', 'keywords',
           'language', 'date', 'location', 'location_type', 'currency',
           'currency_symbol', 'status', 'page_count', 'dish_count'],
          dtype='object')



```python
dropped_col = ['notes', 'call_number', 'currency', 'currency_symbol', 'physical_description', 'status']
df.drop(dropped_col, inplace=True, axis=1)
```


```python
print(df.shape)
```

    (17546, 14)



```python
print(df[df.duplicated(keep=False)])
```

              id name        sponsor      event       venue            place  \
    0      12463  NaN  HOTEL EASTMAN  BREAKFAST  COMMERCIAL  HOT SPRINGS, AR   
    17545  12463  NaN  HOTEL EASTMAN  BREAKFAST  COMMERCIAL  HOT SPRINGS, AR   
    
          occasion  keywords  language       date       location  location_type  \
    0      EASTER;       NaN       NaN  4/15/1900  Hotel Eastman            NaN   
    17545  EASTER;       NaN       NaN  4/15/1900  Hotel Eastman            NaN   
    
           page_count  dish_count  
    0               2          67  
    17545           2          67  



```python
df.drop_duplicates(inplace=True)
```


```python
print(df.shape)
```

    (17545, 14)



```python
print(df.isnull().sum())
```

    id                   0
    name             14348
    sponsor           1561
    event             9391
    venue             9426
    place             9422
    occasion         13754
    keywords         17545
    language         17545
    date               586
    location             0
    location_type    17545
    page_count           0
    dish_count           0
    dtype: int64



```python
menu = df.dropna(thresh=df.shape[0]*0.25,how='all',axis=1)
```


```python
print(menu.shape)
```

    (17545, 9)



```python
print(menu.columns)
```

    Index(['id', 'sponsor', 'event', 'venue', 'place', 'date', 'location',
           'page_count', 'dish_count'],
          dtype='object')



```python
dropped_na = menu.dropna()
print(dropped_na)
```

              id                                            sponsor  \
    0      12463                                      HOTEL EASTMAN   
    1      12464                                   REPUBLICAN HOUSE   
    2      12465                         NORDDEUTSCHER LLOYD BREMEN   
    3      12466                         NORDDEUTSCHER LLOYD BREMEN   
    4      12467                         NORDDEUTSCHER LLOYD BREMEN   
    ...      ...                                                ...   
    10212  27695  CONFRERIE DE LA CHAINE DES ROTISSEURS, NEW ORL...   
    10213  27696  CONFRERIE DE LA CHAINE DES ROTISSEURS, GEORGIA...   
    10214  27697                                  FRANKFURTER STUBB   
    10215  27698                             HOTEL EUROPAISCHER HOF   
    10216  27699  CONFRERIE DE LA CHAINE DES ROTISSEURS, OKLAHOM...   
    
                                          event                 venue  \
    0                                 BREAKFAST            COMMERCIAL   
    1                                  [DINNER]            COMMERCIAL   
    2                      FRUHSTUCK/BREAKFAST;            COMMERCIAL   
    3                                    LUNCH;            COMMERCIAL   
    4                                   DINNER;            COMMERCIAL   
    ...                                     ...                   ...   
    10212                                DINNER  OTHER (PRIVATE CLUB)   
    10213                                DINNER  OTHER (PRIVATE CLUB)   
    10214                            DAILY MENU            HOTEL; FOR   
    10215                                DINNER            HOTEL; FOR   
    10216  INAUGURATION OF THE OKLAHOME CHAPTER  OTHER (PRIVATE CLUB)   
    
                                                       place       date  \
    0                                        HOT SPRINGS, AR  4/15/1900   
    1                                       MILWAUKEE, [WI];  4/15/1900   
    2                     DAMPFER KAISER WILHELM DER GROSSE;  4/16/1900   
    3                     DAMPFER KAISER WILHELM DER GROSSE;  4/16/1900   
    4                     DAMPFER KAISER WILHELM DER GROSSE;  4/16/1900   
    ...                                                  ...        ...   
    10212                     PLIMSOLL CLUB, NEW ORLEANS, LA  5/13/1968   
    10213        PIEDMONT DRIVING  CLUB,  [ATLANTA?] GEORGIA  5/18/1968   
    10214       HOTEL FRANKFURTER, FRANFURT AM MAIN, GERMANY   6/3/1968   
    10215                                HEIDELBERG, GERMANY  6/26/1968   
    10216  OKLAHOMA CITY GOLF AND COUNTRY CLUB, OKLAHOMA ...   7/1/1968   
    
                                                    location  page_count  \
    0                                          Hotel Eastman           2   
    1                                       Republican House           2   
    2                             Norddeutscher Lloyd Bremen           2   
    3                             Norddeutscher Lloyd Bremen           2   
    4                             Norddeutscher Lloyd Bremen           4   
    ...                                                  ...         ...   
    10212  Confrerie De La Chaine Des Rotisseurs, New Orl...           5   
    10213              Confrerie De La Chaine Des Rotisseurs           3   
    10214              Confrerie De La Chaine Des Rotisseurs           3   
    10215  Confrerie De La Chaine Des Rotisseurs, New Orl...           1   
    10216              Confrerie De La Chaine Des Rotisseurs           4   
    
           dish_count  
    0              67  
    1              34  
    2              84  
    3              63  
    4              33  
    ...           ...  
    10212          37  
    10213          22  
    10214          34  
    10215          31  
    10216          24  
    
    [7236 rows x 9 columns]



```python
# pd.to_datetime(dropped_na['date'], dayfirst = False, yearfirst = False)
replaced_dates = dropped_na.replace('0190-03-06', '12-31-2200') 
```


```python
replaced_dates.to_csv("NYPL_NormalMenus.csv")
```


```python

```
