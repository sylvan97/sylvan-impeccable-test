# Design — Dual Direction Locked

<!-- impeccable:design-schema 1 -->

## Locked State

This project carries **two locked visual directions simultaneously**, by user decision (2026-08-20). Both are first-class citizens in the design system; the Astro implementation must support runtime switching between them via a theme toggle.

| File | Direction | Mood | Default? |
|---|---|---|---|
| [`DESIGN-6-field-notebook.md`](./DESIGN-6-field-notebook.md) | Direction A · Field Notebook | 手作笔记本 · 私人感 · 温度 | **Yes**（首次加载） |
| [`DESIGN-1-editorial-ink.md`](./DESIGN-1-editorial-ink.md) | Direction B · Editorial Ink | 编辑印刷感 · 克制 · 文本为王 | No（切换态） |

## Why two locked directions

User rationale (2026-08-20):
- Both directions scored strongly in side-by-side review; user prefers to keep both rather than commit to one at the design phase.
- Aesthetic mood can vary by season or content rhythm — text-heavy weeks vs. media-heavy weeks — and the user wants the site itself to carry that variability.
- A runtime theme switcher in the dynamic island header is an acceptable complexity cost.

## Runtime Theme Switcher (architecture requirement, binding)

The Astro implementation **must** support live switching between Direction A and Direction B at runtime. Concrete requirements:

1. **Token binding** — both directions' design tokens (palette, typography scale, spacing scale, motion grammar, component character) are exposed as CSS custom properties. Each direction is a complete token set; tokens never mix.
2. **Switch trigger** — a `<html data-theme="editorial-ink">` or `<html data-theme="field-notebook">` attribute selects the active token set. No per-element classes for theming.
3. **Switcher UI** — a small theme-toggle lives inside the dynamic island header (right side, next to the section indicator). One-tap toggle; the icon hints at the *other* theme (i.e., when on A, the toggle shows B's icon).
4. **Persistence** — user preference is stored in `localStorage` under key `sylvan:theme`. First load with no preference defaults to **Direction A = Field Notebook** (Field Notebook is the site’s primary voice; Editorial Ink is the alternate).
5. **Per-surface work** — every per-surface new-work round (articles 二/三级, travels 二/三级, albums 二级 + 三级, citywalks 二/三级, `/tags/[tag]`) **must produce two variants** — one per direction. Each variant inherits from its direction's locked spec.
6. **No mid-page theme mixing** — a page is entirely in one direction at a time. Theme switching happens at page load or via the toggle; it is not a continuous blend.

## Implementation Status

- [x] Two locked visual directions
- [x] Candidate mockups for each direction (home only at this point)
- [x] Home page mockup per direction
- [ ] Astro theme scaffold (CSS variables, `data-theme` system, switcher component)
- [ ] Per-surface variants in both directions
- [ ] Theme preference persistence
- [ ] Default theme verification (Direction A = Field Notebook on first load)

## Mockups & Assets

| Direction | Home mockup | Spec file |
|---|---|---|
| A · Field Notebook | `.impeccable/mocks/home/6-field-notebook.html` | this index |
| B · Editorial Ink | `.impeccable/mocks/home/1-editorial-ink.html` | this index |
| (hybrid, superseded) | `.impeccable/mocks/home/8-editorial-notebook-hybrid.html` | `.impeccable/mocks/home/design-8-hybrid.md` |

Hybrid #8 is preserved in the candidate folder but is **not** part of the locked set; do not reference it from the Astro implementation.

## Departure from Skill Convention

The impeccable skill convention is one locked `DESIGN.md` per project, acting as the single visual authority. This project deliberately ships **two** parallel authorities plus this index. The convention is honored in spirit (clear visual authority, both directions are fully specified) while departing in form (two files plus an index, with a runtime switcher).

This departure is recorded so that any later tooling that expects a single `DESIGN.md` does not silently break; tooling should look at this index first and follow the referenced direction files.

## Open Decisions

- Theme toggle placement — currently specified as "inside the dynamic island header, right side"; needs confirmation in per-surface work whether it survives across all surfaces.
- Whether to expose the switcher publicly or hide it behind a keyboard shortcut / dev-only flag — currently spec'd as public.
- First-load default — currently **Direction A = Field Notebook** (2026-08-20 user decision). Editorial Ink is the alternate.

## Next Steps

1. Astro scaffold with `data-theme` system + CSS variables per direction + theme switcher component + `localStorage` persistence
2. Per-surface new-work rounds, each producing two variants (one per direction)
3. Lock the full design system after all surfaces are covered in both directions
4. (Optional, user-decision later) If user chooses to ship with only one direction, archive the other to `.impeccable/mocks/` and reduce `DESIGN.md` to a single-authority form
