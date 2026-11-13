---
title: "Giving a User sudo Rights on CentOS"
date: 2016-05-06 12:00:00
category: "Linux & HPC"
tags: ["centos", "sudo"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2016/05/06/usuario-sudo-no-centos/
---

On CentOS, members of the `wheel` group can use `sudo`. The simplest way is to add the user to that group, as root:

```bash
usermod -aG wheel your_user
```

Log out and back in for the change to take effect.

Alternatively, give the user its own rule. Always edit the sudoers file with `visudo`,
which checks the syntax before saving:

```bash
visudo
```

Below the line `## Allow root to run any commands anywhere`, add:

```text
root       ALL=(ALL)  ALL
your_user  ALL=(ALL)  ALL
```

That's it. The user can now use `sudo`.
