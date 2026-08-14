# Handoff: Solomon Matters home page

## Overview
Marketing home page for **Solomon Matters**, a smart home / home automation consulting business in greater Los Angeles. The business is advisory-and-design only — it does not install. Phase 1 sells to **electricians, builders and ADU developers** (pre-construction low-voltage and automation planning); homeowner services (assessments, second opinions, support retainers) are a secondary, Phase 2 offer. Business context: `context/business-plan-log.md`.

Two designs are included:

- **`design/Solomon Matters Minimal.dc.html`** — the intended launch page. A single-viewport information page: header, two-column main, footer. **Build this one.**
- **`design/Solomon Matters Home.dc.html`** — a longer marketing page (hero, services, capabilities, process, red poster statement, FAQ, contact form). Written for a homeowner-first audience, so its copy is off-message for Phase 1; keep it as a structural reference for a later, fuller site.

## About the design files
The files in this bundle are **design references created in HTML** — prototypes showing intended look and behavior, not production code to copy directly. The task is to **recreate these designs in the target codebase's existing environment** (React/Next, Astro, Vue, plain HTML — whatever the project uses) with its established patterns. If no codebase exists yet: this is a static marketing page with no backend, so a static-site setup (Astro, Next static export, or hand-written HTML/CSS) is the right call. Do not ship the `.dc.html` files as-is — they are authored in a prototyping component format (`<helmet>`, `x-dc` conventions) that is not a web standard. Read them for markup structure, copy and inline styles only.

`design/styles.css` (identical to `design-system/styles.css`) **is** production-usable — it is the design system's real token + component stylesheet and can be ported directly.

## Fidelity
**High-fidelity.** Final colors, typography, spacing, copy and structure. Recreate pixel-accurately using the tokens in `design/styles.css`. Every value below is already a CSS variable in that file — reference the variables, don't re-hardcode hexes.

## Design system: Modernist
Full guide in `design-system/modernist-readme.md`. Non-negotiables:

- Flat and architectural. Nothing floats, nothing is decorated.
- **Zero border radius anywhere** (`--radius-md: 0`).
- **2px dividers** (`var(--color-divider)`) between all major sections and grid cells. Never soften to 1px hairlines for section rules (1px is used only inside lists).
- Everything **flush left**, including button labels and headings. Never center.
- Accent red is used sparingly: primary button, small uppercase kickers, the one full-bleed poster statement.
- Type is **Archivo** (400/600/800) for both headings and body, loaded from Google Fonts by the stylesheet's `@import`. Prefer a self-hosted or `<link rel="preconnect">` load in production.
- Photographs, if added, go through `.grayscale` (`filter: grayscale(1) contrast(1.08)`). Never tinted or colorized.
- Keyboard focus is `outline: 2px solid var(--color-accent); outline-offset: 2px` — never the browser default.

## Design tokens
From `design/styles.css` `:root`:

**Colors**
| Token | Value | Use |
| --- | --- | --- |
| `--color-bg` | `#f3f2f2` | page ground |
| `--color-surface` | `#eae9e9` | tinted cell fills, inputs |
| `--color-text` | `#201e1d` | ink |
| `--color-accent` | `#ec3013` | primary button, poster field, small emphasis |
| `--color-divider` | `color-mix(in srgb, #201e1d 40%, transparent)` | all rules |
| `--color-neutral-400` | `#bab6b6` | large step numerals |
| `--color-neutral-700` | `#605d5d` | section eyebrow labels |
| `--color-neutral-800` | `#444141` | body copy |
| `--color-accent-600` / `-700` | `#dd2b0f` / `#ae1800` | button hover / pressed; accent-colored small text and links |

Accent red on the light ground is ~3:1 — enough for large text and chrome, **not** for body copy. Paragraph-size accent text uses `--color-accent-700`.

**Spacing** `--space-1..8` = 4 / 8 / 12 / 16 / 24 / 32 px. Page gutters in the designs are a flat **48px** horizontal.

