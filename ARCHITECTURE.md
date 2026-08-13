---
name: uExel Landing Page
description: How uexel-landing.html is built — structure, styling system, interactive behaviors, assets, and known gaps.
---

# uExel Landing Page — Build Documentation

This documents `uexel-landing.html`: a single self-contained HTML file (~3,540 lines) with no build step, no framework, and no bundler. Everything — markup, styles, and behavior — lives in one file: a `<style>` block in `<head>`, the page markup in `<body>`, and a `<script>` block at the end of `<body>`. Open it directly in a browser; nothing needs to be compiled.

Companion files in the project root: `DESIGN.md` holds the design tokens (colors, type scale, spacing, radii) as structured data mirroring the CSS custom properties below; `PRODUCT.md` holds product/positioning copy this page's content is drawn from.

## 1. Document anatomy

| Range | Content |
|---|---|
| `1–12` | `<head>` — meta tags, title, Google Fonts preconnect + stylesheet link |
| `13–2180` | `<style>` — all CSS (custom properties, base styles, one block per section) |
| `2183–3018` | `<body>` markup — cursor layer, header, and all page sections in order |
| `3019–3538` | `<script>` — vanilla JS behaviors, each scoped in its own IIFE |

There is no CSS or JS in separate files; everything is inline, so the page has exactly one network request per asset (fonts, images) and no dependency resolution step.

## 2. Dependencies

All loaded directly via `<link>`/`<img src>` — no npm, no package.json:

- **Google Fonts** (`uexel-landing.html:7-12`): `Abel` (display/heading font) and `Inter` weights 400–800 (body/UI font), loaded via `fonts.googleapis.com`.
- **devicon icons via jsdelivr CDN** (`uexel-landing.html:2826-2845`): the "Our Tech Stack" marquee pulls React/Node/Python/AWS/Azure/Docker/Kubernetes/Postgres/MongoDB/GraphQL SVGs from `cdn.jsdelivr.net/npm/devicon@latest/...`. Pinned to `@latest`, not a version — icons can change or break without any change to this file.
- **A hotlinked sprite from an unrelated third-party site** (`uexel-landing.html:1434`): `.process-step-icon` in the "Our Process" accordion loads its background sprite from `https://www.dynamologic.com/wp-content/themes/dynamologic2021/images/sprite.png` — someone else's WordPress theme asset, not something uExel owns or controls. This is fragile (it can 404 or change at any time) and should be replaced with a locally-hosted sprite/SVG before this ships to production.
- **Local images**: `Hero-bg.jpg` (hero background photo), `uexel-logo.png` (header + footer logo), and `logos/*.png|webp` (client logos in the marquee, plus PSEB/SECP/D&B/PASHA accreditation badges in "Why Choose").

No JS libraries are used anywhere — the particle system, scroll-pinning, accordion, carousel, and custom cursor are all hand-rolled vanilla JS against the DOM/Canvas/rAF APIs.

## 3. CSS architecture

### Design tokens
`:root` (`uexel-landing.html:14-32`) defines the entire palette, a shared border radius, and the content max-width as CSS custom properties (`--ink`, `--navy`, `--blue`, `--blue-btn`, `--offwhite`, `--line`, `--radius`, `--maxw: 1280px`, etc.). Every section reuses these rather than hardcoding colors, so a rebrand mostly means editing this block. These same values are mirrored (with friendlier names) in `DESIGN.md`.

### Base + utilities
- `.wrap` — the shared content container (`max-width: var(--maxw)`, horizontal padding), used inside every `<section>`.
- `.eyebrow`, `.display`, heading resets, `.sr-only` (visually-hidden but screen-reader-visible text), and the three button variants `.btn-primary` / `.btn-ghost` / `.btn-outline`.
- Section background helpers: `.section-dark`, `.section-blue-tint`, `.section-offwhite`.

### One block per section
CSS is organized under large banner comments matching each visual section, in page order: `HEADER`, `HERO`, `TRUSTED BY / CLIENTS`, `WE WORK WITH`, `FEATURED WORK`, `EXPERTISE — pinned horizontal scroll`, `OUR PROCESS`, `MARQUEE`, `WHY CHOOSE`, `CTA BANNER`, `FOOTER`, `CUSTOM CURSOR`, `REDUCED MOTION`, `FOCUS-VISIBLE`. Grep `===== .* =====` in the file to jump between them.

