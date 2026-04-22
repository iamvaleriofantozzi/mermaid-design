# Mermaid Design 🎨

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

This skill uses the **open SKILL.md standard** — a single `SKILL.md` file with YAML frontmatter inside a named folder. Works natively across Claude Code, OpenCode, GitHub Copilot CLI (Codex), Antigravity, and any other agent that follows the same convention. No separate versions needed.

### Claude Code
```bash
git clone git@github.com:iamvaleriofantozzi/mermaid-design.git ~/.claude/skills/mermaid-design
```
Restart Claude Code. The skill registers as `mermaid-design`.

### OpenCode / Paseo
```bash
git clone git@github.com:iamvaleriofantozzi/mermaid-design.git ~/.config/opencode/skills/mermaid-design
# or symlink from Claude Code
ln -s ~/.claude/skills/mermaid-design ~/.config/opencode/skills/mermaid-design
```

### GitHub Copilot CLI (Codex)
```bash
# Project-level
git clone git@github.com:iamvaleriofantozzi/mermaid-design.git .github/skills/mermaid-design
# Personal (global)
git clone git@github.com:iamvaleriofantozzi/mermaid-design.git ~/.copilot/skills/mermaid-design
```

### Antigravity
```bash
git clone git@github.com:iamvaleriofantozzi/mermaid-design.git .agents/skills/mermaid-design
```

