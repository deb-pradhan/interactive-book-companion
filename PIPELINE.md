# The two-stage pipeline: compress, then build

A whole book won't fit in a model's context window. A 300-page PDF blows past the limit, and
forcing it in is where the output gets shallow. So for anything book-sized, this repo runs two
skills back to back:

```
   PDF / EPUB
       │
       ▼
┌──────────────────────┐     compressed knowledge base
│   book-to-skill      │     (Tier 1 concept map ~few k tokens
│   (compressor)       │ ──▶  + Tier 2 per-chapter toolkits)
└──────────────────────┘
       │
       ▼
┌──────────────────────────────┐
│  interactive-book-companion  │ ──▶  interactive learning companion
│  (generator)                 │      (mind map, nav, charts, quizzes)
└──────────────────────────────┘
```

## Why two stages

Feeding the companion generator a raw 100k-word book either overflows the context or forces a
lossy skim. Compressing first fixes that: [`book-to-skill`](skills/book-to-skill/) distills the
book into a structured base that holds the important parts (the thesis, the named frameworks, the
per-chapter toolkits, a topic index) in a few thousand tokens, and lets you pull any single
chapter's detail on demand. The companion is then built from that base, so it stays faithful to
the book without ever needing the whole file in memory at once.

## Stage 1 — Compress (book-to-skill)

Vendored from [the-knowledge-guy](https://github.com/vitalysim/the-knowledge-guy) (MIT). It runs
a map-reduce over the book and writes a small skill folder:

- **Tier 1 — `SKILL.md`:** thesis, concept map, 6-10 load-bearing frameworks, chapter index,
  topic index. Always loaded.
- **Tier 2 — `chapters/*.md`:** ~1,000-token toolkit per chapter, plus `nutshell.md`,
  `glossary.md`, `patterns.md`, `cheatsheet.md`. Loaded on demand.

Run it in Claude Code:

```
/book-to-skill /path/to/book.pdf   [skill-name]
```

Text extraction (PyMuPDF / ebooklib, handles scanned pages and embedded images) lives in
[`skills/book-to-skill/scripts/extract.py`](skills/book-to-skill/scripts/extract.py). Install
its dependencies with `skills/book-to-skill/requirements.txt` (needs the `uv` package manager).
See that skill's own [SKILL.md](skills/book-to-skill/SKILL.md) for the full pipeline.

## Stage 2 — Build (interactive-book-companion)

Point [`interactive-book-companion`](skills/interactive-book-companion/) at the compressed base
instead of the raw book:

- The **thesis** becomes the opening bookend and the center of the mind map.
- The **frameworks** become the mind map's branch nodes and the principle cards.
- The **chapter index** seeds the timeline and the clickable deep dives.
- Individual **Tier 2 chapter files** get pulled in only when a topic needs more depth (a case
  study, a chart, a retrieval challenge).

The result is the interactive companion described in the [main README](README.md): an
interactive mind map, persistent navigation, charts and infographics, quizzes, and copy that
reads like a person wrote it.

## No book-to-skill? Compress by hand

On a plain LLM with only a system prompt and no way to run Python, you can't run the pipeline.
The [universal prompt](exports/interactive-book-companion-universal-prompt.md) covers the
fallback: chunk the book, extract the same structure from each chunk (thesis, frameworks,
per-chapter toolkit, topic index), stitch the chunks into one Tier 1 base, then build the
companion from that.

## Small inputs skip Stage 1

A pasted excerpt, an article, or a single chapter fits in context already. Skip compression and
build the companion straight from the text.
