---
title: "Shell Scripting 101: Capturing Command Output"
date: 2018-07-14 12:00:00
category: "Programming"
tags: ["shell-script", "bash", "linux"]
wp_url: https://capivarainformacoes.wordpress.com/2018/07/14/capturando-comandos-linux/
---

*Part 2 of the Shell Scripting 101 series.*

To store the output of a command in a variable, use *command substitution*:

```bash
variable=$(command)
```

Example:

```bash
#!/bin/bash
name=$(whoami)
echo "Hello $name"

dir=$(pwd)
echo "This script is running in $dir"
```

- `whoami` prints the current user's name.
- `pwd` prints the current working directory.

> You may also see the older backtick syntax, `` name=`whoami` ``. Prefer `$(...)`: it is easier to read and can be nested.

Next: [reading user input](/blog/2018/07/14/shell-scripting-reading-input/).
