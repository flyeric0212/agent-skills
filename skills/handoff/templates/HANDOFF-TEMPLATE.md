# Handoff Template

Generate `handoff.md` using the fixed structure below. Delete all placeholder content; besides Done, In Progress, and Blocked under Progress, do not add other fixed headings.

```md
# {Handoff Title}

> This file is the current checkpoint of this project. Detailed requirements, design, and task status are governed by the referenced project documents.

## Goal

{Briefly describe the goal, scope, and delivery boundaries of the current work.}

## Constraints

- {Requirements, preferences, or prohibitions that are still in effect and must be followed.}

## Progress

### Done

- [x] {Completed results with evidence.}

### In Progress

- [ ] {Current work not yet finished; write None when empty.}

### Blocked

- {Blockers, pending decisions, or unverified items; write None when empty.}

## Decisions

- **{Decision}**: {Rationale}

## Next Steps

1. {The first task the next agent can execute directly.}
2. {Follow-up work required to complete the current phase.}
3. {Future-phase tasks and their start conditions.}

## Context

- {Documents and code paths required to take over.}
- {Git state and uncommitted files required to take over.}
- {Verification performed or pending, and its results.}
- {Error, interface, or environment details that must be preserved exactly.}
```
