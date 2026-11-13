# Capybara Informs

My space to write about everything I've run into in computing: the command I spent an afternoon looking for,
the cluster that wouldn't boot, the LaTeX float that refused to stay put, the judge problem that finally got
accepted, and the research that came out of my master's and PhD. If I had to figure it out once, it goes here,
so neither I nor anyone else has to figure it out again.

**Live at:** https://lucasbarbosarocha.github.io/blog

## What you'll find

| Category | Topics |
|---|---|
| **Research** | Papers and code from my master's and PhD at UFMS: the Specific Substring Problem, sequence mapping on De Bruijn graphs, alignment-free DNA clustering |
| **Linux & HPC** | Rocks Cluster setup and troubleshooting, CUDA on GPU nodes, sysadmin how-tos, archives, networking |
| **Programming** | A Shell Scripting 101 series, Python and C snippets, beecrowd (URI) judge solutions |
| **LaTeX** | Installing, compiling, document classes, float placement |

## History

The blog started in 2016 on WordPress.com as *Capivara Informações*, written in Portuguese.
In 2026 it moved here: every post was translated to English and revised. Wrong commands were fixed,
code was reformatted and tested, and posts about software that is no longer maintained (Rocks, CentOS,
the 2016 Redmine/GitLab setups) carry a **legacy** notice. Each migrated post keeps a `wp_url` field
pointing to its original address.

## How it's built

- [Jekyll](https://jekyllrb.com/) on GitHub Pages, served under `/blog` from this repository
- Plain HTML/CSS layouts with light and dark themes; no JavaScript framework
- Client-side search over titles, tags and full text (`search.json`)
- RSS feed (`/feed.xml`), sitemap and SEO tags via the standard GitHub Pages plugins

```
_posts/        posts in Markdown (YYYY-MM-DD-slug.md)
_layouts/      default, post and page templates
assets/        stylesheet, capybara icon, uploaded PDFs and images
index.html     home: research cards, search, category filters, posts by year
about.md       About page
search.json    search index generated at build time
```

## Writing a post

Create `_posts/YYYY-MM-DD-slug.md`:

```markdown
---
title: "Title"
category: "Programming"   # Research | Linux & HPC | Programming | LaTeX
tags: ["python"]
description: "Optional one-line summary for search engines and the feed."
legacy: true              # optional: shows the legacy-content notice
---

Markdown content. Fenced code blocks get syntax highlighting.
```

## Running locally

```bash
bundle install
bundle exec jekyll serve   # http://localhost:4000/blog/
```

Or with Docker, without installing Ruby:

```bash
docker run --rm -p 4000:4000 -v "$PWD":/srv -w /srv ruby:3.3 \
  sh -c 'bundle install && bundle exec jekyll serve --host 0.0.0.0'
```
