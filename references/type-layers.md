# Layer Stack

**Best for:** OSI model, CSS cascade, context hierarchy, tech stack, abstraction layers, memory hierarchy.

## Syntax

Use `block-beta` (Mermaid 10.6+) or fall back to `graph TD` with stacked nodes.

### block-beta (preferred when supported)

```mermaid
block-beta
columns 1
  app["Application Layer"]
  api["API Layer"]
  svc["Service Layer"]
  db["Data Layer"]
```

**Keywords:**
- `columns N` — sets the number of columns.
- `id["Label"]` — a block.
- `id:rowspan` — spans multiple rows (optional).

### Fallback: graph TB

```mermaid
graph TB
    L1[Application Layer] --> L2[API Layer]
    L2 --> L3[Service Layer]
    L3 --> L4[Data Layer]
```

## Layout conventions

- 4–6 layers total.
- Each layer is a full-width block or node. Label clearly.
- Direction indicator: if the stack has a semantic direction (e.g., abstraction ↑, packets ↓), mention it in the diagram title or a note.
- Coral on **one** focal layer — the bottleneck, the pay-rent layer, or the one under discussion.
- In `block-beta`, use `columns 1` for a vertical stack. Labels sit inside blocks automatically.

## Anti-patterns

- Layers that aren't actually hierarchical — use swimlane or architecture instead.
- Skipped numbering (missing L4 between L3 and L5 without explanation).
- Every layer a different color — hierarchy becomes invisible.
- Inconsistent layer heights without reason.

## Limitations

- `block-beta` does not support `classDef` in all viewers. Focal emphasis may rely on naming or position.
- `block-beta` is not supported on GitHub as of early 2025. Use the `graph TB` fallback for maximum portability.

## Example (block-beta)

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
block-beta
columns 1
  app["Application\nReact + Next.js"]
  api["API\nGraphQL Gateway"]
  svc["Services\nNode.js microservices"]
  cache["Cache\nRedis"]
  db["Database\nPostgreSQL"]
```

## Example fallback (graph TB)

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
graph TB
    classDef focal fill:#fdf6f4,stroke:#b5523a,stroke-width:2px,color:#1c1917;
    classDef layer fill:#ffffff,stroke:#1c1917,stroke-width:1px,color:#1c1917;

    L1[Application<br/>React + Next.js] --> L2[API<br/>GraphQL Gateway]
    L2 --> L3[Services<br/>Node.js microservices]
    L3 --> L4[Cache<br/>Redis]
    L4 --> L5[Database<br/>PostgreSQL]

    class L3 focal;
    class L1,L2,L4,L5 layer;

%% Direction: abstraction increases upward
%% Focal: Services layer — where business logic lives
```
