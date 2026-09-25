<h1 align="center">system-design-mastery</h1>

----
<div align="center">
<a href="https://github.com/UdaySharmaGitHub/system-design-mastery/actions/workflows/ci.yml"><img src="https://github.com/UdaySharmaGitHub/system-design-mastery/actions/workflows/ci.yml/badge.svg" alt="CI"></a>
<a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT"></a>
<a href="CONTRIBUTING.md"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome"></a>
<a href="https://github.com/UdaySharmaGitHub/system-design-mastery/stargazers"><img src="https://img.shields.io/github/stars/UdaySharmaGitHub/system-design-mastery?style=social" alt="GitHub Stars"></a>
</div>

> **The free, open-source system design resource you wish existed.**
>
> One repo. One consistent format. High-Level Design, Low-Level Design, architecture patterns, real case studies, and interview prep — all in one place, explained end to end, contributed to by developers who actually build systems for a living.

<p align="center">
<a href="#explore-the-repository">Explore the repository</a> ·
<a href="#contributing">Contributing</a> ·
<a href="https://github.com/UdaySharmaGitHub/system-design-mastery/issues">Pick an issue</a>
</p>

<div align="center">
<img src="https://img.shields.io/badge/learning_paths-5-2563eb?style=flat-square" alt="Five learning paths">
<img src="https://img.shields.io/badge/format-structured-0f766e?style=flat-square" alt="Structured content format">
<img src="https://img.shields.io/badge/contributions-welcome-ea580c?style=flat-square" alt="Contributions welcome">
</div>

## Contents

