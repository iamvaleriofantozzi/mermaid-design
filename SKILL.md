---
name: mermaid-design
description: Create editorial-quality diagrams using Mermaid.js syntax. Eleven diagram types with an opinionated design system, complexity budget, and taste gate. Output is portable Mermaid code that renders in GitHub, Notion, Obsidian, and any Markdown viewer. Inspired by cathrynlavery/diagram-design.
license: MIT
metadata:
  version: "1.0"
---

# Mermaid Design

Create visual diagrams as **portable Mermaid code blocks**, following an opinionated editorial design system.

Eleven diagram types. One shared design system, complexity budget, and taste gate. Type-specific conventions live in `references/` and are loaded only when you pick a type.

Inspired by [cathrynlavery/diagram-design](https://github.com/cathrynlavery/diagram-design) — editorial diagram philosophy adapted for Mermaid.js.

---

## 0. First-time setup — style guide gate

**Before generating your first diagram in a new project, verify the style guide has been customized.**

Open [`references/style-guide.md`](references/style-guide.md) and check the default tokens. If they're still the shipped defaults (paper `#faf7f2`, ink `#1c1917`, accent `#b5523a` rust), **pause and ask the user**:

> *"This is your first diagram in this project. The style guide is still at the default (neutral stone + rust). Do you want to customize it first? Options: (a) paste your brand tokens manually, (b) proceed with the default for now."*

Then branch:
- **(a)** → accept the user's tokens and write them into `style-guide.md` under a new "Custom tokens" section.
- **(b)** → proceed; optionally remind the user they can customize later.

**Once the style guide has been customized** (or the user explicitly opted for default), skip this gate on subsequent runs. A simple way to detect customization: if the `accent` value in `style-guide.md` differs from `#b5523a`, assume custom.

Don't silently ship default-skinned diagrams into a branded project — that's the failure mode this gate exists to prevent.

---

## 1. Philosophy

**The highest-quality move is usually deletion.**

Confident restraint. Earn every element. One color accent, two families, a small spacing vocabulary. If removing it wouldn't hurt the page, remove it.

Applied to diagrams:
- Every node represents a distinct idea. Two nodes that always travel together are one node.
- Every connection carries information. If the relationship is obvious from layout, remove the line.
- Coral is **editorial, not a flag.** 1–2 focal nodes per diagram. Using it on 5 nodes erases the signal.
- The diagram isn't done when everything is added. It's done when nothing can be removed.

**Target density: 4/10.** Enough to be technically complete. Not so dense it needs a guide. Above 9 nodes, it's probably two diagrams.

---

## 2. When to Use

Use for any of the 11 diagram types (§3) when a reader will learn more from a visual than from prose, a table, or a bulleted list.

**Don't use for:**
- Quick unicode diagrams → use **wiretext**.
- Lists of things → table or bullets.
- Simple before/after → table.
- One-shape "diagrams" → just write the sentence.

Before drawing, ask: *Would the reader learn more from this than from a well-written paragraph?* If no, don't draw.

---

## 3. Diagram Types

### Selection guide

| If you're showing… | Use | Reference |
|---|---|---|
| Components + connections in a system | **Architecture** | [type-architecture.md](references/type-architecture.md) |
| Decision logic with branches | **Flowchart** | [type-flowchart.md](references/type-flowchart.md) |
| Time-ordered messages between actors | **Sequence** | [type-sequence.md](references/type-sequence.md) |
| States + transitions + guards | **State machine** | [type-state.md](references/type-state.md) |
| Entities + fields + relationships | **ER / data model** | [type-er.md](references/type-er.md) |
| Events positioned in time | **Timeline** | [type-timeline.md](references/type-timeline.md) |
| Cross-functional process with handoffs | **Swimlane** | [type-swimlane.md](references/type-swimlane.md) |
| Two-axis positioning / prioritization | **Quadrant** | [type-quadrant.md](references/type-quadrant.md) |
| Hierarchy through containment / scope | **Nested** | [type-nested.md](references/type-nested.md) |
| Parent → children relationships | **Tree** | [type-tree.md](references/type-tree.md) |
| Stacked abstraction levels | **Layer stack** | [type-layers.md](references/type-layers.md) |

Rules of thumb:
- If a 3-column table communicates the same thing, pick the table.
- If you're combining two types, pick the dominant axis — don't hybridize grammars.
- If you're past the complexity budget (§7), split into an overview + detail.

**Always load the relevant `references/type-*.md` before drawing** — it contains syntax conventions, anti-patterns, and example code for that type.

---

## 4. Universal Anti-patterns

These mark "AI slop" diagrams of any type:

| Anti-pattern | Why it fails |
|---|---|
| Dark mode + cyan/purple glow | Looks "technical" without design decisions |
| JetBrains Mono as blanket "dev" font | Mono is for *technical* content — ports, commands, URLs. Names go in sans. |
| Identical boxes for every node | Erases hierarchy |
| Legend inside the diagram area | Collides with nodes |
| Arrow labels longer than 14 chars | Breaks layout or overlaps |
| 3 equal-width summary cards as default | Generic grid — vary widths |
| Coral on every "important" node | Coral is 1–2 editorial accents, not a signaling system |

Type-specific anti-patterns live in each `references/type-*.md`.

---

## 5. Design System

**The design system is skinnable.** All colors, typography, and tokens live in a single source of truth — [`references/style-guide.md`](references/style-guide.md). This file describes semantic roles (`paper`, `ink`, `muted`, `accent`, `link`, …). The default skin is neutral editorial (warm paper, ink, coral); to apply your own brand, edit `style-guide.md` directly.

> When specs below or in type references mention "ink", "accent", "muted", etc., look up the current value in `style-guide.md`.

### Semantic roles (at a glance)

| Role | Purpose |
|---|---|
| `paper`, `paper-2` | Background and secondary fill |
| `ink` | Primary text / stroke |
| `muted`, `soft` | Secondary text, default arrows, sublabels |
| `rule`, `rule-solid` | Borders and dividers |
| `accent`, `accent-tint` | 1–2 focal elements per diagram |
| `link` | HTTP/API calls, external arrows |

**Focal rule:** `accent` goes on 1–2 elements max. Everything else is `ink` / `muted` / `soft`. If you're tempted to accent 4 things, you haven't decided what's focal yet.

### Node type → treatment (via classDef)

In Mermaid, apply these via `classDef` and `class` statements. See [`references/mermaid-config.md`](references/mermaid-config.md) for exact syntax.

| Type | Fill | Stroke |
|---|---|---|
| **Focal** (1–2 max) | `accent` bg | `accent` border |
| **Backend / API / Step** | white / `paper-2` | `ink` |
| **Store / State** | `ink` @ 0.05 | `muted` |
| **External / Cloud** | `ink` @ 0.03 | `ink` @ 0.30 |
| **Input / User** | `muted` @ 0.10 | `soft` |
| **Optional / Async** | `ink` @ 0.02 | `ink` @ 0.20 dashed |
| **Security / Boundary** | `accent` @ 0.05 | `accent` @ 0.50 |

### Typography (summary — full spec in style-guide.md)

- **Title** — Sans-serif, 1.75rem, 400 — H1 only
- **Node name** — Sans-serif, 12px, 600 — human-readable labels
- **Sublabel** — Monospace, 9px — ports, URLs, field types
- **Eyebrow / tag** — Monospace, 7–8px, uppercase, tracked — type tags, axis labels
- **Arrow label** — Monospace, 8px — annotation on arrows
- **Editorial aside** — *Italic* serif, 14px — callouts only

**Mono is for technical content.** Names are sans. Page title is serif. *Italic* serif is reserved for annotation callouts. Never JetBrains Mono as a blanket "dev" font.

---

## 6. Core Mermaid Primitives

Universal building blocks. Type-specialized primitives (lifeline, activation bar, region) live in the relevant `references/type-*.md`.

### Init block (always include)

Every diagram starts with an `init` block that sets the theme to `base` and loads the semantic tokens:

```mermaid
%%{init: {
  'theme': 'base',
  'themeVariables': {
    'primaryColor': '#faf7f2',
    'primaryTextColor': '#1c1917',
    'primaryBorderColor': '#1c1917',
    'lineColor': '#57534e',
    'secondaryColor': '#f2ede4',
    'tertiaryColor': '#ffffff',
    'fontFamily': 'Geist, sans-serif'
  }
}%%
```

> Exact variable names differ by diagram type. See [`references/mermaid-config.md`](references/mermaid-config.md) for per-type init blocks.

### Arrow conventions

| Arrow | Syntax | When |
|---|---|---|
| Default | `-->` | Internal, generic |
| Accent | `-->` + `class` focal | Primary / highlighted |
| Link-blue | `-->` + `class` link | HTTP/API calls, external systems |
| Dashed | `-.->` | Optional, passive, return, async |
| Bold/thick | `==>` | Strong emphasis (use sparingly) |

### classDef for focal nodes

```mermaid
classDef focal fill:#fdf6f4,stroke:#b5523a,stroke-width:2px,color:#1c1917;
classDef backend fill:#ffffff,stroke:#1c1917,stroke-width:1px,color:#1c1917;
classDef store fill:#f5f4f3,stroke:#57534e,stroke-width:1px,color:#1c1917;
classDef external fill:#faf9f9,stroke:#b5b3b1,stroke-width:1px,color:#1c1917;
classDef optional fill:#fcfcfc,stroke:#d1d0cf,stroke-width:1px,color:#78716c;
classDef link stroke:#2563eb,color:#2563eb;
```

Apply with: `class NodeName focal;`

### Legend

Place the legend **as a comment block below the diagram**, not inside the diagram area:

```
%% Legend:
%% ■ Focal (coral) — primary integration point
%% □ Backend — service / API
%% ▤ Store — database / cache
%% ▨ External — third-party
```

---

## 7. Layout & Spacing

### Complexity budget (per diagram)

| Limit | Rule |
|---|---|
| Max nodes | 9 |
| Max arrows / transitions | 12 |
| Max focal (coral) elements | 2 |
| Max lifelines (sequence) | 5 |
| Max lanes (swimlane) | 5 |
| Max items (quadrant) | 12 |
| Max entities (ER) | 8 |
| Max nesting levels (nested) | 6 |
| Max tree depth | 4 |
| Max layers (layer stack) | 6 |
| Max annotation callouts | 2 |

If you exceed, split into two diagrams (overview + detail).

### Page layout (full-editorial variant)

When the diagram is the hero of a long-form post, wrap the Mermaid block with a title and summary:

```markdown
## Diagram Title

```mermaid
%%{init: ...}%%
graph TD
  ...
```

**Summary** — 1–2 sentences on what the diagram shows and why it matters.
```

---

## 8. Pre-Output Checklist (Taste Gate)

Run before producing any diagram.

**Type fit:**
- [ ] Right type for what I'm showing? (§3 selection guide)
- [ ] Would a table / paragraph do the same job? (If yes — don't draw.)
- [ ] Loaded the matching `references/type-*.md`?

**Remove test:**
- [ ] Can I remove any node? (Would a reader still understand?)
- [ ] Can I merge any two nodes? (Do they always travel together?)
- [ ] Can I remove any arrow? (Is the relationship obvious from layout?)
- [ ] Can I remove any label? (Does color or shape already signal it?)

**Signal:**
- [ ] Coral used on ≤2 elements? If more, which actually deserve focal status?
- [ ] Legend covers every type used — and nothing extra?
- [ ] Within the type's complexity budget (§7)?

**Technical:**
- [ ] Init block sets `theme: base` with correct `themeVariables`?
- [ ] `classDef` statements defined before they are used?
- [ ] Every arrow label ≤14 characters?
- [ ] Legend is a comment block, not floating nodes?
- [ ] No cyclic dependencies unless intentionally showing a loop?

**Typography:**
- [ ] Human-readable names in sans, not mono?
- [ ] Technical sublabels (ports, commands, URLs) in mono?
- [ ] Page title in serif (if rendered by viewer)?
- [ ] No JetBrains Mono anywhere?

---

## 9. Templates & Variants

Every diagram ships in two variants:

| Variant | How to request | Init block |
|---|---|---|
| **Minimal light** (default) | "Make me a flowchart of..." | `theme: base` with light tokens |
| **Minimal dark** | "...in dark mode" | `theme: dark` or custom dark tokens |

**Hand-drawn look** (optional, applied to any variant):
Add `look: handDrawn` to the init block. Good for essays and presentations, not for technical docs.

```mermaid
%%{init: {
  'theme': 'base',
  'look': 'handDrawn',
  'themeVariables': { ... }
}%%
```

### To create a new diagram

1. Load the matching `references/type-*.md` for syntax conventions.
2. Copy the init block from [`references/mermaid-config.md`](references/mermaid-config.md) for that type.
3. Build the diagram body.
4. Apply `classDef` and `class` for focal nodes.
5. Run the §8 taste gate.

---

## 10. Output

Always produce a single **Mermaid code block** wrapped in triple backticks with the `mermaid` language tag:

- Include the `%%{init}%%` block at the top
- Include `classDef` definitions after the init block
- Include a comment-based legend at the bottom
- No external dependencies — renders in any Mermaid-compatible viewer

Renders correctly in GitHub, Notion, Obsidian, GitLab, VS Code Markdown preview, and any site using Mermaid.js.