**Radius** all `0px`. **Shadows** `--shadow-sm/md/lg` — unused in the minimal page.

**Type scale** `h1 42px`, `h2 32px`, `h3 25px`, `h4 20px`, `h5 16px`, `h6 13px` (uppercase, `0.08em` tracking). Body 15px / 1.55. Headings `font-weight: 800`, `line-height: 1.12`, `letter-spacing: -0.015em`.

## Screen: Minimal home page (`Solomon Matters Minimal.dc.html`)

**Purpose:** a visitor (an electrician, builder, or homeowner who was referred) learns what the business does, that it is advisory-only, and emails Eric.

**Page shell:** `background: var(--color-bg)`, `color: var(--color-text)`, `font-family: var(--font-body)`, `min-height: 100vh`, `display: flex; flex-direction: column`. Full-bleed — no max-width container.

### Header
`display: flex; align-items: center; gap: 24px; padding: 22px 48px; border-bottom: 2px solid var(--color-divider)`.
- Logo `design/logo.png` (blue/orange gear mark + "SOLOMON MATTERS" wordmark), `height: 32px; width: auto; margin-right: auto`. Note: the logo's blue/orange is off-palette from the red accent — it is used as given, unmodified, and is the only color in the page besides the accent.
- `Greater Los Angeles` — `.text-muted`, 13px.
- `eric@solomonmatters.com` — `mailto:` link, 14px, `var(--color-accent-700)`, hover `var(--color-accent)`.

### Main
`flex: 1; display: grid; grid-template-columns: minmax(0, 1.1fr) minmax(0, 0.9fr); border-bottom: 2px solid var(--color-divider)`.
**The `minmax(0, …)` matters** — plain `fr` tracks let wide children blow the grid out horizontally. Apply the same to every multi-column grid.

**Left cell** — `padding: 76px 48px; border-right: 2px solid var(--color-divider); display: flex; flex-direction: column; align-items: flex-start; gap: 24px`:
1. Kicker: `Smart home planning & advisory` — 12px, `letter-spacing: 0.14em`, uppercase, `var(--color-accent-700)`.
2. `h1`: **"Plan the smart home before the drywall goes up."** — `font-size: clamp(34px, 4.4vw, 54px)`, `line-height: 1.04`, `letter-spacing: -0.03em`, `max-width: 20ch`, `margin: 0`.
3. Lead paragraph, 18px / 1.55, `max-width: 50ch`, `var(--color-neutral-800)`: "Solomon Matters works with electricians, builders and ADU developers across greater Los Angeles: pre-construction low-voltage and automation planning, platform selection, and on-call answers during the build."
4. Second paragraph, 16px / 1.55, same width and color: "We advise and design — we do not install. Your crew keeps the work; we make sure the rough-in is right the first time."
5. Primary CTA: `.btn .btn-primary`, `padding: 14px 24px; font-size: 15px`, label **"Talk about a project"**, href `mailto:eric@solomonmatters.com?subject=Project%20consultation`. Solid `--color-accent` fill, `--color-bg` label, Archivo 800, square corners, label flush left. Hover `--color-accent-600`, active `--color-accent-700`.
6. Cost note: wrapper `margin-top: 8px; border-top: 2px solid var(--color-divider); padding-top: 16px; max-width: 52ch`; text 14px / 1.6 `var(--color-neutral-800)` with the two figures in `<strong>`: "Wiring for automation during construction typically runs **$500–$1,500**. Retrofitting the same house later: **$3,000–$5,000+**. The planning conversation pays for itself before rough-in."

**Right cell** — `display: grid; grid-template-rows: repeat(4, minmax(0, auto))`. Four stacked cells, each `padding: 28px 40px`, `display: flex; flex-direction: column; gap: 8px`; cells 1–3 have `border-bottom: 2px solid var(--color-divider)`; cell 4 has `background: var(--color-surface)` and no bottom border. Each cell: `h4` (19px, `margin: 0`) over a 14px / 1.6 paragraph at `max-width: 42ch`, `var(--color-neutral-800)`.

