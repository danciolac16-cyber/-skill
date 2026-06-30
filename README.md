# Personal Codex Skills

这是一个个人 Codex Skills 集合仓库，用来存放可复用的智能体工作流、工具说明和领域方法论。

当前包含两个并列模块：

| Skill | 用途 | 路径 |
|---|---|---|
| WeRead Skills | 微信读书能力：搜书、书架、笔记划线、阅读统计、书评与推荐。 | `weread-skills/` 或原仓库现有 `skills/` 文档 |
| Agent Book Distillation | 三源校验书籍蒸馏：把本地全文、微信读书和外部资料结合，沉淀为智能体可调用的知识库模块。 | `agent-book-distillation/` |

## Agent Book Distillation

路径：[`agent-book-distillation/SKILL.md`](agent-book-distillation/SKILL.md)

这个 skill 用于把书籍从“读书摘要”升级为“智能体可检索、可执行、可质检、可修复的能力模块”。它固化了以下流程：

1. 本地全文、微信读书、外部资料三源校验。
2. 全文抽取、OCR、章节覆盖与完整阅读披露。
3. 提取可复用的方法论，并转换为触发条件、输入字段、控制参数、工作流和输出 Schema。
4. 使用 ABCD 评级与反伪蒸馏门槛，判断模块能否供后续智能体可靠调用。
5. 生成 Prompt 模板、质量检查器、负面约束、修复规则和跨模块调度关系。
6. 标注 `Agent_Capability_Delta`，说明加入本书前后的智能体能力变化。
7. 输出 JSON/search 层，方便迁移到 Obsidian、Notebook 或外接知识库。

### 外部模型守门

Kimi、DeepSeek、Gemini、Claude 等模型适合长文本阅读、章节笔记和第一版提取，但其输出只作为草稿或质量对标，不能直接证明已经完整阅读原书。

Codex 在工作流中承担最终守门职责：

- 对照本地全文、目录、章节覆盖、OCR 和抽取记录验证阅读声明。
- 本地证据与外部模型结论冲突时，以本地证据为准。
- 将外部草稿转换为可调用 Schema、质量检查器和失败修复规则。
- 在证据不足、执行层缺失或伪蒸馏风险较高时限制评级并暂停正式归档。

### 知识来源分层

为了避免把现代常识或模型补写误归因于原书，重要规则可标记为：

- `original_book`：经过本地原书验证的内容。
- `modern_supplement`：面向当前平台、媒介或 AIGC 工作流的现代补充。
- `related_module`：应交给知识库中其他模块处理的能力。
- `unverified_external`：尚未获得充分本地证据的外部材料。
- `unavailable_source`：因缺页、损坏、OCR 失败或未读而无法确认的内容。

现代适配可以提高执行价值，但不能掩盖阅读缺口，也不能抬高原书证据评级。

### 创作风险门不是一刀切禁用

面向电影、恐怖、犯罪、战争、心理惊悚、历史创伤、性别压迫、殖民历史、身体恐怖等创作类模块时，`Gate`、`Blocker`、`禁止`、`安全门` 默认不是删掉艺术手法，而是做分层、路由和强度控制。

Codex 守门时应保留由原书或影片案例支持的黑暗、冲突、暴力、压迫、恐惧和道德不适，把它们转换为可执行的视角、距离、显隐、离屏、后果、象征、声音、剪辑、表演和叙事功能控制。只有命中未经授权真实肖像复刻、受保护画面/音乐/台词复制、操作性现实伤害、创伤猎奇、阴谋论当事实、现代补充误标为原书等硬阻断条件时，才执行 block。

推荐在正式模块中使用 `creative_risk_gate` 字段，至少包含 `default_policy: route_and_control_not_blanket_ban`、`allowed_use`、`representation_mode`、`intensity_level`、`source_layer` 与 `repair_rule`。

### A 级模块要求

完整阅读只是基础。要达到可直接供后续智能体使用的 A 级，归档还应具备：

- 调用时机与必需输入
- 参数或分类控制面板
- 可执行工作流与输出 Schema
- 直接可复用的 Prompt
- 质量检查、负向约束和修复规则
- 跨模块分工与知识来源标记
- 正式生成后的文件、索引和评级复检

适合在处理一本新书、升级旧版蒸馏、或者为第二大脑准备结构化知识节点时调用。

## 通用 Skill 与项目规则

本仓库中的 `agent-book-distillation/SKILL.md` 保存可迁移到其他项目的通用书籍蒸馏方法。

在“智能体书籍知识库”项目中，项目根目录的 `AGENT.md` 优先级更高，负责补充本机路径、文件夹归类、HTML/PDF 成对归档、Manifest、旧版替换记录和 GitHub 同步等项目专用规则。这些本地规则不会原样写入通用 skill；只有可复用的方法论会回写到本仓库。

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
