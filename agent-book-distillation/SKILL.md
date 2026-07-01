---
name: agent-book-distillation
description: Use when distilling books into an AI-agent knowledge base module, especially for AIGC video production such as AI shorts, film, novel adaptation, advertising, concept films, and short video. Covers source verification, executable schemas, video-production controls, prompt hooks, quality checks, repair rules, and legacy-module reinforcement.
metadata:
  short-description: Distill books into agent-ready knowledge modules
---

# Agent Book Distillation

Use this skill when the user provides or references a book and wants it turned into a reusable AI-agent knowledge module rather than a normal summary.

The goal is not "what the book says." The goal is: **what new capability this book gives the user's agents, how that capability is invoked, and how it should be stored for retrieval in an external knowledge base.**

For this project, the downstream system is an **AIGC video-production agent stack**. A module is not complete merely because a general agent can read or discuss it. It must state whether and how it improves development, writing, preproduction, generation, postproduction, distribution, or quality control.

## Core Principle

Distill from evidence, not vibes.

Always prefer this evidence order:

1. **Local full text**: ebook, DOCX, EPUB, PDF text layer, OCR output, or extracted text. This is the primary source.
2. **WeRead / user reading platform**: use for Chinese title, edition, author, readable availability, naming, and user-context verification when available.
3. **External sources**: use publisher pages, library/catalog pages, official excerpts, or credible references to verify edition, table of contents, and known core concepts.

If the three sources disagree, make the disagreement explicit. Do not let external summaries override a readable local full text.

## When To Pause

Before generating final HTML/PDF or archiving a formal distillation, pause for confirmation when:

- The local full text is unreadable, encrypted, mostly OCR noise, or missing major chapters.
- The book already has an older distillation and the new work would replace or duplicate it.
- The evidence is mostly external and the local full text was not read or extracted.
- The module's knowledge-base role is unclear or overlaps heavily with existing modules.

In these cases, output an audit and recommendation first.

## Workflow

### 0. User Project Defaults

For the user's current book-knowledge-base project, apply these defaults unless the user explicitly changes them:

- Project root: `F:\智能体书籍知识库`.
- Formal HTML output: `F:\智能体书籍知识库\html`.
- Formal PDF output: `F:\智能体书籍知识库\PDF`.
- Temporary indexes, extracted text, audits, and working notes must go under a clearly named separate folder such as `F:\智能体书籍知识库\临时索引_阶段整理`; do not put temporary work inside `PDF` or `html`.
- Use this sequence for every book: WeRead lookup + local full-text extraction/read if provided + external verification, then output analysis first.
- Do not generate HTML/PDF until the user confirms with wording such as `确认`, `确定`, or `可以`.
- The pre-distillation analysis should match the user's preferred granular style: reading self-check, extraction scale, source reliability, suggested module name, differences from related modules, core distillation value, planned modules, agent empowerment, black-box JSON, knowledge-base placement, and the next archive/index count.
- Distill methodology and reusable agent capability, not isolated plot details, character trivia, or decorative summaries.
- Formal archived HTML/PDF files must be knowledge-base ready, not thin summary cards. After the user confirms, create a deep enough module for later retrieval: include source audit, module role, per-book/per-volume responsibility when relevant, methodology layers, routing matrices, parameter/control tables, direct-use prompt templates, black-box JSON, quality checks, negative constraints, related modules, and index placement. For preset/library books, include scene/style/preset routing tables and reverse-engineering tags instead of only high-level value statements. The analysis step may be concise, but the formal archive should carry the actionable substance.
- Treat **agent-executable structure** as mandatory, not optional. A formal archive must enable an agent to decide when to invoke the module, what inputs to request, what parameters to set, what workflow to run, what output schema to produce, how to score the result, and how to repair failures. A conceptual summary, even if accurate, is not enough for A-level distillation.
- Treat the **AIGC video-production interface** as mandatory for modules that directly or indirectly support AI shorts, film, novel adaptation, advertising, concept films, trailers, brand content, or short video. State production stages, content types, upstream inputs, observable audiovisual controls, downstream handoff, prompt hooks, video checks, and repair rules.
- Do not use the phrase "usable for AI video" as evidence by itself. Convert the book into concrete decisions such as scene function, character state, performance action, shot size, camera, blocking, continuity, production design, lighting, color, sound, editing, brand intent, or distribution versioning, according to the book's actual responsibility.
- Do not force every book to control every production stage. Mark indirect theoretical or research modules as upstream decision/diagnostic modules and route production work to specialist modules.
- For multi-shot generation, require continuity controls for the dimensions owned by the module: character, costume, prop, space, screen direction, eye-line, action state, light direction, color state, time, weather, sound perspective, or brand behavior.
- For image-heavy books, audit the visual material instead of treating images as decoration. Distinguish scanned page images, merely attractive illustrations, and instructional diagrams that carry method. Sample representative pages or extracted images when possible, describe what the diagrams teach, and convert useful visual demonstrations into agent-readable rules such as composition, shot size, depth, lighting contrast, visual focus, staging, eye-line, and spatial hierarchy.
- For scanned PDFs, image-only PDFs, or PDFs with broken text layers, run an OCR feasibility check before claiming full-text reading. If local OCR is available, perform at least a representative OCR sample before the analysis, and prefer full-book OCR before rating a module as A. Never treat failed PDF text extraction as equivalent to reading the book.
- Every pre-distillation analysis and formal archive must include a quality rating and usability verdict: current evidence grade, expected grade after formal distillation, whether the module is usable for the later agent knowledge base, whether it risks being pseudo-distillation, and what would be required to upgrade it. In the first analysis response, state the expected post-distillation grade proactively; do not wait for the user to ask.
- The first analysis response must include a **full-reading disclosure**: state whether the local main text was completely extracted/read for the analysis. If not complete, list exactly which parts were read or sampled, which parts were not read, why full reading was not possible or not yet performed, and how that limits the expected grade. This prevents concept-only or lazy distillation being mistaken for a full-book module.
- The full-reading disclosure must be internally consistent. If `local_main_text_fully_read_for_this_analysis` is `true`, then `unread_or_sampled_scope` must be empty. If any chapter, volume, appendix, or major case section remains unread or only sampled, set it to `false` and cap the expected grade below A until the missing coverage is completed.
- After formal HTML/PDF generation, perform a **second-step self-check** before the final user response: verify output files, page/text extractability, index updates, replacement/deletion state, actual module depth, and final ABCD rating. Compare the final rating with the expected rating from the first analysis. If they differ, explain where the gap is, whether the archive is still usable, and what concrete repair is required.
- When this skill is improved and synced to GitHub, use a Chinese commit message that clearly states the enhancement area, such as `增强：图片型书籍审计规则` or `增强：确认前不生成归档的流程规则`, so future history shows what each revision changed.

