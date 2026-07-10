# Vendored: book-to-skill

This directory is a vendored copy of the `book-to-skill` skill from
**the-knowledge-guy** by Vitaly Simonovich.

- Upstream: https://github.com/vitalysim/the-knowledge-guy
- Commit: `052049f45f7baa57c23f24c6e0ac5aba9f5133bb` (2026-06-25)
- License: MIT (see [`LICENSE`](LICENSE) in this directory, © 2026 Vitaly Simonovich)

It is included here so the Interactive Book Companion can compress a large PDF or EPUB into a
compact, structured knowledge base before generating the companion. See [`../../PIPELINE.md`](../../PIPELINE.md)
for how the two skills fit together.

The code is used unmodified. To pull upstream fixes, re-copy from the source repo at a newer
commit and update the commit hash above. The original upstream repo also ships a companion
router skill (`the-knowledge-guy`); it is intentionally not vendored here because its rendering
role overlaps with the Interactive Book Companion.
