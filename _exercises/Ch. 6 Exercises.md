---
layout: page
title: Exercises Ch. 6
description: Select exercises from Python Crash Course
---

```python
# 6-1

person = {"firstname": "Stephen", "lastname": "Curry", "age": 34, "city": "San Francisco"}
print(person["firstname"])
print(person["lastname"])
print(person["age"]) 
print(person["city"])
```

    Stephen
    Curry
    34
    San Francisco



```python
# 6-2

numbers = {"Trent":8, "Dennis":15, "Mark":12, "Jonathan":0, "Moses":4}
print("Trent:", numbers["Trent"])
print("Dennis:", numbers["Dennis"])
print("Mark:", numbers["Mark"])
print("Jonathan:", numbers["Jonathan"])
print("Moses:", numbers["Moses"])

```

    Trent: 8
    Dennis: 15
    Mark: 12
    Jonathan: 0
    Moses: 4



```python
# 6-3

glossary = {"loop":"to go through a section of code and perform a set of actions", 
            "key-value":"a pair of terms that are linked in a dictionary",
            "string":"classified by python as text",
            "integer":"a whole number in python", "float":"a decimal number in python"}
print("loop:",glossary["loop"])
print("key-value:",glossary["key-value"])
print("string:",glossary["string"])
print("integer:",glossary["integer"])
print("float:",glossary["float"])

```

    loop: to go through a section of code and perform a set of actions
    key-value: a pair of terms that are linked in a dictionary
    string: classified by python as text
    integer: a whole number in python
    float: a decimal number in python



```python
# 6-4 

keys = list(glossary.keys())
for i in keys:
    print(i+": "+ glossary[i])

glossary["append"] = "to add a value to a list"
glossary["pop"] = "to remove a value from a list"
glossary["strip"] = "to remove whitespace from a string"
glossary["index"] = "to select a value from a list"
glossary["variable"] = "used to store values in a specific location"

print("\n")
keys = list(glossary.keys())
for i in keys:
    print(i+": "+ glossary[i])

```

    loop: to go through a section of code and perform a set of actions
    key-value: a pair of terms that are linked in a dictionary
    string: classified by python as text
    integer: a whole number in python
    float: a decimal number in python
    
    
    loop: to go through a section of code and perform a set of actions
    key-value: a pair of terms that are linked in a dictionary
    string: classified by python as text
    integer: a whole number in python
    float: a decimal number in python
    append: to add a value to a list
    pop: to remove a value from a list
    strip: to remove whitespace from a string
    index: to select a value from a list
    variable: used to store values in a specific location



```python
# 6-5

rivers = {"Amazon River": "South America", "Colorado River": "United States", "Missouri River": "United States"}
river_key = list(rivers.keys())

for i in river_key:
    print("The "+i+" runs through "+rivers[i])
    
```

    The Amazon River runs through South America
    The Colorado River runs through United States
    The Missouri River runs through United States



```python
# 6-6

favorite_languages = {'jen': 'python',
                      'sarah': 'c',
                      'edward': 'ruby',
                      'phil': 'python'}

new_pollers = ["steven", "sarah", "edward", "patty"]

existing_keys = list(favorite_languages.keys())
for i in new_pollers: 
    if i in existing_keys:
        print("Thank you for responding.")
    else:
        print("Please take the poll.")

```

    Please take the poll.
    Thank you for responding.
    Thank you for responding.
    Please take the poll.



```python
# 6-7

people = {"stephcurry": 
          {"firstname": "Stephen", "lastname": "Curry", "age": 34, "city": "San Francisco"}, 
          "lukadoncic": 
          {"firstname":"Luka", "lastname": "Doncic", "age": 23, "city": "Dallas"}, 
          "paulgeorge": {"firstname": "Paul", "lastname": "George", "age": 32, "city": "Los Angeles"}}


for i in people.items():
    print("Full name: "+i[1]["firstname"]+" "+i[1]["lastname"]+", "+"Age: "+str(i[1]["age"])+", City: "+i[1]["city"])

```

    Full name: Stephen Curry, Age: 34, City: San Francisco
    Full name: Luka Doncic, Age: 23, City: Dallas
    Full name: Paul George, Age: 32, City: Los Angeles



```python
# 6-8

pets = {"pet1": 
        {"animal":"dog", "owner":"James Pierce"}, 
        "pet2":
        {"animal":"cat", "owner": "Craig David"},
        "pet3":
        {"animal":"parrot", "owner": "Landon Norris"}}

for i in pets.items():
    print("Animal: "+i[1]["animal"]+", Owner Name: "+i[1]["owner"])
```

    Animal: dog, Owner Name: James Pierce
    Animal: cat, Owner Name: Craig David
    Animal: parrot, Owner Name: Landon Norris



```python
# 6-9

favorite_places = {"Randolph":
                   {"Randolph":"Stockholm"},
                   "Simon":
                   {"Simon":"Berlin"},
                   "Harry":
                   {"Harry":"Paris"},
                   "Ethan":
                   {"Ethan":"London"}}

for i in favorite_places.items():
    print(i[0]+"'s favorite place is "+i[1][i[0]])
```

    Randolph's favorite place is Stockholm
    Simon's favorite place is Berlin
    Harry's favorite place is Paris
    Ethan's favorite place is London



```python
# 6-11

cities = {"Stockholm":
          {"Country":"Sweden", "Population":"975,551", "Fact":"Stockholm is one of the cleanest cities in Europe."},
          "Berlin":
          {"Country":"Germany", "Population":"3,645,000", "Fact":"Berlin is home to the world's longest beer garden."},
          "Paris":
          {"Country":"France", "Population":"2,161,000", "Fact":"Paris has five statues of liberties."},
          "London":
          {"Country":"England", "Population":"8,982,000", "Fact":"London is home to the most billionaires in the world."}}

for i in cities.items():
    print("\nCity: "+i[0]+"\nCountry: "+i[1]["Country"]+"\nPopulation: "+i[1]["Population"]+"\nFact: "+i[1]["Fact"])
```

    
    City: Stockholm
    Country: Sweden
    Population: 975,551
    Fact: Stockholm is one of the cleanest cities in Europe.
    
    City: Berlin
    Country: Germany
    Population: 3,645,000
    Fact: Berlin is home to the world's longest beer garden.
    
    City: Paris
    Country: France
    Population: 2,161,000
    Fact: Paris has five statues of liberties.
    
    City: London
    Country: England
    Population: 8,982,000
    Fact: London is home to the most billionaires in the world.



```python

```
