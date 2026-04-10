---
name: wiki-init
description: Bootstrap a new personal wiki at a user-specified path.
---

# Wiki Init

## Process

### 1. Gather configuration

Ask the user (all at once):
1. **Where should the wiki live?** (absolute path)
2. **What is the domain/purpose?** (one sentence)
3. **What categories should index.md use?** Default: `Sources | Entities | Concepts | Analyses`

### 2. Create directory structure

```
<wiki-root>/
├── SCHEMA.md
├── raw/
├── wiki/
│   ├── index.md
│   ├── log.md
│   ├── overview.md
│   └── pages/
└── assets/
```

All pages live flat in `wiki/pages/` as `<slug>.md`. No subdirectories.

### 3. Write SCHEMA.md

Include:
- Absolute path to wiki root
- Domain description
- Page frontmatter format: `title`, `tags`, `sources`, `updated`
- Cross-reference syntax: `[slug](slug.md)` (GitHub-style relative links)
- Log entry format: `## [YYYY-MM-DD] <operation> | <title>`
- Index categories
- Conventions: raw/ is immutable, log.md is append-only, pages/ is flat

### 4. Write starter files

- `wiki/index.md` — heading per category, empty
- `wiki/log.md` — header + init entry
- `wiki/overview.md` — frontmatter + empty sections (Current Understanding, Open Questions, Key Entities)
