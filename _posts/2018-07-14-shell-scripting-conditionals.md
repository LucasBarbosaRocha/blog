---
title: "Shell Scripting 101: Conditionals (if, elif, else)"
date: 2018-07-14 12:20:00
category: "Programming"
tags: ["shell-script", "bash", "linux"]
wp_url: https://capivarainformacoes.wordpress.com/2018/07/14/condicional-if/
---

*Part 4 of the Shell Scripting 101 series.*

## if

```bash
if [ CONDITION ]; then
  ACTIONS
fi
```

- Every `if` is closed with `fi`.
- Spaces inside the brackets are required: `[ "$a" -gt 0 ]` works, but `["$a" -gt 0]` does not.

Any command can be used as the condition. Its exit status decides the branch:

```bash
if grep -q "root" /etc/passwd; then
  echo "found"
fi
```

## Comparison operators

| Operator | Meaning |
|----------|---------|
| `s1 = s2` | strings are equal |
| `s1 != s2` | strings are different |
| `n1 -eq n2` | integers are equal |
| `n1 -ne n2` | integers are different |
| `n1 -gt n2` | n1 is greater than n2 |
| `n1 -ge n2` | n1 is greater than or equal to n2 |
| `n1 -lt n2` | n1 is less than n2 |
| `n1 -le n2` | n1 is less than or equal to n2 |

Example:

```bash
#!/bin/bash
read -p "Enter a number: " number
if [ "$number" -gt 0 ]; then
  echo "$number > 0"
fi
```

## else

```bash
#!/bin/bash
read -p "Enter a number: " number
if [ "$number" -gt 0 ]; then
  echo "$number > 0"
else
  echo "$number < 0"
fi
```

This version has a bug: entering `0` prints `0 < 0`.

## elif

`elif` adds another condition and fixes the bug:

```bash
#!/bin/bash
read -p "Enter a number: " number
if [ "$number" -gt 0 ]; then
  echo "$number > 0"
elif [ "$number" -eq 0 ]; then
  echo "$number = 0"
else
  echo "$number < 0"
fi
```

Next: [loops](/blog/2018/07/14/shell-scripting-loops/).
