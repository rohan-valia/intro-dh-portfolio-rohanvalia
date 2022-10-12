---
layout: page
title: Exercises Ch. 4
description: Select exercises from Python Crash Course
---

```python
# 4-1

pizzas = ["pepperoni", "meat lovers", "bbq chicken"]

for i in pizzas:
    print("I like "+str(i)+" pizza.")
print("I'm a big fan of pizza!")
```

    I like pepperoni pizza.
    I like meat lovers pizza.
    I like bbq chicken pizza.
    I'm a big fan of pizza!



```python
# 4-2

animals = ["tiger", "jaguar", "leopard"]

for i in animals:
    print("A "+str(i)+" is native to Africa.")
print("All of these animals are in the cat family.")
```

    A tiger is native to Africa.
    A jaguar is native to Africa.
    A leopard is native to Africa.
    All of these animals are in the cat family.



```python
# 4-3
for i in range(1,21):
    print(i)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20



```python
#4-6

even = []
odd = []

for i in range(1,21):
    if i % 2 == 0:
        even.append(i)
    else:
        odd.append(i)
print(odd)
```

    [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]



```python
# 4-10

animals = ["tiger", "jaguar", "leopard", "giraffe", "gorilla", "lion", "monkey", "gazelle", "deer"]

print("The first three items in the list are: "+str(animals[0:3]))
print("The middle three items in the list are: "+str(animals[3:6]))
print("The last three items in the list are: "+str(animals[6:9]))
```

    The first three items in the list are: ['tiger', 'jaguar', 'leopard']
    The middle three items in the list are: ['giraffe', 'gorilla', 'lion']
    The last three items in the list are: ['monkey', 'gazelle', 'deer']



```python
# 4-11

pizzas = ["pepperoni", "meat lovers", "bbq chicken", "the works"]
print("My favorite pizzas are:")
for i in pizzas:
    print(str(i))

```

    My favorite pizzas are:
    pepperoni
    meat lovers
    bbq chicken
    the works



```python
friend_pizzas = ["cheese", "pepperoni", "veggie", "hawaiian"]
print("My friend's favorite pizzas are:")
for i in friend_pizzas:
    print(str(i))
```

    My friend's favorite pizzas are:
    cheese
    pepperoni
    veggie
    hawaiian



```python

```


```python

```
