---
title: "Shell Scripting 101: Loops (for, while, seq)"
date: 2018-07-14 12:30:00
category: "Programming"
tags: ["shell-script", "bash", "linux"]
wp_url: https://capivarainformacoes.wordpress.com/2018/07/14/lacos/
---

*Part 5 of the Shell Scripting 101 series.*

## for

```bash
for i in {0..N}; do
  ACTIONS
done
```

Print the numbers 1 to 5:

```bash
#!/bin/bash
for i in {1..5}; do
  echo "$i"
done
```

C-style syntax:

```bash
#!/bin/bash
for ((i = 1; i <= 5; i++)); do
  echo "$i"
done
```

## seq

`seq` generates a sequence of numbers:

```bash
seq 1 100     # 1, 2, 3, ..., 100
seq 1 2 100   # 1, 3, 5, ..., 99 (step of 2)
```

Using `seq` in a `for` loop:

```bash
#!/bin/bash
for i in $(seq 1 2 100); do
  echo "$i"
done
```

> In Bash, `{1..100..2}` does the same thing without starting an extra process.

## while

```bash
while [ CONDITION ]; do
  ACTIONS
done
```

Print the numbers 0 to 10:

```bash
#!/bin/bash
i=0
while [ "$i" -le 10 ]; do
  echo "$i"
  ((i++))
done
```

Double parentheses `(( ... ))` evaluate arithmetic expressions in Bash, so `((i++))` increments `i`.
