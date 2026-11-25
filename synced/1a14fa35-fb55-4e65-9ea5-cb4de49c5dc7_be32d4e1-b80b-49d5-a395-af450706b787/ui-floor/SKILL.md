---
name: "ui-floor"
description: "Hard quality floor for any UI you build or restyle — web pages, Telegram Mini Apps, dashboards, single components. Read before writing the first line of CSS or UI markup."
---

# UI Floor

A fixed minimum for generated interfaces. Models fall into a narrow set of trained-in defaults, and the result reads as generated rather than designed. These rules block those defaults. Everything above the floor is a free design decision.

Self-contained: no external files, scripts, or data to load.

## 1. Hard rules — never ship a violation

**Tokens**
- Every color and font goes through a custom property declared once at `:root` (or a theme block). No literal hex, `rgb()`, or `font-family` anywhere below the token block.
- Semantic names, not literal ones: `--surface-raised`, `--text-muted`, `--accent` — not `--gray-200`, `--blue`.

**Motion**
- Never `transition: all`. Name the properties.
- Never animate `width`, `height`, `top`, `left`, or `margin`. Use `transform` and `opacity`.
- Every animation needs a `@media (prefers-reduced-motion: reduce)` fallback.
- Content must be visible and usable with JavaScript off.

**Layout containment**
- `overflow-x: clip` on both `html` and `body`. Never `hidden` as the fix, never `100vw` as a width.
- Grid tracks that hold images or long text use `minmax(0, 1fr)`.
- Large display text carries `overflow-wrap: break-word; min-width: 0`.
- The container is capped and centered. At a wide viewport the gutters grow; the measure and the grid do not.

**Accessibility (non-negotiable)**
- Body text contrast 4.5:1 minimum, large text 3:1. Check it, don't estimate it.
- Every interactive element has a visible `:focus-visible` state that appears with no delay. Never remove focus rings without replacing them.
- Touch targets 44x44px minimum, with 8px between them.
- Visible labels on form fields. A placeholder is not a label.
- Errors appear next to the field they belong to, not only in a summary at the top.
- Icon-only buttons carry an accessible name.
- Never convey meaning by color alone — pair it with text, shape, or an icon.

**Honesty**
- Never invent a metric, testimonial, logo, customer count, or case study. Material not supplied is absent, not fabricated. An empty slot is correct; a plausible fake number is not.

## 2. Reflex defaults — avoid unless there is a stated reason

These are the tells of generated UI:

- Purple-to-blue gradients. Any gradient used as the primary visual idea.
- A card nested inside another card.
- Emoji used as icons.
- Hand-drawn browser chrome or OS window frames around a screenshot.
- Eyebrow labels above headings. Labels, captions, table heads, tags, and nav links are the body face, one step smaller, sentence case, untracked — not tracked capitals or small caps.
- Meta strings joined by middle dots. Arrows glued to link text. Decorative status dots.
- One duration for every transition. Timing should match distance and weight.
- Instant state changes with no feedback, or hover-only affordances that die on touch.
- Fixed pixel container widths. Disabled zoom. Horizontal scroll on mobile.
- Body text under 14px. Gray text on a gray surface.
- The default section run: hero, three feature cards, stats row, logo wall, email capture band. Build from what the page actually does instead.

## 3. Order of attention

When there is not time for everything, fix in this order:

1. Accessibility — contrast, keyboard, labels, focus
2. Touch and interaction — target size, feedback on every action, loading states
3. Performance — modern image formats, lazy loading, reserved space so nothing shifts (CLS < 0.1)
4. Layout and responsive — mobile-first, no horizontal scroll, no fixed widths
5. Typography and color — 16px base, 1.5 line-height, tokens only
6. Motion — purposeful, context-aware timing, reduced-motion respected
7. Charts and data — legends, tooltips, never color-only encoding

## 4. Before building

Read the project first, then ask once — a single message, not a series of questions:

1. **Material** — what real content exists? Screenshots, photos, actual numbers, a real quote with an attributable name. Paths or pasted content.
2. **Audience** — who uses this and what do they care about?
3. **Job** — the one action this screen should drive.
4. **Tone** — pick an extreme: editorial, brutalist, soft, utilitarian, luxury, playful, technical, austere. "Clean and modern" is not a tone.

Unanswered fields are opt-outs: infer them, state the inferences in one line, do not follow up. Facts are never inferred — a number or quote not given is absent.

If the prompt already answers all four, or nobody is there to answer, do not ask.

## 5. Shape follows material

- Pages with strong images lead with the images.
- Pages about words carry type and facts.
- Name what a visitor comes to do, then build the sections that job needs. Do not reach for a generic template run.
- **Mirror test:** would a neighboring prompt in the same category produce this exact layout? If yes, change one decision and say which.
- **Signature:** the one thing a visitor would remember — the strongest real thing shown at its best, on the first screen. One idea per screen, not five competing ones.
- Roughly 80 words of text on any one screen. A hero is a headline, one sentence, and its action.
- Headline, supporting sentence, and primary action all visible at 1280x800 without scrolling.

## 6. Self-check before handing back

Walk the list; fix anything that fails:

- [ ] No literal colors or font stacks below the token block
- [ ] No `transition: all`; nothing animating layout properties
- [ ] `prefers-reduced-motion` fallback present; works with JS off
- [ ] `overflow-x: clip` on `html` and `body`; no horizontal scroll at 320px
- [ ] Contrast checked, not guessed
- [ ] `:focus-visible` on every interactive element
- [ ] Touch targets 44px+
- [ ] Every form field has a visible label; errors sit next to fields
- [ ] No invented numbers, quotes, or logos
- [ ] No nested cards, emoji icons, purple-blue gradients, or tracked-capital eyebrows
- [ ] Passes the mirror test — one decision is specific to this prompt