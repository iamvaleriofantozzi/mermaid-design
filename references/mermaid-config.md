# Mermaid Config Reference

Centralized reference for `%%{init}%%` blocks, `classDef` patterns, and per-type `themeVariables`. Load this whenever you need to configure a diagram's look.

---

## Init block pattern

Every diagram must start with an init block that sets `theme: base`. This prevents the viewer's default theme from overriding your editorial palette.

### Universal template

```mermaid
%%{init: {
  'theme': 'base',
  'themeVariables': {
    'primaryColor': '<paper>',
    'primaryTextColor': '<ink>',
    'primaryBorderColor': '<ink>',
    'lineColor': '<muted>',
    'secondaryColor': '<paper-2>',
    'tertiaryColor': '#ffffff',
    'fontFamily': '<sans-stack>'
  }
}%%
```

Replace placeholders with values from [`style-guide.md`](style-guide.md).

### Dark mode variant

```mermaid
%%{init: {
  'theme': 'base',
  'themeVariables': {
    'primaryColor': '#1c1917',
    'primaryTextColor': '#faf7f2',
    'primaryBorderColor': '#faf7f2',
    'lineColor': '#a8a29e',
    'secondaryColor': '#292524',
    'tertiaryColor': '#1c1917',
    'fontFamily': '<sans-stack>'
  }
}%%
```

> **Warning:** `theme: dark` often overrides custom variables. Always use `theme: base` with explicit dark tokens for full control.

### Hand-drawn look

Add `look: handDrawn` to any init block:

```mermaid
%%{init: {
  'theme': 'base',
  'look': 'handDrawn',
  'themeVariables': { ... }
}%%
```

Good for essays, presentations, and informal docs. Avoid for technical architecture diagrams.

---

## classDef library

Define these **once per diagram**, after the init block and before the graph body. Apply with `class NodeName focal;`.

> **Critical:** Mermaid `classDef` only accepts **solid hex colors** (e.g., `#fdf6f4`) or named colors. It does **not** support CSS `rgba()` values or `stroke-dasharray`. Using `rgba()` in a `classDef` will produce an "Invalid Mermaid code" error. Use the hex values below, derived from the design-system tokens.

### Editorial palette classDefs

```mermaid
classDef focal fill:#fdf6f4,stroke:#b5523a,stroke-width:2px,color:#1c1917;
classDef backend fill:#ffffff,stroke:#1c1917,stroke-width:1px,color:#1c1917;
classDef store fill:#f5f4f3,stroke:#57534e,stroke-width:1px,color:#1c1917;
classDef external fill:#faf9f9,stroke:#b5b3b1,stroke-width:1px,color:#1c1917;
classDef input fill:#f0efee,stroke:#78716c,stroke-width:1px,color:#1c1917;
classDef optional fill:#fcfcfc,stroke:#d1d0cf,stroke-width:1px,color:#78716c;
classDef security fill:#faf5f3,stroke:#daaa9d,stroke-width:1px,color:#1c1917;
classDef link stroke:#2563eb,color:#2563eb;
```

### Dark mode classDefs

```mermaid
classDef focal fill:#4a3b34,stroke:#d6724a,stroke-width:2px,color:#faf7f2;
classDef backend fill:#292524,stroke:#faf7f2,stroke-width:1px,color:#faf7f2;
classDef store fill:#3d3a38,stroke:#a8a29e,stroke-width:1px,color:#faf7f2;
classDef external fill:#363432,stroke:#8e8680,stroke-width:1px,color:#faf7f2;
classDef input fill:#3d3a38,stroke:#8e8680,stroke-width:1px,color:#faf7f2;
classDef optional fill:#322f2d,stroke:#6b6864,stroke-width:1px,color:#8e8680;
classDef security fill:#4a3b34,stroke:#daaa9d,stroke-width:1px,color:#faf7f2;
classDef link stroke:#60a5fa,color:#60a5fa;
```

---

## Per-type themeVariables

Mermaid uses **different variable names** for each diagram type. Below are the correct `themeVariables` keys for each type in mermaid-design.

### flowchart / graph

```json
{
  "primaryColor": "#faf7f2",
  "primaryTextColor": "#1c1917",
  "primaryBorderColor": "#1c1917",
  "lineColor": "#57534e",
  "secondaryColor": "#f2ede4",
  "tertiaryColor": "#ffffff",
  "fontFamily": "Geist, sans-serif"
}
```

Additional flowchart-specific variables (optional):

```json
{
  "clusterBkg": "#f2ede4",
  "clusterBorder": "rgba(28,25,23,0.12)",
  "edgeLabelBackground": "#faf7f2",
  "nodeTextColor": "#1c1917"
}
```

### sequenceDiagram