### Manual use
Copy any example below and paste it into the [Mermaid Live Editor](https://mermaid.live/).

---

## Quickstart

```
Make me a flowchart of the login flow: start, validate input, check credentials,
return token or error.
```

Your agent picks the right type, builds the Mermaid code, and outputs it wrapped in triple backticks. Paste it into any Mermaid-compatible viewer.

```
Make me a sequence diagram of the OAuth handshake in dark mode.
```

The agent uses the dark token palette and sets the init block accordingly.

---

## Examples

### Flowchart — Login flow with validation

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
graph TD
    classDef focal fill:#fdf6f4,stroke:#b5523a,stroke-width:2px,color:#1c1917;
    classDef backend fill:#ffffff,stroke:#1c1917,stroke-width:1px,color:#1c1917;

    Start([Start]) --> Submit[Submit credentials]
    Submit --> Validate{Format valid?}
    Validate -->|Yes| CheckPW[Check password]
    Validate -->|No| Reject[Return 401]
    CheckPW -->|OK| TwoFA{2FA enabled?}
    CheckPW -->|Fail| Reject
    TwoFA -->|Yes| Verify[Verify token]
    TwoFA -->|No| Grant[Grant session]
    Verify --> Grant
    Grant --> End([End])
    Reject --> End

    class Grant focal;
    class Submit,CheckPW,Verify,Reject backend;
```

### Sequence — OAuth2 handshake

```mermaid
%%{init: {
  'theme': 'base',
  'themeVariables': {
    'actorBkg': '#faf7f2',
    'actorBorder': '#1c1917',
    'actorTextColor': '#1c1917',
    'actorLineColor': '#57534e',
    'signalColor': '#1c1917',
    'signalTextColor': '#1c1917',
    'labelBoxBkgColor': '#faf7f2',
    'labelBoxBorderColor': '#57534e',
    'labelTextColor': '#1c1917',
    'loopTextColor': '#1c1917',
    'noteBorderColor': '#57534e',
    'noteBkgColor': '#f2ede4',
    'noteTextColor': '#1c1917',
    'activationBorderColor': '#57534e',
    'activationBkgColor': '#f2ede4',
    'fontFamily': 'Geist, sans-serif'
  }
}%%
sequenceDiagram
    participant U as User
    participant C as Client
    participant A as AuthServer
    participant R as API

    U->>C: Click login
    C->>A: Request auth
    A->>U: Redirect login
    U->>A: Credentials
    A-->>C: Auth code
    C->>+A: Exchange code
    A-->>-C: Access token
    C->>R: Request data
    R-->>C: Protected data
```

### Architecture — Web app stack

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
graph LR
    classDef focal fill:#fdf6f4,stroke:#b5523a,stroke-width:2px,color:#1c1917;
    classDef backend fill:#ffffff,stroke:#1c1917,stroke-width:1px,color:#1c1917;
    classDef store fill:#f5f4f3,stroke:#57534e,stroke-width:1px,color:#1c1917;

    Web[Web App] --> API[API Gateway]
    API --> Orders[Order Service]
    API --> Users[User Service]
    Orders --> Cache[(Redis)]
    Orders --> DB[(PostgreSQL)]
    Users --> DB

    class Orders focal;
    class Web,API,Users backend;
    class Cache,DB store;
```

### State — Order lifecycle

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
stateDiagram-v2
    [*] --> Draft
    Draft --> Pending : submit
    Pending --> Approved : approve
    Approved --> Published : publish
    Published --> Archived : archive
    Archived --> [*]
```

### ER — E-commerce model

```mermaid
erDiagram
    CUSTOMER ||--o{ ORDER : places
    CUSTOMER {
        int id PK
        string email UK
        string name
    }
    ORDER ||--|{ LINE_ITEM : contains
    ORDER {
        int id PK
        int customer_id FK
        string created_at
        string status
    }
    LINE_ITEM {
        int id PK
        int order_id FK
        int product_id FK
        int quantity
    }
    PRODUCT ||--o{ LINE_ITEM : "ordered in"
    PRODUCT {
        int id PK
        string sku UK
        string name
        float price
    }
```

### Timeline — Product roadmap

```mermaid
timeline
    title Product Roadmap 2023-2024
    2023 Q1 : Seed funding
            : Core team hired
    2023 Q3 : Public beta launch
    2024 Q1 : V1.0 RELEASE
    2024 Q2 : Enterprise features
            : SOC 2 compliance
    2024 Q4 : Series A
```

### Quadrant — Q2 prioritization

```mermaid
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

### Tree — API gateway dependencies

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
graph TD
    classDef focal fill:#fdf6f4,stroke:#b5523a,stroke-width:2px,color:#1c1917;
    classDef backend fill:#ffffff,stroke:#1c1917,stroke-width:1px,color:#1c1917;
    classDef store fill:#f5f4f3,stroke:#57534e,stroke-width:1px,color:#1c1917;

    API[API Gateway] --> Auth[Auth Service]
    API --> Order[Order Service]
    API --> User[User Service]
    Order --> Cache[(Redis)]
    Order --> DB[(PostgreSQL)]
    User --> Events[(Kafka)]

    class Order focal;
    class Auth,User backend;
    class Cache,DB,Events store;
```

### Swimlane — Feature delivery

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
graph LR
    classDef focal fill:#fdf6f4,stroke:#b5523a,stroke-width:2px,color:#1c1917;
    classDef backend fill:#ffffff,stroke:#1c1917,stroke-width:1px,color:#1c1917;

    subgraph Design [Design]
        D1[Design specs]
    end
    subgraph Engineering [Engineering]
        E1[Build feature]
        E2[Code review]
    end
    subgraph QA [QA]
        Q1[Run tests]
    end
    subgraph Deploy [Deploy]
        P1[Deploy to prod]
    end

    D1 --> E1
    E1 --> E2
    E2 --> Q1
    Q1 --> P1

    class E1 focal;
    class D1,E2,Q1,P1 backend;
```

### Layer stack — Full-stack layers

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

    L1[Client<br/>React + Vite] --> L2[Gateway<br/>Kong / Nginx]
    L2 --> L3[Services<br/>Node.js + gRPC]
    L3 --> L4[Cache<br/>Redis Cluster]
    L4 --> L5[Database<br/>PostgreSQL]

    class L3 focal;
    class L1,L2,L4,L5 layer;
```

### Nested — Config cascade

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
                    Config[config.yaml]
                end
            end
        end
    end

    class Config focal;
```

---

## Viewer compatibility

| Feature | GitHub | Notion | Obsidian | GitLab | VS Code |
|---|---|---|---|---|---|
| `%%{init}%%` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `theme: base` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `classDef` (flowchart) | ✅ | ✅ | ✅ | ✅ | ✅ |
| `architecture-beta` | ❓ | ❓ | ❓ | ❓ | ✅ |
| `quadrantChart` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `timeline` | ✅ | ✅ | ✅ | ✅ | ✅ |
| `mindmap` | ❓ | ❓ | ✅ | ❓ | ✅ |
| `block-beta` | ❓ | ❓ | ❓ | ❓ | ✅ |

### Mermaid version requirements

Some diagram types need a recent Mermaid version. Older apps (e.g., MarkText, legacy VS Code extensions, Jekyll themes) may ship an outdated Mermaid engine and show "Invalid Mermaid code" even for valid syntax.

| Diagram type | Min Mermaid version | Status |
|---|---|---|
| `flowchart` / `graph` | v8.0+ | Universal |
| `sequenceDiagram` | v8.0+ | Universal |
| `stateDiagram-v2` | v9.0+ | Widely supported |
| `erDiagram` | v9.0+ | Widely supported |
| `timeline` | v9.4+ | Fails on older apps |
| `quadrantChart` | v10.6+ | Fails on older apps |
| `architecture-beta` | v10.9+ | Experimental |
| `mindmap` | v9.4+ | Partial support |
| `block-beta` | v10.6+ | Partial support |

> **Tip:** If a diagram renders on [mermaid.live](https://mermaid.live/) but not in your app, the app is likely running an outdated Mermaid version.

---

## License

MIT

---

Made with care by **Valerio Fantozzi** 🦄
