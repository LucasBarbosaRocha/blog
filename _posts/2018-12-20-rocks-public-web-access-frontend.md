---
title: "Opening Port 80 on the Rocks Frontend"
date: 2018-12-20 12:10:00
category: "Linux & HPC"
tags: ["rocks", "hpc", "firewall"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2018/12/20/acesso-publico-ao-frontend/
---

How to allow public HTTP access to the Rocks frontend.

**Rocks 6.2 and earlier:**

```bash
rocks open host firewall localhost network=public protocol=tcp service=www
```

**Rocks 7:**

```bash
rocks remove firewall host=localhost rulename=A40-WWW-PUBLIC-LAN
rocks add firewall host=localhost network=public protocol=tcp service=www chain=INPUT \
   action=ACCEPT flags="-m state --state NEW --source 0.0.0.0/0.0.0.0" \
   rulename=A40-WWW-PUBLIC-NEW
```

Apply the changes:

```bash
rocks sync host firewall localhost
```

Check the active rules:

```bash
rocks report host firewall localhost
```
