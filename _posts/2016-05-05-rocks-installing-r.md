---
title: "Installing R on Rocks Cluster and Its Nodes"
date: 2016-05-05 12:50:00
category: "Linux & HPC"
tags: ["rocks", "hpc", "r"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2016/05/05/instalando-o-r-no-rocks/
---

A quick guide to installing R on a Rocks frontend and its compute nodes.

## Frontend

1. Log in to the frontend.
2. Install R and its libraries:

   ```bash
   sudo yum install R R-devel libRmath libRmath-devel
   ```

## Compute nodes

1. Still on the frontend, download the RPMs for `R`, `R-devel`, `libRmath` and `libRmath-devel`.
   At the time they were available from RepoForge (`apt.sw.be`), a mirror that has since gone offline.
   Today you'd get them from [EPEL](https://docs.fedoraproject.org/en-US/epel/).
2. Also download the libraries R depends on: `blas`, `blas-devel`, `libicu` and `libicu-devel`,
   from the CentOS 6 `os` repository ([vault.centos.org](https://vault.centos.org/)).
3. Copy all the RPMs to the cluster's RPMS directory:

   ```bash
   cp *.rpm /export/rocks/install/contrib/<rocks-version>/<arch>/RPMS
   ```

4. Edit `extend-compute.xml` to declare the new packages:

   ```bash
   sudo nano /export/rocks/install/site-profiles/<rocks-version>/nodes/extend-compute.xml
   ```

   ```xml
   <package>R</package>
   <package>R-devel</package>
   <package>libRmath</package>
   <package>libRmath-devel</package>
   <package>blas</package>
   <package>blas-devel</package>
   <package>libicu</package>
   <package>libicu-devel</package>
   ```

5. Rebuild the Rocks distribution:

   ```bash
   cd /export/rocks/install
   rocks create distro
   ```

6. Reinstall the nodes. R will be available on them afterwards.
   See [Adding Packages to Rocks Cluster Compute Nodes](/blog/2016/05/06/rocks-adding-packages-to-nodes/) for details.
