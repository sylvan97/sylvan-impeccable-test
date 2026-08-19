# Direction Spec — Field Notebook

> Candidate 2 of 4 (user-selected comparison). Visual world: hand-bound personal journal.
> Constraint carried: gabrielbeaugonin.com — whitespace, simplicity, restraint, creative.
> This file documents the candidate. The project's locked `DESIGN.md` is written only after a direction is chosen.

## Palette

| Token            | Value     | Use                                                       |
| ---------------- | --------- | --------------------------------------------------------- |
| `--paper`        | `#EFE8D5` | body background (warm notebook paper)                     |
| `--paper-deep`   | `#E5DCC4` | entry card surfaces                                       |
| `--paper-edge`   | `#D9CFB2` | ruled-line faint edges                                    |
| `--ink`          | `#2A2520` | primary text, ruled borders                               |
| `--ink-soft`     | `#4A4338` | secondary text                                            |
| `--ink-faint`    | `#857A65` | meta, faint annotations                                   |
| `--pencil`       | `#B5483F` | primary accent: meta dates, numbers, hover state          |
| `--tape`         | `#D4A04C` | washi-tape strip on top of entries                        |
| `--green-pen`    | `#3D5A40` | atmospheric border-left accent, hover links (used sparingly) |

Background texture: `repeating-linear-gradient` horizontal lines at 32px interval with ink @ 7%, plus two radial gradient corner washes (pencil @ 4%, green-pen @ 4%).

Contrast: ink on paper = 11.4:1 · ink-soft = 7.6:1 · pencil on paper = 4.7:1. All clear WCAG AA.

## Type System

| Role                | Family             | Weight      | Size                          | Line | Notes |
| ------------------- | ------------------ | ----------- | ----------------------------- | ---- | ----- |
| Signature (display) | Caveat             | 600         | clamp(88px, 14vw, 200px)      | 0.9  | cursive, slight rotation -1deg |
| Site mark (island)  | Caveat             | 600         | 22px                          | —    | with pencil ` ·` suffix |
| Handwriting accents | Caveat             | 400–600     | 18–22px                       | —    | numbers, dates, CTA "翻开" |
| Body                | EB Garamond        | 400         | 18px                          | 1.8  | onum (old-style numerals) on |
| Entry h2            | EB Garamond        | 500         | 34px                          | 1.15 | em label italic 20px below |
| Article h4          | EB Garamond        | 500         | 30px                          | 1.2  | em label in faint 16px |
| Meta / section      | Inter              | 400 / 500   | 10–11px                       | —    | sparingly used |

Body measure: 65–75ch (article p max 62ch).
Tracking: minimal; handwriting font relies on its natural shape.
Fonts self-hosted via Google Fonts (OFL).

## Spacing (irregular; intentional asymmetry)

| Token       | Value     | Use                                       |
| ----------- | --------- | ----------------------------------------- |
| line-rhythm | 32px      | horizontal rule line spacing              |
| tight       | 6–14px    | within entry fields                       |
| normal      | 24–32px   | between entry sections                    |
| loose       | 48px      | between entry blocks                      |
| ruled-offset| 48px      | content offset to clear margin-rule line  |

Layout carries an asymmetric left margin (48px) with a faint pencil vertical line — the journal's binding edge. Content starts at 32px from this line.

## Motion Grammar

**One authored moment** — page-load rise. Each entry has independent rotation that settles to zero.
- Curve: `cubic-bezier(.16, 1, .3, 1)` (exponential ease-out)
- Duration: 900–1000ms
- Stagger: 200ms between elements
- Initial: opacity 0, translateY 14px + slight rotation
- Final: opacity 1, translateY 0, rotation 0

**Dynamic island morph**:
- Same curve, 550ms
- Includes rotation morph: `rotate(-2deg) scale(.92)` (on-hero) → `rotate(-1deg)` (default) → `rotate(-1deg) scale(.92)` (scrolled)
- Border-radius morphs from near-circular to irregular `6px 18px 8px 22px / 20px 6px 22px 8px` to feel hand-drawn

**No** parallax. No scroll-jacking.

## Component Character

### Dynamic Island Header
- Irregular hand-drawn capsule: `border-radius: 6px 18px 8px 22px / 20px 6px 22px 8px`
- 1.5px ink border (heavier than Editorial Ink's 1px) — feels marker-drawn
- Caveat site mark "Sylvan ·" (with pencil-red ` ·` suffix)
- Caveat module entries (no Inter / no uppercase)
- Slight rotation baseline: -1deg; on-hero rotates to -2deg
- Right side: Caveat "— 主页" indicator with pencil color
- Box shadow: `2px 2px 0 rgba(42,37,32,.18)` (the journal's offset shadow)

### Hero
- Side padding 48px desktop / 24px mobile, with ruled-line binding on left at 48px from edge
- Date stamp at top in Caveat 18px, rotated -3deg, ink-faint
- Signature in Caveat 200px, rotated -1deg, with pencil-red `~` after
- Atmospheric paragraph in EB Garamond italic 28px, with washi-tape left-border (3px solid tape color)

### Two Entries
- Notebook-card style: 1px dashed ink border at 35% opacity, slight rotation (0.5deg / -1deg)
- Washi-tape strip across top (`--tape` @ 85% opacity, rotated -2deg)
- Caveat number "壹。" / "贰。" in pencil-red
- H2 in EB Garamond + italic em label below
- Stats in Caveat with pencil ✦ bullet
- CTA in Caveat 22px (the journal's "翻开" verb — open the page)

### Article Row
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
- ❌ No section numbers (壹/贰 are entry labels, not section markers)
- ❌ No glass/blur as decoration (backdrop-blur used only on island, with rationale)
- ❌ No card-of-icon-plus-heading-plus-text pattern (cards are hand-drawn notebook pages, not generic cards)
- ❌ No gradient text
- ❌ No system display face (Caveat and EB Garamond both self-hosted)
- � No Unicode emoji standing in for icons (used ✦ as inline bullet only, not as icon)

## Open Decisions (candidate-level)

- **Rotation amount** — current -1 to -2deg is subtle; some users may find any rotation distracting
- **Whether ruled lines should fade on scroll** — could feel like reading deeper into the journal
- **Photo integration** — currently text-only; photos would need polaroid treatment
- **Caveat legibility at small sizes** — at 14px Caveat gets harder to read; may need Inter fallback below 14px

## Asset Provenance

| Asset        | Source              | License |
| ------------ | ------------------- | ------- |
| Caveat       | Google Fonts        | OFL     |
| EB Garamond  | Google Fonts        | OFL     |
| Inter        | Google Fonts        | OFL     |
| Photos       | none in current     | —       |
| Texture      | CSS-only (gradient + repeating-linear-gradient) | authored |

Mockup file: `.impeccable/mocks/home/6-field-notebook.html` (273 lines, 12.4 KB).
