---
name: handoff
description: Compact the current conversation into a handoff document for another Codex session or agent to pick up.
argument-hint: "What will the next session be used for?"
---

Write a handoff document summarising the current conversation so a fresh Codex session or agent can continue the work. Save it to a temporary markdown file, preferably under `/tmp` with a `handoff-` prefix.

Suggest the skills to be used, if any, by the next session.

Do not duplicate content already captured in other artifacts (PRDs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor the doc accordingly.
