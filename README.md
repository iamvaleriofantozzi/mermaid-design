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

This skill uses the **open SKILL.md standard** — a single `SKILL.md` file with YAML frontmatter inside a named folder. It works natively across Claude Code, OpenCode, GitHub Copilot CLI (Codex), Antigravity, and any other agent that follows the same convention. No separate versions needed.

### Claude Code

**Skills directory:**
```bash
git clone git@github.com:iamvaleriofantozzi/mermaid-design.git ~/.claude/skills/mermaid-design
```
Restart Claude Code. The skill registers as `mermaid-design`.

**Plugin marketplace:**
```bash
/plugin marketplace add iamvaleriofantozzi/mermaid-design
/plugin install mermaid-design@mermaid-design
```

### OpenCode / Paseo

```bash
git clone git@github.com:iamvaleriofantozzi/mermaid-design.git ~/.config/opencode/skills/mermaid-design
# or
ln -s ~/.claude/skills/mermaid-design ~/.config/opencode/skills/mermaid-design
```
OpenCode also searches `.claude/skills/` and `.agents/skills/` automatically, so sharing the same clone with Claude Code works out of the box.

### GitHub Copilot CLI (Codex)

**Project-level** (inside your repo):
```bash
git clone git@github.com:iamvaleriofantozzi/mermaid-design.git .github/skills/mermaid-design
# or
ln -s ~/.claude/skills/mermaid-design .github/skills/mermaid-design
```

**Personal** (global):
```bash
git clone git@github.com:iamvaleriofantozzi/mermaid-design.git ~/.copilot/skills/mermaid-design
# or
ln -s ~/.claude/skills/mermaid-design ~/.copilot/skills/mermaid-design
```
Run `/skills reload` in the CLI if already open.

### Antigravity

**Project-level:**
```bash
git clone git@github.com:iamvaleriofantozzi/mermaid-design.git .agents/skills/mermaid-design
```

**Global:**
```bash
git clone git@github.com:iamvaleriofantozzi/mermaid-design.git ~/.gemini/antigravity/skills/mermaid-design
```

### Manual use

You don't need an AI agent to use this. Copy any example from [`examples/`](examples/) and paste it into the [Mermaid Live Editor](https://mermaid.live/).

---

## Quickstart

```
Make me a flowchart of the login flow: start, validate input, check credentials,
return token or error.
```

Your agent will pick the right type, build the Mermaid code, and output it wrapped in triple backticks. Paste it into GitHub, Notion, Obsidian, or any Mermaid-compatible viewer.

```
Make me a sequence diagram of the OAuth handshake in dark mode.
```

The agent will use the dark token palette and set the init block accordingly.

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

Progressive disclosure. `SKILL.md` is a lean index — it tells the agent how to pick a type and where to look for detail. Every type lives in its own reference file, loaded only when relevant.

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

This keeps the agent's working context tight (only load what you need) and makes the skill easy to extend.

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

## Examples

### Flowchart — User login flow with validation

**Scenario:** A user submits credentials, passes format and password checks, optionally completes 2FA, and is granted a session—or rejected at any failure gate.

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

%% Legend:
%% ■ Focal (coral) — successful session grant
%% □ Backend — process step
```

---

### Sequence — OAuth2 handshake (4 actors)

**Scenario:** A user initiates login through a client, the authorization server issues a code and exchanges it for an access token, and the client calls a protected API.

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

%% Legend:
%% AuthServer is the focal authority
%% Actors: User, Client, AuthServer, API
```

---

### Architecture — Web app → API → services → database

**Scenario:** A single-page web app reaches an API gateway that routes traffic to domain services, each reading from a shared PostgreSQL database and a Redis cache.

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

%% Legend:
%% ■ Focal (coral) — primary service
%% □ Backend — service / gateway
%% ▤ Store — database / cache
```

---

### State — Order lifecycle

**Scenario:** An order moves from draft to pending approval, then through publish to archive, with each transition triggered by an explicit business event.

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

%% Legend:
%% Published is the focal milestone
%% Standard states: Draft, Pending, Approved, Archived
```

---

### ER — E-commerce model

**Scenario:** A customer places orders containing line items, each line item linking to a product, forming a normalized e-commerce domain model.

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
        datetime created_at
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
        decimal price
    }

%% Legend:
%% Central entity: ORDER (aggregate root)
%% || one  ○ zero  { many
```

---

### Timeline — Product roadmap 2023–2024

**Scenario:** A startup ships a public beta in 2023, releases v1.0 and enterprise features in 2024, and closes a Series A by year end.

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
timeline
    title Product Roadmap 2023–2024
    2023 Q1 : Seed funding
            : Core team hired
    2023 Q3 : Public beta launch
    2024 Q1 : V1.0 RELEASE
    2024 Q2 : Enterprise features
            : SOC 2 compliance
    2024 Q4 : Series A

%% Focal milestones: V1.0 RELEASE, Series A
```

---

### Quadrant — Q2 projects by Impact vs Effort

**Scenario:** Six proposed Q2 initiatives are plotted to reveal quick wins, strategic bets, and items that should be deferred.

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

%% Focal: Auth rewrite (Quick Win — high impact, low effort)
%% Top-right position = Do First priority
```

---

### Tree — API gateway dependency tree

**Scenario:** The API gateway fans out to three downstream services, with the order service depending on Redis and PostgreSQL, and the user service depending on Kafka.

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

%% Legend:
%% ■ Focal (coral) — primary downstream service
%% □ Backend — service
%% ▤ Store — database / cache / queue
```

---

### Swimlane — Design → Engineering → QA → Deploy

**Scenario:** A feature moves through four functional lanes, from design specs to production deployment, with code review and testing as explicit gates.

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

%% Legend:
%% ■ Focal (coral) — critical implementation step
%% □ Backend — process step
```

---

### Layer stack — Full-stack application layers

**Scenario:** A modern stack is shown as five descending layers, from the React client down through gateway, services, cache, and PostgreSQL.

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

%% Direction: requests flow downward
%% Focal: Services layer — core business logic
```

---

### Nested — Config cascade (Global → Org → Team → Repo)

**Scenario:** Configuration resolution narrows from global defaults through organization and team scopes, ending at the most specific repository-level file.

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

%% Legend:
%% ■ Focal (coral) — most specific config file
%% □ Node — scoped container
```

---

## License

MIT
