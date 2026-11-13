---
title: "Installing LaTeX on Debian/Ubuntu and Compiling a .tex File"
date: 2016-09-28 12:00:00
category: "LaTeX"
tags: ["latex", "debian"]
wp_url: https://capivarainformacoes.wordpress.com/2016/09/28/instalando-e-compilando-um-arquivo-tex/
---

## Install

On Debian or Ubuntu, install TeX Live plus the extra packages and the language support you need
(Portuguese in this example):

```bash
sudo apt install texlive texlive-latex-extra texlive-lang-portuguese
```

## Compile straight to PDF

```bash
pdflatex document.tex
```

`pdflatex` cannot embed **EPS** images. If your document uses them, either convert them to PDF
(`epstopdf figure.eps`) or use the DVI route below.

## The DVI → PS → PDF route

```bash
latex document.tex        # produces document.dvi
dvips document.dvi        # produces document.ps
ps2pdf document.ps        # produces document.pdf
```

You can also convert DVI straight to PDF:

```bash
dvipdfm document.dvi
```

> **Tip:** `latexmk -pdf document.tex` runs LaTeX, BibTeX and makeindex as many times as needed,
> so cross-references and citations come out right.
