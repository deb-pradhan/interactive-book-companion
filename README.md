# Interactive Book Companion

Turn **any** book, article, paper, or blog post into an **interactive learning companion** built on evidence-based cognitive science: retrieval practice, dual coding, schema activation, the generation effect, and more.

The output is a single self-contained interactive page the reader moves through at their own pace, designed for deep retention instead of passive reading.

This repo is **model- and platform-agnostic**. Use it with Claude, OpenAI GPTs, Gemini, local models (Ollama / LM Studio), or agent frameworks like LangChain, CrewAI, and AutoGen.

## What the generated companion gives you

- An **interactive mind map** built as a real flow diagram: ideas as nodes, connected by lines that show how the book branches out. Click any node to open that topic and go deep.
- **Persistent navigation** so you can jump straight to the mind map, the quizzes, a specific idea, the challenges, or the final takeaway. You're never stuck on a one-way slideshow.
- A **graphics-heavy** design: charts, infographics, stat callouts, icons, and emoji anchors instead of walls of text.
- Copy that **sounds like a person**, not an AI report.
- The learning science underneath: retrieval practice, spaced structure, dual coding, the generation effect, and more.

## Uploading a whole book? It compresses first

A full-length PDF or EPUB won't fit in a model's context window. This repo handles that with a two-stage pipeline: a bundled compressor distills the book into a compact, structured knowledge base, then the companion is built from that. You get a faithful companion for a 400-page book without ever needing the whole file in memory. See **[PIPELINE.md](PIPELINE.md)**.

```
PDF / EPUB  ──▶  book-to-skill (compress)  ──▶  interactive-book-companion (build)  ──▶  companion
```

---

## What's inside

| Path | Format | Use with |
|---|---|---|
| [`skills/interactive-book-companion/`](skills/interactive-book-companion/) | Open [Agent Skill](https://agentskills.io) (`SKILL.md` + `references/`) | Claude Code, Claude.ai, and any agent that supports the Agent Skills spec |
| [`skills/book-to-skill/`](skills/book-to-skill/) | Open Agent Skill (the PDF/EPUB compressor) | Claude Code. Vendored from [the-knowledge-guy](https://github.com/vitalysim/the-knowledge-guy) (MIT). See [PIPELINE.md](PIPELINE.md). |
| [`exports/interactive-book-companion-universal-prompt.md`](exports/interactive-book-companion-universal-prompt.md) | Markdown system prompt | **Any LLM** — paste as the system prompt |
| [`exports/openai-custom-gpt-config.json`](exports/openai-custom-gpt-config.json) | OpenAI Custom GPT config | OpenAI GPTs / Assistants API |
| [`exports/agent-framework-config.json`](exports/agent-framework-config.json) | Structured agent config | LangChain, CrewAI, AutoGen, etc. |
| [`exports/interactive-book-companion.skill`](exports/interactive-book-companion.skill) | Zipped Claude skill package | Import directly into Claude.ai |

---

## Quick start

### Any LLM (system prompt)
Copy the contents of [`exports/interactive-book-companion-universal-prompt.md`](exports/interactive-book-companion-universal-prompt.md) into the system / instructions field, then send:

> Create an interactive learning companion for *Thinking, Fast and Slow* by Daniel Kahneman.

### OpenAI Custom GPT
1. Go to <https://chat.openai.com/gpts/create>
2. Paste the universal prompt into **Instructions**
3. Enable Code Interpreter + File Search, then save.

### Claude (Agent Skill)
Point your agent at the [`skills/interactive-book-companion/`](skills/interactive-book-companion/) folder, or import [`exports/interactive-book-companion.skill`](exports/interactive-book-companion.skill) into Claude.ai via **Save Skill**.

### A whole PDF or EPUB (Claude Code)
Compress the book first, then build the companion from the result:

```
/book-to-skill /path/to/book.pdf        # stage 1: compress into a knowledge base
# then ask the companion to build from that compressed skill
```

The compressor needs the [`uv`](https://github.com/astral-sh/uv) package manager for its Python dependencies. Full walkthrough in [PIPELINE.md](PIPELINE.md).

### Python (OpenAI / Anthropic / Gemini)
```python
# OpenAI example — swap the client for any provider
from openai import OpenAI
client = OpenAI()
system_prompt = open("exports/interactive-book-companion-universal-prompt.md").read()

resp = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": system_prompt},
        {"role": "user", "content": "Create a learning companion for 'Atomic Habits'"},
    ],
    max_tokens=16000,
)
print(resp.choices[0].message.content)
```

### LangChain / CrewAI
Load [`exports/agent-framework-config.json`](exports/agent-framework-config.json) and use its `system_prompt`, `agent`, and `task` fields. Full snippets are in [`exports/`](exports/).

---

## The ten methods

The companion is generated using ten evidence-based learning techniques (retrieval practice, spaced structure, dual coding, elaborative interrogation, concrete examples, interleaving, schema building, the generation effect, metacognition, and transfer). Details in [`skills/interactive-book-companion/references/ten-methods.md`](skills/interactive-book-companion/references/ten-methods.md).

---

## Notes
- The universal prompt is ~45k tokens; use a model with a 128k+ context window (GPT-4o, Claude, Gemini 2.0) for best results.
- Output quality scales with model capability. Frontier models produce the richest companions.
- The universal prompt emits dependency-free vanilla HTML; the Claude skill emits React JSX (rendered natively by Claude artifacts).
- For whole books, compress first (see [PIPELINE.md](PIPELINE.md)); for articles and excerpts, build straight from the text.

## License
[MIT](LICENSE), free to use, modify, and redistribute. The vendored [`skills/book-to-skill/`](skills/book-to-skill/) is also MIT, © 2026 Vitaly Simonovich; its license travels with it in that folder.