### 1. Source Audit

Produce a concise self-check before distillation:

- Local file path(s), format, size, and readable status.
- Extraction workspace path, if created.
- Extracted text scale: characters/words, line count, page count, chapter count, or internal file count.
- OCR/text quality: mojibake/noise, missing pages, repeated headers, encryption, broken encoding.
- WeRead lookup result: title/author/version found or not found.
- External verification: official/publisher/catalog sources and what each confirms.
- Existing distillation status: none, old version, upgraded version, duplicate risk.
- Full-reading disclosure: whether the whole main text was extracted/read; if not, list read scope, unread scope, reason, and grade limitation.
- For image-heavy books: page/image count, whether the file is scanned or born-digital, whether images are decorative or instructional, and what visual method can be extracted from representative samples.
- For scanned or OCR-dependent books: OCR engine used, page range tested, OCR sample quality, failure modes, whether full-book OCR is needed before final A-level rating.

Recommended table:

```markdown
| Evidence Layer | Result | Reliability | Notes |
|---|---|---:|---|
| Local full text | ... | High/Medium/Low | ... |
| WeRead | ... | Medium/Low | ... |
| External sources | ... | Medium/Low | ... |
```

### 1.1 Scanned / OCR Book Handling

When local text extraction is poor, use this decision path:

1. **Classify the file**: born-digital text PDF, scanned PDF, image-only PDF, OCR-damaged PDF, encrypted file, or mixed file.
2. **Run a sample extraction**: extract raw text and inspect representative pages, not only file metadata.
3. **Run OCR sample if needed**: use available local OCR on at least several representative pages: cover/metadata, table of contents, early chapter, middle chapter, late chapter, and one dense page.
4. **State OCR quality plainly**: clean, usable with minor errors, usable but noisy, poor, or failed.
5. **Decide the maximum defensible grade**:
   - If OCR is absent or only a few pages are sampled, do not promise A.
   - If full-book OCR is clean enough and formal distillation is deep, A is possible.
   - If only external sources and partial samples are available, the module may be useful but should be marked as C/B at best depending on depth.

OCR audit fields:

```json
{
  "ocr_required": true,
  "ocr_engine": "",
  "page_range_tested": "",
  "full_book_ocr_available": false,
  "ocr_quality": "clean | usable_minor_errors | noisy_but_usable | poor | failed",
  "max_defensible_grade": "A | B+ | B | C | D",
  "reason": ""
}
```

### 1.2 ABCD Quality And Usability Rating

Every analysis and formal archive must include a rating block. The rating is not decorative; it tells the user whether the distillation can actually power downstream agents. The rating block must appear in the first analysis response for each book, before the user confirms formal generation.

Use this scale:

| Grade | Meaning | Evidence Standard | Agent Usability |
|---|---|---|---|
| A | Final knowledge-base module | Full local text or clean full OCR; source audit is strong; methodology is deeply converted into schemas, routing, prompt templates, quality checks, negative constraints, and cross-module links | Can be directly used by downstream agents for retrieval, generation, reverse engineering, scoring, and repair |
| B+ / A- | Strong stage module | Source is mostly readable, but has limitations such as scanned OCR noise, missing diagrams, or partial external reliance; formal archive is still deep and callable | Usable in production-like workflows, but should be upgraded if cleaner source appears |
| B | Usable module | Core methods are captured and agent controls exist, but source coverage or structure is incomplete | Useful for retrieval and guidance, but not enough for high-confidence expert automation |
| C | Direction card / medium summary | Some concepts and value are captured, but limited schemas, sparse quality checks, weak source evidence, or shallow formalization | Useful for human planning; risky as an autonomous agent module |
| D | Thin summary / not final | Mostly high-level value statements, too short, little source evidence, no meaningful schemas or quality checks | Not recommended for final knowledge base; should be upgraded before agent use |

Required rating output:

```json
{
  "Distillation_Quality_Rating": {
    "current_grade": "D | C | B | B+ / A- | A",
    "expected_after_formal_distillation": "D | C | B | B+ / A- | A",
    "usable_for_agent_kb": true,
    "pseudo_distillation_risk": "low | medium | high",
    "why": "",
    "what_agent_can_do": [],
    "what_agent_cannot_reliably_do_yet": [],
    "upgrade_requirements": []
  }
}
```

