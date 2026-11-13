---
title: "Configuring Redmine to Send Email"
date: 2016-05-04 12:00:00
category: "Linux & HPC"
tags: ["redmine", "email", "postfix"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2016/05/04/configurando-o-servico-de-email-do-redmine/
---

At some point you'll want Redmine to send email notifications.
The simplest way is to install a local mail server such as Postfix and let Redmine use `sendmail`.

```bash
sudo apt-get install postfix
```

Create or edit `/etc/redmine/default/configuration.yml` and add the lines below.
YAML is indentation-sensitive, so keep the two-space indents:

```yaml
production:
  email_delivery:
    delivery_method: :sendmail
```

Then restart Apache:

```bash
sudo service apache2 restart
```
