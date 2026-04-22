# Quadrant

**Best for:** prioritization (Impact × Effort), positioning (Reach × Frequency), portfolio maps, 2×2 decision frames.

## Syntax

```mermaid
quadrantChart
    title Reach and engagement of campaigns
    x-axis Low Reach --> High Reach
    y-axis Low Engagement --> High Engagement
    quadrant-1 We should expand
    quadrant-2 Need to promote
    quadrant-3 Re-evaluate
    quadrant-4 May be improved
    Campaign A: [0.3, 0.6]
    Campaign B: [0.45, 0.23]
```

**Keywords:**
- `title` — chart title.
- `x-axis Label --> Label` — horizontal axis. Left = low, right = high.
- `y-axis Label --> Label` — vertical axis. Bottom = low, top = high.
- `quadrant-N Label` — label for each quadrant (1 = top-right, 2 = top-left, 3 = bottom-left, 4 = bottom-right).
- `Item Name: [x, y]` — data point. x and y are 0.0–1.0.

## Layout conventions

- Axis labels at the ends, never at the midpoint.
- Items: small labeled dots positioned by `[x, y]`. Labels should not overlap.
- The "do first" item (typically top-right) is the natural focal point. No `classDef` needed — position is the signal.
- Limit to ~12 items. Cluster or split beyond that.
- Name items clearly; avoid cryptic acronyms.

## Anti-patterns

- Four filled quadrants in different colors — position + label does the work; color noise weakens it.
- Items placed exactly on axis lines (ambiguous quadrant). Offset slightly if needed.
- Missing axis names — readers can't interpret the chart.
- Too many items in one quadrant — the chart becomes a list.

## Example

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
quadrantChart
    title Q2 Projects by Impact vs Effort
    x-axis Low Effort --> High Effort
    y-axis Low Impact --> High Impact
    quadrant-1 Do First
    quadrant-2 Quick Wins
    quadrant-3 Deprioritize
    quadrant-4 Strategic Bets
    Auth rewrite: [0.2, 0.8]
    Dark mode: [0.3, 0.6]
    API v2: [0.7, 0.9]
    Mobile app: [0.8, 0.4]
    Onboarding revamp: [0.4, 0.7]
    Docs update: [0.2, 0.3]
```

## Note on focal signal

`quadrantChart` does not support individual point styling. The focal signal comes from:
1. **Position** — top-right is the implicit priority zone.
2. **Naming** — the most important item should have the clearest name.
3. **Quadrant label** — name quadrant-1 something active like "Do First" or "Ship Now".
