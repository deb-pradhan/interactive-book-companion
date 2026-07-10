# Vendored: awwwards

This directory is a vendored copy of the **awwwards** creative-direction skill by
`tponscr-debug`.

- Upstream: https://github.com/tponscr-debug/claude-skill-awwwards
- Commit: `d18aa0c42b71fc60bc978b19de8e3181ab193ec5` (2026-03-10)
- License: **MIT**, as stated in the upstream [`README.md`](README.md) ("MIT — Use it, fork it,
  make beautiful things."). The upstream repo ships no standalone LICENSE file or copyright line;
  its README carries the license grant, and that README is included here unchanged.

It is included so the Interactive Book Companion can pull award-level design craft in full
detail: fluid typography, motion easing, layout rhythm, and the Awwwards judging criteria, with
the concrete code examples in `references/`.

**How it relates to our design system.** The companion's own design system
(`../interactive-book-companion/references/design-system.md`, section 18) already encodes the
award-level bar and the parts of this guidance that fit our product. Use this vendored skill for
the deeper technique detail. One adaptation to keep in mind: our companion ships as a single
self-contained artifact (React or vanilla HTML), so where this skill reaches for GSAP, Lenis,
Three.js, or other external libraries, implement the same idea with CSS + `requestAnimationFrame`
(and `recharts`/`framer-motion` only if the runtime already provides them). The principles carry
over; the delivery is dependency-free.

The code and text are used unmodified. To pull upstream changes, re-copy from the source repo at
a newer commit and update the commit hash above.