```json
{
  "actorBkg": "#faf7f2",
  "actorBorder": "#1c1917",
  "actorTextColor": "#1c1917",
  "actorLineColor": "#57534e",
  "signalColor": "#1c1917",
  "signalTextColor": "#1c1917",
  "labelBoxBkgColor": "#faf7f2",
  "labelBoxBorderColor": "#57534e",
  "labelTextColor": "#1c1917",
  "loopTextColor": "#1c1917",
  "noteBorderColor": "#57534e",
  "noteBkgColor": "#f2ede4",
  "noteTextColor": "#1c1917",
  "activationBorderColor": "#57534e",
  "activationBkgColor": "#f2ede4",
  "fontFamily": "Geist, sans-serif"
}
```

### stateDiagram-v2

```json
{
  "primaryColor": "#faf7f2",
  "primaryTextColor": "#1c1917",
  "primaryBorderColor": "#1c1917",
  "lineColor": "#57534e",
  "secondaryColor": "#f2ede4",
  "tertiaryColor": "#ffffff",
  "fontFamily": "Geist, sans-serif"
}
```

### erDiagram

```json
{
  "primaryColor": "#faf7f2",
  "primaryTextColor": "#1c1917",
  "primaryBorderColor": "#1c1917",
  "lineColor": "#57534e",
  "secondaryColor": "#f2ede4",
  "tertiaryColor": "#ffffff",
  "fontFamily": "Geist, sans-serif"
}
```

> Note: `erDiagram` has limited `themeVariables` support. `classDef` does not apply. Focus on simplicity and clean entity naming.

### timeline

```json
{
  "primaryColor": "#faf7f2",
  "primaryTextColor": "#1c1917",
  "primaryBorderColor": "#1c1917",
  "lineColor": "#57534e",
  "secondaryColor": "#f2ede4",
  "tertiaryColor": "#ffffff",
  "fontFamily": "Geist, sans-serif"
}
```

### quadrantChart

```json
{
  "primaryColor": "#faf7f2",
  "primaryTextColor": "#1c1917",
  "primaryBorderColor": "#1c1917",
  "lineColor": "#57534e",
  "secondaryColor": "#f2ede4",
  "tertiaryColor": "#ffffff",
  "fontFamily": "Geist, sans-serif"
}
```

> `quadrantChart` does not support `classDef`. Focal items must be indicated via position (top-right = "do first") and naming, not color.

### architecture-beta

```json
{
  "primaryColor": "#faf7f2",
  "primaryTextColor": "#1c1917",
  "primaryBorderColor": "#1c1917",
  "lineColor": "#57534e",
  "secondaryColor": "#f2ede4",
  "tertiaryColor": "#ffffff",
  "fontFamily": "Geist, sans-serif"
}
```

> `architecture-beta` is experimental and may not support all `themeVariables` consistently across viewers.

---

## Viewer compatibility notes

Not all Mermaid features work everywhere. Use this table to decide what is safe.

| Feature | GitHub | Notion | Obsidian | GitLab | VS Code |
|---|---|---|---|---|---|
| `%%{init}%%` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `theme: base` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `look: handDrawn` | ❌ | ❓ | ✅ | ❓ | ✅ |
| `classDef` in flowchart / graph | ✅ | ✅ | ✅ | ✅ | ✅ |
| `classDef` in sequenceDiagram | ❌ | ❌ | ❌ | ❌ | ❌ |
| `classDef` in stateDiagram-v2 | ❓ | ❓ | ❓ | ❓ | ❓ |
| `classDef` in erDiagram | ❌ | ❌ | ❌ | ❌ | ❌ |
| `classDef` in timeline | ❌ | ❌ | ❌ | ❌ | ❌ |
| `classDef` in quadrantChart | ❌ | ❌ | ❌ | ❌ | ❌ |
| `architecture-beta` | ❓ | ❓ | ❓ | ❓ | ✅ |
| `quadrantChart` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `timeline` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `block-beta` | ❓ | ❓ | ❓ | ❓ | ✅ |
| `mindmap` | ❓ | ❓ | ✅ | ❓ | ✅ |

**Legend:** ✅ Supported | ❌ Not supported | ❓ Untested or partial

**Rule:** For maximum portability, prefer `flowchart`, `sequenceDiagram`, `stateDiagram-v2`, `erDiagram`, `quadrantChart`, and `timeline`. Use `architecture-beta`, `block-beta`, and `mindmap` only when the viewer is known to support them.

---

## Frontmatter (optional)

For deployment on self-hosted sites or the Mermaid Live Editor, you can use YAML frontmatter for configuration:

```mermaid
---
title: Diagram Title
config:
  theme: base
  look: handDrawn
  themeVariables:
    primaryColor: '#faf7f2'
    primaryTextColor: '#1c1917'
---
graph TD
  ...
```

Frontmatter is **not supported** on GitHub. Use `%%{init}%%` for universal compatibility.
