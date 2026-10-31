---
status: Accepted
owner: "Oleksii Smoliankin"
reviewers: []
updated_at: "2026-10-31"
feature_size: "n/a (foundation)"
ticket: "n/a"
---

# 0003 — Organize the app as one package split into web, domain, and db layers

- **Status:** Accepted
- **Date:** 2026-10-31
- **Deciders:** Oleksii Smoliankin (owner), with Claude during `survey` (guided-default)

## Context

Every future feature needs a predictable place for its routes, rules, and persistence. The structure is set once at scaffold time and copied by each feature.

## Decision drivers

- Small app, single process (brief scope): heavy architecture would be overhead.
- Domain rules (money in cents, totals, periods) should be unit-testable without a DB or HTTP.

## Considered options

1. **One `app/` package with `web/`, `domain/`, and `db/` layers**; dependencies point into `domain`.
2. **Full hexagonal modules (`modules/<m>/{domain,app,infra,ports}`)**: stronger isolation, too much ceremony for a few features.
3. **Flat single-file app**: fastest start, but rules, SQL, and HTML get tangled as features grow.

## Decision outcome

**Chosen:** Option 1. It keeps rules testable in isolation while staying small. Each feature adds one file per layer.

## Consequences

**Positive**
- Clear home for each kind of code; domain logic is unit-tested without fixtures.

**Negative**
- A little indirection (repository functions) compared with querying straight from routes.

**Neutral**
- Can be split into per-feature modules later if the app grows.

## Links

- Architecture map: [[../architecture-map.md]] §Module inventory
- Related ADR: [[0001-build-a-local-python-web-app-with-fastapi-and-server-rendered-pages]]
