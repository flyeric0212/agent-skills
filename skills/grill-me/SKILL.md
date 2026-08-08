---
name: grill-me
description: Align on a plan through a structured batch interview that resolves design decisions.
---

The user wants to clarify a plan, proposal, or design through conversation. Focus on substantive decisions that affect outcomes. Ask in compact batches to reduce rounds while keeping alignment.

## Workflow

### Phase 1: Scope output → user confirmation

After analyzing the topic and available context (codebase, docs, discussion history), output a concise dependency-aware batch plan, then wait for the user to confirm, correct, or supplement.

```
This grill covers these decisions, grouped into dependency-safe rounds:

Round 1 (independent)       : API path design, error strategy, pagination
Round 2 (depends on Round 1): request/response structure, permission granularity
...

Is this scope accurate? Any decisions missing or dependencies wrong?
```

Keep it concise: one dependency line plus one decision list per batch is enough. Do not proceed until user confirms.

### Phase 2: Batch progression

Walk batches in order. For each batch, present all decisions in a compact table with recommendation + options, then ask for confirmation.

- Example table:

```markdown
Round 1 — independent decisions:

| Decision | Recommendation | Options |
|----------|---------------|---------|
| API path prefix | /api/v1 | /api / /api/v1 / /api/v2 |
| Error strategy | Global exception handler | Per-controller / Global |
| Pagination | Cursor pagination | Offset / Cursor |

Looks good?
```

### Corrections during progression

If a missing decision, wrong dependency, or scope change is discovered (by user or yourself), update the remaining batch plan and continue.

### Phase 3: Final summary

After all batches are resolved, output the complete decision list (output a Decision / Outcome table) and ask for final sign-off.

### Fast exit (optional)

If the user says "use defaults for the rest" or equivalent, respect it immediately.

## Hard Rules

- Before asking, verify what can be known from context, code, docs, or search. Do not ask users to repeat known or safely inferable information.
- Ask only decision questions that can change the plan, design, scope, implementation, or output. Do not ask preference questions with no execution impact.
- Use the fewest rounds that preserve real dependency order. Group independent decisions together unless one round would be hard to answer clearly.
- Every decision must include a recommended answer and concrete alternatives. Do not ask open-ended questions.
- If the user accepts recommendations, says "use defaults" or "use recommendations", or gives an equivalent shortcut, stop interviewing immediately and proceed.
