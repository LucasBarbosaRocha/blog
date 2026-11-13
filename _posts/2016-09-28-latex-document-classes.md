---
title: "LaTeX Document Classes"
date: 2016-09-28 12:10:00
category: "LaTeX"
tags: ["latex"]
wp_url: https://capivarainformacoes.wordpress.com/2016/09/28/criando-documentos/
---

The first thing in every LaTeX document is its **class**, set with `\documentclass`.
Everything between `\documentclass` and `\begin{document}` is the **preamble**.
The preamble holds settings and packages that apply to the whole document.

```latex
\documentclass[12pt, a4paper]{article}
% preamble: packages and settings
\usepackage[utf8]{inputenc}

\begin{document}
Hello, LaTeX!
\end{document}
```

Common classes:

| Class | Use it for |
|-------|-----------|
| `article` | Journal articles, short reports, program documentation, invitations |
| `IEEEtran` | Papers in the IEEE Transactions format |
| `proc` | Conference proceedings (based on `article`) |
| `minimal` | Only sets a page size and base font; mostly for debugging |
| `report` | Longer reports with chapters, small books, theses |
| `book` | Books |
| `slides` | Simple slides with large sans-serif type |
| `letter` | Letters |
| `beamer` | Modern presentations |
