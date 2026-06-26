# 个人知识库沉淀规范 & Codex 处理规则

## 一、文件命名规范（强制统一）

格式：

```text
YYYYMMDD - [学科大类/项目] - 核心概念/论文简写.md
```

示例：

- `20260625 - Math - Giesekus模型二维收敛性分析草稿.md`
- `20260625 - Dentistry - 牙槽骨嵴曲线无监督提取综述.md`
- `20260625 - Quant - 基于Black-Scholes的期权定价笔记.md`

## 二、目录流转与处理权责

1. **00_Inbox_and_Journal/02_Inbox**：唯一入口。所有网页剪报、AI 零散对话、闪念、未精读的文献，必须先存入此处。AI 代理禁止未经用户确认直接将新内容写入正式目录。
2. **10_Math_and_Theory**：仅存放经过推导验证的数学理论与 FEM 基础。要求逻辑严密，不可存放未经验证的碎片结论。
3. **20_Dentistry & 30_Anesthesia_TCI**：医疗 AI 垂直领域。按具体项目（如分割、靶控建模）存放精读文献、复现模板与数据分析报告。
4. **40_Engineering_and_Other**：工程项目沉淀区。
5. **60_AI_Workflows_and_Prompts**：AI 代理主动识别并提取的高效 Prompt、复现工作流与技巧，统一沉淀至此。
6. **99_Meta**：全局模板库。所有新增的标准格式（如科研复现、理论证明）均需从此处调用。

## 三、标签体系规则（Tagging System）

标签体系以 [[99_Meta/Global Tag List|个人知识库统一标签清单]] 为准。

采用混合分层规则：

1. **一级领域标签用英文**：例如 `#Math`, `#Dentistry`, `#Anesthesia`, `#Engineering`, `#Quant`。
2. **研究模块标签用中文或通用术语**：例如 `#Giesekus模型`, `#有限元_FEM`, `#CBCT分割`, `#PK_PD建模`。
3. **状态、工具、数据集使用嵌套标签**：例如 `#Status/推导中`, `#Status/已复现`, `#Tool/Codex`, `#Dataset/WestChina`。

所有转出 Inbox 的正式文档至少包含：

- 1 个领域标签
- 1 个研究模块或文档类型标签
- 1 个状态标签

## 四、Codex AI 强制沉淀与处理规则

### 1. 前置约束

执行任何归档、总结或提取操作前，必须优先读取本规则，严格遵循命名与目录规范。

### 2. 研究边界强制过滤

- 处理或关联**麻醉靶控（TCI）**相关资料时，严格聚焦于“离线仿真回放”与“影子自适应评估”，自动剔除或标注任何涉及真实硬件实时控制的冗余内容。
- 梳理**核动力仿真**笔记时，核心锚定 MATLAB/Simulink 数值求解与 PID 控制逻辑，强制隔离且不建立任何与强化学习（RL）相关的关联。

### 3. 理论严谨性校验

整理泛函分析笔记（如紧嵌入定理、Bramble-Hilbert 引理的应用）时，若发现推导逻辑链条断裂或条件缺失，必须在文档顶部添加：

```markdown
> [!warning] 逻辑断点待人工核查
```

### 4. 智能摘要与元数据生成

对于迁入正式目录的文献笔记，自动在文首生成 100 字以内的学术摘要（Abstract），并自动补全 YAML 区的作者、年份、DOI 字段。

### 5. 双向链接网络构建

自动识别跨学科概念。例如，当在“Giesekus 模型”中识别到“网格划分”或“Sobolev 空间”时，必须主动使用 `[[ ]]` 语法链接至 `12_Functional_Analysis` 或 `13_Finite_Element_Method` 的基础概念笔记。

### 6. 知识提纯与资产化

当在 `00_Inbox_and_Journal/02_Inbox` 的 AI 对话记录中识别到成功跑通的完整逻辑或极具价值的提示词（Prompt）时，Codex 需主动建议将其抽象化，并剥离至 `60_AI_Workflows_and_Prompts` 目录。

### 7. 定期清理

每周自动扫描空文件、孤立节点（无任何双链的正式笔记）以及无效附件，并输出清理建议清单至 `00_Inbox_and_Journal/01_Daily_Notes`。

## 五、Codex 定时自动化规则

### 1. Daily Inbox Triage

每日 `18:00`（Asia/Shanghai）扫描 `00_Inbox_and_Journal/02_Inbox`。

允许自动处理低风险内容：

- AI 工具使用经验、Prompt 模板、环境配置与踩坑记录。
- 普通会议纪要、日常日志、外部技术博客摘要。
- 代码报错日志、调试过程记录、仿真运行日志和参数尝试记录，但不得总结为最终控制结论。
- 论文初筛笔记，状态必须为 `#Status/待精读`。
- 数学灵感草稿，状态必须为 `#Status/推导中` 或 `#Status/逻辑断点`。
- 工程构想，状态必须为 `#Status/待跑通`。

高风险内容必须留在 Inbox，只生成待确认迁移建议：

- 收敛性证明、误差估计结论、核心 Giesekus 格式推导、泛函分析定理适用条件。
- 麻醉 TCI 真实硬件实时控制、剂量策略、临床决策、PK/PD 参数结论、PINN 有效性断言。
- 核动力仿真中的 PID 最终参数、Simulink 模型结构变更、安全相关推断、强化学习关联内容。
- 患者资料、未脱敏医学数据、来源不明医学影像、医学诊断或临床结论。
- 新主题首次迁入正式目录。

每日报告追加到：

```text
00_Inbox_and_Journal/01_Daily_Notes/YYYY-MM-DD.md
```

审计日志写入：

```text
99_Meta/Automation Logs/YYYY-MM-DD - Inbox Triage Log.md
```

### 2. Weekly Vault Maintenance

每周一 `18:15`（Asia/Shanghai）扫描全库并生成维护报告。

扫描范围：

- 空文件。
- 孤立节点。
- 无效附件。
- 标签异常。
- 高风险积压。
- 可沉淀资产建议。

周报写入：

```text
00_Inbox_and_Journal/01_Daily_Notes/YYYY-MM-DD - Weekly Vault Maintenance.md
```

审计日志写入：

```text
99_Meta/Automation Logs/YYYY-MM-DD - Weekly Maintenance Log.md
```

### 3. 自动化禁止事项

- 不删除文件。
- 不覆盖原始内容。
- 不自动移动 PDF、图片、视频、数据集等附件。
- 不移动高风险内容。
- 不改写数学证明结论。
- 不生成临床建议。
- 不生成真实控制策略。
- 不修改 `AGENTS.md`、`WORKSPACE_RULES.md`、`99_Meta/Global Tag List.md`，除非用户明确要求。
