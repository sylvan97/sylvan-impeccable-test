# Design — Direction B · Editorial Ink

<!-- impeccable:design-direction-schema 1 -->

> Locked visual authority for Direction B. One of two locked directions in this project; see [`DESIGN.md`](./DESIGN.md) for the index and theme-switcher architecture.
> **Alternate direction** (Field Notebook is the default on first load). Toggle via the dynamic island header.

## Identity

- **Mood** — editorial print / literary magazine · restraint · text-first
- **Reference constraints carried** — gabrielbeaugonin.com (whitespace, simplicity, restraint, creative)
- **In a sentence** — A literary-magazine sensibility: ink on paper, serif display, hairline rules, and a brick-red signature accent that carries the only color in the system.

## Palette Tokens

All values are CSS custom properties under the `editorial-ink` theme scope.

| Token              | Value     | Use                                                      | Contrast vs paper |
| ------------------ | --------- | -------------------------------------------------------- | ----------------- |
| `--paper`          | `#F7F4ED` | body background                                          | —                 |
| `--paper-deep`     | `#EDE8DA` | sub-surfaces, hover fills                                | —                 |
| `--ink`            | `#1A1A1A` | primary text, headings, hairlines                        | 14.8 : 1          |
| `--ink-soft`       | `#3A3A3A` | secondary text                                           | 10.1 : 1          |
| `--ink-faint`      | `#7A7368` | meta, dates, captions                                    | 4.6 : 1           |
| `--rule`           | `#1A1A1A` | dividers (1px full opacity or 15% for non-active rows)   | —                 |
| `--accent`         | `#6B1818` | signature first-letter, links, current-section indicator | 7.0 : 1           |

All text-on-paper combinations clear WCAG AA. `--accent` is the only chromatic color in the system; use it sparingly — never for backgrounds, only for emphasis.

## Typography

Fonts self-hosted via Google Fonts (OFL):
- **Cormorant Garamond** — display + serif body accents
- **Source Serif 4** — body text
- **Inter** — meta, nav, stats, all-caps labels

| Role               | Family             | Weight      | Size                          | Line | Tracking |
| ------------------ | ------------------ | ----------- | ----------------------------- | ---- | -------- |
| Signature (h1)     | Cormorant Garamond | 500 italic  | clamp(96px, 16vw, 240px)      | 0.88 | -0.025em |
| Display (h2 / hero)| Cormorant Garamond | 500         | clamp(36px, 4.8vw, 72px)      | 1.05 | -0.01em  |
| Atmospheric        | Cormorant Garamond | 400 italic  | clamp(20px, 2.4vw, 28px)      | 1.5  | 0        |
| Entry h2           | Cormorant Garamond | 500         | 48px                          | 1.1  | -0.01em  |
| Article h3 / h4    | Cormorant Garamond | 500         | 30–32px                       | 1.2  | -0.01em  |
| Body               | Source Serif 4     | 400         | 17–18px                       | 1.7  | 0.005em  |
| Meta / nav / stats | Inter              | 400 / 500   | 10–12px                       | —    | 0.04–0.18em |

- Body measure: 65–75ch (atmospheric max 680px, article body max 62ch).
- Display cap: 240px (signature). Tracking floor: -0.025em.
- Numerals: lining in body and meta; old-style optional in italic contexts.

## Spacing (8px base scale)

| Token   | Value     | Use                                          |
| ------- | --------- | -------------------------------------------- |
| micro   | 6px       | between label and value                      |
| tight   | 14px      | within entry stats                           |
| normal  | 24px      | between entry fields                         |
| loose   | 48px      | between entry blocks, between article rows   |
| section | 80–120px  | between major sections                       |

## Motion

**One authored moment** — page-load rise on signature → atmosphere → entries → article-rows.
- Curve: `cubic-bezier(.16, 1, .3, 1)` (exponential ease-out)
- Duration: 1s
- Stagger: 150–200ms between elements
- Initial state: opacity 0, translateY 12px
- Final state: opacity 1, translateY 0

