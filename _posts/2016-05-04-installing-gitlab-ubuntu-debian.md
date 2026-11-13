---
title: "Installing GitLab on Ubuntu/Debian (Omnibus Package)"
date: 2016-05-04 12:20:00
category: "Linux & HPC"
tags: ["gitlab", "git", "debian", "ubuntu"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2016/05/04/instalando-e-configurando-o-git-no-ubuntudebian/
---

This guide uses the GitLab 7.0 Omnibus package for Ubuntu 12.04, as it was in 2016.
For current versions, follow the [official GitLab install guide](https://about.gitlab.com/install/),
which uses a package repository instead of a manual `.deb` download.

## Download and install

```bash
wget https://downloads-packages.s3.amazonaws.com/ubuntu-12.04/gitlab_7.0.0-omnibus-1_amd64.deb
sudo apt-get install openssh-server
sudo apt-get install postfix   # choose 'Internet Site' when asked
sudo dpkg -i gitlab_7.0.0-omnibus-1_amd64.deb
```

## Set the hostname

```bash
sudo -e /etc/gitlab/gitlab.rb
```

Change:

```ruby
external_url "http://your_domain.com/"
```

to your server's address:

```ruby
external_url "http://<your-ip>"
```

## Configure and start

```bash
sudo gitlab-ctl reconfigure
```

Restart the machine and open the address in a browser. GitLab 7 shipped with these default credentials:

- **Username:** `root`
- **Password:** `5iveL!fe`

You'll be asked to change the password on first login.
