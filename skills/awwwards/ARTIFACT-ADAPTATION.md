# Read this first: adapting awwwards technique to a single-file artifact

The vendored awwwards skill is written for full web projects (Next.js, Vite, npm packages,
CDNs). The Interactive Book Companion ships as **one self-contained artifact** — a single React
or HTML file rendered in a locked-down sandbox. A strict Content-Security-Policy blocks every
external request: no CDN scripts, no external stylesheets or fonts, no remote images, no
`fetch`/XHR/WebSocket. There is no build step and no `npm install`.

So take the awwwards files for their **principles and their exact numbers** (easing curves,
clamp scales, tracking, timing, color math). Do **not** copy their `import`/CDN lines. Anything
that needs an external package will silently fail to load and leave you with a blank or broken
companion. That is the single biggest pitfall here.

## The rule

- **Every visual, every animation, every asset is inline and dependency-free.**
- Allowed: plain CSS (including modern CSS), inline `<style>`, vanilla JS,
  `requestAnimationFrame`, `IntersectionObserver`, inline SVG, `<canvas>` 2D, emoji, CSS
  gradients, data-URI assets.
- In a Claude **React** artifact you may also use the libraries the runtime already provides
  (`recharts`, `lucide-react`, and usually `framer-motion`). Do not add any other package.
- In the **universal HTML** build: vanilla JS only. No libraries at all.

## Technique-by-technique

| awwwards technique | In a single artifact | How |
|---|---|---|
| GSAP + ScrollTrigger | **Do not use** | CSS transitions/keyframes + `IntersectionObserver` (reveal-on-view) + `requestAnimationFrame`. Keep the easing curves and durations exactly. |
| Lenis / smooth scroll lib | **Do not use** | `scroll-behavior: smooth` in CSS, or nothing. Do not fake momentum with JS. |
| CSS scroll-driven animations (`animation-timeline: scroll()/view()`) | **Use freely** | This is the dependency-free replacement for ScrollTrigger. No library needed. Provide a static fallback. |
| Three.js / R3F / OGL / Spline / WebGL / shaders / post-processing | **Do not use** | Skip real 3D. For ambiance use CSS gradients, an animated `<canvas>` 2D field, or inline SVG. A companion never needs WebGL. |
| Framer Motion / Anime.js | **HTML: no.** React: only if the runtime already bundles it | Otherwise CSS + `requestAnimationFrame`. Never load a second animation lib. |
| GSAP SplitText / SplitType | **Do not use** | Split the text yourself: wrap words/lines in `<span>`s in code and stagger their transition-delay. |
| Barba.js / multi-page transitions | **N/A** | It is one page. Swap views with state + a CSS fade/slide. |
| View Transitions API | Optional, in-page only | Fine for same-document view swaps in supporting browsers, but always ship a plain CSS fallback. Never rely on it. |
| Next.js / Astro / SvelteKit / Vite | **N/A** | No framework, no build. One file, one default export (React) or one HTML document. |
| `@font-face` / Google Fonts / font CDN | **Do not link** | Use the system font stack. A web font only if inlined as a data URI, which is usually not worth the weight. Never link a font URL that can be blocked. |
| External / stock images | **Do not use** | Inline SVG, emoji, CSS. No remote image URLs. |
| `localStorage` / `sessionStorage` / cookies | **Do not use** | In-memory state only (React state or JS variables). |
| `fetch` / API calls / analytics | **Do not use** | Everything the companion needs is already in the file. |
| Custom cursor, hover, micro-interactions, loaders, counters | **Use freely** | All pure CSS + vanilla JS. Gate behind `prefers-reduced-motion`. Disable cursor effects on touch. |
| Fluid type, `clamp()`, tracking, `oklch()`, `:has()`, container queries, subgrid, bento grids | **Use freely** | All native CSS. This is where most of the award-level craft lives, and it costs nothing. |

## Pitfall checklist (verify before shipping)

- [ ] No `import` from any package except (React artifact) `react`, `recharts`, `lucide-react`,
      and `framer-motion` if present. No `<script src=...>`, no `<link href=...>` to any host.
- [ ] No `@font-face`/font URL, no remote image `src`, no `background: url(http...)`.
- [ ] No `fetch`, `XMLHttpRequest`, WebSocket, `localStorage`, `sessionStorage`.
- [ ] No GSAP, Lenis, Three.js, Spline, OGL, Anime.js, Barba, SplitText, or any WebGL.
- [ ] All animation is CSS + `requestAnimationFrame`; only `transform`/`opacity` (and SVG
      `stroke-*`) are animated in loops; 60fps; everything degrades under `prefers-reduced-motion`.
- [ ] Any View Transition or scroll-driven animation has a working non-supporting fallback.
- [ ] The file renders and runs with zero console errors offline (no network needed).

If any box is unchecked, the companion will error or render blank in the sandbox. Fix it before
it reaches the QA pass in `../interactive-book-companion/references/qa-checklist.md`.
