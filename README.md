# Kuan'Log

Source for [KuanL1u.github.io](https://KuanL1u.github.io/) — a personal blog by **Kuan Liu** covering machine learning, LLM infrastructure, distributed systems, and monthly retrospectives.

The site is built with [Hugo](https://gohugo.io/) using the [PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme and is deployed automatically to GitHub Pages.

## Tech stack

- **Static site generator:** Hugo (extended, `v0.140.1`)
- **Theme:** [hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod) (vendored as a Git submodule under `themes/PaperMod`)
- **Hosting / CI:** GitHub Pages via GitHub Actions (`.github/workflows/hugo.yaml`)
- **Content format:** Markdown with front matter (supports math, ToC, tags, categories)

## Repository layout

```
.
├── archetypes/                # Front-matter templates for `hugo new`
├── content/
│   └── posts/                 # Blog posts in Markdown
│       ├── build-nano-llm-api.md
│       ├── monthly-retro-2026-jan.md
│       └── monthly-retro-2026-feb.md
├── layouts/                   # Site-level layout overrides
├── static/                    # Static assets (favicon, images, etc.)
├── themes/PaperMod/           # PaperMod theme (Git submodule)
├── public/                    # Hugo build output (generated)
├── hugo.yaml                  # Site configuration
└── .github/workflows/hugo.yaml # Build + deploy pipeline
```

## Getting started

### Prerequisites

- [Hugo Extended](https://gohugo.io/installation/) ≥ `0.140.1`
- Git (with submodule support)

### Clone

```bash
git clone --recurse-submodules https://github.com/KuanL1u/KuanL1u.github.io.git
cd KuanL1u.github.io
```

If you already cloned without submodules:

```bash
git submodule update --init --recursive
```

### Run locally

```bash
hugo server -D
```

The site is served at <http://localhost:1313/>. The `-D` flag includes drafts.

### Build

```bash
hugo --gc --minify
```

The static output is written to `public/`.

## Writing a post

Create a new post under `content/posts/`:

```bash
hugo new content/posts/my-new-post.md
```

A typical front matter looks like:

```yaml
---
title: "My New Post"
date: 2026-05-22
draft: false
tags: ["LLM", "Systems"]
categories: ["Notes"]
summary: "Short description shown in lists and social cards."
ShowToc: true
TocOpen: false
math: true
---
```

Set `draft: false` when you're ready to publish.

## Deployment

Every push to `main` triggers `.github/workflows/hugo.yaml`, which:

1. Installs Hugo Extended and Dart Sass.
2. Checks out the repo (including the PaperMod submodule).
3. Builds the site with `hugo --gc --minify` against the Pages base URL.
4. Uploads the `public/` artifact and deploys it to GitHub Pages.

You can also trigger the workflow manually from the **Actions** tab.

## Configuration

Site-wide settings (title, menu, social icons, analytics, PaperMod params) live in [`hugo.yaml`](./hugo.yaml). Notable params:

- `theme: PaperMod`
- `params.ShowReadingTime`, `params.ShowShareButtons` (`x`, `linkedin`, `reddit`)
- `params.math: true` (KaTeX support)
- `params.socialIcons` — email, LinkedIn, Google Scholar

## License

Blog content (everything under `content/`) is © Kuan Liu, all rights reserved unless otherwise noted in a post.

The PaperMod theme is distributed under its own [MIT license](https://github.com/adityatelange/hugo-PaperMod/blob/master/LICENSE).
