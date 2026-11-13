---
title: "Heuristics for the De Bruijn Graph Sequence Mapping Problem"
date: 2023-07-05 12:00:00
category: "Research"
tags: ["bioinformatics", "de-bruijn-graphs", "algorithms", "heuristics", "phd", "paper"]
description: "ICCSA 2023: an exact algorithm and fast seed-based heuristics for mapping a sequence onto a De Bruijn graph."
wp_url: https://capivarainformacoes.wordpress.com/2023/07/05/heuristics-for-the-de-bruijn-graph-sequence-mapping-problem/
---

- **Published in:** 23rd International Conference on Computational Science and Its Applications (ICCSA 2023),
[Springer LNCS](https://link.springer.com/chapter/10.1007/978-3-031-36805-9_11)
- **Preprint:** [bioRxiv](https://www.biorxiv.org/content/10.1101/2023.02.05.527069v3)
- **Code:** [PMSB on GitHub](https://github.com/LucasBarbosaRocha/PMSB) (folder `variante1/`)

## The problem

De Bruijn graphs are everywhere in genome assembly and pangenomics. Each vertex is a k-mer, and arcs connect
k-mers that overlap by `k − 1` characters. A recurring question is how to **map a sequence onto the graph**:
given a sequence `s` (say, a sequencing read) and a De Bruijn graph `G`, find a walk in `G` whose spelled sequence
is as similar as possible to `s`, here measured by Hamming distance.

An exact algorithm exists, but it runs on a **multilayer graph** with one copy of `G` per position of `s`.
That gets heavy quickly as sequences and graphs grow. This paper proposes heuristics that are much faster and
still find good mappings.

## What I implemented

All in C++, under `variante1/bmt/`:

| Tool | Approach |
|---|---|
| **BSMT** | Exact algorithm: Dijkstra on the multilayer graph. Used as the quality reference, since no heuristic can beat its cost. |
| **BSMT_h1** | Anchors *seeds* (k-mers of `s` that already exist in `G`) and fills each gap between seeds with Dijkstra on a small local subgraph. |
| **BSMT_h1b** | Same as h1, but builds the graph with the [Bifrost](https://github.com/pmelsted/bifrost) library. |
| **BSMT_h2** | Seed-and-extend, allowing substitutions. |
| **BSMT_h3** | Seed-and-extend, allowing substitutions and deletions. |

There are also *cost-only* builds of the exact algorithm and of h1, which skip rebuilding the mapped sequence
and save memory.

The heuristics trade optimality for speed. On some inputs they return a partial mapping, with gaps where they
couldn't cover the sequence. That's expected behavior, and the paper discusses it.

*Authors: Lucas Barbosa Rocha, Francisco Eloi Soares de Araujo and Said Sadique Adi (FACOM, Federal University of Mato Grosso do Sul).*

**Follow-up:** the [2024 preprint](/blog/2024/02/15/de-bruijn-graph-sequence-mapping-changes-in-graph/) studies the version
where the **graph** changes instead of the sequence.
