---
title: "Backing Up Redmine and Moving It to Another Server"
date: 2016-05-04 12:10:00
category: "Linux & HPC"
tags: ["redmine", "mysql", "backup"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2016/05/04/fazendo-backup-do-redmine/
---

How to back up Redmine (database and uploaded files) and restore it on another server.

## Database

List the databases to find Redmine's. `-p` with no value makes MySQL prompt for the password,
so it doesn't end up in your shell history:

```bash
mysql -u root -p -e "SHOW DATABASES;"
```

Dump the Redmine database (Debian's package names it `redmine_default`):

```bash
mysqldump -u root -p redmine_default > redmine_db_backup.sql
```

Copy it to the target server:

```bash
scp redmine_db_backup.sql root@<target-server>:/root/
```

Restore it on the target server. The database must already exist there:

```bash
mysql -u root -p redmine_default < redmine_db_backup.sql
```

## Uploaded files

Attachments are stored in Redmine's `files` directory. As root:

```bash
cd /var/lib/redmine/default
tar -czf files.tar.gz files/
scp files.tar.gz root@<target-server>:/var/lib/redmine/default/
```

On the target server, extract it in the same place and fix the permissions:

```bash
cd /var/lib/redmine/default
tar -xzvf files.tar.gz
chown -R www-data:www-data files
```

> Redmine's built-in server listens on port **3000** by default.
