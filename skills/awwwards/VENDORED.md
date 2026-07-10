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

**READ [`ARTIFACT-ADAPTATION.md`](ARTIFACT-ADAPTATION.md) FIRST.** This skill is written for full
web projects and reaches for GSAP, Three.js, Lenis, Spline, external fonts, npm packages, and
CDNs. Our companion ships as a single self-contained artifact under a strict CSP where none of
those can load — copying an `import` or `<script src>` line from here will leave the companion
blank or broken. The adaptation file maps every technique to its dependency-free equivalent and
lists the exact pitfalls to avoid. Take the principles and numbers from this skill; take the
delivery rules from the adaptation file.

**How it relates to our design system.** The companion's own design system
(`../interactive-book-companion/references/design-system.md`, section 18) already encodes the
award-level bar and the parts of this guidance that fit our product. Use this vendored skill for
the deeper technique detail, filtered through `ARTIFACT-ADAPTATION.md`.

The code and text are used unmodified. To pull upstream changes, re-copy from the source repo at
a newer commit and update the commit hash above.