### Responsive breakpoints
Four `max-width` breakpoints, applied top-down (not mobile-first):

| Breakpoint | What changes |
|---|---|
| `980px` (`:1929`) | Top nav hides in favor of the burger menu; hero, flip-card grid, process grid, and featured-work row all collapse from multi-column to single-column/stacked layouts. |
| `900px` (`:1744`) | "Why Choose" switches from its two-column sticky-rail layout to a single stacked column. |
| `768px` (`:522`, `:1601`, `:2034`) | Clients marquee and tech-stack marquee stack their lede above the scrolling row; the pinned horizontal-scroll "Expertise" section drops the scroll-pin entirely and becomes a plain vertical stack (see §5). |
| `560px` (`:2004`) | Tighter section padding and hero spacing for small phones. |

Beyond fixed breakpoints, most type and spacing uses `clamp()` (e.g. hero `h1` at `clamp(40px, 9vw, 80px)`, `:337`) so sizes scale continuously with viewport width between breakpoints rather than jumping.

### Accessibility affordances baked into the CSS
- `prefers-reduced-motion: reduce` (`:2139-2166`) pauses every indefinite decorative animation (marquees, hero orbs/grid/shimmer, cursor pulse, CTA particles, process-icon micro-animations) via `animation-play-state: paused` rather than `animation: none` — several of those elements are positioned purely by their own keyframes, so removing the animation outright would snap them to an undefined resting position. The hero particle-text canvas has its own separate `matchMedia` check in JS (§4.7) rather than living in this block.
- `:focus-visible` (`:2168-2179`) gives a branded blue outline to links, buttons, and the two custom interactive elements (`.flip-card`, `.work-row`) that are operated via `tabindex`/`role="button"` rather than native form controls.
- Custom cursor (§4.1) is purely a visual layer on top of the OS cursor logic — `cursor: none` is scoped only to interactive targets, and reduced-motion still leaves the cursor itself visible, just without the pulsing ring animation.

## 4. Interactive behavior (script, `uexel-landing.html:3019-3538`)

The script is seven independent IIFEs/functions, executed top-to-bottom on page load — no framework, no event delegation library, just direct `addEventListener` calls.

### 4.1 Custom cursor (`:3021-3039`)
Tracks `mousemove`, lerps a tracked position toward the real cursor position each `requestAnimationFrame` tick (`curX += (mouseX - curX) * 0.18`), and toggles a `.visible` class (plus a "Click Me" label) whenever the hovered element matches `a, button, [role="button"], .flip-card, .work-row`. The native cursor is hidden (`cursor: none`) only on those same targets.

### 4.2 Mobile menu (`:3042-3053`)
Burger button toggles `.open` on `#mobileMenu`; any link tap inside the menu closes it again.

### 4.3 Flip cards — "We Work With" (`:3057-3077`)
Exactly one of the two flip cards (`Startups` / `Enterprises`) is active (flipped open) at a time. Clicking the already-active card flips forward to the next sibling instead of closing to nothing, so there's always exactly one face showing. Also wired for `Enter`/`Space` keyboard activation.

### 4.4 Featured work rows — "Case Studies" (`:3081-3115`)
Each `.work-item` row expands into an image panel on click/tap (toggling `.active` + `aria-expanded`), and each expanded panel has its own tiny prev/next slide carousel (`.work-slides`), independent per item, with nav-button clicks stopped from bubbling to the row toggle.

