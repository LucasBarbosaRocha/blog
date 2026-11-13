---
title: "Compressing and Extracting Files on Linux (tar, gz, bz2, zip, rar, 7z)"
date: 2017-03-05 12:00:00
category: "Linux & HPC"
tags: ["linux", "tar", "cheat-sheet"]
wp_url: https://capivarainformacoes.wordpress.com/2017/03/05/compactar-e-descompactar-arquivos/
---

A cheat sheet for the most common archive formats on Linux.

## Install the tools (Debian/Ubuntu)

```bash
sudo apt install zip unzip bzip2 xz-utils p7zip-full unrar
```

`rar` (creating `.rar` files) is a separate non-free package.

## tar

`tar` bundles files into one archive. Combine it with a compressor to make the archive smaller.

| Format | Create | Extract |
|---|---|---|
| `.tar` | `tar -cvf archive.tar dir/` | `tar -xvf archive.tar` |
| `.tar.gz` / `.tgz` | `tar -czvf archive.tar.gz dir/` | `tar -xzvf archive.tar.gz` |
| `.tar.bz2` | `tar -cjvf archive.tar.bz2 dir/` | `tar -xjvf archive.tar.bz2` |
| `.tar.xz` | `tar -cJvf archive.tar.xz dir/` | `tar -xJvf archive.tar.xz` |

The flags: `c` creates, `x` extracts, `v` lists files as it works (verbose), and `f` names the archive file.
`z`, `j` and `J` select gzip, bzip2 and xz.
Modern GNU tar detects the compression automatically when extracting, so `tar -xvf file` works for all of them.

You can also bundle several individual files:

```bash
tar -czvf archive.tar.gz file1.txt image.jpg notes.md
```

To extract into a specific directory, add `-C`:

```bash
tar -xzvf archive.tar.gz -C /target/dir
```

## gzip / bzip2 on single files

```bash
gzip -9 file.tar        # -> file.tar.gz (maximum compression)
gunzip file.tar.gz      # back to file.tar

bzip2 file.tar          # -> file.tar.bz2
bunzip2 file.tar.bz2    # back to file.tar
```

## zip

```bash
zip -r archive.zip dir/           # create
unzip archive.zip                 # extract here
unzip archive.zip -d /target/dir  # extract to a directory
```

## rar

```bash
rar a archive.rar dir/            # create (needs the non-free rar package)
unrar x archive.rar               # extract, keeping the folder structure
```

## 7z

```bash
7z a archive.7z dir/              # create
7z x archive.7z                   # extract
```
