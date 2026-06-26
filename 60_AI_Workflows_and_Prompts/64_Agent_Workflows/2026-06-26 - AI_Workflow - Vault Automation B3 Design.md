# Vault Automation B3 Design

## Scope

This design specifies a semi-automatic Obsidian vault governance system for `/Users/bulldize/Desktop/Obsidian`.

The system follows the B3 strategy:

- Inbox triage every 4 days at `18:00` Asia/Shanghai.
- Vault maintenance every 2 weeks on Monday at `18:15` Asia/Shanghai.
- Low-risk content can be automatically organized.
- High-risk content remains in Inbox and receives a confirmation proposal.
- All actions are reported in daily notes or biweekly maintenance reports.

This document is a design spec only. It does not implement automations, scripts, or file moves.

## Source Of Truth

Automation behavior must follow these files:

- `AGENTS.md`
- `WORKSPACE_RULES.md`
- `99_Meta/Global Tag List.md`
- `99_Meta/Templates`

Automation must not modify these source-of-truth files unless the user explicitly requests it.

## Architecture

### Inbox Triage

Input:

```text
00_Inbox_and_Journal/02_Inbox
```

Schedule:

```text
Every 4 days at 18:00 Asia/Shanghai
```

Flow:

```text
00_Inbox_and_Journal/02_Inbox
        |
        v
[Inbox Triage]
        |
        +--> Low Risk: automatic migration
        |       - rename
        |       - add YAML
        |       - add abstract
        |       - add tags
        |       - add bidirectional links
        |
        +--> High Risk: confirmation proposal only
        |       - keep in Inbox
        |       - suggest target directory
        |       - state risk reason
        |       - suggest tags and summary
        |
        v
00_Inbox_and_Journal/01_Daily_Notes/YYYY-MM-DD.md
```

### Vault Maintenance

Schedule:

```text
Every 2 weeks on Monday at 18:15 Asia/Shanghai
```

Flow:

```text
Vault root
        |
        v
[Vault Maintenance]
        |
        +--> empty file scan
        +--> orphan note scan
        +--> invalid asset scan
        +--> tag anomaly scan
        +--> high-risk backlog scan
        |
        v
00_Inbox_and_Journal/01_Daily_Notes/YYYY-MM-DD - Biweekly Vault Maintenance.md
```

## Risk Strategy

### Low Risk: Automatic Organization Allowed

The automation can organize content that belongs to one of these categories:

- AI tool usage experience.
- Prompt templates.
- Codex / Gemini / OpenClaw configuration records.
- Environment setup notes and tool pitfalls.
- Ordinary meeting notes.
- Daily logs.
- External technical blog summaries.
- Code error logs and debugging process records.
- Simulation run logs and parameter trials, as long as they are not final control conclusions.
- Paper screening notes with `#Status/待精读`.
- Mathematical inspiration drafts with `#Status/推导中` or `#Status/逻辑断点`.
- Engineering ideas with `#Status/待跑通`.
- Repeated material types whose target directory and tags are already clear.

Automatic organization can use only cautious language:

- 草稿
- 初筛
- 待验证
- 待精读
- 调试记录
- 运行记录
- 整理稿

### High Risk: Confirmation Required

The automation must not move or rewrite content that matches any of these categories:

#### Mathematical conclusions

- Convergence proofs.
- Error estimate conclusions.
- Functional analysis theorem applicability conditions.
- Core Giesekus scheme derivations.
- Any content written as "已证明", "可得", "定理", or equivalent final theorem language.

#### Anesthesia TCI safety boundary

- Real hardware real-time control.
- Dosage strategy suggestions.
- Clinical decision language.
- PK/PD parameter conclusions.
- PINN surrogate model validity assertions.

#### Nuclear engineering control boundary

- Final PID parameter conclusions.
- Simulink model structure changes.
- Nuclear power system safety inferences.
- Reinforcement learning associations.

#### Medical data and privacy

- Patient-related materials.
- Non-anonymized data.
- Medical images with unclear provenance.
- Medical conclusions or diagnosis suggestions.

#### First migration for a new formal topic

When a new topic is first moved from Inbox to a formal directory, the automation must request user confirmation.

### Forbidden Automatic Language

The automation must not automatically write:

- 已证明
- 已验证
- 最终结论
- 临床建议
- 控制策略
- 可直接应用

## File Processing Rules

### Input Rule

All new unstructured material goes to:

```text
00_Inbox_and_Journal/02_Inbox
```

Inbox triage scans only this Inbox for migration. It does not proactively migrate content from formal directories.

### Naming Rule

Automatically migrated low-risk Markdown files use:

```text
YYYYMMDD - [领域/项目] - 标题.md
```

Examples:

```text
20260626 - AI_Workflow - Codex整理Inbox流程复盘.md
20260626 - Engineering - Simulink报错日志整理.md
20260626 - Math - Giesekus模型推导灵感草稿.md
```

