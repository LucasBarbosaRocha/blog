---
title: "Alignment-Free DNA Clustering: Mean Shift vs. K-Means"
date: 2020-07-15 12:00:00
category: "Research"
tags: ["bioinformatics", "clustering", "machine-learning", "python", "k-mers"]
description: "Two Python tools that cluster DNA sequences by k-mer composition, comparing mean shift and k-means."
---

**Code:** [PyMeShClust](https://github.com/LucasBarbosaRocha/PyMeShClust) (mean shift) · [PyKmClust](https://github.com/LucasBarbosaRocha/PyKmClust) (k-means)

Two sibling Python projects, started for an Artificial Intelligence course, that tackle the same problem with
different algorithms so they can be compared side by side.

## The idea

Clustering DNA by aligning every sequence against every other takes O(n²) alignments, which is expensive.
The *alignment-free* alternative compares sequences by their **k-mer composition**:

1. **Sequence → vector.** Each sequence becomes a normalized vector of k-mer frequencies.
   With k = 3 that's 64 positions: AAA, AAC, …, TTT.
2. **Cluster the vectors.** Two strategies:
   - **PyKmClust**, based on a paper that applied k-means to hepatitis B virus (HBV) sequences.
     You choose the number of clusters. It uses k-means++ initialization and keeps the best of 10 runs.
   - **PyMeShClust**, a NumPy reimplementation of [MeShClust](https://doi.org/10.1093/nar/gky315).
     You choose a **similarity threshold** instead, and the number of clusters follows from it.
     A greedy mean-shift phase moves each cluster's center toward the densest region, and a merge phase joins
     clusters whose centers are similar.
3. **Output** in CD-HIT's `.clstr` format, plus an evaluation script (`avaliar.py`) that scores the clustering against
   labels taken from the FASTA headers using ARI, NMI and purity.

## What came out of it

The data: 16 HBV sequences (7 genotypes, 4 genome regions) and 500 bacterial sequences (237 labeled contigs and
263 unlabeled short reads). Best Adjusted Rand Index (ARI) for each method:

| Task | k-means | Mean shift |
|---|---|---|
| HBV genome region | 0.801 | **0.966** |
| HBV genotype | 0.300 | **0.552** |
| Bacteria, species | **0.223** | 0.198 |
| Bacteria, genus (labeled only) | **0.329** | 0.194 |

The main lessons:

- **The representation matters more than the algorithm.** Changing the k-mer size moves the results more than
  switching between k-means and mean shift.
- **Each method assumes a different shape for the groups.** Mean shift handles compact groups (HBV regions) well
  and isolates noise in its own clusters. K-means does better when a class is spread out (bacterial contigs),
  but you need to know *k*.
- **K-mer composition tells you *what kind* of sequence something is, not *how similar* two sequences are.**
  Genotypes that differ in about 8% of positions barely change short k-mer counts. That's why the original MeShClust
  trains a model to predict alignment identity.
- **It scales.** About 200,000 sequences cluster in a few seconds with little memory. That makes it a good first pass
  before an alignment-based method, not a replacement for one.

The full tables are in each repository's `RESULTADOS.md`.