If `usable_for_agent_kb` is false or `pseudo_distillation_risk` is high, pause before final archive unless the user explicitly asks to keep it as a temporary card.

Hard caps:

- If readable local full text exists but was not fully processed, maximum expected grade is **B+ / A-** and A is forbidden.
- If the output lacks trigger conditions, input/output schema, prompt template, and quality checker, maximum final grade is **B** even if the summary is accurate.
- If the output is mostly "core value" and "AI transformation direction" without executable routing, scoring, or repair rules, maximum final grade is **C**.
- If the output is underdeveloped enough that an agent can only read it but cannot act from it, grade it **D or C**, not A.
- If a module is relevant to this project's AIGC video pipeline but lacks a concrete video-production interface, cap the final grade at **B+ / A-**. If it cannot hand off any structured production decision, cap it at **B**.

### 1.3 Full-Reading Disclosure And Second-Step Self-Check

The user's knowledge base is meant for downstream autonomous agents, so every book must distinguish between:

- **analysis-ready reading**: when a readable local full text is available, the first analysis must be based on a complete pass over the extracted main text, not only a table of contents or keyword samples. If the full text is too large, damaged, encrypted, or otherwise impossible to process in full during the current step, say so plainly and cap the expected grade until a full pass is completed;
- **formal full-book distillation**: enough full-text coverage and module depth to become a callable external knowledge module.

Required first-step disclosure:

```json
{
  "Reading_Coverage_Disclosure": {
    "local_main_text_fully_extracted": true,
    "local_main_text_fully_read_for_this_analysis": true,
    "read_scope": [],
    "unread_or_sampled_scope": [],
    "reason_if_not_full": "",
    "impact_on_expected_grade": ""
  }
}
```

Consistency rule:

- `local_main_text_fully_read_for_this_analysis = true` requires `unread_or_sampled_scope = []`.
- If `unread_or_sampled_scope` is non-empty, set `local_main_text_fully_read_for_this_analysis = false` and explicitly downgrade/cap the expected grade.
- Do not hide unread case sections behind "repetitive structure"; if those cases are part of the user's requested knowledge base, they must be counted as unread until processed.

Required post-generation self-check:

```json
{
  "Post_Generation_Self_Check": {
    "html_created": true,
    "pdf_created": true,
    "pdf_text_extractable": true,
    "index_updated": true,
    "old_version_replaced_or_retained_correctly": true,
    "expected_grade_from_analysis": "A- / A",
    "actual_final_grade": "A- / A",
    "grade_changed": false,
    "if_changed_reason": "",
    "repair_required": []
  }
}
```

### 1.4 Anti-Pseudo-Distillation Gate

Before calling any archive final, test it against this gate.

Required executable layers:

| Layer | Required content | Failure cap |
|---|---|---|
| Invocation | Trigger conditions / use-when rules | Max B |
| Inputs | What the downstream agent must receive or ask for | Max B |
| Controls | Parameters, sliders, taxonomies, routing choices, or state variables | Max B |
| Workflow | Step-by-step procedure the agent can run | Max B |
| Output Schema | JSON/table fields the agent should produce | Max B |
| Prompt Template | Direct reusable prompt or system fragment | Max B |
| Quality Checker | Pass/fail checks, score rubric, or error detector | Max B |
| Negative Constraints | What the agent must not do | Max B+ / A- |
| Repair Rules | How to fix failed outputs | Max B+ / A- |
| Cross-links | Related modules and dispatch order | Max A- |

Pseudo-distillation signs:

- It only summarizes concepts.
- It says "AI transformation" but gives no callable fields.
- It lists book chapters but does not convert them into controls or checks.
- It has no trigger conditions.
- It has no scoring or repair layer.
- It cannot answer "what should the agent do next?"

If two or more signs are present, mark `pseudo_distillation_risk` as `high`.

### 1.5 Deep Reading Trace And Distillation Blueprint

For any local full-text book, source extraction is not enough. The analysis must show a **deep reading trace** and a **distillation blueprint** before formal archive generation.

Deep reading trace:

- Record which full-text file was used and how it was processed.
- Identify the book's structural units: volumes, chapters, sections, appendices, case groups, diagrams, tables, or recurring examples.
- State that each major structural unit was processed, not merely searched by keyword.
- Extract the book's repeated operating patterns: definitions, steps, diagnostic questions, examples, exceptions, and failure warnings.
- If the book is multi-volume, confirm each volume was processed separately.
- If the book is image-heavy, distinguish page scans, decorative images, and instructional diagrams before claiming deep reading.
- If a unit was only sampled, mark the reading as incomplete and cap the expected grade.

Required deep reading trace block:

```json
{
  "Deep_Reading_Trace": {
    "full_text_file_used": "",
    "structural_units_detected": [],
    "structural_units_processed": [],
    "unit_processing_method": "full_pass | OCR_full_pass | sampled | external_only",
    "recurring_patterns_extracted": [],
    "unprocessed_units": [],
    "deep_reading_claim": true,
    "limitations": []
  }
}
```

Distillation blueprint:

Before writing HTML/PDF, plan what will be built. This is not a decorative outline; it is the execution design for the future agent module.

The blueprint must include:

