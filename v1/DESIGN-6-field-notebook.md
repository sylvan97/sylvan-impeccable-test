# Design — Direction A · Field Notebook

<!-- impeccable:design-direction-schema 1 -->

> Locked visual authority for Direction A. One of two locked directions in this project; see [`DESIGN.md`](./DESIGN.md) for the index and theme-switcher architecture.
> **Default direction on first load**. Toggle to Direction B (Editorial Ink) via the dynamic island header.

## Identity

- **Mood** — hand-bound personal journal · private · warm · slow
- **Reference constraints carried** — gabrielbeaugonin.com (whitespace, simplicity, restraint, creative)
- **In a sentence** — A paper-and-pen sensibility: ruled notebook paper, handwritten accents, washi tape, slight rotations, and a pencil-red signature accent — interface that reads as a journal page, not a website.

## Palette Tokens

All values are CSS custom properties under the `field-notebook` theme scope.

| Token           | Value     | Use                                                       |
| --------------- | --------- | --------------------------------------------------------- |
| `--paper`       | `#EFE8D5` | body background (warm notebook paper)                     |
| `--paper-deep`  | `#E5DCC4` | entry card surfaces                                       |
| `--paper-edge`  | `#D9CFB2` | ruled-line faint edges                                    |
| `--ink`         | `#2A2520` | primary text, ruled borders                               |
| `--ink-soft`    | `#4A4338` | secondary text                                            |
| `--ink-faint`   | `#857A65` | meta, faint annotations                                   |
| `--pencil`      | `#B5483F` | primary accent: meta dates, numbers, hover state          |
| `--tape`        | `#D4A04C` | washi-tape strip on top of entries                        |
| `--green-pen`   | `#3D5A40` | atmospheric border-left accent, hover links (sparingly)  |

Background texture: `repeating-linear-gradient` horizontal lines at 32px interval with ink @ 7%, plus two radial gradient corner washes (pencil @ 4%, green-pen @ 4%). Texture is a defining element of this direction; do not strip.

Contrast: ink on paper = 11.4:1 · ink-soft = 7.6:1 · pencil on paper = 4.7:1. All WCAG AA clear.

## Typography

Fonts self-hosted via Google Fonts (OFL):
- **Caveat** — handwriting (site mark, dates, numbers, CTA verbs)
- **EB Garamond** — body text
- **Inter** — sparingly for tight meta labels (most labels go through Caveat instead)

| Role               | Family        | Weight      | Size                          | Line | Notes |
| ------------------ | ------------- | ----------- | ----------------------------- | ---- | ----- |
| Signature (h1)     | Caveat        | 600         | clamp(88px, 14vw, 200px)      | 0.9  | cursive, slight rotation -1deg; pencil-red `~` suffix |
| Display (h2)       | EB Garamond   | 500         | 34–42px                       | 1.15 | em label italic 20px below |
| Body               | EB Garamond   | 400         | 18px                          | 1.8  | old-style numerals on (font feature `onum`) |
| Article h4         | EB Garamond   | 500         | 30px                          | 1.2  | em label in faint 16px below |
| Site mark (island) | Caveat        | 600         | 20–22px                       | —    | with pencil ` ·` suffix |
| Handwriting accents| Caveat        | 400–600     | 16–22px                       | —    | dates, numbers, "翻开" verb |
| Meta (sparingly)   | Inter         | 400 / 500   | 10–11px                       | —    | only when Caveat would be illegible at small size |

- Body measure: 65–75ch (article p max 62ch).
- Tracking: minimal; handwriting font relies on its natural shape.
- **Caveat legibility floor** — below 14px, fall back to Inter for that label. Document each fallback in the per-surface spec.

## Spacing (irregular; intentional asymmetry)

| Token       | Value     | Use                                       |
| ----------- | --------- | ----------------------------------------- |
| line-rhythm | 32px      | horizontal rule line spacing              |
| tight       | 6–14px    | within entry fields                       |
| normal      | 24–32px   | between entry sections                    |
| loose       | 48px      | between entry blocks                      |
| ruled-offset| 48px      | content offset to clear margin-rule line  |

Layout carries an asymmetric left margin (48px desktop, 24px mobile) with a faint pencil vertical line — the journal's binding edge. Content starts at 32px from this line. The offset persists across all surfaces to maintain the "journal page" identity.

## Motion

