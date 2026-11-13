---
title: "Specific Substring Problem: An Application in Bioinformatics"
date: 2018-10-30 12:00:00
category: "Research"
tags: ["bioinformatics", "strings", "algorithms", "masters", "paper"]
description: "BSB 2018 short paper introducing the Specific Substring Problem under Hamming distance."
wp_url: https://capivarainformacoes.wordpress.com/2019/02/11/specific-substring-problem-an-application-in-bioinformatics/
---

- **Published in:** 11th Brazilian Symposium on Bioinformatics (BSB 2018), Niterói, Brazil. Short paper.
[SBC OpenLib](https://sol.sbc.org.br/index.php/bsb_estendido/article/view/8801) · [Proceedings PDF](/blog/assets/uploads/2019/02/proceedings-bsb-2018.pdf)
- **Code:** [SSP on GitHub](https://github.com/LucasBarbosaRocha/SSP)

This was the first paper from my master's at UFMS. It presents the **Specific Substring Problem** with
Hamming distance. Given two sets of DNA sequences, A and B, find the substrings of A that do not occur in any
sequence of B, allowing up to `k` mismatches. These *specific* substrings work as signatures: they appear in one
group of sequences and nowhere in the other.

The paper describes exact algorithms for the problem and shows how it applies to biological data.
The [follow-up at BIBE 2019](/blog/2019/10/28/heuristics-specific-substring-problem-hamming-distance/) adds
faster heuristics and a parallel implementation.

*Authors: Lucas Barbosa Rocha, Francisco Eloi Soares de Araujo and Said Sadique Adi (FACOM, Federal University of Mato Grosso do Sul).*
