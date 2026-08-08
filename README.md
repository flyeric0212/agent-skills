# Agent Skills

A collection of small, practical agent skills for everyday engineering and productivity workflows. Instead of heavyweight "universal workflows", each skill captures a single working method that has proven itself in real projects — free to use, modify, and combine.

## Why

The most common agent failures are not about model capability. They come from missing context, missing feedback loops, or being asked to do too much in one shot. These skills address those failure modes directly:

- **Align before acting**: agents that start implementing before understanding the goal are the most predictable source of rework. `grill-me` runs a structured batch interview that settles the decisions actually changing the outcome, in as few rounds as possible.
- **Ask decision-focused questions**: every decision comes with a recommendation and concrete options, never an open-ended question — so a plan can be confirmed or corrected in seconds instead of ten rounds of back-and-forth.

## Skills

| Skill | Description |
|-------|-------------|
| [grill-me](./skills/grill-me/SKILL.md) | Align on a plan, proposal, or design through a structured batch interview that resolves design decisions with minimal rounds. |

Each skill is self-contained in its own directory under `skills/`: a `SKILL.md` (authoritative, English) plus any translations. Adding a new skill is just a new directory and a row in this table.

## How it works

Skills in this repo follow the standard agent skills format: a directory with a `SKILL.md` file using YAML frontmatter. The `description` field tells agents when to invoke the skill; the body is the instruction they follow.

For `grill-me`:

1. **Scope** — after analyzing the topic and available context, the agent presents a dependency-ordered batch plan and waits for confirmation.
2. **Batch progression** — each batch presents decisions in a compact table (recommendation + options); newly discovered decisions or wrong dependencies are merged back into the remaining batches.
3. **Final summary** — a complete decision/outcome table for final sign-off, with a fast exit whenever you say "use defaults for the rest".

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

Clone the repo first, then run the commands below **from the repository root** (they use `$PWD` to reference the skill files):

```sh
git clone https://github.com/flyeric0212/agent-skills.git
cd agent-skills
```

Then copy or symlink `skills/grill-me` into your agent's skills directory:

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
