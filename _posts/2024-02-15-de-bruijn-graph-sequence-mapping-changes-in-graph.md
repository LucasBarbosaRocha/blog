---
title: "The De Bruijn Graph Sequence Mapping Problem with Changes in the Graph"
date: 2024-02-15 12:00:00
category: "Research"
tags: ["bioinformatics", "de-bruijn-graphs", "algorithms", "phd", "paper"]
description: "bioRxiv 2024 preprint: mapping a sequence onto a De Bruijn graph by relabeling the graph turns out to be polynomial (Hungarian algorithm)."
---

- **Preprint on bioRxiv (2024):** [The De Bruijn Graph Sequence Mapping Problem with Changes in the Graph](https://www.biorxiv.org/content/10.1101/2024.02.15.580401v2)
- **Code:** [PMSB on GitHub](https://github.com/LucasBarbosaRocha/PMSB) (folder `variante2/`)

## The problem

In the *De Bruijn graph Sequence Mapping Problem* (BSMP), we get a sequence `s` and a De Bruijn graph `G`.
The goal is to find a walk in `G` whose spelled sequence is as close as possible to `s`.
My [ICCSA 2023 paper](/blog/2023/07/05/heuristics-de-bruijn-graph-sequence-mapping/) attacked the version where the
**sequence** changes. This one looks at the opposite: keep `s` as it is and **change the graph**.
We relabel some vertices (swap a vertex's k-mer for another) until `G` spells `s` exactly.
Each relabel costs the Hamming distance between the old and the new k-mer.

## Why the details matter

Gibney et al. (2022) studied a version of this problem where the graph's **arcs are fixed**:
you can relabel vertices, but who is connected to whom never changes. They proved that version is **NP-complete**.

In a real De Bruijn graph, though, arcs are not stored separately. They are *implied* by the labels: two vertices
are adjacent when the suffix of one k-mer is the prefix of the other. So relabeling a vertex naturally creates
and removes arcs. Once we allow that, the problem becomes **polynomial**. It reduces to a
**minimum-cost bipartite matching**: the distinct k-mers of `s` on one side, the vertices of `G` on the other,
and the Hamming distance as the edge cost. The **Hungarian algorithm** solves that matching optimally.

Same question, one different constraint (fixed arcs vs. implied arcs), and the complexity class drops from
NP-complete to polynomial time.

## What I implemented

- **BMTC** (*De Bruijn sequence Mapping Tool with graph Changes*), in C++ (`variante2/btl/`).
  It builds the Hamming cost matrix between the k-mers of `s` and the vertices of `G`, runs the Hungarian algorithm,
  and applies the minimum-cost relabeling to the graph. It reports the optimal cost and how many windows of `s`
  the edited graph covers.
- A small **local web panel** (`webui/`, plain Python standard library). You pick any of the tools from the thesis,
  compile it with one click, upload a graph and a sequence, and see the result in the browser.

This work is Chapter 6 of my PhD thesis, *O Problema do Mapeamento de Sequências em Grafos de De Bruijn* (UFMS, 2024),
which is available as `Tese_doutorado.pdf` in the repository. A third variant, with changes in **both** the sequence and
the graph, is NP-complete and has no implementation.

*Authors: Lucas Barbosa Rocha, Francisco Eloi Soares de Araujo and Said Sadique Adi (FACOM, Federal University of Mato Grosso do Sul).*
