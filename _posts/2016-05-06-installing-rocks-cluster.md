---
title: "Installing Rocks Cluster (5.5 – 6.2)"
date: 2016-05-06 12:20:00
category: "Linux & HPC"
tags: ["rocks", "hpc", "centos"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2016/05/06/instalando-rocks-cluster-centos/
---

This guide covers Rocks versions 5.5 through 6.2.

Rocks is based on Red Hat Linux, so it supports the same hardware Red Hat supports,
but only on these architectures:

**Processors**

- x86 (ia32, AMD Athlon, etc.)
- x86_64 (AMD Opteron and EM64T)
- IA-64 (Itanium)

**Networks**

- Ethernet (every flavor Red Hat supports, including Intel Gigabit Ethernet)
- Myrinet (Myricom)
- InfiniBand (Voltaire)

## Minimum hardware

| | Frontend | Compute node |
|---|---|---|
| Disk | 20 GB | 20 GB |
| RAM | 512 MB (i386) / 1 GB (x86_64) | 512 MB |
| Ethernet | 2 physical ports (`eth0`, `eth1`) | 1 physical port (`eth0`) |

Download [Rocks](http://www.rocksclusters.org/) and write it to a DVD or USB drive.
Before you start, make sure the frontend and all nodes are powered off.

## Installing the frontend

1. Boot the frontend from the Rocks installation media.
2. On version 6.2 and earlier, you'll see the options `build` and `build rescue`. Choose **build** to install a new frontend.
3. Wait for the initial setup, then click **CD/DVD-based Roll**.
4. A list of available Rolls appears. Selecting all of them is recommended. At minimum, select:
   - `base`
   - `kernel`
   - `os`
5. Click **Submit**.
6. You're back on the first screen, and the selected Rolls are listed on the left. Click **Next**.
7. **Cluster Information**: fill in the general details (name, location, etc.) and click **Next**.
8. **Public Network Interface**: choose `eth0` or `eth1`, then enter the IP address and netmask.
   `eth1` is usually the public one, but either works.
   - *Before Rocks 5.5 you can't choose: `eth0` is always the public interface.*
9. **Private Network Interface** (the internal network between nodes): choose the other card, enter its IP and netmask, and continue.
10. Set the **gateway** and **DNS**, then continue.
11. Set the **root password**.
12. Choose your **time zone**.
13. **Disk partitioning.** With **Auto Partitioning** on a 20 GB disk, the layout is:

    | Partition | Size |
    |---|---|
    | `/` | 4 GB |
    | `/var` | 4 GB |
    | `swap` | 1 GB |
    | `/state/partition1` | rest of the disk |

14. With **Manual Partitioning** you partition the disk as you would on any Linux system,
    but the partitions above **must** exist.
15. Wait for the installation to finish.

## Installing the compute nodes

1. Log in to the frontend.
2. Open a terminal and run `insert-ethers`. This is the tool that discovers and registers new nodes.
3. If the frontend and nodes are connected through a **managed Ethernet switch**, first choose **Ethernet Switches**.
   Many managed switches send DHCP requests to get an IP address for their own management interface.
   `insert-ethers` captures that request, registers the switch in the frontend's MySQL database, and configures it.
   After the switch is detected, or after about 10 minutes, press **F8** to exit.
4. Run `insert-ethers` again.
5. Choose **Compute** and power on the first node.
6. An **Inserted Appliances** window lists each node's MAC address and name, followed by `( )`.
   A `*` inside the parentheses means the installation succeeded. A number means an error code.
7. You can watch the installation on a monitor attached to the node.
   When it finishes, log in with `ssh <node-name>`, for example `ssh compute-0-0`.
8. Repeat for every node.

## Useful commands

| Command | What it does |
|---|---|
| `rocks list host` | List all nodes |
| `insert-ethers --remove <node>` | Remove a node |
| `insert-ethers --rack=3 --rank=4` | Insert a node at rack 3, position 4 (it will be named `compute-3-4`) |
| `insert-ethers --hostname=<name>` | Insert a node with a custom name |
| `w` | Show who is logged in |

## Adding users

On the frontend:

```bash
sudo adduser john_doe
sudo passwd john_doe
rocks sync users        # propagate users to the nodes
```

Source: [rocksclusters.org](http://www.rocksclusters.org/)
