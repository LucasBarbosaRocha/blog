---
title: "Running Old DOS Games and Programs with DOSBox"
date: 2016-05-04 12:40:00
category: "Linux & HPC"
tags: ["linux", "emulation", "games", "dos"]
wp_url: https://capivarainformacoes.wordpress.com/2016/05/04/instalando-o-redmine-no-linux/
---

**DOSBox** is a DOS emulator that runs old games and MS-DOS programs well.

## Install

```bash
sudo apt install dosbox
```

## Run a program

```bash
dosbox program.exe
```

Executables can be `.exe`, `.com` or `.bat` files.
To get a plain DOS prompt, run `dosbox` with no arguments.

## Mount a folder as drive C:

If your games are in `~/games`, type this at the DOSBox prompt:

```text
mount c ~/games
c:
```

## Try it: Dangerous Dave

A great DOS classic is **Dangerous Dave**. You can download it from
[Best Old Games](http://www.bestoldgames.net/eng/old-games/dangerous-dave.php).
Then open a terminal in the game's folder and run:

```bash
dosbox DAVE.EXE
```

Have fun!
