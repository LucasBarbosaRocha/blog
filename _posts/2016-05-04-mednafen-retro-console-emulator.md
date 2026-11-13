---
title: "Mednafen: Emulating Retro Consoles from the Command Line"
date: 2016-05-04 12:50:00
category: "Linux & HPC"
tags: ["linux", "emulation", "games"]
wp_url: https://capivarainformacoes.wordpress.com/2016/05/04/instalando-e-utlizando-o-mednafen-no-debian/
---

**Mednafen** is a command-line, multi-system emulator. It runs consoles such as:

- Game Boy / Game Boy Color
- Game Boy Advance
- NES
- Super Nintendo / Super Famicom
- Virtual Boy
- and more.

## Install

```bash
sudo apt install mednafen     # Debian/Ubuntu
sudo dnf install mednafen     # Fedora
```

Installing is easy. The part I always forget is the configuration, so here are a few things worth knowing first:

1. **Configuration directory.** Mednafen keeps its settings and saves in `~/.mednafen`.
2. **F1 is your friend.** It opens a short help screen in the emulator.
3. **Most settings are command-line arguments.** Some games only run well with a specific option, so learn the main ones.

## Run a game

```bash
mednafen [OPTIONS] game.rom > /dev/null
```

`> /dev/null` hides the flood of log messages. Options are optional, so this is enough:

```bash
mednafen game.rom
```

## Map the controls

- `Shift+Alt+1` maps player 1's controller.
- `Shift+Alt+2` maps player 2's controller, and so on.

A message at the bottom of the screen tells you which button to press next (for example `LEFT`).
Press each key **twice** to confirm it.

## Save states

- `-` and `=` choose the save slot. A thumbnail shows what was saved in that slot.
- `F5` saves the state, and `F7` loads it.

## Other shortcuts

| Key | Action |
|---|---|
| `Alt+Enter` | Toggle fullscreen |
| `F9` | Screenshot |
| `F10` | Soft reset (the console's Reset button) |
| `F11` | Hard reset (power off and on) |
| `Esc` / `F12` | Quit. Save your state first! |

Have fun.
