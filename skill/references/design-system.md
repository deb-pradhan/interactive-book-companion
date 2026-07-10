# Interactive Book Companion — Complete Design System

This document is the single source of truth for every visual decision in the companion.
Any AI agent reading this file should be able to produce an interface indistinguishable
from one designed by a senior Apple/Google design lead. Follow every specification literally.
When in doubt, choose the calmer, more spacious, more restrained option.

---

## 1. Design Philosophy

The visual language is derived from five principles observed in best-in-class learning and
wellness interfaces (the Roam learning platform and HealthyLife dashboard families):

1. **Soft environmental canvas.** The background is never pure white — it is a tinted, muted
   surface that makes the entire screen feel like a calm physical environment rather than a
   harsh digital grid. Cards float on this canvas with elevation.

2. **Card-first information architecture.** Every discrete piece of content lives inside a
   card. Cards are the atomic unit of the UI. They have generous radius, soft shadows, and
   ample internal breathing room. Information density is managed by the number of cards
   visible, not by cramming content into fewer cards.

3. **Color as functional language.** Each interaction type has a dedicated accent color. The
   user learns the color vocabulary within the first two minutes and can then predict what
   a screen will ask of them before reading a word. Color is never decorative — it always
   signals function.

4. **One focus at a time.** The interface never shows two competing demands for attention.
   Stepper screens show one concept. Quiz screens show one question. Cards show one principle.
   Density is for dashboards; learning is sequential.

5. **Friendly authority.** The tone is warm but not childish. Rounded shapes signal
   approachability; consistent spacing and typographic hierarchy signal expertise. The
   interface should feel like a brilliant friend who happens to be a professor — not a
   textbook, not a toy.

---

## 2. Color System

### 2.1 Canvas and Surface Colors

These form the spatial depth of the interface. Three layers: canvas → card → elevated card.

| Token | Hex | RGB | Usage |
|---|---|---|---|
| `canvas` | `#E0E4F7` | 224, 228, 247 | Full-page background. A soft periwinkle-lavender that gives warmth without being warm. Every screen sits on this. |
| `surface-primary` | `#FFFFFF` | 255, 255, 255 | Primary card backgrounds. The dominant surface the user reads on. |
| `surface-raised` | `#F8F9FE` | 248, 249, 254 | Nested cards, input fields, or secondary panels sitting on top of a white card. Barely visible lift. |
| `surface-sunken` | `#F1F3FB` | 241, 243, 251 | Inset areas: text input backgrounds, code blocks, fill-in-the-blank slots. Pushed in rather than lifted. |
| `surface-dark` | `#12121F` | 18, 18, 31 | Bookend screens, dark feature cards (milestones, AI assistant panels). A deep navy-black, never pure #000. |
| `surface-dark-secondary` | `#1E1E30` | 30, 30, 48 | Secondary elements on dark surfaces — nested cards, input areas on dark backgrounds. |

### 2.2 Text Colors

| Token | Hex | Opacity variant | Usage |
|---|---|---|---|
| `text-primary` | `#0D0F1A` | — | Headings, body text on light surfaces. Near-black with a cool undertone. |
| `text-secondary` | `#6B7280` | — | Supporting text, labels, captions, metadata. |
| `text-tertiary` | `#9CA3AF` | — | Placeholder text, disabled labels, timestamps. |
| `text-on-dark` | `#F8F9FE` | — | All text on `surface-dark`. |
| `text-on-dark-secondary` | `#A5A6C4` | — | Secondary text on dark surfaces. Muted lavender-gray. |
| `text-on-accent` | `#FFFFFF` | — | Text sitting on any accent-colored background. Always pure white. |

### 2.3 Accent Colors — The Functional Palette

Each accent has a **full** value (for backgrounds, icons, active states), a **soft** value
(for light backgrounds, tags, and containers), and a **deep** value (for text-on-soft and
hover states).

| Role | Full | Soft | Deep | Function in the companion |
|---|---|---|---|---|
| `accent-indigo` | `#6366F1` | `#EEF2FF` | `#4338CA` | **Quiz & retrieval.** Schema activation questions, fill-in-the-blank, flashcard borders, recall challenges. The "testing" color. |
| `accent-amber` | `#F59E0B` | `#FEF3C7` | `#D97706` | **Progress & prediction.** Progress bars, predict-then-reveal prompts, completion percentages, streak indicators. The "forward motion" color. |
| `accent-orange` | `#F97316` | `#FFF7ED` | `#C2410C` | **Energy & activity.** Course cards, active learning states, timer elements, "overdue" signals. The "do it now" color. |
| `accent-rose` | `#EC4899` | `#FDF2F8` | `#BE185D` | **Creative & synthesis.** Case study modules, creative exercises, the "connect the dots" interactions, narrative/story elements. |
| `accent-emerald` | `#10B981` | `#ECFDF5` | `#047857` | **Success & completion.** Correct answers, completed sections, milestone checkmarks, principle mastery indicators. |
| `accent-violet` | `#8B5CF6` | `#F5F3FF` | `#6D28D9` | **Principle & insight.** Principle card accents, mind map nodes, "aha moment" highlights, key takeaway markers. |
| `accent-black` | `#12121F` | `#F3F4F6` | `#0D0F1A` | **Primary CTAs.** The main action button (Next, Continue, Submit). Always a dark pill on light backgrounds. Inverted to white pill on dark backgrounds. |

