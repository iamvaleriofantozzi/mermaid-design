# Style Guide

**The single source of truth for colors, typography, and tokens.** Every diagram draws from this — not from hex values inlined in other reference files. If you want to change the visual skin of mermaid-design, change this file.

Default skin is a neutral editorial palette — warm stone paper, deep charcoal ink, rust accent. It's designed to look good out of the box for any user without matching any specific brand. Swap these values and every new diagram inherits the new skin without touching any type-specific logic.

To customize, edit the tables below by hand. There is no URL-based onboarding — Mermaid renders in the viewer's environment, so font and color availability depends on the platform (GitHub, Notion, Obsidian, etc.).

---

## Tokens

### Semantic roles

Every token is referred to by **semantic role**, not by its hex value. Type references (`type-*.md`) and SKILL.md say `accent`, not `#b5523a`.

| Role | Purpose | Default (light) | Default (dark) |
|---|---|---|---|
| `paper` | Page background, default node fill | `#faf7f2` | `#1c1917` |
| `paper-2` | Secondary fill, subgraph bg | `#f2ede4` | `#292524` |
| `ink` | Primary text, primary stroke | `#1c1917` | `#faf7f2` |
| `muted` | Secondary text, default arrow stroke | `#57534e` | `#a8a29e` |
| `soft` | Sublabels, boundary labels | `#78716c` | `#8e8680` |
| `rule` | Hairline borders | `rgba(28,25,23,0.12)` | `rgba(250,247,242,0.12)` |
| `rule-solid` | Stronger borders, baselines | `rgba(120,113,108,0.25)` | `rgba(168,162,158,0.25)` |
| `accent` | Focal / 1–2 max per diagram | `#b5523a` | `#d6724a` |
| `accent-tint` | Fill for accent-bordered boxes | `#fdf6f4` | `rgba(214,114,74,0.10)` |
| `link` | HTTP/API calls, external arrows | `#2563eb` | `#60a5fa` |

> **Note:** Dark mode values are suggestions. Mermaid's `theme: dark` overrides many custom tokens. For full dark-mode control, use `theme: base` and set every `themeVariable` explicitly.

### Inversion rule (light → dark)

Any `rgba(28,25,23, X)` in light becomes `rgba(250,247,242, X)` in dark. Same opacities, RGB flipped. The accent gets a slight hue-shift brighter to read on dark paper.

---

## Typography

| Role | Family | Size | Weight | Usage |
|---|---|---|---|---|
| `title` | Serif (Instrument Serif or system serif) | 1.75rem | 400 | Page H1 |
| `node-name` | Sans-serif (Geist or system sans) | 12px | 600 | Human-readable labels |
| `sublabel` | Monospace (Geist Mono or system mono) | 9px | 400 | Port, protocol, URL, field type |
| `eyebrow` | Monospace | 7–8px | 500, tracked 0.18em, uppercase | Type tags, axis labels |
| `arrow-label` | Monospace | 8px | 400, tracked 0.06em | Arrow annotations |
| `callout` | Serif *italic* | 14px | 400 | Editorial asides only |

### Font stack

Mermaid respects `themeVariables.fontFamily`, but the font must be available in the rendering environment:

- **GitHub** — system fonts only (no custom Google Fonts). Use `fontFamily: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif`.
- **Notion / Obsidian / VS Code** — may load custom fonts if installed locally.
- **Self-hosted sites** — can load Google Fonts via `<link>` before the Mermaid script.

**Load-bearing rule:** Mono is for *technical* content (ports, commands, URLs, field types). Names go in sans. Page title is serif. Italic serif is reserved for annotation callouts. **Never JetBrains Mono** as a blanket "dev" font.

---

## Stroke, radius, spacing

Mermaid does not expose all of these as `themeVariables`. Where unsupported, rely on defaults or `classDef` overrides.

| Token | Value | Mermaid equivalent |
|---|---|---|
| `stroke-thin` | `0.8` | `stroke-width:1px` in `classDef` (closest) |
| `stroke-default` | `1` | `stroke-width:1px` in `classDef` |
| `stroke-strong` | `1.2` | `stroke-width:2px` in `classDef` |
| `radius-sm` | `4` | Not configurable per-node; use `[Text]` for slight rounding |
| `radius-md` | `6` | Default for `()` and `{}` shapes |
| `radius-lg` | `8` | Not directly configurable |
| `grid` | `4` | Layout is automatic (Dagre/ELK); spacing not pixel-controllable |

> **Important:** Mermaid uses automatic layout engines (Dagre or ELK). You cannot set exact coordinates or enforce a 4px grid. Trust the layout engine, but keep the complexity budget tight so the result stays readable.

---

## Node type → treatment

Semantic role combinations — reference these by name in type specs and apply via `classDef`.

| Type | Fill | Stroke | `classDef` example |
|---|---|---|---|
| `focal` (1–2 max) | `accent-tint` | `accent` | `fill:#fdf6f4,stroke:#b5523a,stroke-width:2px` |
| `backend` | `#ffffff` (white) | `ink` | `fill:#ffffff,stroke:#1c1917,stroke-width:1px` |
| `store` | `ink @ 0.05` | `muted` | `fill:#f5f4f3,stroke:#57534e` |
| `external` | `ink @ 0.03` | `ink @ 0.30` | `fill:#faf9f9,stroke:#b5b3b1` |
| `input` | `muted @ 0.10` | `soft` | `fill:#f0efee,stroke:#78716c` |
| `optional` | `ink @ 0.02` | `ink @ 0.20` dashed | `fill:#fcfcfc,stroke:#d1d0cf` |
| `security` | `accent @ 0.05` | `accent @ 0.50` dashed | `fill:#faf5f3,stroke:#daaa9d` |

---

## Customizing the skin

Two options:

1. **Edit by hand** — change the hex values in the tables above. Run the pre-output taste gate afterward to verify the accent still reads as "focal" against the new paper color.
2. **Brand handoff** — paste your existing design-token JSON into a new section here and map its tokens to the semantic roles above.

### Constraints (don't break these)

- **Contrast:** `ink` must hit WCAG AA on `paper`. `muted` must hit AA on `paper` for 11px+ text.
- **One accent:** pick one color for `accent`. Two accents erases the focal signal.
- **No rainbow palette:** if your brand ships 8 colors, pick 3 (paper, ink, accent). The rest become `muted` variants.
- **Serif + sans + mono:** three families, not more. If brand typography is all sans, keep a serif for `title` and `callout` anyway — the contrast is load-bearing.
- **Paper is warm-neutral, not pure white:** pure white turns the design sterile. Pick a cream, bone, or light grey with a hint of warmth.
