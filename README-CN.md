# Agent Skills

一个面向真实工程与日常生产力场景的 Agent 技能集合。不追求一套笨重的"万能流程"，而是把在真实项目中反复验证有效的做法，拆成小而清晰、可以自由使用、修改和组合的技能。

> 本文件是 [README.md](./README.md) 的非权威中文翻译，内容以英文版为准。

## 为什么需要这些技能

很多 Agent 的失败并不是模型不够聪明，而是缺少上下文、缺少反馈循环，或者一开始就被要求做一件过大的事。这些技能直接针对这些失败模式：

- **先对齐，再动手**：没搞清目标就急着实现的 Agent，是最可预期的返工来源。`grill-me` 通过结构化分批访谈，用尽可能少的轮次敲定真正影响结果的决策。
- **只问有决策意义的问题**：每个决策都给出推荐答案和具体选项，不抛开放式问题——几秒内即可确认或纠正计划，而不是来回十轮问答。

## 技能列表

| 技能 | 描述 |
|------|------|
| [grill-me](./skills/grill-me/SKILL.md) | 通过结构化分批访谈对齐计划、方案或设计，以最少轮次解决设计决策。 |

每个技能自包含在 `skills/` 下的独立目录中：一个 `SKILL.md`（英文权威版本）加任意翻译。新增技能只需新建目录并在表格中加一行。

## 工作原理

本仓库的技能采用标准 Agent Skills 格式：一个目录 + 带 YAML frontmatter 的 `SKILL.md`。`description` 用于 Agent 判断何时调用技能，正文是 Agent 遵循的指令。

以 `grill-me` 为例：

1. **输出全景**——分析主题和可用上下文后，给出按依赖关系分组的批次计划，等待用户确认。
2. **分批推进**——每个批次用紧凑表格（推荐 + 选项）呈现决策；新发现的决策或错误的依赖关系折入剩余批次。
3. **最终汇总**——输出完整决策/结论表供最终确认；说"剩下的按推荐走"即可快速退出。

## 安装

### 使用 `npx skills` 快速安装（推荐）

使用 [skills CLI](https://github.com/vercel-labs/skills)——开源 Agent 技能生态的官方安装器。它会自动检测你已安装的编码 Agent，并将本仓库中的每个技能以符号链接方式安装到各 Agent：

```sh
npx skills add flyeric0212/agent-skills
```

常用变体：

- `--skill grill-me` — 只安装指定技能
- `-g` — 全局安装（`~/<agent>/skills/`），而不是仅当前项目
- `-a codex -a claude-code` — 只安装到指定 Agent，而非全部检测到的
- `--copy` — 复制文件而非符号链接
- `npx skills list` — 查看已安装技能；`npx skills update` / `npx skills remove` — 管理已安装技能

更喜欢项目级安装？`npx skills add` 默认就安装在**当前项目**（`./<agent>/skills/`），只有需要所有项目可用时才加 `-g`。

### 手动安装

先克隆仓库，然后在**仓库根目录**下执行以下命令（`$PWD` 用于引用技能文件）：

```sh
git clone https://github.com/flyeric0212/agent-skills.git
cd agent-skills
```

再将 `skills/grill-me` 复制或符号链接到 Agent 的 skills 目录：

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

#### 项目级安装

不习惯全局安装？可以只安装到单个项目。在项目根目录，符号链接到 Agent 的项目 skills 目录（Codex、Cursor、opencode 用 `.agents/skills/`；Claude Code 用 `.claude/skills/`）：

```sh
# Codex, Cursor, opencode
mkdir -p .agents/skills
ln -s /path/to/agent-skills/skills/grill-me .agents/skills/grill-me

# Claude Code
mkdir -p .claude/skills
ln -s /path/to/agent-skills/skills/grill-me .claude/skills/grill-me
```

项目级技能随仓库提交、团队成员共享；全局安装（`~/<agent>/skills/`）则让本机所有项目都能用。

## 贡献

- 新增或修改 `skills/<技能名>/SKILL.md`，并更新上方技能列表中的对应条目。
- `SKILL.md` 是权威指令，以英文维护；翻译（如 `SKILL-CN.md`）不得加入其中不存在的规则。

## License

[MIT](./LICENSE)
