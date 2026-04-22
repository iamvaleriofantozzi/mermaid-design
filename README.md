# Mermaid Design

**Editorial-quality diagrams as portable Mermaid code.**

Eleven diagram types. One shared design system, complexity budget, and taste gate. Renders everywhere — GitHub, Notion, Obsidian, GitLab, VS Code, and any Markdown viewer that supports Mermaid.

Inspired by [cathrynlavery/diagram-design](https://github.com/cathrynlavery/diagram-design) — editorial diagram philosophy adapted for Mermaid.js.

---

## What it makes

| Type | Best for | Mermaid syntax |
|---|---|---|
| **Flowchart** | Decision logic, algorithms, branching flows | `graph TD` |
| **Sequence** | Request/response, protocol exchanges, API traces | `sequenceDiagram` |
| **Architecture** | System overviews, data-flow, integration maps | `graph LR` / `architecture-beta` |
| **State machine** | Order status, auth state, connection lifecycle | `stateDiagram-v2` |
| **ER / data model** | Database schemas, API resource relationships | `erDiagram` |
| **Timeline** | Release history, milestones, roadmaps | `timeline` |
| **Quadrant** | Prioritization, 2×2 positioning, portfolio maps | `quadrantChart` |
| **Tree** | Org charts, dependency trees, taxonomy | `graph TD` / `mindmap` |
| **Swimlane** | Cross-functional processes, handoffs | `graph TD` + `subgraph` |
| **Layer stack** | OSI model, tech stack, abstraction layers | `graph TB` / `block-beta` |
| **Nested** | Scope boundaries, containment hierarchies | `graph TD` + `subgraph` |

All diagrams ship with an editorial palette (warm paper, ink, coral accent) and a pre-output taste gate.

---

## Install

### Claude Code (skills directory)

```bash
git clone git@github.com:iamvaleriofantozzi/mermaid-design.git ~/.claude/skills/mermaid-design
```

Restart Claude Code. The skill registers as `mermaid-design` and activates whenever you ask Claude to make a diagram.

### Claude Code (plugin)

```bash
/plugin marketplace add iamvaleriofantozzi/mermaid-design
/plugin install mermaid-design@mermaid-design
```

### Manual use

You don't need Claude Code to use this. Copy any example from [`examples/`](examples/) and paste it into the [Mermaid Live Editor](https://mermaid.live/).

---

## Quickstart

```
Make me a flowchart of the login flow: start, validate input, check credentials,
return token or error.
```

Claude will pick the right type, build the Mermaid code, and output it wrapped in triple backticks. Paste it into GitHub, Notion, Obsidian, or any Mermaid-compatible viewer.

```
Make me a sequence diagram of the OAuth handshake in dark mode.
```

Claude will use the dark token palette and set the init block accordingly.

---

## Design system

- **One accent** (coral/rust) on 1–2 focal elements max.
- **Warm paper** background, **ink** text, **muted** secondary lines.
- **Sans-serif** for names, **monospace** for technical sublabels (ports, URLs, field types).
- **No shadows, no gradients, no neon glow.**
- **Complexity budget**: max 9 nodes, max 12 arrows, max 2 focal elements.

Full spec in [`references/style-guide.md`](references/style-guide.md).

---

## Architecture

Progressive disclosure. `SKILL.md` is a lean index — it tells Claude how to pick a type and where to look for detail. Every type lives in its own reference file, loaded only when relevant.

```
mermaid-design/
├── SKILL.md                    # Philosophy, selection guide, taste gate
├── references/
│   ├── style-guide.md          # Colors, typography, tokens
│   ├── mermaid-config.md       # Init blocks, classDef, viewer compatibility
│   ├── type-flowchart.md
│   ├── type-sequence.md
│   ├── type-architecture.md
│   ├── type-state.md
│   ├── type-er.md
│   ├── type-timeline.md
│   ├── type-quadrant.md
│   ├── type-tree.md
│   ├── type-swimlane.md
│   ├── type-layers.md
│   └── type-nested.md
├── examples/                   # One working .mmd per type
└── README.md
```

This keeps Claude's working context tight (only load what you need) and makes the skill easy to extend.

---

## Viewer compatibility

| Feature | GitHub | Notion | Obsidian | GitLab | VS Code |
|---|---|---|---|---|---|
| `%%{init}%%` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `theme: base` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `classDef` (flowchart/sequence/state) | ✅ | ✅ | ✅ | ✅ | ✅ |
| `architecture-beta` | ❓ | ❓ | ❓ | ❓ | ✅ |
| `quadrantChart` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `timeline` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `mindmap` | ❓ | ❓ | ✅ | ❓ | ✅ |
| `block-beta` | ❓ | ❓ | ❓ | ❓ | ✅ |

For maximum portability, prefer `graph TD`, `sequenceDiagram`, `stateDiagram-v2`, `erDiagram`, `quadrantChart`, and `timeline`.

---

## When not to use this

- **Quick unicode diagrams** for tweets or terminal output → wiretext.
- **Lists of anything** → a table or bullets.
- **Before/after comparisons** → a table.
- **One-shape "diagrams"** — a single box with a label → just write the sentence.

Before drawing, ask: *Would a reader learn more from this than from a well-written paragraph?* If no, don't draw.

---

## License

MIT