If the title cannot be judged reliably, the file remains in Inbox and receives a report entry:

```text
YYYYMMDD - Inbox - 待人工命名.md
```

### YAML Metadata

Automatically migrated Markdown files must include YAML:

```yaml
---
created: 2026-06-26
source: inbox
status: draft
risk_level: low
tags:
  - Math
  - Giesekus模型
  - Status/推导中
summary: "100 字以内摘要。"
---
```

The exact tags must follow `99_Meta/Global Tag List.md`.

High-risk files are not modified; their metadata suggestions appear only in the Inbox triage report.

### Body Structure

Automatically migrated low-risk notes use this structure:

```md
# 标题

## Abstract

100 字以内摘要。

## Source

- 原始文件：
- 来源类型：
- 自动处理时间：

## Notes

原始内容清洗后的主体。

## Links

- 相关目录：
- 相关概念：
```

### Attachment Handling

- PDF, image, video, and dataset files are not moved automatically.
- The report can suggest target locations.
- If an attachment is clearly bound to a low-risk Markdown note, the Markdown note can preserve relative links.
- Large datasets are not copied. Only paths, metadata, or source links are recorded.

## Directory Routing Rules

### AI Workflows And Tool Experience

Target:

```text
60_AI_Workflows_and_Prompts
```

Routing:

- Prompt templates -> `61_Prompt_Library`
- Tool skills, pitfalls, MCP, Codex configuration -> `62_AI_Skills_and_Logs`
- Custom system instructions -> `63_Custom_Instructions`
- Automation flows and retrospectives -> `64_Agent_Workflows`

### Logs And Daily Records

Target:

```text
00_Inbox_and_Journal/01_Daily_Notes
```

Includes:

- Daily logs.
- Ordinary meeting notes.
- Work records that do not assert research conclusions.

### Mathematical Inspiration Drafts

Target:

```text
10_Math_and_Theory
```

Allowed only when status and language remain draft-level:

- `#Status/推导中`
- `#Status/逻辑断点`
- `#理论草稿`

Routing:

- Giesekus -> `11_Giesekus_Model`
- Functional analysis -> `12_Functional_Analysis`
- FEM -> `13_Finite_Element_Method`

The automation must not state final theorems or conclusions.

### Engineering Debug Records

Target:

```text
40_Engineering_and_Other
```

Allowed:

- Debug records.
- Run records.
- Parameter trials.
- Ideas marked `#Status/待跑通`.

Routing:

- Simulink / PID / nuclear pressurizer -> `41_Nuclear_Simulation`
- ADAS / RCR -> `42_Auto_Driving`
- Environment and node configuration -> `43_Agent_and_Infra`

### Medical AI Screening Notes

Possible targets:

```text
20_Dentistry
30_Anesthesia_TCI
```

Must satisfy:

- Status is `#Status/待精读`.
- No clinical advice.
- No final assertion of model validity.
- No patient privacy or non-anonymized data.

### High-Risk Routing Proposal

High-risk content remains in Inbox. The Inbox triage report includes:

```md
### 待确认迁移：文件名

- 建议目录：
- 风险等级：
- 风险原因：
- 建议标签：
- 建议摘要：
- 需要你确认的问题：
```

## Report Formats

### Inbox Triage Report

Location:

```text
00_Inbox_and_Journal/01_Daily_Notes/YYYY-MM-DD.md
```

Append section:

```md
## Inbox Triage Report

### 自动迁移

| 原文件 | 新位置 | 风险 | 标签 | 说明 |
|---|---|---|---|---|
|  |  | low |  |  |

### 待确认迁移

#### 文件名

- 建议目录：
- 风险等级：
- 风险原因：
- 建议文件名：
- 建议标签：
- 建议摘要：
- 需要你确认的问题：

### 留在 Inbox

| 文件 | 原因 | 下一步 |
|---|---|---|
|  | 信息不足 / 命名不清 / 无法判断 | 人工补充上下文 |

### 异常

- 文件读取失败：
- 链接解析失败：
- 标签冲突：
```

Rules:

- Append only; do not overwrite existing daily note content.
- If the daily note does not exist, create it.
- Do not paste long source text into reports.
- For high-risk materials, report proposals only.

### Biweekly Vault Maintenance Report

Location:

```text
00_Inbox_and_Journal/01_Daily_Notes/YYYY-MM-DD - Biweekly Vault Maintenance.md
```

Structure:

```md
# Biweekly Vault Maintenance - YYYY-MM-DD

## Summary

- 扫描范围：
- 空文件数量：
- 孤立节点数量：
- 无效附件数量：
- 标签异常数量：
- 高风险积压数量：

## Empty Files

| 文件 | 建议 |
|---|---|

## Orphan Notes

| 文件 | 建议链接方向 |
|---|---|

## Invalid Assets

| 附件 | 问题 | 建议 |
|---|---|---|

## Tag Issues

| 文件 | 问题 | 建议 |
|---|---|---|

## High Risk Backlog

| 文件 | 风险原因 | 建议动作 |
|---|---|---|

## Suggested Distillation

| 来源 | 可沉淀资产 | 目标目录 |
|---|---|---|
```

