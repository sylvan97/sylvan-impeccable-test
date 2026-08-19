# Direction Spec — Editorial Ink

> Candidate 1 of 4 (user-selected comparison). Visual world: editorial print / literary magazine.
> Constraint carried: gabrielbeaugonin.com — whitespace, simplicity, restraint, creative.
> This file documents the candidate. The project's locked `DESIGN.md` is written only after a direction is chosen.

## Palette

| Token              | Value     | Use                                                      |
| ------------------ | --------- | -------------------------------------------------------- |
| `--paper`          | `#F7F4ED` | body background                                          |
| `--paper-deep`     | `#EDE8DA` | sub-surfaces, hover fills                                |
| `--ink`            | `#1A1A1A` | primary text, headings, hairlines                        |
| `--ink-soft`       | `#3A3A3A` | secondary text                                           |
| `--ink-faint`      | `#7A7368` | meta, dates, captions                                    |
| `--rule`           | `#1A1A1A` | dividers (1px solid at full opacity or 15% for hovers)   |
| `--accent`         | `#6B1818` | signature first-letter, links, current-section indicator|

Contrast: ink on paper = 14.8:1 · ink-soft = 10.1:1 · ink-faint = 4.6:1. All clear WCAG AA at body sizes.

## Type System

| Role                | Family                | Weight      | Size                          | Line | Tracking |
| ------------------- | --------------------- | ----------- | ----------------------------- | ---- | -------- |
| Signature (display) | Cormorant Garamond    | 500 italic  | clamp(72px, 12vw, 180px)      | 0.92 | -0.02em  |
| Atmospheric         | Cormorant Garamond    | 400 italic  | clamp(20px, 2.4vw, 28px)      | 1.5  | 0        |
| Entry h2            | Cormorant Garamond    | 500         | 48px                          | 1.1  | -0.01em  |
| Article h4          | Cormorant Garamond    | 500         | 32px                          | 1.2  | -0.01em  |
| Body                | Source Serif 4        | 400         | 17px                          | 1.7  | 0.005em  |
| Meta / nav          | Inter                 | 400 / 500   | 11–12px                       | —    | 0.04–0.18em |
| Reading time strong | Cormorant Garamond    | 500 italic  | 22px                          | —    | 0        |

Body measure: 65–75ch (atmospheric max 680px, article body 62ch).
Display cap: 180px (clamp 72–180px). Tracking floor: -0.02em.
Fonts self-hosted via Google Fonts (OFL).

## Spacing (8px base)

| Token   | Value | Use                                    |
| ------- | ----- | -------------------------------------- |
| micro   | 6px   | between label and value                |
| tight   | 14px  | within entry stats                     |
| normal  | 24px  | between entry fields                   |
| loose   | 48px  | between entry blocks, between articles |
| section | 80–120px | between major sections             |

## Motion Grammar

**One authored moment** — page-load rise on signature → atmosphere → entries → article-rows.
- Curve: `cubic-bezier(.16, 1, .3, 1)` (exponential ease-out)
- Duration: 1s
- Stagger: 150–200ms between elements
- Initial: opacity 0, translateY 12px
- Final: opacity 1, translateY 0

**Dynamic island morph** (scroll-driven):
- Same curve
- Duration: 550ms
- States: `on-hero` (smaller, more transparent, top: 14px) → default → `scrolled` (compact) → `expanded` (on hover/focus)

**No** repeated entrance animations on scroll. No scroll-jacking. No parallax.

## Component Character

### Dynamic Island Header
- Capsule, semi-transparent paper (`rgba(247,244,237,.55)`) with `backdrop-filter: blur(22px) saturate(160%)`
- 1px ink border at 18% opacity
- Site mark "Sylvan" in Cormorant Garamond italic, 16px
- Module entries: Inter 12px, no uppercase, 0.04em tracking
- Right side: section indicator with brick-red bullet (5px · )
- Hover/focus expands to show all module labels

### Hero
- Side padding 48px desktop / 24px mobile
- Meta line at top (Inter 11px, 0.18em, uppercase, ink-faint)
- Signature display as focal anchor
- Atmospheric paragraph (italic, max-width 680px, 28px clamp)
- Two entries below: hairline rule above, I/II roman numerals

### Two Entries
- 1fr 1fr grid; single column on mobile
- Roman numeral "I." / "II." in Inter 10px
- H2 in Cormorant Garamond + italic em label
- Description in Source Serif 4, max-width 38ch
- Stats: Inter 11px uppercase with brick-red · separators
- CTA: Inter 12px uppercase, brick-red gap + color on hover

### Article Row
- 2-col grid: date | body (no reading-time column — see locked DESIGN-1)
- Hairline divider (1px ink @ 15%) → full ink on hover
- H4 Cormorant Garamond · body Source Serif 4

## Imagery Stance

- Photos: monochrome or sepia-toned, large format, framed with thin border
- Live Photo: small corner indicator (· LIVE), hover (desktop) / tap (mobile) to play
- Caption: italic, right-aligned, Inter 11px

## Browser Surface

- Selection: ink background, paper text
- Caret: ink
- Focus ring: 1px solid brick-red, offset 3px
- Underline offset: 3px
- Scrollbar: minimal, `--paper-deep` thumb on `--paper` track

## Anti-patterns Explicitly Avoided

- ❌ No kicker / eyebrow above headings (per craft-floor ban)
- ❌ No section numbers (01/02/03) — roman numerals are entry labels only, not section markers
- � No modal for any task
- ❌ No card-of-icon-plus-heading-plus-text pattern
- ❌ No gradient text
- ❌ No hard offset shadows (only soft 1px blur shadows on island)
- ❌ No system display face (Impact / Arial Black / platform sans)
- ❌ No Unicode glyphs / emoji standing in for icons

## Open Decisions (candidate-level)

- **Hero signature as focal vs. atmospheric-only** — user feedback 2026-08-20 questioned the giant Sylvan signature as "weird"; needs revisiting
- **Whether to keep roman numerals** — they add editorial weight but increase visual chrome
- **Whether to include a single atmospheric photo on the home** — current mockup is text-only

## Asset Provenance

| Asset          | Source                                              | License         |
| -------------- | --------------------------------------------------- | --------------- |
| Cormorant Garamond | Google Fonts                                    | OFL             |
| Source Serif 4 | Google Fonts                                         | OFL             |
| Inter          | Google Fonts                                         | OFL             |
| Photos         | Unsplash (when added)                                | Unsplash free   |

Mockup file: `.impeccable/mocks/home/1-editorial-ink.html` (259 lines, 12.8 KB).
