# Agent instructions

This repo is the **Interactive Book Companion** skill: it turns a book, article, paper, PDF, or
EPUB into a single interactive learning companion built on cognitive science. This file tells an
AI agent how to use it. Many agents read `AGENTS.md` automatically; if yours doesn't, paste the
block below into its system prompt, custom instructions, or rules file (`.cursorrules`,
`CLAUDE.md`, etc.).

## When to use it

Whenever the user wants to turn a book, article, paper, PDF, or EPUB into an interactive learning
companion, or asks to summarize, study, learn, absorb, or retain a text.

## Instructions (agents that can read this repo)

1. **Load the skill.** Read [`skills/interactive-book-companion/SKILL.md`](skills/interactive-book-companion/SKILL.md)
   and its [`references/`](skills/interactive-book-companion/references/) (`design-system.md`,
   `ten-methods.md`, `qa-checklist.md`) and follow them literally. For award-level design detail,
   also consult [`skills/awwwards/`](skills/awwwards/) — but read
   [`skills/awwwards/ARTIFACT-ADAPTATION.md`](skills/awwwards/ARTIFACT-ADAPTATION.md) FIRST, since
   it maps each technique to what actually works inside a single self-contained artifact.
2. **Big files: compress first.** If the source is a PDF or EPUB too large to fit in context,
   compress it with [`skills/book-to-skill`](skills/book-to-skill/) (see [`PIPELINE.md`](PIPELINE.md)),
   then build the companion from the compressed knowledge base.
3. **Non-negotiables:**
   - The goal is **understanding, not decoration.** Every idea gets a real explanation (what,
     why, how) plus a concrete worked example. Never ship thin, pretty-but-empty screens.
   - Output **one self-contained artifact**: a React component (in Claude) or a single HTML file.
     No external libraries, fonts, images, CDNs, or network calls. Inline SVG + CSS +
     `requestAnimationFrame` only.
   - The mind map is an **animated, top-down tree**, four logical levels deep; every node opens a
     substantial mini-lesson (multi-paragraph explanation + a worked example).
   - Persistent navigation; graphics-rich, but text carries the teaching (dual coding); write in
     a human voice with no em dashes.
   - **Test before delivering.** Run [`qa-checklist.md`](skills/interactive-book-companion/references/qa-checklist.md),
     drive every flow, confirm the console is clean and there are no known bugs, and loop until
     green.
4. Deliver the companion with a short orientation and an honest test report.

## Paste-ready version

```
You have the Interactive Book Companion skill in this repo.

Trigger: the user wants to turn a book/article/paper/PDF/EPUB into an interactive
learning companion, or to summarize/study/learn/retain a text.

1. LOAD THE SKILL: read skills/interactive-book-companion/SKILL.md and its
   references/ (design-system.md, ten-methods.md, qa-checklist.md) and follow
   them literally. For award-level craft see skills/awwwards/, but read
   skills/awwwards/ARTIFACT-ADAPTATION.md first.
2. BIG FILES: if the source is a PDF/EPUB too large for context, compress it
   with skills/book-to-skill (see PIPELINE.md), then build from the result.
3. NON-NEGOTIABLES:
   - Goal is UNDERSTANDING. Every idea gets a real explanation (what/why/how) +
     a worked example. No thin, decorative screens.
   - Output ONE self-contained artifact: React (Claude) or one HTML file. No
     external libs/fonts/images/CDNs/network. Inline SVG + CSS + rAF only.
   - Mind map = animated TOP-DOWN tree, 4 logical levels; every node opens a
     substantial mini-lesson (multi-paragraph explanation + example).
   - Persistent nav; graphics-rich but text carries the teaching; human voice,
     no em dashes.
   - TEST BEFORE DELIVERING: run references/qa-checklist.md, drive every flow,
     console clean, no known bugs. Loop until green.
4. Deliver with a short orientation and an honest test report.
```

## Agents that cannot read this repo

The universal prompt is fully self-contained (the whole skill is embedded), so no repo access is
needed. Set it as the system prompt:

- **API (any provider):** load [`exports/interactive-book-companion-universal-prompt.md`](exports/interactive-book-companion-universal-prompt.md)
  and pass it as the `system` / system message.
- **OpenAI Custom GPT / Assistant:** paste that file into the **Instructions** field.
- **LangChain / CrewAI / AutoGen:** use [`exports/agent-framework-config.json`](exports/agent-framework-config.json)
  (`system_prompt`, `agent`, `task`).

Then the user says: *"Create an interactive learning companion for [book]."*

## Placement cheat-sheet

| Agent | Where the instruction goes |
|---|---|
| Claude Code | `.claude/skills/` (auto-discovered), or this file / `CLAUDE.md` |
| Cursor / Windsurf / Cline | this file, or `.cursorrules` |
| Generic coding agent | this `AGENTS.md` |
| OpenAI GPT / API / Gemini / local | the universal prompt (self-contained, no repo needed) |
