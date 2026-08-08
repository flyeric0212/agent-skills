# Agent Instructions

Instructions for AI agents and contributors working in this repository.

## Scope

Skills live in flat directories under `skills/`:

```
skills/
├── grill-me/
│   ├── SKILL.md        # authoritative instruction (English)
│   └── SKILL-CN.md     # non-authoritative Chinese translation
└── <skill-name>/       # one directory per skill
```

No category subdirectories. If a new skill needs to be added, create `skills/<skill-name>/` with at least a `SKILL.md`.

## Hard Rules

- Every skill under `skills/` must be listed in the top-level `README.md` (and `README-CN.md`), with the skill name linked to its `SKILL.md` and a one-line description.
- `SKILL.md` is the single authoritative source for agent execution.
- Do not use XML-style wrapper tags such as `<workflow>` or `<hard-rules>`. Organize skill bodies with Markdown headings: `##` for top-level sections, `###` for subsections.

## Language Policy

- Maintain `SKILL.md` and `README.md` in English; they are authoritative.
- Translations (`SKILL-CN.md`, `README-CN.md`) are non-authoritative. A translation must not introduce behavior, workflow steps, hard rules, or output requirements absent from the authoritative file.
- On conflict, the English file wins. Update the English file first for every change, then synchronize every existing translation.

## Contribution Workflow

1. Create or modify `skills/<skill-name>/SKILL.md`.
2. Add or update the row in the Skills table of `README.md` and `README-CN.md`.
3. Keep the skill lightweight: one clear purpose, short and direct instructions, no multi-stage ceremony for simple skills.
4. Verify the frontmatter is valid YAML and the description accurately states when the skill applies.
