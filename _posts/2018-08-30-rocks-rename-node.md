---
title: "Renaming a Node in Rocks Cluster"
date: 2018-08-30 12:00:00
category: "Linux & HPC"
tags: ["rocks", "hpc"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2018/08/30/renomeando-um-no/
---

To rename a node (here, `devel-server-0-0` becomes `new-devel-server-0-0`):

```bash
rocks set host name devel-server-0-0 new-devel-server-0-0
rocks set host interface name new-devel-server-0-0 eth0 new-devel-server-0-0
rocks set host interface name new-devel-server-0-0 eth1 new-devel-server-0-0
rocks sync config
rocks sync host network new-devel-server-0-0
```

Then reboot the node:

```bash
ssh new-devel-server-0-0 "shutdown -r now"
```
