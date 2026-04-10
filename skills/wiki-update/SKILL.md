---
name: wiki-update
description: Revise existing wiki pages when knowledge changes.
---

# Wiki Update

## Pre-condition

Find `SCHEMA.md` to locate the wiki root.

## Process

### 1. Identify target pages

Determine which pages need updating based on the user's request. Read them.

### 2. Propose changes

Show diffs for each page — what changes and why.

### 3. Apply on confirmation

Update page content, frontmatter `updated` date, and `sources` list.

### 4. Update navigation files

- `wiki/index.md` — update summaries if they changed
- `wiki/overview.md` — update if the synthesis shifted
- `wiki/log.md` — append entry listing pages updated