**Dynamic island morph** (scroll-driven):
- Curve: same as above
- Duration: 550ms
- States: `on-hero` (smaller, more transparent, top: 14px) → default → `scrolled` (compact) → `expanded` (on hover/focus)

**No** repeated entrance animations on scroll. No scroll-jacking. No parallax.

## Component Character

### Dynamic Island Header
- Capsule, semi-transparent paper (`rgba(247,244,237,.55)`) with `backdrop-filter: blur(22px) saturate(160%)`
- 1px ink border at 18% opacity
- Site mark "Sylvan" in Cormorant Garamond italic, 16px
- Module entries: Inter 12px, no uppercase, 0.04em tracking
- Right side: section indicator with brick-red bullet (5px ●)
- Hover/focus expands to show all module labels; right-side indicator stays visible

### Hero
- Side padding 48px desktop / 24px mobile
- Meta line at top (Inter 11px, 0.18em, uppercase, ink-faint)
- **Giant Sylvan signature as focal anchor** (NOT a tagline paragraph)
- Two entries below: hairline rule above, I / II roman numerals

### Two Entries
- 1fr 1fr grid; single column on mobile
- Roman numeral "I." / "II." in Inter 10px, uppercase, 0.28em tracking
- H2 in Cormorant Garamond + italic em label
- First letter brick-red (signature accent)
- Description in Source Serif 4, max-width 38ch
- Stats: Inter 11px uppercase with brick-red · separators
- CTA: Inter 12px uppercase, brick gap + color on hover

### Article Row
- 2-col grid: date | body
- Hairline divider (1px ink @ 15%) → full ink on hover
- H4 Cormorant Garamond · body Source Serif 4
- **No reading time** — articles are for unhurried reading; quantifying duration would impose a productivity frame the site explicitly rejects

## Imagery Stance

- Photos: monochrome or sepia-toned, large format, framed with thin border
- Live Photo: small corner indicator (`● LIVE`), hover (desktop) / tap (mobile) to play
- Caption: italic, right-aligned, Inter 11px

## Browser Surface

- Selection: ink background, paper text
- Caret: ink
- Focus ring: 1px solid brick-red, offset 3px
- Underline offset: 3px
- Scrollbar: minimal, `--paper-deep` thumb on `--paper` track

## Anti-patterns Explicitly Avoided

- ❌ No kicker / eyebrow above headings (per craft-floor ban)
- ❌ No section numbers (01 / 02 / 03) — roman numerals are entry labels only
- ❌ No modal for any task
- ❌ No card-of-icon-plus-heading-plus-text pattern
- ❌ No gradient text
- ❌ No hard offset shadows (only soft 1px blur shadows on island)
- ❌ No system display face (Impact / Arial Black / platform sans)
- ❌ No Unicode glyphs / emoji standing in for icons
- ❌ No atmospheric / tagline paragraph on home — giant signature carries the focal weight
- � No reading time / "X 分钟阅读" — articles are for unhurried reading, not quantified productivity (2026-08-20 user decision)

## Asset Provenance

| Asset               | Source                                          | License         |
| ------------------- | ----------------------------------------------- | --------------- |
| Cormorant Garamond  | Google Fonts                                    | OFL             |
| Source Serif 4      | Google Fonts                                    | OFL             |
| Inter               | Google Fonts                                    | OFL             |
| Photos              | Unsplash (when added)                           | Unsplash free   |
| Live Photo assets   | Source TBD (Coverr / Pexels / self-recorded)    | per-asset       |

## Open Decisions

- Hero signature rotation / drift — current spec keeps it static; minor letterpress-jitter could be added in future revision
- Whether atmospheric paragraphs return on sub-pages (e.g., article detail hero) — currently absent from spec, may be re-introduced per-surface