### 4.5 Expertise — pinned horizontal scroll (`:3119-3229`)
The most involved piece of JS on the page. `.expertise-pin` is a tall (`220vh`) wrapper containing a `position: sticky` inner section; as the user scrolls through that tall wrapper, JS computes a 0–1 "scroll progress" (`targetProgress`, based on how far `.expertise-pin`'s top has scrolled past the viewport) and uses it to translate `.expertise-cards` horizontally while fading out the background "Builds Digital Products" text. Progress is **eased** each animation frame (`currentProgress += (target - currentProgress) * 0.12`) rather than snapped directly to scroll position, so trackpad/wheel steps read as a smooth glide instead of jumps. Card geometry (start/end translateX) is computed once via `computeMotion()` and cached, recomputed only on resize — never inside the scroll loop. Below `768px` this entire mechanism is disabled and the section becomes a plain flex column (CSS handles that fallback layout; JS just clears the inline transform/opacity it had set).

### 4.6 Our Process — accordion + ring (`:3233-3314`)
Clicking a step header (`Discovery` → `Planning` → ... → `Launch & Support`) calls `setActive(index)`, which simultaneously:
- Toggles `.active` on the clicked step and marks all prior ring dots `.done`.
- Animates the circular SVG progress ring by setting `stroke-dashoffset` on `.ring-progress` as a fraction of its circumference (`CIRCUMFERENCE = 565.5`).
- Swaps which of the six `.pf-icon` SVG illustrations is visible in the ring's center.
- Cross-fades the slogan text below the ring (`.is-swapping` class, text swapped mid-transition via `setTimeout`).
- Sends a "comet" element traveling around the ring's CSS `offset-path` to the newly-lit dot, plus a one-shot ping burst at that dot (both skipped on the initial render via `{ animate: false }`, so only real interactions move — not first paint).

### 4.7 Hero particle text (`:3317-3538`, invoked via `initHeroParticles()`)
Canvas-based particle text effect in the hero: ~2,600 particles assemble into each word in `["IMPACT.", "GROWTH.", "VALUE.", "REALITY."]` in turn, then scatter into a random ellipse, then reassemble into the next word, on a fixed timing loop (`scheduleCycle`). Word shapes are sampled by rendering each word to an offscreen canvas and reading back which pixels are opaque (`samplePoints`), then randomly downsampling to the particle budget so the shuffle doesn't visually favor any one region of the glyph. Respects `prefers-reduced-motion` by snapping straight to the first word and never starting the animation loop. Startup is deferred until `document.fonts.ready` (so the sampled glyph uses the real "Abel" font, not a fallback) with a hard 1200 ms timeout fallback in case font loading hangs.

## 5. Section-by-section map

Each row is the section's `id` (for anchor links / `nav` targets), its purpose, and the JS behavior driving it (if any).

| `id` | Section | Behavior |
|---|---|---|
| — | Header (`:2188`) | Sticky nav bar; burger menu on mobile (§4.2) |
| `top` | Hero (`:2219`) | Particle-text canvas (§4.7), decorative orbs/grid/shimmer, animated stat counters |
| — | Hero lede pull-quote (`:2271`) | none — static |
| `clients` | Client logo marquee (`:2283`) | CSS-only infinite scroll (`@keyframes clients-scroll-right`) |
| `work-with` | "We Work With" flip cards (`:2346`) | Flip-card toggle (§4.3) |
| `featured` | "Case Studies" work list (`:2413`) | Row expand + slide carousel (§4.4) |
| `expertise` | "Our Expertise" (`:2523`) | Pinned horizontal scroll (§4.5) |
| `process` | "Our Process" accordion (`:2585`) | Accordion + progress ring (§4.6) |
| — | Tech stack marquee (`:2820`) | CSS-only infinite scroll (`@keyframes scroll`) |
| `testimonials` | "Why Choose uExel" (`:2852`) | none — sticky rail via CSS only |
| `contact` | CTA banner (`:2917`) | none — static SVG illustration, `.cta-3d-float` animated by CSS |
| — | Footer (`:2974`) | none — static |

## 6. Content status / known gaps

Worth knowing before treating this as production-ready:

- **Case studies are placeholders** (`uexel-landing.html:2428-2518`): work items are named `ABC`/`DEF`/`GHI` with empty `.work-shot` divs (no real screenshots wired in yet).
- **Several nav links are `#` stubs**: `About`, `Services`, `Product`, `Industries`, `Blog` in the header nav (`:2195-2199`) and `View All Projects` (`:2418`) don't point anywhere yet — only `Home` and `Book A Call` resolve to real in-page anchors.
- **Placeholder contact details**: footer phone (`+925123456700`, `:2986`) and address (`Islamabad Pakistan 44000`, `:2983`) read as placeholder-shaped rather than confirmed real values — worth double-checking before publishing.
- **External hotlink risk**: the process-step icon sprite pulled from `dynamologic.com` (§2) and the `devicon@latest` unpinned CDN version are both dependencies outside this project's control.
- A second file, `uexel-landing-studio.html`, exists alongside this one in the project root — check whether it's an alternate/earlier version before assuming `uexel-landing.html` is the only canonical copy.
