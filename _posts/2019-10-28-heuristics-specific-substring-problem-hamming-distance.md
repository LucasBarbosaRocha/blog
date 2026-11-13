---
title: "Heuristics for the Specific Substring Problem with Hamming Distance"
date: 2019-10-28 12:00:00
category: "Research"
tags: ["bioinformatics", "strings", "heuristics", "mpi", "masters", "paper"]
description: "BIBE 2019: heuristics and an MPI-parallel implementation for the Specific Substring Problem under Hamming distance."
wp_url: https://capivarainformacoes.wordpress.com/2020/07/22/heuristics-for-the-specific-substring-problem-with-hamming-distance/
---

- **Published in:** 19th IEEE International Conference on Bioinformatics and Bioengineering (BIBE 2019), Athens, Greece.
[IEEE Xplore](https://ieeexplore.ieee.org/document/8941997) · [PDF](/blog/assets/uploads/2020/07/bibe.pdf)
- **Code:** [SSP on GitHub](https://github.com/LucasBarbosaRocha/SSP)

This paper continues my master's work on the
[Specific Substring Problem](/blog/2018/10/30/specific-substring-problem-bioinformatics/).
We have two sets of sequences, A and B. For the sequences in A, we look for substrings that are *specific* to them:
substrings that don't occur in any sequence of B, not even approximately, with up to `k` mismatches
(Hamming distance). Substrings like these help tell one group of sequences apart from another.

Exact solutions compare every position of each sequence in A with every position of each sequence in B,
so they get slow on real genomic data. This paper proposes **heuristics** that compute only part of that
comparison space and still give good answers.

## What I implemented

All in C++, in the `SSP` repository:

| Folder | Contents |
|---|---|
| `Exato/` | Two exact algorithms: a cubic one, and a quadratic one based on Maass's algorithm. |
| `Heuristica/` | Two heuristics that compute only the cells on or near a line through the comparison matrix, instead of the whole matrix. |
| `Paralelo/` | An **MPI** version of the second heuristic. It splits the sequences of A across the nodes of a cluster. |
| `Entradas/` | Example inputs (`alpha.fasta`, `beta.fasta`). |

The parallel version ran on a [Rocks cluster](/blog/2016/05/06/installing-rocks-cluster/). Its `maquinas`
file is just the list of compute nodes (`compute-1-0`, `compute-1-1`, …). Many of the Rocks posts on this blog
came out of keeping that cluster running.

*Authors: Lucas Barbosa Rocha, Francisco Eloi Soares de Araujo and Said Sadique Adi (FACOM, Federal University of Mato Grosso do Sul).*