**One authored moment** — page-load rise. Each entry has independent rotation that settles to zero.
- Curve: `cubic-bezier(.16, 1, .3, 1)` (exponential ease-out)
- Duration: 900–1000ms
- Stagger: 200ms between elements
- Initial state: opacity 0, translateY 14px + slight rotation
- Final state: opacity 1, translateY 0, rotation 0

**Dynamic island morph**:
- Same curve, 550ms
- Includes rotation morph: `rotate(-2deg) scale(.92)` (on-hero) → `rotate(-1deg)` (default) → `rotate(-1deg) scale(.92)` (scrolled)
- Border-radius morphs from near-circular to irregular `6px 18px 8px 22px / 20px 6px 22px 8px` to feel hand-drawn

**No** parallax. No scroll-jacking.

## Component Character

### Dynamic Island Header
- Irregular hand-drawn capsule: `border-radius: 6px 18px 8px 22px / 20px 6px 22px 8px`
- 1.5px ink border (heavier than Direction A's 1px) — feels marker-drawn
- Caveat site mark "Sylvan ·" with pencil-red ` ·` suffix
- Caveat module entries (no Inter / no uppercase by default; below 14px may fall back)
- Slight rotation baseline: -1deg; on-hero rotates to -2deg
- Right side: Caveat "— 主页" / "— 近期" indicator with pencil color, always visible
- Box shadow: `2px 2px 0 rgba(42,37,32,.18)` (the journal's offset shadow)

### Hero
- Side padding 48px desktop / 24px mobile, with ruled-line binding on left at 48px from edge
- Date stamp at top in Caveat 18px, rotated -3deg, ink-faint
- Giant signature in Caveat 200px, rotated -1deg, with pencil-red `~` after
- Two entries below at padding-left 32px (clearing binding-line)

### Two Entries
- Notebook-card style: 1px dashed ink border at 35% opacity, slight rotation (0.5deg / -1deg)
- Washi-tape strip across top (`--tape` @ 85% opacity, rotated -2deg)
- Caveat number "壹。" / "�。" in pencil-red
- H2 in EB Garamond + italic em label below
- Stats in Caveat with pencil ✦ bullet
- CTA in Caveat 22px (the journal's "翻开" verb — open the page)
- Hover: rotation → 0, translateY -2px, border → ink

### Article Row
- 2-col grid: Caveat date | body (no reading-time column — articles are for unhurried reading)
- Dashed bottom border (1px dashed ink @ 30%) → full ink on hover
- Caveat date in pencil-red
- H4 EB Garamond, body italic
- Side padding maintains ruled-line offset

## Imagery Stance

- Photos: rare, polaroid-style if used, taped corners
- Live Photo: pencil annotation "·live·" corner
- No background images — texture is CSS only

## Browser Surface

- Selection: pencil background, paper text
- Caret: ink
- Focus ring: 1.5px dashed pencil, offset 3px
- Underline offset: 4px, thickness 1.5px
- Scrollbar: paper-deep thumb with rough edges (no border-radius)

## Anti-patterns Explicitly Avoided

- ❌ No kicker / eyebrow above headings
- ❌ No section numbers (01 / 02 / 03) — 壹 / 贰 are entry labels, not section markers
- ❌ No glass/blur as decoration (backdrop-blur used only on island, with rationale)
- ❌ No card-of-icon-plus-heading-plus-text pattern (cards are hand-drawn notebook pages)
- ❌ No gradient text
- ❌ No system display face
- ❌ No Unicode emoji standing in for icons (used ✦ as inline bullet only, not as icon)
- ❌ No reading time / "X 分钟阅读" on articles — productivity frame excluded (2026-08-20 user decision, project-wide)

## Asset Provenance

| Asset          | Source                                              | License         |
| -------------- | --------------------------------------------------- | --------------- |
| Caveat         | Google Fonts                                        | OFL             |
| EB Garamond    | Google Fonts                                        | OFL             |
| Inter          | Google Fonts                                        | OFL             |
| Photos         | rare — polaroid-style from Unsplash if added        | Unsplash free   |
| Texture        | CSS-only (gradient + repeating-linear-gradient)     | authored        |

## Open Decisions

- Rotation amount — current -1 to -2deg is subtle; some users may find any rotation distracting
- Whether ruled lines should fade on scroll — could feel like reading deeper into the journal
- Photo integration — currently text-only; photos would need polaroid treatment
- Caveat legibility fallback rules — minimum size below which Inter takes over
