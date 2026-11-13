---
title: "Adding Packages to Rocks Cluster Compute Nodes"
date: 2016-05-06 12:30:00
category: "Linux & HPC"
tags: ["rocks", "hpc", "rpm"]
legacy: true
wp_url: https://capivarainformacoes.wordpress.com/2016/05/06/adicionando-pacote-nos-nos/
---

In Rocks, compute nodes are installed from a *distribution* built on the frontend.
To add a package to every node, put it into that distribution and reinstall the nodes.

## 1. Copy the RPM

Download the RPM and put it in:

```bash
/export/rocks/install/contrib/<rocks-version>/<arch>/RPMS
```

`<rocks-version>` is your Rocks version and `<arch>` is the architecture (`i386` or `x86_64`).

## 2. Declare the package

```bash
cd /export/rocks/install/site-profiles/<rocks-version>/nodes
```

If `extend-compute.xml` doesn't exist there yet, create it from the skeleton.
Copying keeps `skeleton.xml` as a backup:

```bash
cp skeleton.xml extend-compute.xml
```

Open `extend-compute.xml` and find this line:

```xml
<!-- <package> insert 1st package name here and uncomment the line</package> -->
```

Replace it with one `<package>` tag per package. Use **only the package name**, without the version or architecture.
For example, for `R-2-323.x86_64.rpm` and `R-devel-234.x86_64.rpm`:

```xml
<package>R</package>
<package>R-devel</package>
```

To require a specific architecture, append it to the name:

```xml
<package>libpciaccess.i686</package>
<package>libstdc++.x86_64</package>
```

## 3. Rebuild the distribution

The distribution works like an installation image for the nodes:

```bash
cd /export/rocks/install
rocks create distro
```

## 4. Reinstall the nodes

**A single node:**

```bash
rocks set host boot <node-name> action=install
ssh <node-name> reboot
```

**All nodes** (as root):

```bash
/opt/gridengine/examples/jobs/sge-reinstall.sh
```

Source: [Rocks base roll documentation](http://central6.rocksclusters.org/roll-documentation/base/6.1.1/index.html)
