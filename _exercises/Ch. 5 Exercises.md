---
layout: page
title: Exercises Ch. 5
description: Select exercises from Python Crash Course
---

```python
# 5-1

headphones = "Bose"

print("Are headphones == 'Bose'? I predict True.")
print(headphones == "Bose")

print("Are headphones == 'Beats'? I predict False.")
print(headphones == "Beats")

wallet = "Coach"
print("\nIs wallet == 'Coach'? I predict True.")
print(wallet == "Coach")

print("Is wallet == 'Prada'? I predict False.")
print(wallet == "Prada")

backpack = "North Face"
print("\nIs backpack == 'North Face'? I predict True.")
print(backpack == "Bose")

print("Is backpack == 'Patagonia'? I predict False.")
print(backpack == "Patagonia")

pants = "Nike"
print("\nAre pants == 'Nike'? I predict True.")
print(pants == "Nike")

print("Are pants == 'Adidas'? I predict False.")
print(pants == "Adidas")

laptop = "Apple"
print("\nIs laptop == 'Apple'? I predict True.")
print(laptop == "Apple")

print("Is laptop == 'Dell'? I predict False.")
print(laptop == "Dell")



```

    Are headphones == 'Bose'? I predict True.
    True
    Are headphones == 'Beats'? I predict False.
    False
    
    Is wallet == 'Coach'? I predict True.
    True
    Is wallet == 'Prada'? I predict False.
    False
    
    Is backpack == 'North Face'? I predict True.
    False
    Is backpack == 'Patagonia'? I predict False.
    False
    
    Are pants == 'Nike'? I predict True.
    True
    Are pants == 'Adidas'? I predict False.
    False
    
    Is laptop == 'Apple'? I predict True.
    True
    Is laptop == 'Dell'? I predict False.
    False



```python
# 5-2

name = "Darius"
print(name == "Trent")
print(name == "Darius")

store = "Walgreens"
print(store.lower() == "walgreens")
print(store.lower() == "Walgreens")

number = 16
print(number == 55)
print(number == 16)
print(number < 4)
print(number > 10)
print(number >= 22)
print(number <= 16)

number2 = 32
print(number > 14 and number < 40)
print(number > 20 or number > 56)

numbers = [5, 10, 15, 20, 25, 30]
if 14 in numbers:
    print("True")
else:
    print("False")
    
if 15 in numbers:
    print("True")
else:
    print("False")
    

```

    False
    True
    True
    False
    False
    True
    False
    True
    False
    True
    True
    False
    False
    True



```python
# 5-6

person = 37

if person < 2:
    print("This person is a baby.")
elif person > 2 and person < 4:
    print("This person is a toddler.")
elif person > 4 and person < 13:
    print("This person is a kid.")
elif person > 13 and person < 20: 
    print("This person is a teenager.")
elif person > 20 and person < 65:
    print("This person is an adult.")
else:
    print("This person is an elder.")
```

    This person is an adult.



```python
# 5-7

favorite_fruits = ["peach", "watermelon", "grapes"]

if "watermelon" in favorite_fruits:
    print("Watermelon is in my top three fruit.")
if "strawberries" in favorite_fruits:
    print("Strawberries is in my top three fruit.")
if "pineapple" in favorite_fruits:
    print("Pineapple is in my top three fruit.")
if "grapes" in favorite_fruits:
    print("Grapes is in my top three fruit.")
if "peach" in favorite_fruits:
    print("Peach is in my top three fruit.")


```

    Watermelon is in my top three fruit.
    Grapes is in my top three fruit.
    Peach is in my top three fruit.



```python
# 5-8

usernames = ["Howard", "Darius","admin", "Zach", "Jayson"]
for i in usernames:
    if i == "admin":
        print("Hello admin, would you like to see a status report?")
    else: 
        print("Hello "+str(i)+", thank you for logging in again.")
```

    Hello Howard, thank you for logging in again.
    Hello Darius, thank you for logging in again.
    Hello admin, would you like to see a status report?
    Hello Zach, thank you for logging in again.
    Hello Jayson, thank you for logging in again.



```python
# 5-9

usernames.remove("Howard")
usernames.remove("Darius")
usernames.remove("admin")
usernames.remove("Zach")
usernames.remove("Jayson")

if len(usernames) > 0:
    print("There are usernames")
else:
    print("We need to find some users!")
```

    We need to find some users!



```python
# 5-10

current_users = ["anthonyd23", "dariusg10", "zachl8", "jaysont0", "blakeg32", "paytonp11"]
new_users = ["jordanp3", "montem12", "willb5", "jaysont0", "brandoni14", "scottieb4", "dariusg10"]

for i in new_users:
    if i in current_users:
        print("This username has already been used. Enter a new username.")
    else:
        print("This username is available.")

```

    This username is available.
    This username is available.
    This username is available.
    This username has already been used. Enter a new username.
    This username is available.
    This username is available.
    This username has already been used. Enter a new username.



```python

```
