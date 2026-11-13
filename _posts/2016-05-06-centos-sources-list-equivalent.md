---
title: "Where Is sources.list on CentOS?"
date: 2016-05-06 12:10:00
category: "Linux & HPC"
tags: ["centos", "yum"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2016/05/06/sources-list-no-centos-2/
---

CentOS has no `/etc/apt/sources.list`. Repositories are configured in:

- `/etc/yum.conf`: global settings
- `/etc/yum.repos.d/*.repo`: one file per repository

List the enabled repositories with:

```bash
yum repolist
```

On newer systems (RHEL/Rocky/Alma 8+), `dnf` replaces `yum` and reads the same directory.
