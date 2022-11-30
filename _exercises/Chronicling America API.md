---
layout: page
title: Chronicling America API Assignment
description: Here is the python notebook for the Chronicling America API assignment.
---

```python
# imports
import requests
import json
import math
import pandas as pd
import spacy
```


```python
# initial search

url = 'https://chroniclingamerica.loc.gov/search/pages/results/?state=&date1=1901&date2=1963&proxtext=capitalism&x=10&y=24&dateFilterType=yearRange&rows=20&searchType=basic&format=json'
response = requests.get(url)  
raw = response.text  
results = json.loads(raw)
```


```python
# find total amount of pages
results.keys()

total_pages = math.ceil(results['totalItems'] / results['itemsPerPage'])
total_pages
```




    179389




```python
# query the api and save to dict 

data = []
start_date = '1901'
end_date = '1963'
search_term = 'capitalism'
for i in range (1,11):
    url = (f'https://chroniclingamerica.loc.gov/search/pages/results/?state=&date1={start_date}'
           f'&date2={end_date}&proxtext={search_term}&x=16&y=8&dateFilterType=yearRange&rows=20'
           f'&searchType=basic&format=json&page={i}')  # f-string
    response = requests.get(url)
    raw = response.text
    print(response.status_code)  # checking for errors
    results = json.loads(raw)
    items_ = results['items']
    for item_ in items_:
        temp_dict = {}
        temp_dict['title'] = item_['title_normal']
        temp_dict['city'] = item_['city']
        temp_dict['date'] = item_['date']
        temp_dict['raw_text'] = item_['ocr_eng']
        data.append(temp_dict)
```

    200
    200
    200
    200
    200
    200
    200
    200
    200
    200



```python
# convert dict to dataframe
df = pd.DataFrame.from_dict(data)
```


```python
# convert date column from string to date-time object
df['date'] = pd.to_datetime(df['date'])
```


```python
# sort by date
sorted_df = df.sort_values(by='date')
```


```python
# write function to process text
nlp = spacy.load("en_core_web_sm")

def process_text(text):
    """Remove new line characters and lemmatize text. Returns string of lemmas"""
    text = text.replace('\n', ' ')
    doc = nlp(text)
    tokens = [token for token in doc]
    no_stops = [token for token in tokens if not token.is_stop]
    no_punct = [token for token in no_stops if token.is_alpha]
    lemmas = [token.lemma_ for token in no_punct]
    lemmas_lower = [lemma.lower() for lemma in lemmas]
    lemmas_string = ' '.join(lemmas_lower)
    return lemmas_string
```


```python
# apply process_text function to raw_text column
sorted_df['lemmas'] = sorted_df['raw_text'].apply(process_text)
```


```python
# save to csv
sorted_df.to_csv('chronicling_america_api.csv', index=False)
```


```python

```