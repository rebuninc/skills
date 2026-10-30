---
name: simple-spec
description: Lightweight spec-driven development. Every new feature or behavior change starts with a short numbered spec in docs/specs/NNN-name.md, written by interviewing the user one question at a time, confirmed before coding, and checked against its acceptance criteria when done. Use when the user asks to build a feature, change behavior, write/update a spec, or says "simple-spec", "spec first", "write a spec".
---

# Simple Spec

Specs are small markdown files that say what changes, what doesn't, and how to know it's done. Code follows the spec, never the other way around.

## Rules

1. **Every new feature or behavior change starts with a spec** in `docs/specs/NNN-name.md` — zero-padded, sequential, kebab-case (e.g. `001-project-invites.md`). Next number = highest existing + 1. Create `docs/specs/` if missing.
2. **Specs live only in `docs/specs/`.** Issues and cards (Linear, Jira, GitHub) are not specs.
3. **No spec? Interview the user — one question at a time — and write it before any code.**
   - Ask through the `AskUserQuestion` tool when available, never as plain chat text. This applies to every question: interview, clarifications, choosing between approaches.
4. **Don't implement anything that isn't in the spec.** If something is missing, ask.
5. **Before coding, list in 3 to 6 bullets what will change and in which files, and wait for the user's confirmation.**
6. **When done, check every acceptance criterion, tick it (`- [x]`), and say which ones passed.**
7. **If behavior changes during implementation, update the spec.**
8. **Never put lint, format or typecheck in acceptance criteria** — those run in hooks/CI. Criteria describe behavior only.
9. **Link related specs in both directions.** When a spec changes, continues, or replaces behavior from another, both get a `## Related` section right below the title with relative links: the new one lists `Changes`/`Continues`, the older one gets `Changed by`/`Continued by` (e.g. `- Changed by: [002 — account-references](./002-account-references.md) — renames members[].user`). Also applies when editing an existing spec touches another. Omit the section when there are no relations.

Write specs in the project's language. Keep them short: behavior, not implementation essays.

## Template

```markdown
# Spec: <name>

## Related
- <Changes | Changed by | Continues | Continued by>: [NNN — name](./NNN-name.md) — <what changes>

## Goal
<1 or 2 sentences: what changes and why>

## Out of scope
- <what will NOT be done>

## Behavior
1. <what happens>
2. <what happens>

## Edge cases
- <unusual situation> → <expected result>

## Acceptance criteria
- [ ] Given <X>, when <Y>, then <Z>
```

If the project already has `docs/specs/_template.md`, use it instead.

## Flow

1. Look for an existing spec covering the request (`docs/specs/`). Found → use it (update per rule 7 if behavior differs).
2. Not found → interview (rule 3), write the spec, show it.
3. Plan in 3–6 bullets with files (rule 5), wait for confirmation.
4. Implement only what's specced (rule 4).
5. Check each criterion, tick it, report pass/fail (rule 6).
