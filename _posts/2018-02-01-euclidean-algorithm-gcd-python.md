---
title: "Euclidean Algorithm for the GCD in Python"
date: 2018-02-01 12:10:00
category: "Programming"
tags: ["python", "algorithms", "math"]
wp_url: https://capivarainformacoes.wordpress.com/2018/02/01/mdc-de-euclides/
---

The Euclidean algorithm finds the **greatest common divisor (GCD)** of two numbers.
The GCD is the last non-zero remainder of repeated divisions.
In the code below, `b` holds that remainder when the loop ends.

```python
def gcd(a, b):
    remainder = a % b
    while remainder != 0:
        a = b
        b = remainder
        remainder = a % b
    return b
```

A more compact version that does the same thing:

```python
def gcd(a, b):
    while b:
        a, b = b, a % b
    return a
```

In real code, use the built-in `math.gcd(a, b)`.

For the math behind it, see this
[explanation from OBMEP (in Portuguese)](http://clubes.obmep.org.br/blog/sala-de-estudos-algoritmo-de-euclides-para-determinacao-de-mdc/diagramas/).
