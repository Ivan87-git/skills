---
name: update-feature-docs
description: Update durable feature documentation so behavior and implementation decisions are understandable without reverse-engineering code. Use when the user says "/update-feature-docs", after implementing a feature or bug fix, when behavior changes, or when implementation choices should be documented alongside code.
---

# Update Feature Docs

Use this skill to keep product behavior and implementation knowledge current as code changes.

Feature docs are not PRDs. A PRD describes what we intend to build. A feature doc describes what the application now does.

## Where Documentation Lives

Prefer `docs/features/<feature-slug>.md` for durable behavior documentation.

Use other docs only for their specific purpose:

- `CONTEXT.md` — domain vocabulary and relationships only.
- `docs/adr/` — hard-to-reverse decisions with real trade-offs.
- `README.md` or package docs — setup, runtime, deployment, integration, or public usage.
- `docs/agents/` — agent workflow configuration only.

Create `docs/features/` lazily when the first feature doc is needed.

## Process

### 1. Gather Inputs

Read the relevant source material: PRD, issue, implementation diff, tests, related `CONTEXT.md` terms, and related ADRs.

If there is no existing feature doc, infer the feature slug from the issue, branch, route, module, or user wording.

### 2. Decide What Changed

Document behavior and decisions a future maintainer should understand without reading every file:

- user-visible behavior
- system behavior and invariants
- important edge cases
- data model states or transitions
- interactions with external systems
- non-obvious implementation decisions
- explicit out-of-scope behavior

Do not document obvious code mechanics, file-by-file implementation steps, or temporary debugging notes.

### 3. Update The Feature Doc

Use this structure unless the repo already has a feature-doc convention:

```md
# Feature Name

## Purpose
What user or system problem this feature solves.

## Behavior
- Normal path
- Edge cases
- Explicitly unsupported behavior

## User-Facing Rules
- Rule 1
- Rule 2

## System Interactions
- Owning modules or contexts
- External systems
- Events, API calls, jobs, or side effects

## Data Model
Important entities, fields, states, and invariants.

## Implementation Notes
Short notes that explain non-obvious design choices without duplicating code.

## Related Decisions
- ADRs
- Issues
- PRDs
```

Keep the doc concise and maintainable. Link to ADRs, issues, PRDs, and code entry points instead of copying long details.

### 4. Route Other Knowledge Correctly

- New domain term or relationship? Update `CONTEXT.md`.
- Hard-to-reverse trade-off? Add or update an ADR.
- Setup or operational instruction? Update README or package docs.
- Agent workflow detail? Update `docs/agents/`.

### 5. Final Check

Before finishing, verify:

- The feature doc describes current behavior, not just planned behavior.
- A new maintainer can understand the feature without reverse-engineering the diff.
- Tests and docs agree on behavior.
- Any ADR or `CONTEXT.md` updates are linked from the feature doc when relevant.