- Module responsibility: what this book owns inside the total knowledge base.
- Capability target: what the agent will be able to do after ingestion.
- Planned modules: each module's trigger, input, process, output, checker, and repair rule.
- Control parameters: the variables that will become sliders, tags, schemas, or routing rules.
- Cross-module dispatch: which existing books should be called before/after this module.
- Archive scope: what will be included in the formal HTML/PDF and what will be intentionally excluded.
- Expected final grade and the exact conditions required to reach it.

Required blueprint block:

```json
{
  "Distillation_Blueprint": {
    "module_responsibility": "",
    "capability_target": "",
    "planned_executable_modules": [
      {
        "name": "",
        "trigger": [],
        "required_inputs": [],
        "workflow": [],
        "output_schema": {},
        "quality_checker": [],
        "repair_rules": []
      }
    ],
    "control_parameters": {},
    "cross_module_dispatch": [],
    "archive_scope": [],
    "excluded_scope": [],
    "expected_final_grade": "",
    "conditions_to_reach_grade": []
  }
}
```

Hard rule:

- If there is no deep reading trace, do not claim "full-book distillation".
- If there is no distillation blueprint, do not proceed to formal archive generation.
- If the plan only says "蒸馏方向" but does not define trigger/input/workflow/output/checker/repair, mark it as planning-incomplete.

### 1.6 Benchmark Sample And Granularity Gate

When the user provides a Kimi, DeepSeek, Gemini, Claude, or other competing distillation sample, treat it as a **quality benchmark**, not as content to copy.

Before proceeding to formal HTML/PDF generation, compare the planned output against the benchmark and state plainly:

- What the benchmark does well.
- What the current plan/output does better.
- What the current plan/output is still weaker at.
- Whether the current plan/output is **stronger than, equal to, or weaker than** the benchmark for the user's downstream agent knowledge base.
- What must be added before it can beat or match the benchmark.

If the current plan/output is weaker than the benchmark in agent usability, do not archive it as final. Upgrade the analysis or formal module first, unless the user explicitly asks to preserve it only as a temporary note.

Minimum first-step granularity:

Every first-step analysis for a readable full-text book must go beyond "planned modules" and include at least:

- Core model or operating principle extracted from the book.
- Trigger conditions: when the downstream agent should invoke this module.
- Required inputs: what the agent must receive or ask the user for.
- Output schema: what the agent should produce.
- Control parameters: variables, sliders, taxonomies, states, or routing choices.
- Workflow: the procedure the agent can run.
- Quality checker: how to detect whether the method was actually used.
- Negative constraints: what the agent must avoid.
- Repair rules: how the agent should fix failed outputs.
- Cross-module division of labor: how this book differs from related books already in the knowledge base.
- Expected post-distillation grade and why that grade is defensible.

If any of these are missing from the first-step analysis, the response may still be an audit, but it should not claim to be a strong distillation plan. Mark the weakness and repair it before formal generation.

Full reading is necessary but not sufficient:

- A complete text pass only proves source coverage.
- It does not prove agent usability.
- A-level requires converting the book into executable retrieval, generation, reverse-engineering, scoring, and repair behavior.
- If the output remains a concept summary after full reading, cap the grade at **C or B** depending on structure.

Benchmark comparison block:

```json
{
  "Benchmark_Comparison": {
    "benchmark_source": "Kimi | DeepSeek | Gemini | user sample | other",
    "benchmark_strengths": [],
    "our_current_strengths": [],
    "our_current_weaknesses": [],
    "agent_usability_verdict": "stronger | equal | weaker | not_comparable",
    "required_repairs_before_archive": []
  }
}
```

### 1.7 Locked Output Formats

Use locked formats so every book can be compared, audited, and upgraded consistently. Do not improvise a loose structure for book analysis unless the user explicitly asks for a different shape.

First-step analysis format:

````markdown
## 读取自检
- 本地文件：
- 格式/大小：
- 抽取结果：
- 正文规模：
- 图片/图表：
- 乱码/OCR：
- 微信读书：
- 外部校验：
- 旧版状态：

## 完整阅读披露
```json
{
  "Reading_Coverage_Disclosure": {}
}
```

## 深度阅读轨迹
```json
{
  "Deep_Reading_Trace": {}
}
```

## 当前评级与预计评级
```json
{
  "Distillation_Quality_Rating": {}
}
```

## 这本书在知识库中的职责
- 模块类型：
- 主责能力：
- 不负责什么：
- 与相关书籍分工：

## 建议蒸馏名
`...`

## 蒸馏蓝图
```json
{
  "Distillation_Blueprint": {}
}
```

## 准备蒸馏什么
1. 模块名
   - 触发条件：
   - 输入字段：
   - 控制参数：
   - 工作流：
   - 输出字段：
   - 质检器：
   - 修复规则：

## 对智能体的补强
- Before：
- After：
- 新增能力：
- 可做到：
- 不能可靠做到：

## 可调用黑盒 JSON 草案
```json
{}
```

## 对标样例比较（如用户提供）
```json
{
  "Benchmark_Comparison": {}
}
```

## 归档建议
- 是否建议进入正式蒸馏：
- 预计 HTML/PDF 深度：
- 是否替换旧版：
- 临时索引如何更新：
````

Formal archive format:

```markdown
# 书名_AI知识库蒸馏版

## 0. Source Audit And Reading Coverage
## 1. Module Identity And Responsibility
## 2. Invocation Rules / Trigger Conditions
## 3. Required Inputs
## 4. Control Parameters
## 5. Core Methodology Converted To Workflow
## 6. Executable Modules
## 7. Output Schema
## 8. Prompt Templates
## 9. Quality Checker
## 10. Negative Constraints
## 11. Repair Rules
## 12. Cross-Module Dispatch
## 13. Agent Capability Delta
## 14. Black-Box JSON
## 15. Search Tags / Obsidian Links
## 16. Final Rating And Usability Verdict
## 17. AIGC Video Production Interface
## 18. Video Quality, Continuity And Repair
```

