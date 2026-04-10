---
name: wiki-query
description: Ask a question against the wiki. Always reads pages first — never answers from memory.
---

# Wiki Query

## Pre-condition

Find `SCHEMA.md` to locate the wiki root.

## Process

### 1. Find relevant pages

Read `wiki/index.md`. Identify pages likely to contain the answer.

### 2. Read and follow links

Read identified pages. Follow one level of cross-reference links if they seem relevant.

### 3. Answer

Synthesize an answer grounded in wiki content. Cite sources using `[slug](slug.md)` references. Do not use general knowledge for claims the wiki covers — if the wiki doesn't have it, say so.