### 2.4 Semantic Colors

| Token | Hex | Usage |
|---|---|---|
| `success` | `#22C55E` | Correct answers, passed checks, completion badges |
| `error` | `#EF4444` | Incorrect answers (momentary), overdue items, alerts |
| `warning` | `#F59E0B` | Shared with accent-amber. Caution states, unsaved progress |
| `info` | `#6366F1` | Shared with accent-indigo. Informational tooltips, hints |

### 2.5 Colored Card Backgrounds

Some cards use a full-bleed accent-soft background instead of white. These are used sparingly
for visual rhythm — breaking up a long scroll of white cards.

| Card type | Background | Text color on it |
|---|---|---|
| Scheduled / stat highlight | `#FDE68A` (warm yellow) | `text-primary` |
| Creative / rose highlight | `#FBCFE8` (soft pink) | `text-primary` |
| Active / energy highlight | `#FDBA74` (soft orange) | `text-primary` |
| Insight / violet highlight | `#DDD6FE` (soft violet) | `text-primary` |
| Dark feature card | `#12121F` | `text-on-dark` |

**Rule:** No more than one colored card per visible viewport. Colored cards are punctuation,
not the paragraph.

---

## 3. Typography System

### 3.1 Font Stack

Use the system font stack for maximum performance and native feel:

```css
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
```

The references show a rounded, geometric sans-serif with friendly letterforms. If importing
a web font is possible, use **Inter** (body) and **Plus Jakarta Sans** (headings). If not,
the system stack provides an excellent approximation.

### 3.2 Type Scale

Every text element in the interface maps to exactly one of these roles. No ad-hoc sizes.

| Role | Tailwind | Size | Weight | Line height | Letter spacing | Usage |
|---|---|---|---|---|---|---|
| `display` | `text-4xl` | 36px | 800 (extrabold) | 1.1 | -0.02em | Book title on opening bookend. One instance per companion. |
| `heading-1` | `text-2xl` | 24px | 700 (bold) | 1.25 | -0.01em | Section titles ("Mind Map", "Key Principles", "Final Challenge"). |
| `heading-2` | `text-xl` | 20px | 600 (semibold) | 1.3 | -0.005em | Card titles, principle headlines, quiz section headers. |
| `heading-3` | `text-lg` | 18px | 600 (semibold) | 1.4 | 0 | Sub-headings within cards, step titles in the stepper. |
| `body` | `text-lg` | 18px | 400 (regular) | 1.65 | 0 | Primary reading text. All explanations, narratives, case studies. NEVER smaller than 18px for learning content. |
| `body-small` | `text-base` | 16px | 400 (regular) | 1.6 | 0 | Card meta-text, secondary descriptions, supporting context. |
| `caption` | `text-sm` | 14px | 500 (medium) | 1.5 | 0.01em | Labels, step counters ("Step 4 of 18"), metadata, timestamps. |
| `overline` | `text-xs` | 12px | 600 (semibold) | 1.5 | 0.05em | Eyebrow labels above headings (e.g., "METHOD 3", "CASE STUDY"). Always uppercase. |
| `stat-number` | `text-3xl` | 30px | 700 (bold) | 1.0 | -0.02em | Large stat numbers in dashboard-style cards (e.g., "67%", "5/7"). |
| `cta-label` | `text-base` | 16px | 600 (semibold) | 1.0 | 0.01em | Button text, chip labels, action labels. |

### 3.3 Typography Rules

