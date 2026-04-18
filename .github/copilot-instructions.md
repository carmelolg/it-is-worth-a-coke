# Copilot Instructions

## Project Overview

This is a Hugo static site blog — ["It's worth a Coke"](https://carmelolg.github.io/it-is-worth-a-coke/) — a personal technical blog by carmelolg. It uses the [hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod) theme (included as a git submodule under `themes/hugo-PaperMod/`).

## Build Commands

```bash
# Local development server
hugo server

# Production build (output goes to docs/ for GitHub Pages)
hugo --destination docs
```

The `docs/` directory is the built output **committed to the repository** and served via GitHub Pages. The CI workflow (`main.yml`) runs `hugo --destination docs` on every push to `master` and commits the result automatically.

## Content Structure

Posts live in `content/posts/` as directories named with the convention `[Category] Post Title/`:

```
content/posts/
  [AI] Agentic Flow Architecture/
    index.md          # English version (published)
    _italian.md       # Italian version (set to far-future date like 2999 to keep as draft)
    *.png             # Any images are co-located with the post
```

### Front Matter Conventions

- `draft: true` is the default for new posts (see `archetypes/default.md`)
- `date` controls publication; Italian translations use a far-future date (e.g., `2999-...`) to effectively keep them unpublished
- `tags`, `categories`, and `series` are the available taxonomies

### Creating a New Post

The default archetype generates:
```yaml
---
title: "Post Title"
date: <current date>
draft: true
---
```

Use `hugo new posts/[Category] Post Title/index.md` to scaffold a post.

## Key Configuration (hugo.yaml)

- **Output formats**: The home page outputs HTML, RSS, JSON, and a custom `llms` format (plain text at `/llms.txt` for LLM consumption)
- **Languages**: English (`en`) is the primary language; Italian content exists but is managed via `_italian.md` files with far-future dates, not through Hugo's multilingual mode
- **Syntax highlighting**: Uses CSS classes (`pygmentsUseClasses: true`, `noClasses: false`) — HLJS is disabled (`disableHLJS: true`)
- **Markdown**: `unsafe: true` is set on Goldmark, meaning raw HTML in Markdown is rendered as-is

## Bilingual Content Pattern

Each post may have two files:
- `index.md` — English, the published version
- `_italian.md` — Italian translation, kept at a far-future date (not a Hugo i18n translation; just a separate file in the same directory)

When adding or updating content, maintain both files if Italian coverage is desired.