Post-generation final reply format:

```markdown
已完成正式蒸馏。

- HTML：
- PDF：
- 旧版处理：
- 索引更新：
- 预计评级：
- 实际评级：
- 是否可供后期智能体调用：
- 若评级变化，原因：
```

Hard rule:

- If the first-step analysis does not follow the locked format, mark it as format-incomplete and repair it before asking the user to confirm.
- If the formal archive does not contain the required archive sections, do not call it A-level.
- The locked format may be expanded for special books, but the required sections must not be removed.

### 1.8 External Model Collaboration Gate

The user may use Kimi, DeepSeek, Gemini, Claude, or another model to perform long-text reading and first-pass distillation. Treat external model output as a **draft supplier and benchmark**, not as verified truth.

Recommended division of labor:

- External model, especially Kimi: long-text reading, chapter-by-chapter notes, examples, first-pass module extraction, language polishing.
- This agent: source audit, coverage verification, anti-pseudo-distillation checks, schema conversion, executable module design, HTML/PDF generation, index update, old-version replacement, and final ABCD rating.

External handoff package required from the user:

```json
{
  "External_Model_Handoff": {
    "model_name": "",
    "source_file_claimed": "",
    "prompt_or_task_used": "",
    "claimed_reading_scope": [],
    "chapter_or_unit_notes": [],
    "proposed_modules": [],
    "control_parameters": {},
    "quality_checkers": [],
    "repair_rules": [],
    "quotes_or_evidence": [],
    "known_limitations": []
  }
}
```

Gatekeeping rules:

- Never accept external output as proof of full reading by itself.
- Verify the external claims against local files, extraction audit, chapter list, keyword distribution, structural coverage, and a complete local reading pass when the source is readable.
- If the external model gives strong content but weak evidence, keep the content as draft material and mark evidence as unverified.
- If external output conflicts with the local text, local text wins.
- If external output is richer than this agent's first analysis, use it as a granularity benchmark and upgrade the plan.
- If external output lacks trigger/input/workflow/output/checker/repair, it is not executable enough for formal archive.
- The final archive must state whether external model material was used and how it was checked.

### 1.8.1 Codex Gatekeeping Requires Bidirectional Full-Text Comparison

For this user's AIGC book-knowledge-base project, **Codex gatekeeping is not a light pre-check**. If the user asks Codex to 守门 an external model draft, the minimum standard is:

1. Codex must read/process the local source itself, not merely inspect metadata, table of contents, keyword hits, or the external model's self-report.
2. Codex must compare the external draft against the local source in both directions:
   - **source-to-draft**: important chapters, sections, images, examples, claims, concepts, warnings, and methods in the local source that the draft omitted or weakened;
   - **draft-to-source**: claims, examples, visual descriptions, modern additions, prompt hooks, ratings, and rules in the draft that are unsupported, misattributed, overgeneralized, or contradicted by the local source.
3. For image-heavy books, Codex must inspect the visual material itself when possible: page thumbnails, extracted images, or rendered representative pages. If images are numerous, use a systematic page/image audit and state the coverage. Do not accept another model's image count or image interpretation as proof.
4. The gatekeeping report must include a **Bidirectional_Gatekeeping_Matrix** before it can be called final.
5. If Codex has only done file verification, extraction statistics, keyword distribution, contact sheets, or structural inspection, label the result as `pre_gate_audit`, `initial_guard_review`, or `守门预审`, not final 守门.
6. A module cannot be rated A or moved to formal archive on the basis of external-model draft quality unless this bidirectional comparison is complete or the limitations are explicitly disclosed and the grade is capped below A.
7. Do not use "Kimi says it read the whole book" or "the draft looks detailed" as a substitute for Codex's own source pass. Detail can be hallucinated; only local evidence and bidirectional comparison distinguish true from false.

Required block:

```json
{
  "Bidirectional_Gatekeeping_Matrix": {
    "codex_local_source_pass_completed": true,
    "source_units_checked": [],
    "source_to_draft_omissions": [
      {
        "source_unit": "",
        "local_evidence": "",
        "draft_gap": "",
        "severity": "minor | moderate | major | fatal",
        "repair_action": ""
      }
    ],
    "draft_to_source_unsupported_claims": [
      {
        "draft_claim": "",
        "local_evidence_status": "verified | partial | unsupported | contradicted",
        "source_location_or_audit_note": "",
        "severity": "minor | moderate | major | fatal",
        "repair_action": ""
      }
    ],
    "image_or_diagram_cross_check": {
      "required": false,
      "coverage": "",
      "unsupported_visual_claims": [],
      "usable_visual_rules": []
    },
    "modern_layer_cross_check": {
      "modern_items_in_draft": [],
      "correctly_layered": [],
      "misattributed_to_book": [],
      "repair_action": []
    },
    "final_gatekeeping_status": "pre_gate_audit | final_gate_pass | final_gate_repair_required | return_to_external_model",
    "grade_cap_if_incomplete": ""
  }
}
```

Hard caps:

- If the local source is readable but Codex has not completed its own source pass, maximum status is `pre_gate_audit`; do not call it final 守门.
- If the bidirectional matrix is absent, maximum grade is **B+ / A-**, and formal archive must pause unless the user explicitly accepts a temporary non-final module.
- If multiple major unsupported draft claims are found, cap at **B** until repaired.
- If the draft attributes modern supplements, external knowledge, or invented examples to the book, A is forbidden until provenance is repaired.

External comparison block:

```json
{
  "External_Model_Gatekeeping_Report": {
    "external_model_used": true,
    "accepted_as": "draft | benchmark | rejected | partial",
    "verified_against_local_text": true,
    "coverage_match": "full | partial | unclear | conflict",
    "useful_contributions": [],
    "rejected_or_repaired_claims": [],
    "remaining_risks": [],
    "gatekeeper_verdict": ""
  }
}
```

### 1.9 Original-Book Evidence And Modern-Adaptation Layers

Keep old-book modernization useful without contaminating attribution. A model's awareness of the current date does not prove which rules came from the book, which were added later, or which channels they fit.

Activate provenance layering when any of these apply:

- The book's medium, software, channel, technology, or operating context is dated.
- The method is being adapted to short video, ecommerce, social media, AIGC, current software, or current platform rules.
- An external model added modern knowledge absent from the local text.
- Current compliance, platform, technical, or ethical constraints modify the historical method.
- Local pages are missing, damaged, unread, sampled, or supplemented externally.
- The archive combines book-derived methodology with Codex engineering extensions.

Use these layers:

- `original_book`: locally verified book content.
- `modern_supplement`: current adaptation; never attribute it to the book.
- `related_module`: knowledge owned by another archived module; route to it instead of duplicating it.
- `unverified_external`: plausible external/model material without sufficient local evidence; exclude it from autonomous execution.
- `unavailable_source`: content hidden by missing pages, damaged images, unread scope, or failed OCR; never fill it silently from general knowledge.

Attach provenance to important rules, lists, controls, prompts, and schema fields:

```json
{
  "knowledge_layer": "original_book | modern_supplement | related_module | unverified_external | unavailable_source",
  "source_status": "verified_local | partial_local | external_verified | unavailable",
  "attributed_to_book": true,
  "applicable_period": "original_context | current",
  "applicable_channels": [],
  "requires_current_validation": false
}
```

Rules:

- Preserve dated original wording or categories when they are methodologically meaningful. Add a modern interpretation beside them; do not replace them because they look old-fashioned.
- Put modern hooks, platform terminology, software controls, CTA patterns, A/B testing, and current compliance rules in `modern_supplement` unless the local book explicitly contains them.
- Prefer cross-module dispatch when an existing module already owns the modern capability.
- Never use modern supplements to hide missing pages, unread scope, OCR limits, or weak source evidence.
- When the modern rule conflicts with the book, state both scopes and routing conditions; never silently overwrite the book.
- Add provenance-confusion checks to the Quality Checker: wrong attribution, period mismatch, channel mismatch, and supplement presented as book content.
- Do not require layering when the archive contains only verified book methodology, when wording changes preserve the same rule and attribution, or when modern behavior is fully delegated to another module.

Rating:

- Score original-book fidelity separately from modern executability.
- Strong modern adaptation cannot raise the evidence grade of incomplete book coverage.
- Unmarked source mixing, wholesale list replacement, or false attribution forbids A. If it can contaminate autonomous execution, cap the module at B until repaired.

### 1.9.1 Creative Risk Gates Are Not Blanket Bans

For film, horror, crime, war, psychological, historical-trauma, domestic-violence, child-fear, gender-oppression, colonial-history, body-horror, or other art-making modules, do not treat `Gate`, `Safety Gate`, `Blocker`, or `Constraint` as automatic removal or artistic sanitization.

Default meaning: **route and control, not blanket ban**.

Use gates to:

- separate source layers: original book evidence, film case evidence, external-model draft, modern AIGC translation, current safety/copyright/ethics constraints;
- route work to the right creative module: writing, performance, camera, sound, editing, production design, historical context, adaptation boundary, or safety QC;
- control intensity: keep darkness, conflict, violence, oppression, fear, discomfort, and moral ugliness when they serve the work, but specify view, distance, explicitness, offscreen/aftermath/symbolic treatment, and narrative function;
- extract method instead of copying: learn the cinematic function rather than reproducing exact frames, actor likenesses, book images, concrete music tracks, or protected compositions;
- repair cheap outputs: if AIGC collapses into gore, ghost faces, shock, trauma decoration, or conspiracy-as-fact, repair toward stronger story, space, performance, sound, history, and theme.

Rules:

1. Dark content, violent conflict, horror devices, oppressive relationships, and moral discomfort are not grading penalties by themselves. If local evidence supports them and they serve story, character, space, sound, history, or aesthetics, preserve them as executable creative controls.
2. Use hard blocking only for unauthorized recognizable real-person likeness, exact protected frame/image/music copying, sensationalized child or vulnerable-subject victimization, operational harm instructions, decorative use of real trauma, conspiracy theory presented as fact, or modern supplements falsely attributed to the book.
3. Preserve style calls when the user asks for them. Convert director/type/era/film style names into observable parameters: shot duration, camera height, movement, composition, material, sound function, editing rhythm, performance intensity, and spatial relation. Do not delete a useful style call merely because it has risk.
4. Prefer fields such as `allowed_use`, `representation_mode`, `intensity_control`, `narrative_function`, and `repair_rule` over a flat `blocked` label.
5. Separate artistic negative constraints from safety/copyright/source constraints. "Do not make it cheap jump scare" is a quality constraint; "do not recreate a specific actor's face" is a likeness/copyright constraint.
6. In formal archives, prefer gate names like `Router`, `Intensity Control`, `Representation Mode`, `Context Gate`, or `Style Call Gate` when the intent is controlled use rather than prohibition.