## Distill Rules

Automation can propose asset distillation when repeated or closed-loop patterns appear.

### Theory Assets

Triggers:

- Same topic appears repeatedly.
- Derivation chain becomes nearly complete.
- Reusable lemma, estimate technique, or discretization structure appears.
- Content relates to `#有限元_FEM`, `#Giesekus模型`, or `#泛函分析`.

Target:

```text
10_Math_and_Theory
```

Automation only proposes theory distillation; it does not write final theory conclusions.

### Code Assets

Triggers:

- Stable reusable function appears in debug logs.
- Same script pattern appears across projects.
- Environment setup or data processing process can be templated.

Targets:

```text
40_Engineering_and_Other/43_Agent_and_Infra
60_AI_Workflows_and_Prompts/64_Agent_Workflows
```

If real project code is involved, automation proposes extraction but does not rewrite project code.

### Prompt And AI Workflow Assets

Triggers:

- Reusable Prompt appears in AI dialogue.
- Codex / Gemini / OpenClaw process proves effective.
- Paper reproduction, debugging, or note-cleaning workflow can be standardized.

Targets:

```text
60_AI_Workflows_and_Prompts/61_Prompt_Library
60_AI_Workflows_and_Prompts/64_Agent_Workflows
```

Low-risk prompt and workflow assets can be automatically distilled as drafts.

## Retrieve Rules

When a new task starts or a task is blocked, Codex should retrieve context in this order:

1. `WORKSPACE_RULES.md`
2. `99_Meta/Global Tag List.md`
3. Relevant domain index files.
4. `60_AI_Workflows_and_Prompts`
5. Historical `Inbox Triage Report` sections.
6. Historical `Biweekly Vault Maintenance` reports.
7. Relevant project notes, reproduction records, debug records, and theory drafts.

Typical retrieval goals:

- Find historical errors and fixes.
- Find similar mathematical structures or proof techniques.
- Find reusable prompts.
- Find paper reproduction templates.
- Generate literature review outlines.
- Generate proposal or opening-report outlines from tagged notes.

### Cross-Domain Connection Rule

Codex may propose cross-domain links, but must mark them as tentative:

```md
> [!note] 跨域启发，待人工验证
```

Examples:

- FEM mesh concepts <-> medical image 3D mesh processing.
- PINN physical constraints <-> PK/PD surrogate modeling.
- Giesekus numerical stability <-> nonlinear dynamical simulation stability.

## Failure Handling

### Read Failure

Keep the file in place and record:

```md
### 异常

- 文件读取失败：路径
- 原因：
- 建议：
```

### Low Classification Confidence

Keep the file in Inbox and record:

```md
### 留在 Inbox

| 文件 | 原因 | 下一步 |
|---|---|---|
| 文件名 | 分类置信度不足 | 人工补充上下文 |
```

### Tag Conflict

Do not force tag changes. Report:

```md
- 标签冲突：文件名
- 当前标签：
- 建议标签：
- 需要确认：
```

### Filename Conflict

If a target filename exists, append a numeric suffix:

```text
YYYYMMDD - Domain - Title.md
YYYYMMDD - Domain - Title - 2.md
```

Record the conflict and final path in the Inbox triage report.

### Automation Interruption

The next run rescans Inbox.

Already migrated files are not reprocessed if:

- They are no longer in Inbox.
- Their YAML contains `source: inbox`.
- They appear in a prior Inbox triage migration report.

## Audit Logs

Each run should create a light audit log:

```text
99_Meta/Automation Logs/YYYY-MM-DD - Inbox Triage Log.md
99_Meta/Automation Logs/YYYY-MM-DD - Biweekly Maintenance Log.md
```

Logs record:

- Run time.
- Number of scanned files.
- Number of automatic migrations.
- Number of confirmation-required files.
- Number of exceptions.
- Concrete operation paths.

## Non-Goals

The system does not:

- Delete files.
- Overwrite original content.
- Move PDFs, images, videos, or datasets automatically.
- Move high-risk content into formal directories.
- Rewrite mathematical proof conclusions.
- Generate clinical advice.
- Generate real control strategies.
- Modify `AGENTS.md`, `WORKSPACE_RULES.md`, or `99_Meta/Global Tag List.md` without explicit user request.

## Open Implementation Decisions

These are intentionally left for the implementation plan:

- Whether scheduling is implemented through Codex automations, a local script, or both.
- Whether semantic classification is performed entirely by Codex or assisted by a deterministic pre-scan script.
- Exact MCP calls or filesystem operations used during implementation.
- Whether the vault should be initialized as a git repository before automation is enabled.
