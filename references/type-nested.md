# Nested Containment

**Best for:** hierarchy through containment — scope boundaries, config cascade, trust zones, folder nesting, blast radius. Outer = broader, inner = more specific.

## Syntax

Use `graph TD` + nested `subgraph` blocks. Mermaid supports nesting `subgraph` inside `subgraph` up to 2–3 levels reliably.

```mermaid
graph TD
    subgraph Outer [Global]
        subgraph Middle [Organization]
            subgraph Inner [Project]
                Core[Core Config]
            end
        end
    end
```

## Layout conventions

- 3–5 levels of nesting. Mermaid handles nesting visually with nested boxes.
- Each level labeled clearly. The outermost label should describe the broadest scope.
- Stroke hierarchy: Mermaid applies the same stroke to all subgraph borders by default. Use `classDef` on subgraph labels (nodes inside) to create visual hierarchy.
- Fills: `subgraph` background colors can be set via `themeVariables.clusterBkg` and `clusterBorder`, but individual subgraph colors are not configurable per-subgraph in most viewers.
- Coral on the innermost focal node, not the container itself.

## Anti-patterns

- More than 5 levels of nesting — information disappears inward.
- Empty subgraphs — every container should have at least one node.
- Coral on multiple levels — hierarchy collapses.
- Using nested containment to show sequence or flow — that's a flowchart.

## Limitations

- Deep nesting (>3 levels) may break layout in some viewers or produce unreadable diagrams.
- `subgraph` styling is global via `themeVariables`. You cannot color individual subgraph borders differently in standard Mermaid.
- For very deep hierarchies, consider a `tree` diagram or a bulleted list instead.

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
    'clusterBkg': '#f2ede4',
    'clusterBorder': 'rgba(28,25,23,0.12)',
    'fontFamily': 'Geist, sans-serif'
  }
}%%
graph TD
    classDef focal fill:#fdf6f4,stroke:#b5523a,stroke-width:2px,color:#1c1917;
    classDef node fill:#ffffff,stroke:#1c1917,stroke-width:1px,color:#1c1917;

    subgraph Global [Global Scope]
        subgraph Org [Organization]
            subgraph Team [Team]
                subgraph Repo [Repository]
                    Config[.editorconfig]
                end
            end
        end
    end

    class Config focal;

%% Outer = broadest scope
%% Inner = most specific (focal)
```
