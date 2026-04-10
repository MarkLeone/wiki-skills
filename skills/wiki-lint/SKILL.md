---
name: wiki-lint
description: Audit wiki health — broken links, missing frontmatter, orphan pages.
---

# Wiki Lint

## Pre-condition

Find `SCHEMA.md` to locate the wiki root.

## Process

### 1. Scan all pages

Read every file in `wiki/pages/`. Build an inventory of slugs, `[slug](slug.md)` references, and frontmatter fields.

### 2. Check for issues

- **Broken links** — `[slug](slug.md)` references pointing to pages that don't exist
- **Missing frontmatter** — pages missing required fields (`title`, `tags`, `sources`, `updated`)
- **Orphan pages** — pages with no inbound links (exclude index.md and overview.md from this check)

### 3. Report

List all issues inline. If there are fixable issues, offer to fix them all at once.
