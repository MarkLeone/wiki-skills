# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A Claude Code plugin implementing Karpathy's LLM Wiki pattern — five skills that build and maintain a structured, interlinked markdown knowledge base. No build system, no dependencies — the entire implementation is SKILL.md files (structured prompts that Claude Code executes directly).

## Repository Structure

```
.claude-plugin/
├── plugin.json          # Plugin metadata (name, version, author)
└── marketplace.json     # Marketplace listing
skills/
├── wiki-init/SKILL.md   # Bootstrap a new wiki with directory structure + SCHEMA.md
├── wiki-ingest/SKILL.md # Add a source, create pages, run backlink audit
├── wiki-query/SKILL.md  # Query the wiki (always reads pages, never from memory)
├── wiki-lint/SKILL.md   # Audit: broken links, orphans, missing frontmatter
└── wiki-update/SKILL.md # Revise pages with diffs, update navigation files
```

## Architecture

Each skill is a self-contained SKILL.md with YAML frontmatter (`name`, `description`) followed by step-by-step instructions. Skills operate on a wiki directory with this layout:

- `SCHEMA.md` — conventions + absolute wiki root path (how skills locate the wiki)
- `raw/` — immutable source documents (user-managed, skills never modify)
- `wiki/index.md` — content catalog of every page
- `wiki/log.md` — append-only operation log (never rewritten)
- `wiki/overview.md` — evolving synthesis, updated on ingest/update
- `wiki/pages/` — flat directory of slug-named markdown pages (no subdirectories)

## Key Design Decisions

- **Flat pages** — all pages are `wiki/pages/<slug>.md`, no nesting. Slugs are lowercase, hyphen-separated.
- **Bidirectional `[slug](slug.md)` links** — GitHub-style relative links; the backlink audit in wiki-ingest scans existing pages to add cross-references to/from new content.
- **YAML frontmatter required** — every page: `title`, `tags`, `sources` (list), `updated` (date).
- **Append-only log** — `wiki/log.md` entries use format: `## [YYYY-MM-DD] <operation> | <title>`.

## Editing Skills

When modifying a SKILL.md, preserve:
1. The YAML frontmatter block (`name` and `description` fields)
2. The step-by-step numbered structure — Claude Code executes these as instructions
3. References to wiki structure files (index.md, log.md, overview.md, SCHEMA.md)
