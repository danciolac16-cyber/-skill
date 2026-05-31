---
name: agent-book-distillation
description: Use when distilling books into an AI-agent knowledge base module with three-source verification, full-text extraction checks, core methodology, agent capability gains, JSON/search layers, prompt templates, quality checks, and Obsidian/Notebook-ready knowledge links.
metadata:
  short-description: Distill books into agent-ready knowledge modules
---

# Agent Book Distillation

Use this skill when the user provides or references a book and wants it turned into a reusable AI-agent knowledge module rather than a normal summary.

The goal is not "what the book says." The goal is: **what new capability this book gives the user's agents, how that capability is invoked, and how it should be stored for retrieval in an external knowledge base.**

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

### 1. Source Audit

Produce a concise self-check before distillation:

- Local file path(s), format, size, and readable status.
- Extraction workspace path, if created.
- Extracted text scale: characters/words, line count, page count, chapter count, or internal file count.
- OCR/text quality: mojibake/noise, missing pages, repeated headers, encryption, broken encoding.
- WeRead lookup result: title/author/version found or not found.
- External verification: official/publisher/catalog sources and what each confirms.
- Existing distillation status: none, old version, upgraded version, duplicate risk.

Recommended table:

```markdown
| Evidence Layer | Result | Reliability | Notes |
|---|---|---:|---|
| Local full text | ... | High/Medium/Low | ... |
| WeRead | ... | Medium/Low | ... |
| External sources | ... | Medium/Low | ... |
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
