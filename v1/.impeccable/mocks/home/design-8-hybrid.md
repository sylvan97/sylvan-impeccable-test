# Direction Spec — Editorial × Notebook Hybrid (#8)

> Candidate 3 of 4 (user-fused from #1 + #6).
> Visual world: editorial print's I/II discipline × notebook's handcrafted warmth.
> Constraint carried: gabrielbeaugonin.com — whitespace, simplicity, restraint, creative.
> **Critical user feedback 2026-08-20 applied**:
>   - KEEP giant Sylvan signature on home — signature is the focal anchor.
>   - REMOVE `.atmospheric` paragraph (the "沉积的文字、影像与足迹..." line) — felt like a personal signature and was redundant with the giant Sylvan signature.
>   - Dynamic island default state right side ALWAYS shows current section (never empty).
> This file documents the candidate. The project's locked `DESIGN.md` is written only after a direction is chosen.

## Provenance of the Fusion

| Element                         | Source     | Notes                                                |
| ------------------------------- | ---------- | ---------------------------------------------------- |
| I / II roman numerals           | #1         | editorial weight, restraint                          |
| Hairline rule above entries     | #1         | editorial structure                                  |
| Brick-red first-letter on h2    | #1         | signature accent, current-page indicator             |
| Cormorant Garamond display      | #1         | atmosphere anchor, scale                              |
| Inter 11px meta / stats         | #1         | tight uppercase meta, hairline rule                   |
| Caveat site mark in island      | #6         | handwritten "Sylvan ·"                              |
| EB Garamond body                | #6         | warmer than Source Serif, old-style numerals on      |
| Washi-tape strip on entries     | #6         | paper-tape accent at top of each entry               |
| Slight rotation on entries      | #6         | 0.3deg / -0.5deg (more subtle than #6 alone)         |
| Faint horizontal ruled lines    | #6         | notebook binding feel (lighter than #6)              |
| Binding-line on hero left       | #6         | 1px pencil @ 35% opacity vertical                     |
| Atmospheric paragraph w/ washi-tape left border | #6 | tape-color 3px border-left                          |

## Palette

| Token           | Value     | Use                                                      |
| --------------- | --------- | -------------------------------------------------------- |
| `--paper`       | `#F2EAD8` | body background (between #1 and #6, slightly warmer)     |
| `--paper-deep`  | `#E8DFC6` | entry card surfaces                                      |
| `--paper-edge`  | `#DBCFB0` | ruled-line faint edges                                   |
| `--ink`         | `#2A2520` | primary text (from #6 — notebook ink is warmer than #1's)|
| `--ink-soft`    | `#4A4338` | secondary text                                           |
| `--ink-faint`   | `#857A65` | meta, faint annotations                                  |
| `--brick`       | `#6B1818` | primary accent (from #1) — first-letter, links, indicator |
| `--brick-soft`  | `#8A2A2A` | hover state on brick                                     |
| `--pencil`      | `#B5483F` | secondary accent (from #6) — meta dates, numbers, washi suffix |
| `--tape`        | `#D4A04C` | washi-tape (from #6)                                     |

Background texture (lighter than #6 alone): `repeating-linear-gradient` horizontal lines at 40px interval with ink @ 5%, plus two soft radial corner washes.

Contrast: ink on paper = 11.6:1 · ink-soft = 7.5:1 · brick on paper = 6.7:1 · pencil on paper = 4.7:1. All WCAG AA clear.

## Type System

| Role                     | Family             | Weight      | Size                          | Line | Tracking |
| ------------------------ | ------------------ | ----------- | ----------------------------- | ---- | -------- |
| **Signature (display)**  | Cormorant Garamond | 500 italic  | clamp(96px, 16vw, 240px)     | 0.88 | -0.025em |
| Site mark (island)       | Caveat             | 600         | 20px                          | —    | 0        |
| Hero wordmark            | Caveat             | 600         | 24px                          | —    | 0        |
| Handwriting accents      | Caveat             | 400–600     | 18–22px                       | —    | 0        |
| Body                     | EB Garamond        | 400         | 18px                          | 1.75 | 0        |
| Entry h2                 | Cormorant Garamond | 500         | 42px                          | 1.1  | -0.005em |
| Article h4               | Cormorant Garamond | 500         | 32px                          | 1.18 | -0.005em |
| Meta / nav / stats       | Inter              | 400 / 500   | 10–12px                       | —    | 0.04–0.28em |
| Footer / site-name       | Caveat + Inter     | mixed       | 20 + 10px                     | —    | mixed    |

Body measure: 62ch max for article p.
Display cap: 240px (signature). Giant signature IS the focal anchor — explicitly retained per user feedback.
Tracking floor: -0.015em.

**Critical**: Giant signature IS the hero focal. The signature uses Cormorant Garamond italic at clamp(96px, 16vw, 240px) — large enough to be the focal anchor without competing with the entries below.

## Spacing

8px base, with notebook offset for binding-line content.
- micro: 6–8px
- tight: 14px
- normal: 24–32px
- loose: 48–56px
- section: 80–120px
- ruled-offset: 32px (content starts after binding line at 48px)

## Motion Grammar

Same as #1 + #6:
- One authored moment: page-load rise
- Curve: `cubic-bezier(.16, 1, .3, 1)`
- Page-load duration: 1s
- Stagger: 200ms
- Initial: opacity 0, translateY 14px
- Final: opacity 1, translateY 0

Dynamic island morph:
- Curve: same
- Duration: 550ms
- Includes slight rotation morph (notebook character): -0.6deg (on-hero) → -0.4deg (default) → -0.2deg (scrolled)
- Includes scale morph: 0.95 (on-hero) → 1.0 (default) → 0.94 (scrolled)

## Component Character

### Dynamic Island Header (CRITICAL — default state right side ALWAYS shows current section)

- Capsule, `rgba(242,234,216,.7)` paper background with backdrop-blur (22px)
- 1px ink border at 22% opacity
- Subtle box shadow: `1px 1px 0 rgba(42,37,32,.1)` (the journal's offset)
- Slight baseline rotation: -0.4deg
- Caveat site mark "Sylvan ·" with pencil-red suffix
- Inter module entries (12px, no uppercase)
- **Right side `.here` is ALWAYS visible, never empty**:
  - Default state: shows "● 主页" (with brick bullet)
  - On featured: shows "● 近期"
  - Hover/focus: full expansion of nav + "● 主页"
- States:
  - **on-hero**: scale 0.95, rotate -0.6deg, smaller padding, more transparent
  - **default**: full size, full opacity, rotate -0.4deg
  - **scrolled**: scale 0.94, rotate -0.2deg, more opaque (compact)
  - **expanded** (hover/focus): nav visible alongside `.here`

### Hero (signature IS the focal)

- Side padding 48px desktop / 24px mobile
- Binding-line on left at 48px from edge (pencil @ 35%, 1px)
- Top meta row:
  - Caveat wordmark "Sylvan·" (24px)
  - Inter site-name "沉淀站 · Atlas No.03" (10px uppercase)
  - Caveat date "2026 · 春" (18px, rotated -2deg, right-aligned)
- **Giant Sylvan signature as the focal anchor**:
  - Cormorant Garamond italic, clamp(96px, 16vw, 240px)
  - First letter brick-red
  - Pencil-red period after the signature
  - Padding-left 32px to clear binding-line
- NO atmospheric / tagline paragraph (removed per user feedback)
- Two entries below at padding-left 32px

### Two Entries

- Notebook-card style: 1px ink border at 18% opacity, slight rotation
  - Entry 1: rotate 0.3deg
  - Entry 2: rotate -0.5deg
- Washi-tape strip at top (64×18px, rotated -3deg, tape @ 82% opacity)
- Roman numeral "I · Articles" / "II · Footprints" in Inter 10px uppercase (pencil color)
- H2 in Cormorant Garamond + italic em label
  - First letter brick-red (signature accent from #1)
- Description (EB Garamond, max 36ch)
- Stats: Inter 10px uppercase, separated by brick · bullets
- Top hairline divider within entry (above stats)
- CTA: Inter 11px uppercase, brick gap + color on hover
- Hover: rotation → 0, translateY -2px, border → ink

### Article Row

- 2-col grid: Caveat date | body (no reading-time column — see locked DESIGN-1 / DESIGN-6)
- Date in pencil-red Caveat 22px + small Inter day label below
- Reading time in Caveat 22px + small Inter "READING" label below
- H4 Cormorant Garamond, body EB Garamond
- Dashed bottom border (1px dashed ink @ 25%) → full ink on hover

## Imagery Stance

- Photos: rare, polaroid-style if used, taped corners
- Live Photo: pencil annotation "·live·" corner
- No background images — texture is CSS only

## Browser Surface

- Selection: brick background, paper text
- Caret: ink
- Focus ring: 1px solid brick, offset 3px
- Underline offset: 4px
- Scrollbar: paper-deep thumb

## Anti-patterns Explicitly Avoided

- ❌ No atmospheric / tagline paragraph on home (user feedback — removed as redundant)
- ❌ No empty right side on dynamic island default state (user feedback)
- ❌ No kicker / eyebrow above headings
- ❌ No section numbers (01/02/03)
- ❌ No card-of-icon-plus-heading-plus-text pattern
- ❌ No gradient text
- ❌ No system display face
- ❌ No Unicode glyphs / emoji standing in for icons

## Open Decisions

- Atmospheric paragraph size — 76px cap may be too large; verify on real content
- Whether to add a single atmospheric photo on the home — currently text-only
- Entry rotation amount — 0.3/-0.5 is intentionally subtle; could increase to match #6
- Whether binding-line should fade out below the fold — could reduce visual noise later

## Asset Provenance

| Asset        | Source              | License |
| ------------ | ------------------- | ------- |
| Caveat       | Google Fonts        | OFL     |
| Cormorant Garamond | Google Fonts   | OFL     |
| EB Garamond  | Google Fonts        | OFL     |
| Inter        | Google Fonts        | OFL     |
| Photos       | none in current     | —       |
| Texture      | CSS-only (gradient + repeating-linear-gradient) | authored |

Mockup file: `.impeccable/mocks/home/8-editorial-notebook-hybrid.html` (340 lines, 16.2 KB).