- **Headings** use `text-primary` (#0D0F1A). Never gray for headings.
- **Body text** uses `text-primary` for main content, `text-secondary` for supporting.
- **Numbers and stats** are always `font-bold` or `font-extrabold`. Large numbers draw the eye
  and should feel confident — never regular weight.
- **Maximum line width** for body text: 65 characters (~640px at 18px). Beyond this, reading
  becomes fatiguing. Use `max-w-2xl` (672px) for text-heavy screens.
- **Paragraph spacing**: `mb-4` (16px) between paragraphs. `mb-8` (32px) before a new heading.
- **No underlines** except on actual links. Even links may use color+font-weight instead of underline.
- **Emoji** can be used sparingly in overline labels and section openers (e.g., "🧠 Schema Quiz",
  "🔮 Make a Prediction"). Maximum one emoji per heading. Never in body text.

---

## 4. Spacing System

Use Tailwind's 4px base grid exclusively. Every margin, padding, and gap must be a multiple of 4px.

### 4.1 Spacing Scale

| Token | Value | Typical use |
|---|---|---|
| `space-1` | 4px | Micro gaps: icon-to-label, inline badge padding |
| `space-2` | 8px | Tight internal gaps: between lines in a group, chip padding |
| `space-3` | 12px | Small component gaps: between radio options, list items |
| `space-4` | 16px | Standard gap: paragraph spacing, card grid gaps on mobile |
| `space-5` | 20px | Medium gap: between card sections, before sub-headings |
| `space-6` | 24px | Card internal padding (standard card). Grid gaps on desktop. |
| `space-8` | 32px | Large card internal padding. Between major sections. |
| `space-10` | 40px | Section breaks in stepper. Generous vertical breathing room. |
| `space-12` | 48px | Screen-level vertical padding (top/bottom of full screens). |
| `space-16` | 64px | Bookend screen vertical padding. Maximum breathing room. |

### 4.2 The Breathing Room Rule

The references consistently show more whitespace than most designers are comfortable with.
Follow this hierarchy:

- **Inside cards**: `p-6` (24px) minimum. `p-8` (32px) for primary reading cards.
- **Between cards**: `gap-4` (16px) on mobile. `gap-6` (24px) on desktop.
- **Between sections**: `py-10` (40px) minimum. `py-12` (48px) for major section transitions.
- **Screen edges**: `px-4` (16px) on mobile. `px-6` (24px) on tablet. Desktop content centered with `max-w-5xl`.

**When in doubt, add more space, not less.** The periwinkle canvas is your ally — it's not
wasted space, it's the room that lets the content breathe.

---

## 5. Border Radius System

The references are defined by their generous, pillowy border radius. This is non-negotiable —
it's the single strongest visual signature.

| Element | Tailwind | Pixels | Notes |
|---|---|---|---|
| Page-level container | `rounded-3xl` | 24px | The outermost visible frame (if used). Rarely needed since the canvas fills the viewport. |
| Primary cards | `rounded-2xl` | 16px | The standard card radius. ALL cards use this. No exceptions. |
| Nested cards / inner panels | `rounded-xl` | 12px | Cards inside cards, stat boxes, sub-sections within a card. |
| Buttons (primary CTA) | `rounded-full` | 9999px | Pill-shaped. Always. The primary button is a dark pill. |
| Chips / Tags / Pills | `rounded-full` | 9999px | Category chips, status pills, method labels. |
| Input fields | `rounded-xl` | 12px | Text inputs, text areas, search bars. |
| Avatars / Icons in circles | `rounded-full` | 9999px | Profile pictures, icon containers, step indicators. |
| Image containers | `rounded-xl` | 12px | Any image, illustration, or visual asset. |
| Tooltips / Popovers | `rounded-xl` | 12px | Floating panels, dropdowns. |
| Progress bars | `rounded-full` | 9999px | Both the track and the fill. |

**Critical rule:** Never use `rounded-md` (6px) or `rounded-lg` (8px) for any card or
container. Those values produce the "generic Bootstrap" look. This design system lives at
`rounded-xl` (12px) minimum, `rounded-2xl` (16px) standard.

---

## 6. Shadow and Elevation System

Shadows in the references are diffuse, cool-toned, and subtle. They create gentle lift
without hard edges. No drop shadows with visible offsets.

| Level | Tailwind | CSS equivalent | Usage |
|---|---|---|---|
| `elevation-0` | (none) | — | Flat elements: colored backgrounds, sunken inputs, inline elements. |
| `elevation-1` | `shadow-sm` | `0 1px 3px rgba(15, 15, 35, 0.06), 0 1px 2px rgba(15, 15, 35, 0.04)` | Subtle lift: chips, pills, small cards that don't need to dominate. |
| `elevation-2` | `shadow-md` | `0 4px 12px rgba(15, 15, 35, 0.07), 0 2px 4px rgba(15, 15, 35, 0.04)` | **Standard card elevation.** The default for all primary cards on the canvas. |
| `elevation-3` | `shadow-lg` | `0 8px 24px rgba(15, 15, 35, 0.10), 0 4px 8px rgba(15, 15, 35, 0.05)` | Elevated focus: the active card in a carousel, modal-like overlays, the mind map when expanded. |
| `elevation-4` | `shadow-xl` | `0 16px 40px rgba(15, 15, 35, 0.12), 0 8px 16px rgba(15, 15, 35, 0.06)` | Floating panels: popovers, tooltips, the expanded bookend card. Use sparingly. |

**Shadow color rule:** Shadows are always blue-tinted (#0F0F23 base), never pure black.
This matches the periwinkle canvas and makes the shadows feel integrated rather than harsh.

---

## 7. Component Library

### 7.1 Cards

The card is the fundamental building block. Every piece of content is housed in a card.

**Standard Card (white)**
```
Container: bg-white rounded-2xl shadow-md p-6 (mobile) / p-8 (desktop)
Title: heading-2, text-primary, mb-2
Subtitle: body-small, text-secondary, mb-4
Body: body, text-primary
```

**Colored Card (accent background)**
```
Container: bg-[accent-soft] rounded-2xl p-6 shadow-none (the color IS the elevation)
Title: heading-2, text-primary
Body: body-small, text-primary
Icon: 40px circle with accent-full background and white icon inside
```

**Dark Card**
```
Container: bg-[surface-dark] rounded-2xl p-6 shadow-md
Title: heading-2, text-on-dark
Body: body-small, text-on-dark-secondary
CTA: White pill button (inverted primary CTA)
```

**Stat Card**
```
Container: bg-white (or accent-soft) rounded-2xl p-6 shadow-md
Number: stat-number, text-primary
Label: caption, text-secondary, mt-1
Optional icon: 32px circle, top-right or left of number
Optional badge: Small pill with +/- percentage
```

### 7.2 Buttons

**Primary CTA (the main action)**
```
Shape: px-8 py-3 rounded-full
Background: bg-[#12121F] (surface-dark)
Text: text-white font-semibold text-base
Hover: bg-[#2A2A40] (lighten slightly)
Active: scale-[0.97] (subtle press)
Disabled: opacity-40, pointer-events-none
Min-width: 160px on desktop, full-width on mobile stepper screens
```

On dark backgrounds, invert: `bg-white text-[#12121F]`.

**Secondary CTA**
```
Shape: px-6 py-2.5 rounded-full
Background: bg-[surface-sunken] (#F1F3FB)
Text: text-primary font-semibold text-sm
Border: 1px solid #E5E7EB
Hover: bg-[#E8EAF0]
```

**Ghost / Text button**
```
No background, no border
Text: text-[accent-indigo] font-semibold text-sm
Hover: underline or bg-[accent-indigo]/5 rounded-lg px-3 py-1.5
Used for: "Skip", "Show hint", "Learn more"
```

**Icon button**
```
Shape: w-10 h-10 rounded-full flex items-center justify-center
Background: bg-[surface-sunken]
Icon: 20px, text-secondary
Hover: bg-[#E0E2EA], icon becomes text-primary
Used for: Back arrows, close, settings, overflow menus
```

### 7.3 Chips and Pills

**Category chip (e.g., "Logic", "Visual", "Focus")**
```
Shape: px-4 py-2 rounded-full flex items-center gap-2
Default: bg-white border border-gray-200 text-sm font-medium text-secondary
Active: bg-[surface-dark] text-white border-transparent
Icon: 16px icon left of label
```

**Status pill**
```
Shape: px-3 py-1 rounded-full inline-flex items-center gap-1.5
Variants:
  success: bg-[accent-emerald-soft] text-[accent-emerald-deep]
  warning: bg-[accent-amber-soft] text-[accent-amber-deep]
  error:   bg-red-50 text-red-700
  info:    bg-[accent-indigo-soft] text-[accent-indigo-deep]
  neutral: bg-gray-100 text-gray-600
Font: text-xs font-semibold
Optional: 6px dot circle before text
```

**Method label (overline chip)**
```
Shape: px-3 py-1 rounded-full
Background: The accent-soft of the relevant method's color
Text: text-xs font-bold uppercase tracking-wider, accent-deep color
Example: "RETRIEVAL PRACTICE" in indigo on indigo-soft background
```

### 7.4 Progress Indicators

**Linear progress bar (global progress)**
```
Track: h-1.5 w-full bg-gray-200 rounded-full (fixed to top of viewport)
Fill: h-full bg-[accent-amber] rounded-full transition-all duration-500
```

**Circular progress (completion percentage)**
```
Size: 48px (small) / 64px (medium) / 96px (large)
Track: stroke-[#E5E7EB] stroke-width-3
Fill: stroke-[accent-amber] stroke-width-3 stroke-linecap-round
Center: stat-number with percentage
Animation: Stroke-dashoffset transition, 800ms ease-out
```

**Step indicator (dot-based)**
```
Track: flex gap-2 items-center
Completed dot: w-2 h-2 rounded-full bg-[accent-indigo]
Current dot: w-3 h-3 rounded-full bg-[accent-indigo] ring-4 ring-[accent-indigo]/20
Future dot: w-2 h-2 rounded-full bg-gray-300
```

**Step counter text**
```
Format: "Step {current} of {total}"
Style: caption, text-secondary
Position: Above or below the progress bar, centered
```

### 7.5 Quiz and Interaction Elements

**Multiple-choice option (unselected)**
```
Container: w-full p-4 rounded-xl border-2 border-gray-200 bg-white cursor-pointer
  hover: border-[accent-indigo]/40 bg-[accent-indigo-soft]
Text: body-small, text-primary
Leading element: w-6 h-6 rounded-full border-2 border-gray-300 (empty radio circle)
```

**Multiple-choice option (selected, pre-submit)**
```
Container: border-[accent-indigo] bg-[accent-indigo-soft]
Radio: bg-[accent-indigo] with white inner dot (checked state)
Text: font-medium
```

**Multiple-choice option (correct, post-submit)**
```
Container: border-[accent-emerald] bg-[accent-emerald-soft]
Icon: Check circle in accent-emerald
Text: font-medium text-[accent-emerald-deep]
```

**Multiple-choice option (incorrect, post-submit)**
```
Container: border-red-300 bg-red-50
Icon: X circle in red-500
Text: text-red-700
Fade: opacity-70 after 2s (de-emphasize the wrong answer, guide eye to correct)
```

**Text input (prediction, free response)**
```
Container: w-full p-4 rounded-xl bg-[surface-sunken] border-2 border-transparent
  focus: border-[accent-indigo] bg-white ring-4 ring-[accent-indigo]/10
Placeholder: text-tertiary italic
Text: body, text-primary
Min-height: 80px for multi-line (textarea), single line for short answers
```

**Fill-in-the-blank slot**
```
Inline: border-b-2 border-dashed border-[accent-indigo] px-1 min-w-[80px]
  filled: border-solid bg-[accent-indigo-soft] rounded-md px-2 py-0.5
Text: font-medium text-[accent-indigo-deep] when filled
```

### 7.6 Mind Map Nodes

**Level 1 (Thesis) — center node**
```
Container: bg-[surface-dark] rounded-2xl px-6 py-4 shadow-lg
Text: heading-2, text-on-dark, text-center, max-w-xs
Ring: 3px solid [accent-violet] (outer glow effect)
```

**Level 2 (Causal chain) — primary nodes**
```
Container: bg-white rounded-xl px-5 py-3 shadow-md border-2 border-[accent-violet]/20
Text: heading-3, text-primary
Connector line: 2px stroke, [accent-violet]/40, with subtle curve (SVG path)
Click affordance: Small expand icon (ChevronDown) in top-right, text-tertiary
```

**Level 3 (Details) — leaf nodes**
```
Container: bg-[accent-violet-soft] rounded-lg px-4 py-2.5 shadow-sm
Text: body-small, text-primary
Connector line: 1.5px stroke, [accent-violet]/25, straight or gentle curve
```

### 7.7 Flashcard

**Front (question visible)**
```
Container: bg-white rounded-2xl shadow-lg p-8 min-h-[240px] flex flex-col justify-between
Top: overline chip with method label (e.g., "RETRIEVAL PRACTICE")
Center: heading-2, text-primary, text-center
Bottom: Ghost button "Reveal Answer →"
```

**Back (answer revealed)**
```
Container: bg-[accent-indigo-soft] rounded-2xl shadow-lg p-8 min-h-[240px]
Top: Same overline chip
Center: body, text-primary
Bottom: "Got it" (success pill) / "Need review" (warning pill) self-assessment
Transition: 3D Y-axis flip (rotateY 180deg) over 400ms, or a simple crossfade
```

### 7.8 Navigation / Bottom Bar (if applicable)

**Tab bar (mobile, fixed bottom)**
```
Container: bg-white border-t border-gray-100 px-4 py-2 flex justify-around
Tab item: flex flex-col items-center gap-1
  Icon: 24px
  Label: text-xs font-medium
  Default: text-secondary
  Active: text-[accent-indigo], icon filled instead of outlined
Active indicator: 4px dot below the icon, bg-[accent-indigo], rounded-full
```

---

## 8. Layout System

### 8.1 The Bento Grid (Dashboard/Overview Screens)

The references heavily use a bento-grid layout on desktop — asymmetric cards of varying sizes
arranged in a visually balanced grid. This applies to the mind map overview and the companion
dashboard (if showing multiple sections at once).

```
Desktop grid: grid grid-cols-12 gap-6
  Full-width card: col-span-12
  Two-thirds card: col-span-8
  One-third card: col-span-4
  Half card: col-span-6
  Small card: col-span-4 or col-span-3

Mobile: All cards become col-span-12 (stacked, full width)
Tablet (md): Use col-span-6 for half-cards, col-span-12 for others
```

**Bento rhythm rule:** Never place two cards of identical size adjacent to each other.
Alternate between wider and narrower cards to create visual rhythm. If you have three
equal-importance items, use a 5-4-3 or 8-4 split, not 4-4-4.

### 8.2 The Stepper Layout (Sequential Learning Screens)

The stepper is the primary learning mode — one concept at a time.

```
Container: min-h-screen bg-[canvas] flex flex-col
Header: Fixed top bar with progress bar + step counter
Content: flex-1 flex items-center justify-center px-4
  Inner: max-w-2xl w-full
Footer: Fixed bottom with primary CTA + optional back button
  Layout: flex justify-between items-center px-6 py-4
  Background: bg-white/80 backdrop-blur-md border-t border-gray-100
```

### 8.3 The Bookend Layout (Opening and Closing Screens)

```
Container: min-h-screen bg-[surface-dark] flex flex-col items-center justify-center px-6
Content: max-w-xl text-center
Title: display, text-on-dark, mb-6
Body: body (or heading-3), text-on-dark-secondary, mb-8
CTA: Primary button (inverted — white pill on dark)
Decorative: Optional subtle radial gradient or abstract shape in background
  (e.g., a soft indigo glow behind the text, like the AI assistant orb in the references)
```

### 8.4 The Card Carousel Layout (Principle Cards, Flashcards)

```
Container: overflow-x-auto snap-x snap-mandatory scrollbar-hide
  flex gap-4 px-4 (mobile) / flex gap-6 justify-center (desktop, if ≤4 cards)
Card: snap-center shrink-0 w-[85vw] max-w-sm (mobile) / w-80 (desktop)
Indicators: Dot indicators below, centered, using step indicator dot style
Navigation: Left/right arrows on desktop (icon buttons), swipe on mobile
```

---

## 9. Iconography

### 9.1 Icon Style

Use **Lucide React** icons exclusively. The references show outlined icons (not filled) with
a consistent 1.5px stroke weight and rounded caps/joins. Lucide matches this exactly.

### 9.2 Icon Sizing

| Context | Size | Tailwind |
|---|---|---|
| Inline with text | 16px | `w-4 h-4` |
| Inside buttons | 18px | `w-[18px] h-[18px]` |
| Card leading icon (small) | 20px | `w-5 h-5` |
| Card leading icon (standard) | 24px | `w-6 h-6` |
| Feature icon (in circle) | 24px icon in 48px circle | `w-6 h-6` in `w-12 h-12 rounded-full` |
| Hero icon | 32px icon in 64px circle | `w-8 h-8` in `w-16 h-16 rounded-full` |

### 9.3 Icon Containers

Icons often sit inside colored circles in the references. The pattern:

```
Container: w-12 h-12 rounded-full bg-[accent-soft] flex items-center justify-center
Icon: w-6 h-6 text-[accent-full]
```

For dark backgrounds:
```
Container: w-12 h-12 rounded-full bg-white/10 flex items-center justify-center
Icon: w-6 h-6 text-white
```

### 9.4 Suggested Icons Per Method

| Method | Icon (Lucide name) | Accent |
|---|---|---|
| Macrostructure (mind map) | `Network` or `GitBranch` | violet |
| Principle cards | `Lightbulb` | violet |
| Dual coding (visuals) | `Eye` or `Image` | rose |
| Cognitive load (stepper) | `Footprints` or `ArrowRight` | neutral |
| CAC bridge (case studies) | `Route` or `Puzzle` | rose |
| Schema activation (quiz) | `Brain` or `Sparkles` | indigo |
| Retrieval practice | `RotateCcw` or `CheckCircle` | indigo |
| Generation effect | `Wand2` or `MessageCircle` | amber |
| Bookends | `BookOpen` or `Award` | dark/white |
| Narrative timeline | `Clock` or `MapPin` | emerald |

---

## 10. Data Visualization

### 10.1 Chart Colors

Charts use the accent palette in this priority order:
1. `accent-indigo` (#6366F1) — primary data series
2. `accent-amber` (#F59E0B) — secondary data series
3. `accent-rose` (#EC4899) — tertiary
4. `accent-emerald` (#10B981) — quaternary
5. `accent-violet` (#8B5CF6) — fifth series (rarely needed)

### 10.2 Chart Styles (from references)

**Bar charts:**
- Bars: rounded-top (`rx: 6`), solid fill with primary accent
- Width: 60% of available space (generous gaps between bars)
- Background grid: Horizontal lines only, `stroke: #E5E7EB`, `stroke-dasharray: 4 4`
- Labels: caption style, text-secondary

**Donut charts:**
- Stroke-width: 24px (thick, substantial ring)
- Gap between segments: 3px (white gaps)
- Center: Large stat number + small caption label
- Legend: Below or right, using dot + label format

**Line charts (heart rate style):**
- Line: 2px stroke, accent color, rounded joins
- Dots: Hidden by default, shown on hover (6px circle)
- Area fill: Gradient from accent/10 at top to transparent at bottom
- Contrast elements: Red vertical bars for anomaly markers

### 10.3 Mind Map Visualization

The mind map is the most complex visual element. Build it as positioned HTML divs with
CSS/SVG connector lines, NOT as a pure SVG diagram.

```
Layout: Relative container, nodes positioned with CSS
Connectors: SVG overlay with path elements using cubic bezier curves
  Stroke: 2px, accent-violet/30
  No arrowheads (the hierarchy implies direction)
Animation: Nodes fade in sequentially (stagger 100ms) when expanded
Interaction: Click node to expand/collapse children
  Expanded: Children slide in from parent position, opacity 0→1, 300ms
  Collapsed: Children slide back and fade out, 200ms
```

---

## 11. Motion and Animation

### 11.1 Timing

| Transition type | Duration | Easing | Example |
|---|---|---|---|
| Micro-interaction | 150ms | ease-out | Button press, hover color change, chip select |
| Element entrance | 250ms | ease-out | Card fade-in, step change, answer reveal |
| Layout change | 350ms | ease-in-out | Expand/collapse, mind map node growth |
| Page transition | 400ms | ease-in-out | Stepper step change (combined fade out + fade in) |
| Emphasis | 600ms | spring (CSS: cubic-bezier(0.34, 1.56, 0.64, 1)) | Correct answer bounce, completion celebration |
| Chart/data | 800ms | ease-out | Progress bar fill, donut chart draw-in, stat number count-up |

### 11.2 Entrance Animations (React)

```jsx
// Standard card entrance
className="animate-in fade-in slide-in-from-bottom-4 duration-300"

// Staggered list items (use inline style for stagger delay)
style={{ animationDelay: `${index * 80}ms` }}

// For React: use state-driven opacity and transform
const [visible, setVisible] = useState(false);
useEffect(() => { setVisible(true); }, []);

<div className={`transition-all duration-300 ${visible ? 'opacity-100 translate-y-0' : 'opacity-0 translate-y-4'}`}>
```

### 11.3 Reduced Motion

```jsx
const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

// Apply: skip all transform animations, keep opacity fades (shorter: 100ms)
// Never skip: color changes, layout updates (these are instant anyway)
```

---

## 12. Interaction States

Every interactive element has five states. Define all five.

| State | Visual treatment |
|---|---|
| **Default** | Base styling as defined in component spec |
| **Hover** | Background lightens or darkens by one step. Border may appear or intensify. Cursor: pointer. Transition: 150ms. |
| **Focused** | Ring: `ring-2 ring-[accent-indigo] ring-offset-2`. Visible on keyboard navigation. |
| **Active/Pressed** | Scale: `scale-[0.97]` for buttons. Background deepens to accent-deep for colored elements. |
| **Disabled** | `opacity-40 pointer-events-none cursor-not-allowed`. No hover/focus styles apply. |

**Specific state examples:**

Quiz option hover: `border-[accent-indigo]/40 bg-[accent-indigo-soft]`
Card hover (when clickable): `shadow-lg translate-y-[-2px]` (subtle lift)
CTA hover: Background shifts from `#12121F` to `#2A2A40`
Ghost button hover: `bg-[accent-indigo]/5`

---

## 13. Responsive Behavior

### 13.1 Breakpoints

| Name | Min-width | Tailwind prefix | Key adaptations |
|---|---|---|---|
| Mobile | 0px | (default) | Single column. Full-width cards. Bottom CTA bar. 16px edge padding. |
| Tablet | 768px | `md:` | Two-column where appropriate. Side-by-side flashcards. 24px edge padding. |
| Desktop | 1024px | `lg:` | Bento grid for overview. Centered content (max-w-5xl). 32px edge padding or auto margins. |
| Wide | 1280px | `xl:` | Content remains max-w-5xl centered. Extra canvas visible on sides. No content stretching. |

### 13.2 Mobile-Specific Rules

- All touch targets: minimum 44×44px (following Apple HIG and Material 3).
- Quiz options: Full-width tap area, not just the radio circle.
- Cards: Full-width with 16px horizontal margin (`mx-4`).
- CTA buttons: Full-width (`w-full`) in the stepper footer.
- Flashcard carousel: Single card visible, swipe to navigate.
- Mind map: Horizontally scrollable with pinch-to-zoom if possible, or simplified to a
  collapsible list on very small screens.
- Bottom safe area: `pb-safe` (env(safe-area-inset-bottom)) on iOS for the CTA bar.

### 13.3 Desktop-Specific Rules

- Content never stretches beyond `max-w-5xl` (1024px).
- The periwinkle canvas is always visible on the sides — content floats in the center.
- Flashcard carousels show 2–3 cards simultaneously.
- Mind map has room to expand fully without scrolling.
- CTAs return to their natural width (160–200px), right-aligned in footer.

---

## 14. Accessibility

### 14.1 Color Contrast

| Text/Background combination | Minimum ratio | WCAG level |
|---|---|---|
| `text-primary` on `surface-primary` | 15.2:1 | AAA |
| `text-primary` on `canvas` | 12.8:1 | AAA |
| `text-secondary` on `surface-primary` | 4.6:1 | AA |
| `text-on-dark` on `surface-dark` | 16.1:1 | AAA |
| `accent-indigo` on `accent-indigo-soft` | 4.8:1 | AA |
| `accent-emerald-deep` on `accent-emerald-soft` | 5.1:1 | AA |
| White on `accent-indigo` | 4.6:1 | AA |

If any accent text on accent-soft background falls below 4.5:1, use the accent-deep variant.

### 14.2 Non-Color Indicators

- Correct answers: Green color + checkmark icon + "Correct!" text label.
- Incorrect answers: Red color + X icon + "Not quite" text label.
- Current step: Larger dot + ring + screen reader "Current step" aria-label.
- Selected option: Color change + filled radio + bold text weight.
- Progress: Color bar + percentage text + step counter text.

### 14.3 Keyboard Navigation

- Tab order follows visual layout (top-to-bottom, left-to-right).
- All cards with click handlers have `tabIndex={0}` and `onKeyDown` for Enter/Space.
- Quiz options navigable with arrow keys within the group (`role="radiogroup"`).
- Escape key closes any expanded element (mind map node, flashcard back, hints).
- Focus ring: `ring-2 ring-[accent-indigo] ring-offset-2 ring-offset-white`.
  On dark backgrounds: `ring-offset-[surface-dark]`.

### 14.4 Screen Reader Considerations

- Progress bar: `role="progressbar" aria-valuenow={current} aria-valuemin={0} aria-valuemax={total}`.
- Quiz: `role="radiogroup"` with `aria-label="Question: [text]"`.
- Flashcard: `aria-live="polite"` on the answer region so it's announced on reveal.
- Step transitions: `aria-live="polite"` on the main content area.
- Mind map: Semantic tree structure with `role="tree"` and `role="treeitem"`.

---

## 15. Illustration and Decorative Elements

### 15.1 Abstract Background Elements

The references feature subtle decorative elements on feature screens:

- **AI/insight orb:** A soft, semi-transparent abstract mesh or gradient orb behind key
  content. Implement as a radial gradient: `radial-gradient(ellipse at center, [accent-violet]/8 0%, transparent 70%)`.
  Size: 300–400px. Position: centered behind the primary heading or visual.

- **Dot grid:** Faint dot pattern on bookend screens. `radial-gradient(circle, #FFFFFF15 1px, transparent 1px)` with `background-size: 20px 20px`.

- **Gradient accents:** Subtle linear gradients in card backgrounds for special sections.
  Never a full rainbow — use two adjacent accent colors. Example: `linear-gradient(135deg, [accent-indigo-soft], [accent-violet-soft])`.

### 15.2 What NOT to Include

- No 3D character illustrations (those in the references are product-specific assets).
- No photographs or stock imagery.
- No complex SVG illustrations.
- No animated background effects that distract from learning content.
- No gradients that reduce text legibility.

The companion's visual richness comes from the color-coded interaction system, the generous
spacing, and the card-based architecture — not from decorative illustration.

---

## 16. Dark Mode Considerations

The companion does NOT ship with a dark mode toggle. The periwinkle canvas and white cards
are the brand. However, the bookend screens (opening and closing) use a dark palette, which
provides visual contrast and signals "this is special."

If dark mode is explicitly requested by the user in the future, the mapping would be:

| Light token | Dark equivalent |
|---|---|
| `canvas` #E0E4F7 | `#0F0F1A` |
| `surface-primary` #FFFFFF | `#1A1A2E` |
| `surface-raised` #F8F9FE | `#22223A` |
| `surface-sunken` #F1F3FB | `#14142A` |
| `text-primary` #0D0F1A | `#E8E9F0` |
| `text-secondary` #6B7280 | `#8B8D9A` |
| All accent-full values | Same (unchanged — accents are designed to work on both) |
| All accent-soft values | Reduce opacity to /10 instead of explicit light colors |

---

## 17. Anti-Patterns — What to Avoid

These are the things that will make the companion look generic or broken. Avoid at all costs.

1. **Pure white (#FFFFFF) full-page background.** Always use the periwinkle canvas.
2. **Sharp corners on cards.** Never below `rounded-xl` (12px) for any container.
3. **Hard black shadows.** Shadows are always cool-tinted and diffuse.
4. **Competing accent colors on one screen.** One accent dominates per screen/section.
5. **Dense paragraph blocks without spacing.** Max 3 sentences per visual paragraph.
6. **Borders instead of shadows for card elevation.** Cards float with shadow, not outline.
7. **Default browser form elements.** Every input, radio, and checkbox is custom-styled.
8. **Small text for body content.** Never below 18px for learning content.
9. **Generic gray buttons.** CTAs are always the dark pill or a colored accent button.
10. **Centered body text.** Body text is always left-aligned. Only headings and bookend
    display text may be centered.
11. **More than 4 colors visible simultaneously.** The canvas + one or two accents + text
    colors. That's it. If you see a rainbow, you've gone wrong.
12. **Stacking multiple cards with the same visual weight.** Vary card sizes, colors, and
    content types to create rhythm.
