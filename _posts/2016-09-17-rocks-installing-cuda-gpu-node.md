---
title: "Installing CUDA on a Rocks Cluster GPU Node"
date: 2016-09-17 12:00:00
category: "Linux & HPC"
tags: ["rocks", "hpc", "cuda", "nvidia"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2016/09/17/instalando-cuda-no-rocks-cluster/
---

In this example the GPU node is called **nvidia-0-0**.

1. Download the [CUDA installer](https://developer.nvidia.com/cuda-downloads) (`.run` file)
   and put it on the frontend in `/export/apps`. Nodes see that directory as `/share/apps`.

2. Log in to the node as root:

   ```bash
   ssh root@nvidia-0-0
   ```

3. Disable the default open-source video driver (`nouveau`) and rebuild the initramfs:

   ```bash
   echo 'blacklist nouveau' >> /etc/modprobe.d/blacklist.conf
   mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r).img.bak
   dracut -v /boot/initramfs-$(uname -r).img $(uname -r)
   reboot
   ```

4. Run the installer:

   ```bash
   /share/apps/cuda_7.5.18_linux.run
   ```

   Install the NVIDIA driver, OpenGL libraries and the CUDA toolkit. You can skip the samples.
   The answers I used were: `accept, y, y, y, [enter], y, n`.

5. Add CUDA to the system-wide `PATH` and library path:

   ```bash
   echo 'export PATH=$PATH:/usr/local/cuda/bin' >> /etc/bashrc
   echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64' >> /etc/bashrc
   ```
