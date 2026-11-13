---
title: "Configuring a Network Interface from the Terminal"
date: 2016-05-05 12:40:00
category: "Linux & HPC"
tags: ["linux", "networking"]
wp_url: https://capivarainformacoes.wordpress.com/2016/05/05/configurando-interface-de-rede-eth0/
---

To configure a static IP by hand, replace the example addresses with your own.

**With `ip` (current tool):**

```bash
sudo ip addr add 192.168.0.10/24 dev eth0
sudo ip link set eth0 up
sudo ip route add default via 192.168.0.1
```

**With `ifconfig` and `route` (legacy `net-tools`):**

```bash
sudo ifconfig eth0 192.168.0.10 netmask 255.255.255.0 up
sudo route add default gw 192.168.0.1
```

**DNS:** edit `/etc/resolv.conf` and add one `nameserver` line per server:

```text
nameserver 1.1.1.1
nameserver 8.8.8.8
```

These settings don't survive a reboot. To make them permanent, use your distribution's network configuration:
`/etc/network/interfaces` on Debian, NetworkManager (`nmcli`), or netplan on Ubuntu.
