---
title: "Fixing \"Error Populating Transaction\" on Rocks 7"
date: 2018-12-20 12:30:00
category: "Linux & HPC"
tags: ["rocks", "hpc", "troubleshooting"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2018/12/20/solved-error-populating-transaction-no-rocks-7/
---

The **Error Populating Transaction** message usually means a compute node has an invalid configuration.
In my case, the node had only 2 GB of RAM. By default Rocks 7 requires at least 4 GB,
but a node with 2 GB still runs without problems.

To get around the check, disable the install tracker for that node:

```bash
rocks set host installaction compute-0-0 "install notracker"
rocks set host attr compute-0-0 UseTracker False
```

The node will then install normally.
