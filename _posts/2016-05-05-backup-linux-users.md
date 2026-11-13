---
title: "Backing Up Linux Users and Home Directories"
date: 2016-05-05 12:20:00
category: "Linux & HPC"
tags: ["linux", "backup"]
wp_url: https://capivarainformacoes.wordpress.com/2016/05/05/backup-dos-usuarios-linux/
---

To back up user accounts and their files, archive the home directories together with the account databases:

```bash
sudo tar -czvf users-backup.tar.gz /home /etc/passwd /etc/shadow /etc/group /etc/gshadow
```

Restore it on the target machine:

```bash
sudo tar -xzvf users-backup.tar.gz -C /
```

> **Careful:** restoring `/etc/passwd`, `/etc/shadow` and `/etc/group` *replaces* the target system's files,
> including its system accounts. Only do this on an identical or freshly installed system.
> Otherwise, copy over just the user entries (UID ≥ 1000).
