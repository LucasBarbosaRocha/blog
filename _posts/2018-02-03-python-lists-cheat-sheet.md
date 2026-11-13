---
title: "Python Lists: A Quick Cheat Sheet"
date: 2018-02-03 12:00:00
category: "Programming"
tags: ["python"]
wp_url: https://capivarainformacoes.wordpress.com/2018/02/03/usando-uma-lista/
---

Common operations on Python lists.

## Creating a list

```python
fruits = []                          # empty list
zeros = [0] * 5                      # [0, 0, 0, 0, 0]
fruits = ["banana", "grape", "apple"]
```

Lists grow as needed, so however you create one, you can keep adding elements.

## Adding elements

```python
fruits.append("papaya")       # add to the end
fruits.insert(1, "melon")     # insert at index 1
fruits.extend(["kiwi", "fig"])  # add several at once
```

## Changing elements

```python
fruits[1] = "soursop"         # replace the item at index 1
```

## Removing elements

```python
fruits.remove("grape")    # remove the first matching value
del fruits[0]             # remove by index
last = fruits.pop()       # remove and return the last element
first = fruits.pop(0)     # remove and return the element at index 0
del fruits[2:4]           # remove indexes 2 and 3 (slice end is exclusive)
fruits.clear()            # remove all elements
del fruits                # delete the variable itself
```
