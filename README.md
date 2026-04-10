# wiki-skills

A Claude Code plugin implementing [Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) — a persistent, compounding knowledge base maintained by your LLM.

Instead of RAG (re-deriving answers from raw documents every time), this system builds and maintains a **wiki**: a structured, interlinked collection of markdown files that gets richer with every source you add and every question you ask.

Forked from [kfchou/wiki-skills](https://github.com/kfchou/wiki-skills/) and simplified (see below).

## Installation

Install as a [Claude Code plugin](https://code.claude.com/docs/en/plugins.md):

```
/plugin marketplace add MarkLeone/wiki-skills
/plugin install wiki-skills@wiki-skills
/reload-plugins
```

## Skills

| Skill | Description |
|---|---|
| `wiki-init` | Bootstrap a new wiki for any domain |
| `wiki-ingest` | Add a source (paper, URL, file, transcript) to the wiki |
| `wiki-query` | Ask a question against the wiki |
| `wiki-lint` | Health audit: broken links, orphans, missing frontmatter |
| `wiki-update` | Revise existing pages when knowledge changes |

## How It Works

```
<wiki-root>/
├── SCHEMA.md        # Conventions + wiki root path (how skills find the wiki)
├── raw/             # Immutable source documents (you manage)
├── wiki/
│   ├── index.md     # Content catalog — every page, one-line summary
│   ├── log.md       # Append-only operation log
│   ├── overview.md  # Evolving synthesis of everything known
│   └── pages/       # All wiki pages, flat, slug-named
└── assets/          # Images, PDFs, attachments
```

```
wiki-init          → bootstrap a new wiki
wiki-ingest        → add sources one at a time (repeat)
wiki-query         → ask questions against the wiki
wiki-lint          → periodic health check
wiki-update        → revise pages when knowledge changes
```

## Simplifications from upstream

This fork strips the skills down to bare essentials, removing ceremony that slowed the LLM without adding proportional value:

- **No confirmation gates** — `wiki-ingest` no longer pauses to surface takeaways and ask "anything to emphasize?" before writing. Just ingest; use `wiki-update` to adjust later.
- **No per-item approval** — `wiki-lint` offers to fix all issues at once instead of asking per-item. `wiki-update` shows diffs but doesn't require per-page confirmation.
- **No mandatory report pages** — `wiki-lint` reports inline instead of always creating a `lint-<date>.md` page.
- **No "always offer to save"** — `wiki-query` answers the question and stops. No unsaved-query logging.
- **No contradiction sweep / downstream checks** — `wiki-update` fixes the requested pages; `wiki-lint` catches the rest.
- **No emoji severity tiers** — `wiki-lint` uses plain text.
- **GitHub-style links** — `[slug](slug.md)` instead of `[[slug]]`.
- **Simpler init** — asks all config questions at once instead of one at a time.

The backlink audit in `wiki-ingest` is preserved — that's the step that makes the wiki compound.

## Inspired By

[Andrej Karpathy's LLM Wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) (April 2026)

## License

MIT
