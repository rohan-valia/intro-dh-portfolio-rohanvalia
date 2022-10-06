---
layout: page
title: Exercises Ch. 3
description: Select exercises from Python Crash Course
---


```python
# 3-1
names = ["Trey","Randy","Ryan"]
print(names[0])
print(names[1])
print(names[2])
```

    Trey
    Randy
    Ryan



```python
# 3-2
message = "Great to see you, "
print(message+str(names[0]))
print(message+str(names[1]))
print(message+str(names[2]))
```

    Great to see you, Trey
    Great to see you, Randy
    Great to see you, Ryan



```python
# 3-3
akers = ["Mercedes-Benz", "BMW", "Range Rover"]
message = "I would someday like to own a "
print(message+str(makers[0]))
print(message+str(makers[1]))
print(message+str(makers[2]))
```

    I would someday like to own a Mercedes-Benz
    I would someday like to own a BMW
    I would someday like to own a Range Rover



```python
# 3-4
guests = ["Lebron James","Barack Obama","Roger Federer"]
print("Hi "+guests[0]+", would you like to join me for dinner?")
print("Hi "+guests[1]+", would you like to join me for dinner?")
print("Hi "+guests[2]+", would you like to join me for dinner?")
```

    Hi Lebron James, would you like to join me for dinner?
    Hi Barack Obama, would you like to join me for dinner?
    Hi Roger Federer, would you like to join me for dinner?



```python
# 3-5
print(guests[0])
guests.remove("Lebron James")
guests.append("Kevin Durant")
print("Hi "+guests[0]+", would you like to join me for dinner?")
print("Hi "+guests[1]+", would you like to join me for dinner?")
print("Hi "+guests[2]+", would you like to join me for dinner?")
```

    Lebron James
    Hi Barack Obama, would you like to join me for dinner?
    Hi Roger Federer, would you like to join me for dinner?
    Hi Kevin Durant, would you like to join me for dinner?



```python
# 3-6
print("Hello all, I have found a larger dinner table!")
guests.insert(0, "Drake")
guests.insert(2, "Tom Cruise")
guests.append("Jimmy Kimmel")
print(guests)
```

    Hello all, I have found a larger dinner table!
    ['Drake', 'Barack Obama', 'Tom Cruise', 'Roger Federer', 'Kevin Durant', 'Jimmy Kimmel']



```python
# 3-6
print("Hi "+guests[0]+", would you like to join me for dinner?")
print("Hi "+guests[1]+", would you like to join me for dinner?")
print("Hi "+guests[2]+", would you like to join me for dinner?")
print("Hi "+guests[3]+", would you like to join me for dinner?")
print("Hi "+guests[4]+", would you like to join me for dinner?")
print("Hi "+guests[5]+", would you like to join me for dinner?")
```

    Hi Drake, would you like to join me for dinner?
    Hi Barack Obama, would you like to join me for dinner?
    Hi Tom Cruise, would you like to join me for dinner?
    Hi Roger Federer, would you like to join me for dinner?
    Hi Kevin Durant, would you like to join me for dinner?
    Hi Jimmy Kimmel, would you like to join me for dinner?



```python
# 3-7
print("Hello all, our table unfortunately now only has space for guests.")
print("Hi "+guests[0]+", I apologize but you are no longer invited to dinner.")
guests.pop(0)
print("Hi "+guests[1]+", I apologize but you are no longer invited to dinner.")
guests.pop(1)
print("Hi "+guests[1]+", I apologize but you are no longer invited to dinner.")
guests.pop(1)
print("Hi "+guests[1]+", I apologize but you are no longer invited to dinner.")
guests.pop(1)
```

    Hello all, our table unfortunately now only has space for guests.
    Hi Drake, I apologize but you are no longer invited to dinner.
    Hi Tom Cruise, I apologize but you are no longer invited to dinner.
    Hi Roger Federer, I apologize but you are no longer invited to dinner.
    Hi Kevin Durant, I apologize but you are no longer invited to dinner.





    'Kevin Durant'




```python
# 3-7
print("Hi "+guests[0]+" and "+guests[1]+", you are still invited to dinner!")
```

    Hi Barack Obama and Jimmy Kimmel, you are still invited to dinner!



```python
# 3-8

```
