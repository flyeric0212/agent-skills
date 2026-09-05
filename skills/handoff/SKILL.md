---
name: handoff
description: Generate or update an engineering handoff.md recording verifiable goals, progress, decisions, and next steps so another session or agent can continue the work. Use when pausing development, switching sessions, or handing off unfinished work.
---

# Handoff

Generate or update an engineering checkpoint using [HANDOFF-TEMPLATE.md](templates/HANDOFF-TEMPLATE.md). Prefer the user-specified path and project conventions; when neither exists, write to `docs/requirements/{yyyyMMdd-slug}-handoff/handoff.md`.

## Workflow

1. Determine the handover scope: read the user's message, project context, project rules, and related documents.
2. If a handoff already exists, treat it as the previous checkpoint: keep still-valid information, add new progress, move completed items, and remove stale details and resolved blockers.
3. Generate a complete checkpoint strictly following the template; never write unsupported items into Done, and explicitly mark anything speculative.
4. Keep the content concise and self-contained, and make the first Next Step directly executable by the next agent.
