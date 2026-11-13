---
title: "Giving a User sudo Rights on Debian"
date: 2016-05-05 12:10:00
category: "Linux & HPC"
tags: ["debian", "sudo"]
wp_url: https://capivarainformacoes.wordpress.com/2016/05/05/deixando-o-usuario-como-sudo/
---

## 1. Make sure apt can install packages

A fresh Debian install from DVD often keeps the DVD as a package source, so `apt` keeps asking for the disc.
Become root and edit the sources list:

```bash
su -
nano /etc/apt/sources.list
```

Comment out the lines that start with `deb cdrom:`, for example:

```text
# deb cdrom:[Debian GNU/Linux 8.2.0 _Jessie_ - Official amd64 DVD Binary-1 20150912]/ jessie main
```

Save the file (`Ctrl+O`, then `Ctrl+X`) and update:

```bash
apt update
apt install sudo
```

## 2. Add the user to the sudo group

```bash
usermod -aG sudo your_user
```

Log out and back in, and you're done.

Alternatively, use `visudo` to add a rule under `# User privilege specification`:

```text
root       ALL=(ALL:ALL) ALL
your_user  ALL=(ALL:ALL) ALL
```
