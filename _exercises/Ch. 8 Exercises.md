---
layout: page
title: Exercises Ch. 8
description: Select exercises from Python Crash Course
---

```python
# 8-1 

def display_messages():
    print("We are learning functions in this chapter.")

display_messages()
```

    We are learning functions in this chapter.



```python
# 8-2

def favorite_book(title):
    print("One of my favorite books is "+title+".")

favorite_book("The Giver")
```

    One of my favorite books is The Giver.



```python
# 8-3

def make_shirt(size, text):
    print("The size of the t-shirt is "+size+".")
    print("The text on the shirt will say "+text+".")

make_shirt("Medium", "United States of America")

make_shirt(text="United States of America", size="Medium")
    
```

    The size of the t-shirt is Medium.
    The text on the shirt will say United States of America.
    The size of the t-shirt is Medium.
    The text on the shirt will say United States of America.



```python
# 8-5

def describe_city(city, country="England"):
    print(city+" is in "+country+".")
    
describe_city("London")
describe_city("Manchester")
describe_city("Dublin")

```

    London is in England.
    Manchester is in England.
    Dublin is in England.



```python
# 8-6

def city_country(city,country):
    print(city+", "+country)
    
city_country("Stockholm","Sweden")
city_country("Milan","Italy")
city_country("Vienna","Austria")
```

    Stockholm, Sweden
    Milan, Italy
    Vienna, Austria



```python
# 8-7

def make_album(artist_name, album_title):
    album = {"artist":artist_name, "album":album_title}
    return album

print(make_album("Michael Jackson", "Thriller"))
print(make_album("The Beatles", "Abbey Road"))
print(make_album("Pink Floyd", "The Dark Side of the Moon"))

    
```

    {'artist': 'Michael Jackson', 'album': 'Thriller'}
    {'artist': 'The Beatles', 'album': 'Abbey Road'}
    {'artist': 'Pink Floyd', 'album': 'The Dark Side of the Moon'}



```python
# 8-7
def make_album(artist_name, album_title, song_count=None):
    if song_count:
        album = {"artist":artist_name, "album":album_title, "songs": song_count}
    else:
        album = {"artist":artist_name, "album":album_title}
    return album

print(make_album("Michael Jackson", "Thriller", 7))
print(make_album("Michael Jackson", "Thriller"))

```

    {'artist': 'Michael Jackson', 'album': 'Thriller', 'songs': 7}
    {'artist': 'Michael Jackson', 'album': 'Thriller'}



```python

```
