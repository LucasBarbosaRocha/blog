---
title: "beecrowd 2136 – Friends of Habay (Python)"
date: 2017-02-20 12:10:00
category: "Programming"
tags: ["python", "beecrowd", "competitive-programming"]
wp_url: https://capivarainformacoes.wordpress.com/2017/02/20/exercicio-2136-uri/
---

Problem: [beecrowd 2136](https://judge.beecrowd.com/en/problems/view/2136)

Read names until `FIM` and split them into those who answered `YES` and those who answered `NO`, without duplicates.
Print each group in alphabetical order. The winner is the longest name among the `YES` answers.

```python
yes, no = [], []

name, answer = input().split()
while name != "FIM":
    if answer == "YES" and name not in yes:
        yes.append(name)
    elif answer == "NO" and name not in no:
        no.append(name)
    name, answer = input().split()

# The winner is the longest name among the YES answers (first one in case of a tie)
winner = ""
for friend in yes:
    if len(friend) > len(winner):
        winner = friend

for friend in sorted(yes):
    print(friend)
for friend in sorted(no):
    print(friend)

print("\nAmigo do Habay:\n%s" % winner)
```

> URI Online Judge is now called **beecrowd**. The output messages stay in Portuguese because the judge checks them exactly.
