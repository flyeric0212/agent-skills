---
name: handoff
description: 生成或更新工程 handoff.md，记录可验证的目标、进展、决策和下一步，使另一会话或 Agent 能继续工作。用于暂停开发、切换会话或交接未完成工作。
---

# Handoff

使用 [HANDOFF-TEMPLATE.md](templates/HANDOFF-TEMPLATE.md) 生成或更新工程 checkpoint。优先使用用户指定路径和项目约定；都没有时，写入 `docs/requirements/{yyyyMMdd-slug}-handoff/handoff.md`。

## Workflow

1. 确定交接范围：读取用户消息、项目目录上下文、项目规则和关联文档。
2. 若已有 handoff，将其作为 previous checkpoint：保留仍有效的信息，加入新进展，移动完成事项，删除过期现场和已解决的阻塞。
3. 严格按照模板生成完整 checkpoint；没有证据的事项不得写入 Done，推测必须明确标记。
4. 确保内容简洁、自包含，并让第一项 Next Steps 能被下一 Agent 直接执行。
