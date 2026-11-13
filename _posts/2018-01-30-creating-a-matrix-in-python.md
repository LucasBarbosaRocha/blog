---
title: "Creating a Matrix in Python"
date: 2018-01-30 12:00:00
category: "Programming"
tags: ["python"]
wp_url: https://capivarainformacoes.wordpress.com/2018/01/30/criando-uma-matriz/
---

Python has no built-in matrix type, but a **list of lists** works well for small matrices.
Each element of the outer list is a row, and each row is a list of columns.
After building it, you index it as `A[row][col]`, for example `A[0][1]`.

The function below creates a `rows × cols` matrix filled with random integers from 1 to 10:

```python
import random


def create_matrix(rows, cols):
    A = []
    for _ in range(rows):
        row = []
        for _ in range(cols):
            row.append(random.randint(1, 10))
        A.append(row)
    return A


if __name__ == "__main__":
    matrix = create_matrix(2, 3)
    print(matrix)
```

The same thing with a list comprehension:

```python
matrix = [[random.randint(1, 10) for _ in range(cols)] for _ in range(rows)]
```

> **Pitfall:** don't write `[[0] * cols] * rows`. It creates `rows` references to the *same* inner list,
> so changing one row changes all of them.

For numerical work, use [NumPy](https://numpy.org/) arrays instead.
