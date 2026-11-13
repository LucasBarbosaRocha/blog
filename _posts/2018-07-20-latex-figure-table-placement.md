---
title: "Controlling Figure and Table Placement in LaTeX"
date: 2018-07-20 12:00:00
category: "LaTeX"
tags: ["latex"]
wp_url: https://capivarainformacoes.wordpress.com/2018/07/20/forcar-a-posicao-de-figura-tabela/
---

Figures and tables are *floats*: LaTeX moves them to where it thinks they fit best.
You can influence that with placement specifiers inside square brackets:

| Specifier | Meaning |
|-----------|---------|
| `h` | *here*: roughly where the float appears in the source |
| `t` | *top* of a page |
| `b` | *bottom* of a page |
| `p` | on a separate page with only floats |
| `!` | relax LaTeX's internal rules for what counts as a "good" position |
| `H` | *exactly* here (requires `\usepackage{float}`) |

Usage:

```latex
\begin{table}[h]
  % table content
\end{table}
```

Combining specifiers gives LaTeX more options, for example `[!htbp]`.
Use `H` only when the float really must stay in place, because it can leave large gaps on the page.
