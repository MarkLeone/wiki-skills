---
name: wiki-ingest
description: Add a source (file, URL, or pasted text) to the wiki. One ingest may touch 10-15 pages.
---

# Wiki Ingest

## Pre-condition

Find `SCHEMA.md` starting from the current directory and upward. If not found, tell the user to run `wiki-init` first. Read it to learn wiki root path and conventions.

## Process

### 1. Accept and read the source

- **File path** — read it; copy to `raw/` if not already there
- **URL** — fetch it; save to `raw/<slug>.<ext>`
- **Pasted text** — use as-is

Read all content. Do not skip sections.

### 2. Write the source summary page

Write `wiki/pages/<slug>.md` with frontmatter (`title`, `tags`, `sources`, `updated`) and sections:
- **Summary** — 2-3 paragraph synthesis in your own words
- **Key Takeaways** — bullet list
- **Entities & Concepts** — `[slug](slug.md)` links to entity/concept pages
- **Relation to Other Wiki Pages** — how this connects to existing knowledge

### 3. Update entity and concept pages

For each entity/concept this source touches:
- **Page exists:** update it — add info, add this source to frontmatter `sources`, update date
- **Page doesn't exist:** create it with Description, Appearances in Sources, Related Concepts

### 4. Backlink audit

Scan all existing pages in `wiki/pages/` for mentions of this source's entities/concepts that don't yet link to the new pages. Add `[slug](slug.md)` references where appropriate. This is what makes the wiki compound.

### 5. Update navigation files

- `wiki/index.md` — add entries under correct categories
- `wiki/overview.md` — update if this source shifts the synthesis
- `wiki/log.md` — append entry listing pages written and updated

### 6. Report

List: summary page created, entity/concept pages created or updated, pages that received backlinks.
