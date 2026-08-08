# Agent Skills

A collection of agent skills that fix real alignment problems: agents that assume too much, ask too many rounds of questions, or produce something other than what you asked for.

Each skill is small, self-contained, and practical — no heavyweight "universal workflow". They were born from real project work and real personal productivity needs, and they are free to use, modify, and combine.

## Why these skills

Many AI agent failures are not about the model being "not smart enough". The failures come from missing context, missing feedback loops, missing shared language — or from being handed a task that is too large to begin with. These skills exist to correct those failure modes.

- **Alignment before action**: Agents that start implementing before understanding what you want produce the most predictable kind of waste. `grill-me` aligns on a plan through a structured batch interview — resolving the decisions that actually change the outcome, in as few rounds as possible.
- **Compact, decision-focused questioning**: Instead of open-ended questions, every decision is presented with a recommendation and concrete options, so a plan can be confirmed or corrected in seconds rather than ten back-and-forth turns.

## Skills

| Skill | Description |
|-------|-------------|
| [grill-me](./skills/grill-me/SKILL.md) | Align on a plan, proposal, or design through a structured batch interview that resolves design decisions with minimal rounds. |

Each skill lives in its own directory under `skills/` and is self-contained: `SKILL.md` (authoritative, English) plus any translations. Adding a new skill is just a new directory plus a row in this table.

## How it works

Skills here use plain Markdown with YAML frontmatter. The `description` in the frontmatter is what agents use to decide when to invoke the skill; the body is the instruction the agent follows.

For `grill-me`, the workflow is:

1. **Scope output** — after analyzing the topic and available context, the agent outputs a dependency-aware batch plan and waits for confirmation.
2. **Batch progression** — each batch presents decisions as a compact table (recommendation + options); missing decisions or wrong dependencies are folded back into the remaining batches.
3. **Final summary** — a complete decision/outcome table for sign-off, with an optional fast exit when you say "use defaults for the rest".

## Installation

### Quick install with `npx skills` (recommended)

Use the [skills CLI](https://github.com/vercel-labs/skills) — the official installer for the open agent skills ecosystem. It auto-detects which coding agents you have installed and symlinks every skill in this repo into each one:

```sh
npx skills add flyeric0212/agent-skills
```

Useful variants:

- `--skill grill-me` — install only a specific skill
- `-g` — install globally (`~/<agent>/skills/`) instead of only in the current project
- `-a codex -a claude-code` — target specific agents instead of all detected ones
- `--copy` — copy files instead of symlinking
- `npx skills list` — show installed skills; `npx skills update` / `npx skills remove` — manage them

Prefer project-scoped installs? `npx skills add` installs into the **current project** (`./<agent>/skills/`) by default — only add `-g` when you want the skill available in every project.

### Manual install

Copy or symlink `skills/grill-me` into your agent's skills directory.

#### Codex

```sh
mkdir -p ~/.codex/skills
ln -s "$PWD/skills/grill-me" ~/.codex/skills/grill-me
```

#### Claude Code

```sh
mkdir -p ~/.claude/skills
ln -s "$PWD/skills/grill-me" ~/.claude/skills/grill-me
```

#### Cursor

```sh
mkdir -p ~/.cursor/skills
ln -s "$PWD/skills/grill-me" ~/.cursor/skills/grill-me
```

#### opencode

```sh
mkdir -p ~/.config/opencode/skills
ln -s "$PWD/skills/grill-me" ~/.config/opencode/skills/grill-me
```

#### Project-scoped install

Don't want a global install? Install the skill into a single project instead. From the project root, symlink into the agent's project skills directory (`.agents/skills/` for Codex, Cursor, and opencode; `.claude/skills/` for Claude Code):

```sh
# Codex, Cursor, opencode
mkdir -p .agents/skills
ln -s /path/to/agent-skills/skills/grill-me .agents/skills/grill-me

# Claude Code
mkdir -p .claude/skills
ln -s /path/to/agent-skills/skills/grill-me .claude/skills/grill-me
```

Project-scoped skills are committed with the repo and shared with your team. Global installs (`~/<agent>/skills/`) make the skill available in every project on your machine.

## Contributing

- Add or update `skills/<skill-name>/SKILL.md` and its row in the Skills table above.
- `SKILL.md` is the authoritative instruction, maintained in English; translations (e.g. `SKILL-CN.md`) must not add rules absent from `SKILL.md`.

## License

[MIT](./LICENSE)