- [Explore the repository](#explore-the-repository)
- [Why this exists](#why-this-exists)
- [The HLD ↔ LLD connection](#the-hld--lld-connection)
- [What makes this different](#what-makes-this-different)
- [How topics are structured](#how-topics-are-structured)
- [Contributing](#contributing)
- [Roadmap](#roadmap)
- [License](#license)

## Explore the Repository

Choose a path, open an issue, or improve a topic you already know well.

| Path | Best for | Start here |
|---|---|---|
| **High-Level Design** | Architecture, scale, data flow, and trade-offs | [Browse HLD](hld/README.md) |
| **Low-Level Design** | OOP, class diagrams, patterns, and code | [Browse LLD](lld/README.md) |
| **System Design Patterns** | Reusable building blocks such as rate limiting and CQRS | [Browse patterns](patterns/README.md) |
| **Case Studies** | End-to-end systems from requirements to implementation | [Browse case studies](case-studies/README.md) |
| **Architecture Decision Records** | Architectural choices, alternatives, trade-offs, and consequences | [Browse ADRs](architecture-decisions/README.md) |
| **Interview Playbook** | Clear, structured answers under interview pressure | [Browse interview prep](interview-prep/README.md) |

### Pick Your Next Step

| I want to... | Recommended action |
|---|---|
| Learn a new concept | Start with [HLD fundamentals](hld/fundamentals/README.md) or [LLD fundamentals](lld/fundamentals/README.md) |
| Practice a complete design | Explore the [case studies](case-studies/README.md) |
| Add a focused topic | Check the [roadmap](#roadmap), then claim an issue |
| Fix a typo or unclear explanation | Open a small [documentation PR](CONTRIBUTING.md) |
| Understand the contribution workflow | Read [CONTRIBUTING.md](CONTRIBUTING.md) |

----

## Why This Exists

Learning system design today means stitching together scattered blog posts, paywalled courses, YouTube explainers, and link-dump "awesome lists." None of them tell the full story. `system-design-mastery` is the place where that stitching is already done — no paywall, no inconsistency, no gaps between diagram and code.

----

## The HLD ↔ LLD Connection

Most resources teach HLD and LLD as separate tracks and leave you to figure out how they relate. This repo treats their connection as the core unit of learning.

Every case study is a bridge. The same system — the same requirements — is walked at both levels, so you see exactly which architectural choices in the HLD drive the class design in the LLD, and where the trade-offs land at each layer.

> **Example:** The URL Shortener flow below is illustrative; each case study will have its own HLD and LLD design.

```mermaid
flowchart TB
    START([URL Shortener])

    subgraph HLD[High-Level Design]
        direction TB
        HLD1[Load Balancer]
        HLD2[API Gateway]
        HLD3[Cache]
        HLD4[Database]
        HLD5[Replication]
        HLD1 --> HLD2 --> HLD3 --> HLD4 --> HLD5
    end

    subgraph LLD[Low-Level Design]
        direction TB
        LLD1[URLService]
        LLD2[ShortURL]
        LLD3[Repository]
        LLD4[Encoder]
        LLD5[CacheService]
        LLD1 --> LLD2 --> LLD3 --> LLD4 --> LLD5
    end

    START --> HLD
    START --> LLD
    HLD --> TRADEOFFS{Trade-offs}
    LLD --> TRADEOFFS
    TRADEOFFS --> END([Interview Answer])

    classDef start fill:#2563eb,color:#ffffff,stroke:#1d4ed8,stroke-width:2px
    classDef hld fill:#eff6ff,color:#1e3a8a,stroke:#60a5fa,stroke-width:1.5px
    classDef lld fill:#ecfdf5,color:#065f46,stroke:#34d399,stroke-width:1.5px
    classDef decision fill:#fff7ed,color:#9a3412,stroke:#fb923c,stroke-width:1.5px
    classDef finish fill:#0f766e,color:#ffffff,stroke:#0f766e,stroke-width:2px

    class START start
    class HLD1,HLD2,HLD3,HLD4,HLD5 hld
    class LLD1,LLD2,LLD3,LLD4,LLD5 lld
    class TRADEOFFS decision
    class END finish
    style HLD fill:#f8fbff,stroke:#93c5fd,stroke-width:1px,color:#1e3a8a
    style LLD fill:#f0fdf4,stroke:#86efac,stroke-width:1px,color:#065f46
```

**Why this matters:** In an interview — and on the job — you are never asked to design only one layer. You are asked to design a *system*. This repo trains you to think that way.

----

## What Makes Each Topic Useful

| Section | What you'll find |
|---|---|
| **High-Level Design (HLD)** | Scalability, load balancers, caching, databases, message queues, and the trade-offs between them |
| **Low-Level Design (LLD)** | Class structures, interfaces, OOP design principles, and working code |
| **System Design Patterns** | Rate limiting, consistent hashing, leader election, and other reusable building blocks |
| **Case Studies** | URL shortener, chat system, notification system, feed ranking — walked from requirements to architecture to code |
| **Interview Playbook** | How to structure a 45-minute system design answer under real interview pressure |

----

## What Makes This Different

Two things this repo does that most system design resources skip entirely:

**Production Reality** — every case study covers what actually breaks in production, not just the happy path. Each topic answers: what happens if Redis goes down? What happens when traffic spikes 100×? What happens if a Kafka partition becomes a hot partition? Scalability, reliability, security, and observability are treated as first-class parts of the design — not afterthoughts.

**Why NOT?** — every significant architectural decision includes the alternatives that were rejected and the reasoning behind the choice. Why Redis over Memcached? Why Kafka over a simple job queue? Why a hash-based short URL over a sequential counter? Explicit trade-off reasoning, not just assertions. This is what separates an engineer who can recite an architecture from one who can defend it.

----

## How Topics Are Structured

Every entry follows the same path, so readers can move from the problem to the trade-offs without hunting for context:

```mermaid
flowchart LR
    A([Problem statement]) --> B[Requirements]

    subgraph DESIGN[Design the system]
        direction LR
        C[High-Level Design] --> D[Low-Level Design & code]
    end

    B --> C
    D --> E{Trade-offs}
    E --> F([Interview angle])

    classDef start fill:#2563eb,color:#ffffff,stroke:#1d4ed8,stroke-width:2px
    classDef core fill:#eff6ff,color:#1e3a8a,stroke:#60a5fa,stroke-width:1.5px
    classDef decision fill:#fff7ed,color:#9a3412,stroke:#fb923c,stroke-width:1.5px
    classDef finish fill:#0f766e,color:#ffffff,stroke:#0f766e,stroke-width:2px

    class A start
    class B,C,D core
    class E decision
    class F finish
    style DESIGN fill:#f8fafc,stroke:#cbd5e1,stroke-width:1px,color:#334155
```

No diagrams without reasoning. No code without context. See the [contributor standards](CONTRIBUTING.md#content-standards) before adding a topic.

----

## Getting Started

No installation required — this is a documentation and learning repository. To use it:

```bash
# Clone the repo
git clone https://github.com/UdaySharmaGitHub/system-design-mastery.git

# Navigate into it
cd system-design-mastery

# Browse topics — start anywhere that interests you
```

Or [browse it directly on GitHub](https://github.com/UdaySharmaGitHub/system-design-mastery).

## Contributing

### Contribute in a Few Minutes

Every contribution helps make a difficult subject easier to learn. You do not need to be a senior engineer; a precise explanation, corrected diagram, useful example, or thoughtful review is valuable.

| Contribution | Fastest route |
|---|---|
| Report an error or gap | Open a [Bug Report](.github/ISSUE_TEMPLATE/bug_report.md) |
| Request a topic | Open a [Feature Request](.github/ISSUE_TEMPLATE/feature_request.md) |
| Claim a roadmap item | Find an open issue and comment before starting |
| Improve existing content | Read [CONTRIBUTING.md](CONTRIBUTING.md), then open a focused PR |
| Review a contribution | Check the [open pull requests](https://github.com/UdaySharmaGitHub/system-design-mastery/pulls) |

```bash
# Fork, clone, and create a focused branch
git clone https://github.com/<your-username>/system-design-mastery.git
cd system-design-mastery
git checkout -b docs/clear-topic-explanation

# Validate Markdown before opening a PR
markdownlint "**/*.md" --ignore node_modules
```

See the [pull request template](.github/pull_request_template.md) for the review checklist and the [Code of Conduct](CODE_OF_CONDUCT.md) for community expectations.

### Community Links

- [Contribution guide](CONTRIBUTING.md) — workflow, branch names, and content standards
- [Code of Conduct](CODE_OF_CONDUCT.md) — expectations for respectful collaboration
- [Security policy](SECURITY.md) — please do **not** open a public issue for security reports
- [Changelog](CHANGELOG.md) — notable project updates

----

## Roadmap

- [ ] Repo structure, contribution guide, and issue templates
- [ ] HLD fundamentals (scaling, load balancing, caching, databases, queues)
- [ ] LLD fundamentals (OOP principles, common design patterns, class-diagram conventions)
- [ ] First 5 fully worked case studies (URL shortener, rate limiter, chat system, notification system, feed ranking)
- [ ] System design interview playbook
- [ ] Ongoing: new case studies and patterns as the community contributes them

Track progress and claim topics on the [Issues tab](https://github.com/UdaySharmaGitHub/system-design-mastery/issues).

----

## License

MIT — see [LICENSE](LICENSE). Use it, fork it, learn from it. No restrictions.
