# Architecture Decision Records

Architecture Decision Records (ADRs) capture important choices made while designing a system. Each record explains the context, constraints, alternatives, decision, trade-offs, and consequences so that readers can understand not only what was chosen, but why.

ADRs are decision records, not generic technology guides. A database-selection guide compares databases in general; an ADR answers which database fits a particular system and its requirements.

## Why This Repository Uses ADRs

System design is more than drawing components. The most useful learning happens when an architectural choice is tied to explicit requirements and defended against realistic alternatives.

ADRs help contributors and readers:

- make architectural reasoning visible and reviewable
- connect requirements to HLD and LLD decisions
- preserve rejected alternatives and their trade-offs
- revisit decisions when requirements or scale assumptions change
- practice the explanation expected in a system design interview

## General vs. Case-Study ADRs

| Location | Purpose | Example |
|---|---|---|
| [`general/`](general/) | Reusable decisions that apply across many systems | Choosing a relational database for transactional workloads |
| [`case-studies/`](case-studies/) | Decisions made for one specific system and its requirements | Choosing a key-value store for a URL Shortener |

A general ADR should stay broadly reusable. A case-study ADR should name the system, state its assumptions, and avoid presenting a local decision as a universal rule.

## When to Create an ADR

Create an ADR when a decision:

- significantly affects scalability, reliability, security, cost, or operability
- has meaningful alternatives that a contributor or reader might reasonably choose
- changes the shape of an HLD, LLD, pattern, or case study
- is useful to revisit if requirements or constraints change

Do not create an ADR for a minor implementation detail, a generic product explanation, or a decision with no meaningful trade-off. Start with an [Architecture Decision issue](../.github/ISSUE_TEMPLATE/architecture_decision.md) when the question needs discussion before the decision is finalized.

## How ADRs Connect to the Repository

- **HLD** describes the system architecture and major component interactions.
- **LLD** describes classes, interfaces, and implementation structure.
- **Patterns** explain reusable system-level building blocks.
- **Case Studies** walk through a complete system from requirements to design.
- **ADRs** record the important choices that connect those layers to specific constraints.

Link a relevant ADR from the HLD, LLD, pattern, or case-study document. Link back to those documents from the ADR when the decision depends on their context.

## Structure and Naming

- General ADRs use `architecture-decisions/general/<number>-<short-kebab-case-title>.md`.
- Case-study ADRs use `architecture-decisions/case-studies/<system-name>/<number>-<short-kebab-case-title>.md`.
- Use three-digit, zero-padded numbers beginning at `001` within each directory.
- Numbers are never reused, even if an ADR is superseded or rejected.
- Keep the filename short and describe the decision, not only the technology.
- Copy [`template.md`](template.md) for every new ADR.

### Example Structure

```text
architecture-decisions/
│
├── general/
│   ├── 001-caching-strategy.md
│   ├── 002-message-queue-selection.md
│   ├── 003-id-generation.md
│   └── 004-api-versioning.md
│
└── case-studies/
    ├── url-shortener/
    │   └── 001-database-selection.md
    │
    ├── payment-system/
    │   └── 001-database-selection.md
    │
    └── chat-system/
        └── 001-message-storage.md
```

Suggested statuses are `Proposed`, `Accepted`, `Rejected`, `Deprecated`, and `Superseded`.

## Example Decisions

- [`001-database-selection.md`](general/001-database-selection.md) explains when a relational database is a good general default for transactional systems.
- [`case-studies/url-shortener/001-database-selection.md`](case-studies/url-shortener/001-database-selection.md) applies a database decision to the URL Shortener's access patterns, consistency needs, and scale assumptions.

The second example is intentionally not a copy of the first: the system's requirements determine the decision.

## ADR Template

Use [`template.md`](template.md) as the starting point. Discuss the architectural question in an issue first when the alternatives or constraints are still unclear.
