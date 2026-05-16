---
name: adapt-external-skills
description: Import, fork, or update skills from an external source such as GitHub, then adapt them conservatively for Codex while preserving upstream intent. Use when the user says "/adapt-external-skills" or wants Codex to bring in new skills, sync a skill repo, rename or customize imported skills, or maintain a local fork of third-party skills.
---

# Adapt External Skills

Use this skill to turn upstream skills into a maintainable Codex-focused fork without rewriting them unnecessarily.

## Principles

- Preserve upstream intent and structure unless there is a concrete Codex mismatch.
- Prefer small, reviewable commits: one skill or one coherent repo-wide rename per commit.
- Keep upstream sync possible. Avoid broad rewrites that make future merges painful.
- Update references when renaming skills so links and setup instructions do not drift.
- Do not silently change behavior. Show the diff or proposed diff before committing unless the user has already approved the exact change.

## Workflow

### 1. Establish Source And Target

Identify:

- Upstream source repo or path.
- Local fork or clone location.
- Target branch for adaptations.
- Whether the local repo should preserve an `upstream` remote for future sync.

If creating a fork, set `origin` to the user's fork and keep `upstream` fetch-only when practical.

### 2. Inventory Skills

List available skills and group them:

- core skills to adapt now
- optional skills to defer
- deprecated or source-specific skills to skip

Start with the skills that directly support the user's workflow.

### 3. Adapt Conservatively

For each skill:

1. Read `SKILL.md` and any directly referenced files.
2. Identify only the mismatches with Codex, such as:
   - trigger text mentioning another agent
   - slash-command-only invocation text
   - setup-skill names that changed
   - subagent instructions that need Codex wording
   - file targets that should prefer `AGENTS.md`
3. Propose a small diff.
4. Apply the approved change.
5. Commit and push before moving to the next skill, unless the user asks to batch.

Keep useful upstream language. Do not rephrase just for style.

## Common Adaptations

- Replace "the agent" with "Codex" only when it improves trigger accuracy.
- Replace "me" with "the user" inside reusable skill instructions.
- Remove slash-command syntax when it is not meaningful for Codex, unless the user wants to keep it as a trigger phrase.
- Prefer `AGENTS.md` for Codex repo guidance, while preserving compatibility with existing `CLAUDE.md` when useful.
- For hard dependencies on repo setup, point to the local setup skill by name.
- For soft dependencies, say "repo guidance", "domain glossary", or "ADRs" without forcing setup.
- Preserve original wording when the user explicitly wants upstream behavior.

## Rename Checklist

When renaming a skill:

- Rename the directory.
- Update frontmatter `name`.
- Update README links.
- Update references in ADRs, context docs, setup templates, and other skills.
- Search for the old name before committing.
- Prefer one atomic commit for the rename and its reference updates.

## Commit Discipline

Before committing:

- Run `git diff` for the touched files.
- Run `git status --short --branch`.
- Confirm no unrelated files are staged.

Commit message style:

- `Adapt <skill> for Codex`
- `Rename <skill> for Codex`
- `Point <skill group> at <setup-skill>`

Push after each commit when working on a shared fork.
