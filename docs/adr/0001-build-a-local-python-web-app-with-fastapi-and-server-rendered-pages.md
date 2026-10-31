---
status: Accepted
owner: "Oleksii Smoliankin"
reviewers: []
updated_at: "2026-10-31"
feature_size: "n/a (foundation)"
ticket: "n/a"
---

# 0001 — Build a local Python web app with FastAPI and server-rendered pages

- **Status:** Accepted
- **Date:** 2026-10-31
- **Deciders:** Oleksii Smoliankin (owner), with Claude during `survey` (guided-default)

## Context

The repo is empty. The idea brief describes a personal expense tracker for one user on one computer: an entry form, an editable list, totals per category, and spending over time. A language, framework, and UI approach must be chosen before anything can be scaffolded. Changing them later means a rewrite.

## Decision drivers

- Single user, one computer, data entered in batches (brief §3). No phone or multi-device need.
- No required technology or deadline (brief §4/§5).
- The UI is forms, tables, and a few charts, so it needs no rich client-side interaction.
- Already installed: Python 3.12, Node 22, Go 1.22.

## Considered options

1. **Python 3.12 + FastAPI + Jinja2 server-rendered pages + Chart.js**: one language and no frontend build step.
2. **TypeScript on Node 22 (Express/Fastify) + server templates + Vitest**: the same shape in JS/TS.
3. **Go 1.22 standard-library server + html/template**: a single compiled binary, more code to write.

## Decision outcome

**Chosen:** Option 1. The owner accepted the recommended set. It meets the form/list/chart needs with the least moving parts (one language, no JS toolchain), and it runs locally with one command.

## Consequences

**Positive**
- Simple to run and to test end to end (`TestClient`).
- No frontend build pipeline to maintain.

**Negative**
- Every interaction is a full page load; rich interactivity would need extra JS later.
- Needs a Python virtualenv to run; it's not a single binary.

**Neutral**
- If phone or multi-device use is wanted later, the app could be hosted, but that would need authentication first.

## Links

- Brief: [[../idea-brief.md]]
- Architecture map: [[../architecture-map.md]] §Stack
- Related ADR: [[0002-store-data-in-a-local-sqlite-file-with-sqlalchemy-and-alembic]], [[0003-organize-the-app-as-one-package-split-into-web-domain-and-db-layers]]
