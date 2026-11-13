---
title: "Forcing a User to Change Their Password at Next Login"
date: 2018-12-20 12:00:00
category: "Linux & HPC"
tags: ["linux", "security"]
wp_url: https://capivarainformacoes.wordpress.com/2018/12/20/forcando-o-usuario-a-trocar-a-senha/
---

This command forces a user to change their password the next time they log in:

```bash
sudo chage -d 0 <username>
```

It sets the date of the last password change to day 0, so the password counts as expired.
`sudo passwd --expire <username>` does the same thing.
