---
title: "Resetting ALSA Audio on Linux"
date: 2016-05-06 11:50:00
category: "Linux & HPC"
tags: ["linux", "debian", "audio"]
wp_url: https://capivarainformacoes.wordpress.com/2016/05/06/utilitario-de-audio-no-linux/
---

If the sound stops working, try restoring ALSA's default state:

```bash
sudo alsactl init
```

On older Debian/Ubuntu systems with SysV init scripts, use:

```bash
sudo /etc/init.d/alsa-utils reset
```

If the ALSA utilities are missing or broken, reinstall them:

```bash
sudo apt purge alsa-utils
sudo apt install alsa-utils
```

To adjust volumes and unmute channels, open the mixer in the terminal:

```bash
alsamixer
```

> Modern desktops run PulseAudio or PipeWire on top of ALSA. If the problem continues, restart the user audio service:
> `systemctl --user restart pipewire pipewire-pulse` (or `pulseaudio -k`).
