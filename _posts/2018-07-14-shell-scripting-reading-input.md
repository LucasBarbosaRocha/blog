---
title: "Shell Scripting 101: Reading User Input"
date: 2018-07-14 12:10:00
category: "Programming"
tags: ["shell-script", "bash", "linux"]
wp_url: https://capivarainformacoes.wordpress.com/2018/07/14/entrada-de-dados/
---

*Part 3 of the Shell Scripting 101 series.*

Use the `read` builtin to read input from the user:

```bash
read variable_name
```

Example:

```bash
#!/bin/bash
echo "What is your name?"
read name
echo "Hello $name"
```

`read` accepts options. For example, it can print the prompt itself:

```bash
#!/bin/bash
read -p "What is your name? " -d '.' name
echo -e "\nHello $name"
```

- `-p` prints a prompt before reading.
- `-d '.'` keeps reading until a `.` is typed, instead of stopping at a newline.
- `echo -e` interprets escape sequences such as `\n`.

Next: [conditionals](/blog/2018/07/14/shell-scripting-conditionals/).
