# brightiny9.github.io

A pen-name blog by **brightiny9**: introductions of the products we build, and side-by-side breakdowns of similar products. Bilingual (Korean/English), built by GitHub Pages' native Jekyll build with the [Tale](https://github.com/chesterhow/tale) theme (`remote_theme`). Our `_layouts`, `_includes` and `assets/main.scss` override the theme where needed. No ads, no tracking.

Posts arrive as PRs from the brightiny9 bot; merging publishes.

## Post contract

Each post is a pair of files sharing a slug:

- `_posts/YYYY-MM-DD-<slug>-ko.md`
- `_posts/YYYY-MM-DD-<slug>-en.md`

Front matter:

```yaml
---
layout: post
title: "<title>"
lang: ko            # or en
ref: <slug>
date: YYYY-MM-DD
permalink: /ko/<slug>/   # or /en/<slug>/
---
```

`_layouts/post.html` links each post to its translation (same `ref`, other `lang`).
