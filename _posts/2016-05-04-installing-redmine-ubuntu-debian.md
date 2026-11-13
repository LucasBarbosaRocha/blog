---
title: "Installing Redmine on Ubuntu/Debian"
date: 2016-05-04 12:30:00
category: "Linux & HPC"
tags: ["redmine", "debian", "ubuntu", "ruby"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2016/05/04/instalando-o-redmine-no-ubuntudebian/
---

This guide installs Redmine from the distribution packages, as they were in 2016 (Ruby 1.8, Rails 2.3).
For current releases, follow the [official Redmine install guide](https://www.redmine.org/projects/redmine/wiki/RedmineInstall).

## Prepare the server

Install Apache and MySQL:

```bash
sudo apt-get install apache2
sudo apt-get install mysql-client mysql-common mysql-server
```

Install Ruby and the libraries Redmine needs:

```bash
sudo apt-get install ruby1.8 ruby1.8-dev rubygems ruby-blankslate ruby-builder ruby-coderay \
  ruby-i18n ruby-mysql ruby-net-ldap ruby-rack ruby-rails-2.3 ruby-rchardet ruby-text-format ruby-tmail
```

## Install Redmine

```bash
sudo apt-get install redmine redmine-mysql
```

Link Redmine's public directory into the web root and fix the permissions:

```bash
sudo ln -s /usr/share/redmine/public /var/www/redmine
sudo chmod a+x /usr/share/redmine/public
```

## Start Redmine at boot

Create an Upstart job at `/etc/init/redmine.conf`:

```bash
sudo nano /etc/init/redmine.conf
```

```bash
# Redmine

description "Redmine"

start on runlevel [2345]
stop on runlevel [!2345]

expect daemon
exec ruby /usr/share/redmine/script/server webrick -e production -b 0.0.0.0 -d
```

Start the services:

```bash
sudo service apache2 start
sudo service redmine start
```

Open `http://<server-ip>:3000` in your browser and sign in with `admin` / `admin`.
**Change that password right away.**
