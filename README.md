# Personal Codex Skills

这是一个个人 Codex Skills 集合仓库，用来存放可复用的智能体工作流、工具说明和领域方法论。

当前包含两个并列模块：

| Skill | 用途 | 路径 |
|---|---|---|
| WeRead Skills | 微信读书能力：搜书、书架、笔记划线、阅读统计、书评与推荐。 | `weread-skills/` 或原仓库现有 `skills/` 文档 |
| Agent Book Distillation | 三源校验书籍蒸馏：把本地全文、微信读书和外部资料结合，沉淀为智能体可调用的知识库模块。 | `agent-book-distillation/` |

## Agent Book Distillation

路径：[`agent-book-distillation/SKILL.md`](agent-book-distillation/SKILL.md)

这个 skill 用于把书籍从“读书摘要”升级为“智能体能力模块”。它固化了以下流程：

1. 本地全文、微信读书、外部资料三源校验。
2. 全文抽取质量与版本自检。
3. 提取核心方法论，而不是章节摘要。
4. 标注对智能体的补强 `Agent_Capability_Delta`。
5. 输出 JSON/search 层，方便迁移到 Obsidian、Notebook 或外接知识库。
6. 生成 Prompt 模板、质量检查器、负面约束和知识库连接。

适合在处理一本新书、升级旧版蒸馏、或者为第二大脑准备结构化知识节点时调用。

## WeRead Skills

原微信读书相关内容保留为本仓库的一个能力模块，主要用于：

- 搜索书籍
- 查看书架
- 导出笔记和划线
- 阅读统计
- 浏览书评
- 发现和推荐书籍

如果使用微信读书 API，仍需按原模块要求配置 `WEREAD_API_KEY`。

## Recommended Layout

```text
-skill/
  README.md
  agent-book-distillation/
    SKILL.md
    agents/openai.yaml
  weread-skills/          # if maintained as local skill folder
  skills/                 # existing WeRead reference docs, if present
```

## Notes

这个仓库不是单一微信读书 skill 仓库，而是个人 Skills 总仓库。后续可以继续新增 Obsidian、Notebook、知识库迁移、视觉风格蒸馏等独立 skill。
