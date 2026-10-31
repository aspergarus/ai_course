---
status: Accepted
owner: "Oleksii Smoliankin"
reviewers: []
updated_at: "2026-10-31"
feature_size: "n/a (foundation)"
ticket: "n/a"
---

# 0002 — Store data in a local SQLite file with SQLAlchemy and Alembic

- **Status:** Accepted
- **Date:** 2026-10-31
- **Deciders:** Oleksii Smoliankin (owner), with Claude during `survey` (guided-default)

## Context

Expenses must persist between runs and support listing, per-category totals, and totals over time periods. The storage engine and how the schema evolves are hard to change once real data exists.

## Decision drivers

- One user, one computer (brief §3): no concurrent writers, no server.
- Aggregations (sum by category, sum by period) are natural in SQL.
- Backup should be trivial for a personal tool.

## Considered options

1. **SQLite file + SQLAlchemy 2.x + Alembic migrations**: an embedded relational DB with versioned schema changes.
2. **PostgreSQL server (e.g. in Docker)**: more capable, but a server to run for one user.
3. **JSON/CSV file**: simplest, but aggregation and safe concurrent edits are hand-written.

## Decision outcome

**Chosen:** Option 1. SQL aggregation with zero infrastructure; the Python driver is built in; backup means copying one file. Alembic keeps schema changes versioned and reversible.

## Consequences

**Positive**
- No DB server; tests use a real SQLite file, so there's no mocking and no Docker.
- Money as integer cents and simple integer IDs fit SQLite well.

**Negative**
- SQLite has limited `ALTER TABLE`, so some Alembic migrations need batch mode.
- Not suitable as-is if the app later becomes multi-user and hosted.

**Neutral**
- Moving to PostgreSQL later is possible through SQLAlchemy but would need a data migration.

## Links

- Brief: [[../idea-brief.md]]
- Architecture map: [[../architecture-map.md]] §Datastores
- Related ADR: [[0001-build-a-local-python-web-app-with-fastapi-and-server-rendered-pages]]
