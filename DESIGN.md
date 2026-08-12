---
name: uExel
description: A software consulting & product engineering partner, with a lead specialty in Healthcare IT
colors:
  signal-blue: "#0b7ec9"
  signal-blue-btn: "#0972b8"
  signal-blue-dark: "#075a93"
  frost-sky: "#eaf4fd"
  soft-sky: "#cfe6fa"
  deep-navy: "#0d3a5c"
  midnight-navy: "#0a2e49"
  near-black: "#0a0d11"
  ink: "#0b0f14"
  offwhite: "#f5f8fc"
  white: "#ffffff"
  slate: "#5b6472"
  steel-gray: "#8b96a3"
  signal-blue-tint: "#5fb3e6"
  muted-on-dark: "#9aa2ab"
typography:
  display:
    fontFamily: "Abel, Inter, sans-serif"
    fontSize: "clamp(50px, 9vw, 90px)"
    fontWeight: 400
    lineHeight: 0.98
    letterSpacing: "0.005em"
  headline:
    fontFamily: "Abel, Inter, sans-serif"
    fontSize: "clamp(34px, 5vw, 50px)"
    fontWeight: 400
    letterSpacing: "0.01em"
  title:
    fontFamily: "Abel, Inter, sans-serif"
    fontSize: "32px"
    fontWeight: 400
    lineHeight: 1.05
  body:
    fontFamily: "Inter, -apple-system, BlinkMacSystemFont, 'Segoe UI', Arial, sans-serif"
    fontSize: "17px"
    fontWeight: 400
    lineHeight: 1.6
  label:
    fontFamily: "Inter, sans-serif"
    fontSize: "13px"
    fontWeight: 600
    letterSpacing: "0.18em"
rounded:
  pill: "999px"
  card: "10px"
  cardMd: "12px"
  cardLg: "14px"
  cardXl: "22px"
  sharp: "0px"
spacing:
  section: "110px"
  sectionLg: "96px"
  gap: "40px"
  gapSm: "20px"
components:
  button-primary:
    backgroundColor: "{colors.signal-blue-btn}"
    textColor: "{colors.white}"
    rounded: "{rounded.pill}"
    padding: "16px 34px"
  button-primary-hover:
    backgroundColor: "{colors.signal-blue-dark}"
  button-ghost:
    backgroundColor: "{colors.white}"
    textColor: "{colors.ink}"
    rounded: "{rounded.pill}"
    padding: "16px 34px"
  button-outline:
    backgroundColor: "transparent"
    textColor: "{colors.white}"
    rounded: "{rounded.pill}"
    padding: "16px 34px"
  tag-chip:
    backgroundColor: "{colors.white}"
    textColor: "{colors.deep-navy}"
    rounded: "{rounded.sharp}"
    padding: "9px 16px"
---

# Design System: uExel

## Overview

**Creative North Star: "The Blueprint Desk"**

uExel's page reads like a confident engineering firm's own materials: a near-black control-room base, one signal-blue accent doing all the pointing, and condensed technical numerals stamped on everything from stat counters to case-study indices. The signature move is literal — cards for expertise areas and service categories sit tilted at odd angles (−8°/+8°), as if scattered spec sheets on a drafting table rather than snapped into a rigid grid. A canvas-particle animation dissolves and reforms the hero's closing word ("IMPACT.", "GROWTH.", "VALUE.", "REALITY."), the one moment of overt spectacle in an otherwise disciplined, restrained system.

