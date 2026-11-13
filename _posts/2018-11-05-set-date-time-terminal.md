---
title: "Setting the Date and Time from the Terminal"
date: 2018-11-05 12:00:00
category: "Linux & HPC"
tags: ["linux"]
wp_url: https://capivarainformacoes.wordpress.com/2018/11/05/atualizando-data-e-hora/
---

Set the date and time manually:

```bash
sudo date -s "5 NOV 2018 18:00:00"
```

or, with the long option:

```bash
sudo date --set="5 NOV 2018 18:00:00"
```

On systems with systemd, `timedatectl` is the recommended tool.
It can also turn on automatic time sync over NTP:

```bash
sudo timedatectl set-time "2018-11-05 18:00:00"
sudo timedatectl set-ntp true
```
