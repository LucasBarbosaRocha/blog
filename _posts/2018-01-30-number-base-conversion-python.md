---
title: "Converting Between Binary, Decimal and Hexadecimal in Python"
date: 2018-01-30 12:10:00
category: "Programming"
tags: ["python"]
wp_url: https://capivarainformacoes.wordpress.com/2018/01/30/mudanca-de-base-bin-hex-ou-dec/
---

`int(text, base=n)` parses a string written in base `n`.
`bin()` and `hex()` turn an integer back into a binary or hexadecimal string.

```python
number = input()  # the input is a string

# Binary -> decimal / hexadecimal
dec = int(number, base=2)
hexa = hex(int(number, base=2))

# Decimal -> binary / hexadecimal
bina = bin(int(number, base=10))
hexa = hex(int(number, base=10))

# Hexadecimal -> decimal / binary
dec = int(number, base=16)
bina = bin(int(number, base=16))
```

`bin()` and `hex()` add a prefix (`0b`, `0x`). To get the digits without it, use `format()`:

```python
format(255, "b")  # '11111111'
format(255, "x")  # 'ff'
```
