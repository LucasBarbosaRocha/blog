---
title: "Shell Scripting 101: Your First Script"
date: 2018-07-13 12:00:00
category: "Programming"
tags: ["shell-script", "bash", "linux"]
wp_url: https://capivarainformacoes.wordpress.com/2018/07/13/teste/
---

*Part 1 of the Shell Scripting 101 series.*

## Create the file

```bash
touch script.sh
```

## Make it executable

To run the file as a program, it needs execute permission:

```bash
chmod +x script.sh
```

> Avoid `chmod 777`: it gives read, write and execute permission to **every** user on the system.
> `+x` is all you need.

## Write the script

Open the file in an editor such as `nano`:

```bash
nano script.sh
```

The first line, called the *shebang*, tells the system which interpreter runs the script.
We will use Bash:

```bash
#!/bin/bash
```

Now add a variable and print it:

```bash
#!/bin/bash
name="World"
echo "Hello $name"
```

- `name` is a variable. Variable names must start with a letter or an underscore.
- Don't put spaces around `=` in an assignment: `name = "World"` is an error.
- `echo` prints its arguments. Inside double quotes, `$name` is replaced by the variable's value.

## Run it

```bash
./script.sh
# Hello World
```

Next: [capturing command output](/blog/2018/07/14/shell-scripting-command-output/).