1. **Pre-construction planning** — "Rough-in scopes, structured cabling and panel notes marked on your plan set — including repeatable packages for ADUs and standard floor plans."
2. **Platform & vendor selection** — "Matter, networking, lighting and energy gear chosen on the merits. No commissions, no hardware sales, no lock-in you have to explain to the client later."
3. **On-call build support** — "A number to call when the spec meets the site. Flat-fee packages for builders, hourly for one-off questions."
4. **Homeowners** (the tinted cell — visually secondary on purpose) — "Home assessments, second opinions on integrator quotes, and support retainers for houses that already have the gear."

### Footer
`padding: 22px 48px; display: flex; align-items: center; gap: 24px; flex-wrap: wrap`. Left, `.text-muted` 13px, `margin-right: auto`: "Advisory and design services — not an installation contractor." (Keep this line — it is the licensing-boundary disclaimer, see Open questions.) Then the `mailto:` link at 13px, then `© 2026 Solomon Matters` `.text-muted` 13px.

## Interactions & behavior
The minimal page has **no JavaScript**. All interaction is CSS state plus two `mailto:` links.
- Buttons/links: hover and active tints come from the stylesheet's accent ramp — don't restyle per page.
- Focus: 2px accent `:focus-visible` ring, 2px offset.
- `::selection` is a 30% accent tint.
- **Responsive:** not yet designed. The desktop layout holds down to roughly 900px. Below ~860px, collapse main to a single column (`grid-template-columns: 1fr`), drop the `border-right` to a `border-bottom`, and reduce gutters from 48px to 24px. The `clamp()` on the h1 already handles type scaling. Header should wrap the location/email onto a second line or hide the location label under ~600px.

## State management
None. Static page, no data fetching, no forms. (The longer `Solomon Matters Home.dc.html` reference has one piece of state — a contact form's submitted flag swapping the button label to a thank-you — and an `IntersectionObserver` that reveals `[data-reveal]` elements on scroll with a 620ms `cubic-bezier(.2,.7,.2,1)` opacity + 16px translateY, staggered 70ms in groups of four. Neither is needed for the minimal page.)

## Assets
- `design/logo.png` — the Solomon Matters logo, user-supplied. Colored gear mark + wordmark on transparent background. Used at 32px height in the header. **Get a vector (SVG) version before launch** — the raster is small and will soften on retina displays.
- No photographs are used in the minimal page. `design/image-slot.js` is a prototyping-only drag-and-drop image placeholder used by the longer reference page; **do not port it** — replace those slots with real `<img>`/`<picture>` elements wrapped in `.grayscale`.
- Icons: the design system specifies **Lucide** (https://lucide.dev). The minimal page uses none.

## Files in this bundle
```
README.md                                  this document
design/Solomon Matters Minimal.dc.html     the page to build
design/Solomon Matters Home.dc.html         longer page, structural reference only
design/styles.css                          design-system tokens + components (portable)
design/logo.png                            logo asset
design/image-slot.js                        prototyping placeholder — do not port
design-system/modernist-readme.md          full design-system guide
design-system/styles.css                   same stylesheet, canonical copy
context/business-plan-log.md               business plan and positioning background
```

## Open questions for the developer / owner
- **Phone number and service-area specifics** are not in the design — no number was provided. Add one if the business wants inbound calls.
- **Licensing disclaimer:** the footer line "Advisory and design services — not an installation contractor" reflects the California C-7 low-voltage licensing boundary discussed in the business plan. Have the exact wording reviewed before launch; do not remove it silently.
- **Dollar figures** ($500–$1,500 vs $3,000–$5,000+) come from the owner's own market research in `context/business-plan-log.md`. Verify before publishing, and consider citing a source.
- No analytics, cookie banner, or SEO metadata is specified. Add `<title>`, meta description, Open Graph tags and a Google Business Profile link at implementation time.
