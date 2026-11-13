---
title: "Fixing httpd Failing to Start on Rocks 7"
date: 2018-12-20 12:20:00
category: "Linux & HPC"
tags: ["rocks", "hpc", "apache", "troubleshooting"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2018/12/20/solved-httpd-problem-no-rocks-7/
---

After installing Rocks 7, `httpd` was installed but would not start because its runtime directory
`/run/httpd` had not been created. The fix is to create it with the right owner and permissions:

```bash
mkdir /run/httpd
chown root:apache /run/httpd
chmod 0710 /run/httpd
service httpd start
```

`/run` is a temporary filesystem, so if the problem returns after a reboot, add a `tmpfiles.d` rule:

```bash
echo 'd /run/httpd 0710 root apache -' > /etc/tmpfiles.d/httpd.conf
```
