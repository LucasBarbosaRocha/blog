---
title: "Reading Input Until EOF in Python and C"
date: 2018-02-01 12:00:00
category: "Programming"
tags: ["python", "c", "competitive-programming"]
wp_url: https://capivarainformacoes.wordpress.com/2018/02/01/eof/
---

Many online-judge problems give you an unknown number of input lines and end at EOF (end of file).
Here is how to read that kind of input.

**Python**

```python
while True:
    try:
        line = input()
    except EOFError:
        break
    # process line here
```

A shorter alternative that reads the whole input at once:

```python
import sys

for line in sys.stdin:
    pass  # process line here
```

**C**

```c
#include <stdio.h>

int main(void)
{
    int n;
    while (scanf("%d", &n) != EOF) {
        /* process n here */
    }
    return 0;
}
```
