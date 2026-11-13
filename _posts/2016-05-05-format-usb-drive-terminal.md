---
title: "Formatting a USB Drive from the Terminal"
date: 2016-05-05 12:30:00
category: "Linux & HPC"
tags: ["linux"]
wp_url: https://capivarainformacoes.wordpress.com/2016/05/05/formatando-pendrive-via-terminal/
---

> **Warning:** formatting erases everything on the device. Double-check the device name before running `mkfs`.

1. Find the device name (for example `/dev/sdb1`):

   ```bash
   lsblk
   ```

2. Unmount it:

   ```bash
   sudo umount /dev/sdX1
   ```

3. Format it as FAT32 with a label:

   ```bash
   sudo mkfs.vfat -n MYDRIVE /dev/sdX1
   ```

   To format the whole device without a partition table, use `-I` on the device itself, for example `/dev/sdX`.

4. Optionally, check for bad blocks while formatting (much slower):

   ```bash
   sudo mkfs.vfat -c -v -n MYDRIVE /dev/sdX1
   ```

For large files (over 4 GB), use exFAT instead: `sudo mkfs.exfat -n MYDRIVE /dev/sdX1`.
