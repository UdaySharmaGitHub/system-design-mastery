# ADR 001: Use a Relational Database as the URL Shortener Source of Truth

- **Status:** Accepted
- **Date:** 2026-09-25
- **Scope:** URL Shortener case study
- **Related:** [Case studies](../../../case-studies/README.md), [HLD case studies](../../../hld/case-studies/README.md), [General database-selection ADR](../../general/001-database-selection.md)

## Context

The URL Shortener creates a short code for a submitted long URL and resolves that code on every redirect. The core record maps one short code to one destination URL and may include ownership, creation time, expiration, and status metadata.

The illustrative design assumes that redirects are read-heavy, short codes must be unique, and a newly created mapping should be immediately reliable. A cache may accelerate popular redirects, but the durable mapping must remain recoverable when the cache is cold or unavailable.

## Requirements / Constraints

- Guarantee uniqueness of each short code.
- Keep a newly created mapping durable before returning success.
- Support point lookups by short code with low latency.
- Support expiration, ownership, and administrative queries.
- Scale reads independently through caching and read replicas where appropriate.
- Preserve the mapping if the cache is unavailable.

## Decision

Use a relational database as the durable source of truth for URL mappings. Store the short code under a unique constraint, store the destination URL and lifecycle metadata in the same record, and use a cache as a read-through acceleration layer rather than as the authoritative store.

## Alternatives Considered

### Key-Value Database

A key-value database matches the dominant lookup pattern of `short_code -> destination_url` and can scale point reads horizontally with simple access paths.

### Document Database

A document database could store the mapping and optional metadata without a rigid schema, but the current case study does not need document-specific flexibility.

### Cache as the Primary Store

Keeping mappings only in a cache would minimize redirect latency but would make cache eviction, outage, or data loss an availability and correctness problem.

## Why This Decision

The URL Shortener needs a unique short-code invariant, durable creation, and lifecycle metadata in addition to fast reads. A relational database provides the unique constraint and transactional write needed for creation, while the cache absorbs repeated redirect traffic.

This choice is intentionally scoped to the case-study assumptions. If the system grows to an extreme global read volume with a simple, immutable mapping and a mature multi-region strategy, a key-value database could become a better source of truth.

## Trade-offs

The relational model adds schema and write-path operational work compared with a simple key-value store. In return, it provides strong uniqueness guarantees, flexible administrative queries, and a durable fallback below the cache. Read replicas and cache warming can increase capacity, but cache invalidation and replica lag must be handled explicitly.

## Consequences

### Positive

- Duplicate short codes are rejected by the database rather than relying only on application checks.
- Cache misses and cache outages can fall back to durable storage.
- Expiration, ownership, and administrative queries remain straightforward.

### Negative or Follow-up Work

- Redirect latency depends on database capacity during cache misses.
- High-volume writes or global traffic may require partitioning, replicas, or a later database migration.
- The cache needs an invalidation and expiration policy that does not compromise correctness.

## Related Concepts / References

- [URL Shortener case study](../../../case-studies/README.md)
- [General database-selection ADR](../../general/001-database-selection.md)
- [Caching fundamentals](../../../hld/fundamentals/README.md)
