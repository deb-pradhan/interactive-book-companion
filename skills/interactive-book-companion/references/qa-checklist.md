# QA Checklist — test the companion before you ship it

The companion is not done when it is written. It is done when it is verified. Reviewers keep
finding bugs that a five-minute pass would have caught (a mind map whose nodes did not respond
to clicks because a pan handler was swallowing the event, charts rendering empty, a nav item
going nowhere). This file is the guardrail. Run it every time, and do not present the companion
until every applicable item passes.

## How to use this

1. **Build the test plan.** Copy the master checklist below into your working notes and make it
   specific to the companion you actually built: list its real nav items, every mind map node,
   every quiz, every chart. A generic checklist is not enough; enumerate the actual components.
2. **Verify each item.**
   - If you can run a browser (Claude Code, or any agent with a browser tool): serve the file,
     open it, and actually drive it. Click every nav item, expand every mind map branch, open
     and close every drawer, answer every quiz, submit, resize to mobile, toggle reduced motion.
     Read the browser console after each interaction. A clean render is not a pass; a driven
     interaction with no console error is.
   - If you cannot run a browser (a plain LLM with only a system prompt): trace each interaction
     through the code by hand. For every `onClick`/handler, confirm it is actually reachable
     (nothing overlays it, nothing captures the pointer first, the element is not `pointer-events:
     none`), that it reads and writes the right state, and that the state it sets is actually
     rendered. Read the code as an adversary trying to make each control fail.
3. **Fix and re-test.** Any failure: fix the code, then re-run the affected checks. A fix can
   break something else, so re-verify, do not assume.
4. **Loop until green.** Do not stop at "mostly works." Do not present a companion with a known
   bug and a caveat. Keep going until every applicable box is checked. Only then deliver.

State the result honestly when you present: "I tested every section, the mind map at all four
levels, all N quizzes, and both viewports; console is clean." If you could not run it live, say
so and say you traced it by hand instead.

---

## Master checklist

### A. Load and build
- [ ] The companion renders. No blank screen, no error boundary, no red overlay.
- [ ] Browser console is clean on load: no errors, no unresolved-import or undefined-variable
      warnings, no `key` warnings from lists.
- [ ] React: exactly one default export; every used hook is imported; `recharts` and
      `lucide-react` imports resolve and every icon name used actually exists.
- [ ] HTML: valid structure, every tag closed, one `<script>` runs without throwing.
- [ ] No leftover `TODO`, placeholder, lorem ipsum, or "[book title]" tokens.

### B. Navigation and flow
- [ ] Every nav item routes to the correct section and highlights as active.
- [ ] Every section is reachable from the nav (list them and check each).
- [ ] The guided path works end to end: Continue/Next advances, Back returns, no step is skipped
      or duplicated, and the final step leads to the closing bookend.
- [ ] Progress indicator reflects the true position and updates as you move.
- [ ] Mind map jump-links land on the right section, and back-to-map returns.
- [ ] No dead ends: every screen has a way forward and (except the first) a way back.

### C. Mind map (highest-risk component — test hard)
- [ ] Center + all major-idea branches render on load.
- [ ] EVERY node is clickable and its handler actually fires. Explicitly confirm nothing
      swallows the click: no pan/drag pointer-capture on the container intercepting it, no SVG
      or overlay sitting on top with pointer events, no `pointer-events:none` on the node body.
      (This is the exact bug that shipped before. Check it deliberately.)
- [ ] Expand/collapse works at every level and reveals the correct children (thesis → idea →
      subtopic → detail, four levels).
- [ ] The detail panel opens with the correct content for the clicked node, and closes via the
      X, the backdrop, and the Escape key.
- [ ] Pan works (drag moves the canvas) and does not fight node clicks. Zoom in/out/reset work.
- [ ] Idle animation runs; edges follow their nodes; the active node and its path highlight.
- [ ] Under `prefers-reduced-motion`, the drift and flow stop and the map is still fully usable.
- [ ] No two nodes overlap in a way that makes one unclickable.

### D. Quizzes and interactive learning
- [ ] Warm-up quiz: options select, one answer registers, the bridge sentence shows.
- [ ] Multiple choice: correct and incorrect states render correctly; the right answer is marked;
      you cannot break it by clicking twice or submitting empty.
- [ ] Fill-in-the-blank: accepts typing, validates, reveals answers.
- [ ] Predict-then-reveal: captures the prediction, then reveals and compares.
- [ ] Flashcards: flip/reveal works; self-assessment buttons respond.
- [ ] Retrieval / recall challenges: input works; nothing crashes on empty or long input.

### E. Charts, infographics, visuals
- [ ] Every chart renders with real, non-empty data (no NaN, no zero-height everything, no empty
      donut).
- [ ] Legends match the segments; tooltips (including the black value pill) show correct values.
- [ ] Progress rings animate to the correct percentage and land there.
- [ ] Stat grids, pictographs, timelines render and are not clipped or overflowing their cards.
- [ ] Every screen actually has its graphics (this doubles as the "not text-heavy" check).

### F. State integrity and edge cases
- [ ] Rapid repeated clicks do not desync state or throw.
- [ ] Empty or unexpected input (blank answer, very long text) is handled without a crash.
- [ ] Moving away from a section and back does not lose or corrupt its state.
- [ ] No `undefined`/`NaN` ever appears in the rendered UI.

### G. Responsive
- [ ] Mobile (~375px): no horizontal page scroll; cards stack; nav becomes the bottom bar; the
      mind map falls back to the collapsible tree; touch targets are at least ~44px.
- [ ] Tablet and desktop: content is centered and does not stretch past its max width.
- [ ] Wide content (charts, tables, the map) scrolls inside its own container, never the page.

### H. Theme, accessibility, motion
- [ ] If both themes ship: both are legible, and the accent works on both grounds.
- [ ] Keyboard: you can tab to every control, Enter/Space activate it, focus is visible, and
      Escape closes any open drawer/overlay.
- [ ] Non-color cues exist for correct/incorrect (icon + text, not color alone).
- [ ] `prefers-reduced-motion` is respected everywhere, not just the mind map.

### I. Copy and content
- [ ] The copy reads like a person: no AI-vocabulary, no em dashes, varied sentence length.
- [ ] Every jump-link, "see the principle card", etc. points at something that exists.
- [ ] No jargon without an immediate plain-language definition or analogy.

---

## Sign-off

Do not present the companion until you can say, truthfully, that every applicable box above is
checked and you either drove it live or traced every interaction by hand. If a genuine
environmental limit stops one check (for example, you cannot emulate touch), say exactly which
check and why, and verify everything around it. "It probably works" is not sign-off.