Recommended field:

```json
{
  "creative_risk_gate": {
    "default_policy": "route_and_control_not_blanket_ban",
    "allowed_use": [],
    "representation_mode": "direct | restrained | implied | offscreen | aftermath | symbolic | blocked",
    "intensity_level": "low | medium | high | extreme_blocked",
    "narrative_function": "",
    "source_layer": "original_book | case_derived_transfer | modern_supplement | safety_constraint",
    "must_not_degrade_into": [],
    "repair_rule": ""
  }
}
```

### 1.10 AIGC Video Production Interface

Every analysis and formal archive must classify the module's relationship to AIGC video:

```json
{
  "AIGC_Video_Production_Interface": {
    "aigc_video_role": "core | support | reference | not_directly_applicable",
    "production_stages": [
      "development | writing | preproduction | generation | postproduction | distribution | quality_control"
    ],
    "supported_content_types": [
      "ai_short_drama | film | novel_adaptation | advertisement | concept_film | trailer | brand_content | short_video"
    ],
    "upstream_inputs": [],
    "video_control_parameters": {},
    "structured_handoff": {},
    "downstream_modules": [],
    "generation_prompt_hooks": [],
    "video_quality_checks": [],
    "video_repair_rules": [],
    "cross_shot_consistency_rules": []
  }
}
```

Map the book only to controls it genuinely owns:

| Book responsibility | Video-production conversion |
|---|---|
| Narrative / screenwriting | scene goal, conflict, beat, reveal, character state, scene entry/exit, adaptation constraint |
| Character / dialogue / acting | objective, subtext, action verb, emotional turn, performance intensity, voice, eye-line, reaction |
| Directing / camera | shot size, camera position, lens intent, movement, blocking, axis, eye-line, spatial continuity |
| Production design / worldbuilding / style | set assets, architecture, material, costume, prop, period, culture, weather, motif, forbidden elements |
| Lighting / color | motivated source, direction, softness, contrast, exposure, color temperature, palette relationship, shot matching |
| Editing / sound | cut point, duration, rhythm, transition, sound point of view, ambience, music function, audiovisual relationship |
| Advertising / brand | audience, desire, brand persona, communication goal, audiovisual hook, proof, CTA, channel version |
| Novel / literature | adaptable scene unit, relationship state, point of view, key image, world rule, protected source boundary |
| Theory / research | decision lens, diagnostic questions, evidence requirement, bias check, applicable and excluded conditions |

Rules:

- A prompt is an interface, not proof of capability. Also provide structured output, checks, and repairs.
- Translate abstract style words into observable properties. Reject adjective-only prompt lists.
- Separate `original_book` methodology from Codex's video conversion and current model/platform controls.
- Include a `structured_handoff` that a downstream script, storyboard, image, video, sound, editing, or QC agent can consume.
- For indirect books, specify the upstream decision or constraint and the specialist module that performs production.
- Add video-specific checks to the Quality Checker.
- Add repair routing to writing, storyboard, generation prompt, asset bible, continuity state, editing, sound, color, or distribution as applicable.

### 1.11 Legacy Module Video Reinforcement

After the main book backlog is distilled, audit existing formal modules for missing AIGC video interfaces. Do not automatically re-distill every book.

Use these levels:

- `V0_no_interface`: summary/general-agent module; no video handoff.
- `V1_routable`: production stage and downstream routing exist, but controls are vague.
- `V2_executable`: inputs, controls, structured handoff, prompt hooks, checks, and repairs exist.
- `V3_production_ready`: adds cross-shot consistency, SOP dispatch, failure routing, and verifiable delivery.

Workflow:

1. Scan formal HTML/PDF, Manifest, replacement records, and rating tables.
2. Record module name, source grade, current video level, missing interface fields, domain, priority, and related modules.
3. Prefer incremental reinforcement when source audit and core methodology are already sound.
4. Re-distill only when the existing module is thin, factually unreliable, missing source coverage, or cannot support the required interface.
5. Reinforce by domain batches: narrative; character/dialogue; directing/camera; production design/style; lighting/color; editing/sound; advertising/brand; novel adaptation.
6. Preserve one primary module entry. Update the existing archive and Manifest instead of creating parallel untracked main versions.
7. Keep source fidelity grade separate from `video_production_level`; modern video adaptation cannot raise book-evidence quality.
8. Require a reinforcement queue and post-update self-check.

Minimum reinforcement record:

```json
{
  "module_title": "",
  "source_grade": "",
  "video_production_level_before": "V0 | V1 | V2 | V3",
  "missing_video_fields": [],
  "reinforcement_mode": "incremental | partial_redistill | full_redistill",
  "priority": "P0 | P1 | P2",
  "video_production_level_after": "",
  "manifest_updated": false,
  "status": "pending | completed | blocked"
}
```

### 2. Knowledge-Base Role

Classify what the book is responsible for inside the user's system.

Do not classify only by subject. Classify by agent capability:

- Narrative structure
- Shot/camera/lens/blocking
- Editing/sound/rhythm
- Color/light/visual style
- Advertising/copy/conversion
- Media/platform/distribution
- Layout/type/motion design
- Worldbuilding/genre/lore
- Character/dialogue/performance
- Research/control/quality evaluation

