# ADR 001: Choose a Relational Database for Transactional Domain Data

- **Status:** Accepted
- **Date:** 2026-09-25
- **Scope:** General
- **Related:** [HLD fundamentals](../../hld/fundamentals/README.md), [Case-study ADRs](../case-studies/)

## Context

Many systems need to store entities whose relationships and invariants matter: users, orders, accounts, permissions, or inventory. The design must support reliable updates, queries across related entities, and a clear consistency model without making every invariant an application-only responsibility.

This ADR is a reusable default for transactional domain data. It is not a claim that relational storage is the right choice for every workload.

## Requirements / Constraints

- Preserve invariants across related records.
- Support atomic transactions for multi-record updates.
- Provide expressive queries and well-understood indexing.
- Make schema and migration changes reviewable.
- Allow read scaling through replicas where eventual consistency is acceptable.

## Decision

Use a relational database as the system of record for transactional domain data. Model relationships explicitly, enforce critical invariants with constraints, and add indexes based on measured access patterns.

## Alternatives Considered

### Document Database

A document database can simplify storage for aggregate-shaped or rapidly changing records and can scale horizontally for some access patterns.

### Wide-Column Database

A wide-column database can provide high write throughput and predictable performance at very large scale when queries are known in advance.

### In-Memory Store

An in-memory store can provide very low latency, but it is better suited to caches, ephemeral state, and coordination than durable system-of-record data.

## Why This Decision

A relational database provides transactions, foreign keys, constraints, mature query capabilities, and operational tooling that directly support the stated requirements. It keeps important business invariants close to the data instead of distributing them across every application path.

The decision should be revisited when the workload is dominated by aggregate documents, requires globally distributed writes at extreme scale, or has access patterns that a relational model cannot serve efficiently.

## Trade-offs

The team accepts schema management, migration planning, and vertical scaling considerations in exchange for stronger integrity guarantees and flexible querying. Read replicas and careful indexing can extend read capacity, but writes still require attention to contention and partitioning strategy.

## Consequences

### Positive

- Related data and invariants have a clear, enforceable home.
- Transactions reduce partial-update failure modes.
- Query plans, indexes, backups, and migrations are well supported.

### Negative or Follow-up Work

- Schema changes require reviewed migrations.
- High write volume may require partitioning, sharding, or a specialized store later.
- Replicas introduce replication lag for read paths that do not require strong consistency.

## Related Concepts / References

- [HLD fundamentals](../../hld/fundamentals/README.md)
- [System Design Patterns](../../patterns/README.md)
- [PostgreSQL documentation](https://www.postgresql.org/docs/)