The system rejects decorative color: outside the signal-blue accent and its navy-gradient companions, everything is near-black, white, or muted gray. It also rejects heavy shadow — most surfaces sit flat against a tinted or dark background, with soft diffuse elevation reserved for a handful of interactive surfaces (the primary CTA's glow, the flip-cards) rather than applied uniformly.

**Key Characteristics:**
- Near-black + navy base, one signal-blue accent, no other hues
- Abel (condensed uppercase display) for numerals and headings, Inter for body copy
- Tilted "fanned" cards as the recurring signature motif (expertise cards, service flip-cards)
- Pill-shaped CTAs contrast deliberately with sharp-cornered data tags — soft/human vs. precise/technical
- Flat by default; shadow appears only on a small set of elevated interactive surfaces

## Colors

A near-monochrome dark/light system anchored by a single blue accent; no secondary or tertiary hue family exists.

### Primary
- **Signal Blue** (#0b7ec9): the one accent color in the system — links, arrow glyphs (↘), stat numbers, card index numbers, active states. Used sparingly against dark backgrounds so it reads as a highlight, not a fill.
- **Signal Blue (Button)** (#0972b8): a deliberately darker sibling of Signal Blue, used only where white text sits directly on the fill (primary CTA background, testimonial avatar gradient) — plain Signal Blue only clears ~4.3:1 against white text, this variant clears 4.5:1+ AA.
- **Signal Blue (Dark)** (#075a93): the CTA hover/pressed state, one step darker still than the button variant so hover remains visually distinct.
- **Signal Blue (Tint)** (#5fb3e6): a lightened variant used specifically for index numerals ("001", "002") sitting on a dark-navy card face (dark expertise cards, flip-card fronts) — plain Signal Blue's own radial-gradient highlight on those faces is close enough in value that the plain accent nearly disappears into it; the tint keeps the numeral legible.

### Neutral
- **Near-Black** (#0a0d11): the base surface for dark sections — header, hero, Featured Work, footer.
- **Ink** (#0b0f14): default heading/body text color on light surfaces; nearly indistinguishable from Near-Black but kept as a separate token for text vs. surface roles.
- **Deep Navy** (#0d3a5c) / **Midnight Navy** (#0a2e49): the gradient pair behind dark expertise cards, flip-card fronts, and the testimonial avatar circles — the system's only non-blue, non-black hue family, always used as a diagonal gradient rather than a flat fill.
- **Frost Sky** (#eaf4fd): the tinted section background for "We Work With" and "Our Expertise" — the lightest way the page varies from pure white without introducing a new hue.
- **Soft Sky** (#cfe6fa): a pale accent used only as the tag-chip border, tying chips back to the blue family without adding contrast weight.
- **Offwhite** (#f5f8fc): the marquee strip's background, one step off pure white.
- **Slate** (#5b6472): default body copy on light backgrounds.
- **Steel Gray** (#8b96a3): secondary/label text on light or near-black chrome — eyebrows, unfilled placeholder state.
- **Muted (On Dark)** (#9aa2ab): default secondary/body copy specifically on dark-section surfaces (Why Choose uExel, testimonial ledes, footer body text) — a touch lighter than Steel Gray so paragraph text stays readable against Near-Black without competing with Steel Gray's label role.

### Named Rules
**The One Accent Rule.** Signal Blue is the only hue in the system besides navy and near-black/white. If a new UI element needs color emphasis, reach for Signal Blue or a tint of it before introducing anything else.

**The Text-on-Fill Rule.** Any white text sitting directly on a blue fill uses the darker Signal Blue (Button) variant (#0972b8), never plain Signal Blue (#0b7ec9) — the plain accent is calibrated for text/icons *on* dark or light neutral backgrounds, not as a background *under* white text.

## Typography

**Display Font:** Abel (with Inter, sans-serif fallback)
**Body Font:** Inter (with -apple-system, BlinkMacSystemFont, "Segoe UI", Arial fallback)

**Character:** Abel is a condensed, uppercase-leaning geometric face used exclusively for numerals and headings — it's what gives the page its "stamped/engineered" feel. Inter carries every sentence of actual reading, kept plain and highly legible in contrast to Abel's stylization.

### Hierarchy
- **Display** (400, `clamp(50px, 9vw, 90px)`, line-height 0.98): the hero headline only.
- **Headline** (400, `clamp(34px, 5vw, 50px)`): section titles ("Our Expertise", "We Work With", "Featured Work"), always paired with the Signal Blue "↘" arrow glyph.
- **Title** (400, 32px, line-height 1.05): expertise-card and flip-card titles; set with tight leading so a two-line title (service name + index number) reads as one unit.
- **Body** (400, 17px, line-height 1.6): default paragraph text.
- **Label** (600, 13px, letter-spacing 0.18em, uppercase): eyebrow labels and section micro-copy.

### Named Rules
**The All-Caps Numerals Rule.** Every numeral that isn't a live statistic sits in Abel and is treated as a graphic element (card index "001.", stat counters, work-item index) — never render a number in Inter when it's meant to carry visual weight.

## Layout

Content is capped at 1280px (`--maxw`) and centered with 40px side padding (the `.wrap` pattern), the same recipe used for every section including the pinned horizontal-scroll "Our Expertise" area, so nothing stretches edge-to-edge on wide monitors. Section vertical rhythm runs large and consistent: 110px top/bottom padding for standard sections, 96px for the hero. The header is sticky with a translucent, blurred backdrop (`rgba(10,13,17,0.92)` + `backdrop-filter: blur(10px)`) so page content is always legible scrolling underneath it. Below 768px, tilted/rotated cards flatten to `rotate(0)` and horizontal-scroll sections collapse to a plain stacked column — the system trades its signature diagonal motif for legibility on small screens rather than trying to preserve it.

## Elevation & Depth

Flat by default. Most surfaces — cards, sections, the sticky header — carry no shadow at all and rely on flat color contrast (dark section vs. light section, white card vs. tinted background) for separation. Shadow is reserved for a small, deliberate set of elevated/interactive surfaces: the primary CTA's colored glow and the flip-cards' lift off the page. Rotation, not shadow, is this system's primary depth cue — tilted cards read as "scattered on top of" the flat background purely through overlap and angle.

### Shadow Vocabulary
- **CTA Glow** (`box-shadow: 0 10px 30px -8px rgba(11, 126, 201, 0.55)`): a colored (not neutral) shadow under the primary button, tinted to match Signal Blue rather than a generic dark shadow.
- **Card Lift** (`box-shadow: 0 30px 60px -25px rgba(11, 15, 20, 0.25)`): the diffuse lift under flip-cards and expertise cards — large spread, negative offset, low opacity, so it reads as ambient depth rather than a hard drop shadow.

### Named Rules
**The Flat-First Rule.** Default every new surface to no shadow. Add one of the two shadows above only when the element genuinely floats above other content (a lifted card, a genuinely elevated overlay) — never as decoration on a static section.

## Shapes

Two deliberately opposed corner languages coexist. CTAs and links are fully pill-shaped (`border-radius: 999px`) — soft, approachable, human. Data-bearing chips (the tag list on "We Work With" cards) are perfectly square-cornered (`border-radius: 0`) — precise, technical, spec-sheet-like. Cards sit in between: expertise cards at 12px, flip-cards and the work-panel accordion at 10px, client-logo tiles, case-study thumbnails, and the "Why Choose uExel" proof panel at 14px. A `--radius: 22px` token is declared in the stylesheet but not currently applied anywhere — worth resolving (either wire it to a real surface or remove it) rather than treating it as an active part of the system.

### Named Rules
**The Pill-or-Sharp Rule.** A rounded element is either fully pill-shaped (actions: buttons, links) or has a small consistent radius (containers: cards, panels, 10-14px). Nothing should land on an in-between radius like 6px or 8px — that reads as indecisive against the two established languages. Data chips are the one deliberate exception, at a full 0px.

## Components

### Buttons
- **Shape:** fully pill-shaped (`border-radius: 999px`), 16px/34px padding, uppercase 14px/700-weight label text with 0.06em letter-spacing.
- **Primary:** Signal Blue (Button) fill (#0972b8), white text, tinted glow shadow. Hover: darkens to Signal Blue (Dark) (#075a93) and lifts 2px (`translateY(-2px)`).
- **Ghost:** white fill, ink text; hover fills with Frost Sky.
- **Outline:** transparent fill, 1.5px white-alpha border, white text; hover fills with a faint white wash (`rgba(255,255,255,0.08)`).

### Chips (Tags)
- **Style:** white background, Deep Navy text, 1px Soft Sky border, 0px radius, 9px/16px padding, uppercase 11.5px/700-weight.
- **Usage:** the capability list on "We Work With" service cards ("MVP DEVELOPMENT", "PROTOTYPING," etc.) — always plural, always a short label, never a sentence.

### Cards / Containers
- **Expertise cards** (pinned horizontal-scroll section): 400px wide, 500px tall, 12px radius, alternating white/navy-gradient fill, rotated ±8° (flattens to 0° under 768px), no shadow — depth comes from the tilt and overlap alone.
- **Flip-cards** ("We Work With"): 3D-flipped on click (`rotateY(180deg)`, 1s ease), 10px radius, 38px/34px padding, Card Lift shadow on both faces; front face is a navy diagonal gradient with white text, back face is white with ink text.
- **Featured Work accordion rows:** no card chrome at all — flat rows on the Near-Black background that expand via a `grid-template-rows: 0fr → 1fr` transition, revealing an image-slide panel.
- **Client-logo tiles** ("Trusted By"): 14px radius, Offwhite fill, hairline border, logo grayscale at rest and full color on hover with a 6px lift — the one place logo marks (not the system's own type/color) carry the visual weight.
- **Proof panel** ("Why Choose uExel" affiliations block): 14px radius, translucent Deep Navy → Midnight Navy diagonal gradient fill (distinct from the section's flat Near-Black background so it reads as an inset panel), hairline white-alpha border; badge marks inside it sit on a transparent ground.

### Focus State
No distinct focus-visible treatment existed at first pass; buttons, links, and the two custom keyboard-operable controls (flip-cards, case-study rows) now share a 2px Signal Blue outline at 3px offset on `:focus-visible`, layered on top of whatever native shape the element already has rather than replacing it.

### Navigation
- **Style:** uppercase 14px/600-weight links, letter-spacing 0.04em, light gray (`#d7dce1`) at rest, Signal Blue on hover, inside a sticky/blurred header. Mobile collapses to a full-width stacked menu behind a hamburger toggle.

### Signature: Tilted Card Fan
The system's one unmistakable custom pattern: any card grouping meant to feel "curated" or "browsable" (expertise areas, service categories) rotates each card by a small alternating angle (currently ±8°) rather than aligning them in a grid. It's the single strongest brand signal in the implementation and should be the first thing preserved in any redesign or new surface that reuses this card family.

## Do's and Don'ts

### Do:
- **Do** keep Signal Blue as the only accent hue; reach for a tint/shade of it (Frost Sky, Soft Sky, the darker button variant) before introducing a new color.
- **Do** use the darker Signal Blue (Button) variant (#0972b8), not plain Signal Blue, anywhere white text sits directly on a blue fill.
- **Do** keep the tilted-card motif (±8°, alternating direction) for any new "browsable options" card grouping — it's the system's signature, not a one-off.
- **Do** default new surfaces to no shadow; add one of the two named shadows only for genuinely floating/elevated elements.
- **Do** use Abel for numerals and headings, Inter for everything read as a sentence — never swap the pairing's roles.

### Don't:
- **Don't** introduce a second accent hue (a green success color, an orange warning color, etc.) without a deliberate decision — the system currently has none, on purpose.
- **Don't** use a mid-range border-radius (6-8px) on any container; commit to either a full pill (actions) or the established 10-14px card/panel scale.
- **Don't** apply the tilted-card treatment to content that isn't a browsable grouping of options (e.g. don't rotate a single hero image or a form).
- **Don't** treat `--radius: 22px` as a real, load-bearing token — it's currently unused; resolve or remove it rather than building on it.