State whether the book is:

- A **core engine**: provides a reusable operating model.
- A **specialist module**: handles one narrow capability.
- A **preset library**: provides cases, styles, or examples.
- An **upgrade**: deepens or replaces an older distillation.
- A **reference supplement**: useful but not a standalone module.

### 3. Core Methodology Extraction

Extract the reusable method, not chapter-by-chapter notes.

Look for:

- Concepts that become controls, sliders, parameters, or tags.
- Step-by-step processes that become workflows.
- Diagnostic rules that become quality checks.
- Contrasts, taxonomies, matrices, or decision trees.
- Anti-patterns, negative constraints, and failure cases.
- Examples that reveal method, without reproducing protected text.

Avoid:

- Long book summaries.
- Full chapter replacement.
- Decorative quotes.
- Overly generic "this book is about creativity/storytelling/design" claims.

### 4. Agent Capability Delta

Every formal distillation must explain how the user's agent improves after this book is added.

Use this exact structure when possible:

```json
{
  "Agent_Capability_Delta": {
    "Before": "What the agent tended to do poorly, vaguely, or incorrectly before this module.",
    "After": "What the agent can now judge, generate, route, or verify.",
    "New_Controls": ["parameters, panels, checkers, routing rules, taxonomies"],
    "Use_When": ["tasks or user intents that should trigger this module"],
    "Quality_Gain": "How output quality improves and how that improvement can be verified."
  }
}
```

Keep this section practical. It should answer: **what can the agent do now that it could not reliably do before?**

### 5. JSON And Search Layers

Create a black-box JSON layer for future retrieval, routing, and Obsidian/Notebook migration.

Use this base schema and adapt only where needed:

```json
{
  "module_identity": {
    "book_title": "",
    "author": "",
    "module_name": "",
    "module_type": "core_engine | specialist_module | preset_library | upgrade | supplement",
    "knowledge_domain": []
  },
  "source_audit": {
    "local_full_text": "",
    "weread_check": "",
    "external_verification": [],
    "extraction_quality": "",
    "existing_version_status": ""
  },
  "trigger_conditions": [],
  "core_methodology": {
    "principles": [],
    "models": [],
    "workflow": [],
    "decision_rules": []
  },
  "agent_capability_delta": {
    "before": "",
    "after": "",
    "new_controls": [],
    "use_when": [],
    "quality_gain": ""
  },
  "input_schema": {},
  "output_schema": {},
  "quality_checks": [],
  "negative_constraints": [],
  "related_modules": [],
  "obsidian_links": {
    "aliases": [],
    "tags": [],
    "backlinks": [],
    "map_of_content": ""
  }
}
```

At minimum, every formal archive should expose these retrieval/execution blocks somewhere in the HTML/PDF:

```json
{
  "trigger_conditions": [],
  "required_inputs": {},
  "control_parameters": {},
  "workflow": [],
  "output_schema": {},
  "prompt_templates": [],
  "quality_checks": [],
  "negative_constraints": [],
  "repair_rules": [],
  "cross_module_links": [],
  "knowledge_provenance": [],
  "aigc_video_production_interface": {},
  "video_quality_checks": [],
  "cross_shot_consistency_rules": []
}
```

If a book's domain makes one block inapplicable, explain why and replace it with the nearest equivalent. Do not omit silently.

### 6. Prompt And Output Templates

When the book provides an actionable method, include at least one direct-use prompt template.

Prompt templates should include:

- Role: what specialist agent is being invoked.
- Inputs: what the user must provide.
- Required output fields.
- Checks: how to verify the result used the method.
- Negative constraints: what not to do.

### 7. Quality Checker

Add a compact checker that can grade whether an output actually used the distilled module.

Good checkers ask:

- Did the output use the book's specific controls or just generic words?
- Are the controls connected to story/user intent/business goal?
- Are required fields missing?
- Are there contradictions between parameters?
- Are negative constraints respected?
- Can the result be routed to related modules?

### 8. Knowledge Links

End by naming where the module sits in the larger knowledge base.

Include:

- Primary domain/module.
- Secondary domains.
- Related existing books/modules.
- Whether it upgrades, duplicates, or complements an older distillation.
- Suggested Obsidian tags and backlinks.

Use links to local files when referencing real project artifacts.

## Output Shapes

### Audit-Only Output

Use when the user has not confirmed final generation:

```markdown
## Reading Audit
## Three-Source Verification
## Existing Version Decision
## Recommended Handling
## Planned Distillation
## Expected Agent Capability Delta
## Formal Archive Recommendation
```

### Formal Distillation Output

Use when the user asks for the final module:

```markdown
## Source Audit
## Core Distillation Value
## Trigger Conditions
## Core Methodology
## Parameters / Control Panel
## Agent Invocation JSON
## Prompt Template
## Quality Checker
## Agent Capability Delta
## Existing Knowledge-Base Links
## Negative Constraints
## One-Sentence System Instruction
```

## Style Rules

- Write in the user's knowledge-base style: dense, modular, practical, and agent-oriented.
- Prefer "engine", "control panel", "checker", "router", "matrix", and "schema" only when they describe real reusable behavior.
- Keep source-audit claims evidence-backed.
- Do not pretend the full book was read if only metadata or excerpts were available.
- Do not generate final HTML/PDF before the user confirms when evidence or versioning is uncertain.
- Preserve older versions when upgrading unless the user explicitly asks to overwrite.
