---
title: "Claude Code Skill 开发方法论"
description: "Zhenyu 自己摸索并实践的 Claude Code Skill 开发范式——SKILL.md 工作流 + 辅助数据文件分层 + human-in-loop + 数据飞轮 + 结构化长期记忆"
publish: true
lang: bilingual
---

# Claude Code Skill 开发方法论 (Claude Code Skill Authoring Methodology)

> **页面用途**：Zhenyu 在 2025-2026 年摸索并实践的一套 Claude Code Skill 开发范式。

## 中文版

### 定义

**Claude Code Skill** 是 Anthropic 在 2025 年底推出的新范式：把复杂的多步骤 agent 工作流封装成一个标准化的、可被 Claude Code CLI 自动发现和加载的 "skill"。最小单位是一个目录，里面包含：
- 一个 `SKILL.md` 主文件（带 frontmatter `name` / `description` / `allowed-tools`，主体是 markdown 格式的工作流指令）
- 任意数量的辅助数据/规则文件（可以是 persona、examples、blocklist 等）
- 可选的脚本或工具（shell scripts、AppleScripts 等）

Zhenyu 在此基础上发展出了一套**个人偏好的 Skill 架构范式**，这套范式的核心不是"调 API"，而是"**把一个反复要做的任务工程化为 Claude 可以安全、迭代、自演进地完成的 agent**"。

### 核心论点（Zhenyu 的 Skill 架构范式）

**1. 工作流分阶段明确化**
- 在 SKILL.md 中把 agent 的工作分成清晰 Phase（例如"打开目标 → 循环处理每个对象 → 出具总结"）
- 每个 Phase 内部列出具体步骤（截图 → 识别 → 决策 → 执行）
- 预先把已知 UI/交互位置写死（如"Discover 图标大致在 x=22, y=220"），让 agent 无需"探索"即可直达

**2. 数据与逻辑分层**
- `SKILL.md` = 工作流（How）
- (persona file) / `profile` 类文件 = 用户/场景上下文（Who）
- (examples corpus) = 风格语料 / few-shot 样本（What tone）
- (blocklist file) / (safe-action file) / 行为规则文件 = 硬规则（Must / Must-not）
- (memory file) / 结构化 journal = 长期记忆（State）
- 好处：每个维度可独立演进，LLM 上下文加载时也可以按需读取而不是一次性全载

**3. Human-in-the-loop + 数据飞轮**
- Agent 执行高风险动作前（发送留言、下单、发邮件、真正修改外部状态）一律 pause，把草稿交给用户确认
- 用户"ok"或修改后的最终结果**自动写回 examples / 记忆文件**——这条样本立刻成为下次生成的参考
- 飞轮效应：skill 用得越多，生成的内容越贴近用户个人风格；**不需要训练，靠 in-context learning 堆语料实现个性化**

**4. 行为规则的层级化**
- 硬规则（blocklist）: 彻底跳过
- 半硬规则（like-only）: 局部退化为安全动作
- 频率/间隔规则（如"张宸话痨规则"）: 时间维度的去重
- Persona-level soft rules（如"对 X 禁用'羡慕'"）: 细粒度语言偏好
- 各层 rules 的**自动更新触发条件**必须精心设计：只有用户显式指示 或 Claude 推荐并被确认 才能入库，避免"用户改了一次稿"被误学为长期偏好

**5. 结构化长期记忆 vs 运行时上下文**
- (memory file) 这类文件不是 log 而是**按实体组织的 journal**：一人一节，标题 + 背景 + 当前位置 + 近况记录（按日期 append 到各自节里）
- 好处：下次读同一朋友的帖子可以立刻拉到他/她的全部既有信息做上下文
- 对比：纯时间线 log 读起来是 O(n) 检索，按实体分节读起来是 O(1)

**6. Skill = 把 LLM 能力"产品化"的最小单位**
- 与"写一个 Python 脚本"的本质区别：Skill 承认 agent 不是 deterministic 的，把不确定性交给 LLM 判断 + 人类兜底，而不是试图写死所有分支
- 与"直接 ChatGPT 对话"的区别：Skill 沉淀可复用的上下文和规则，每次不用重新解释

### 不同观点 / 常见错误范式

**错误范式 A：把 Skill 写成"prompt 模板"**
- 只有一个 SKILL.md，所有规则/样本/人设塞在一起——后期维护困难，LLM 上下文也会爆
- Zhenyu 的范式：分成多个 markdown 文件，按维度拆分

**错误范式 B：完全自动化，不留 human-in-loop**
- 看起来效率高，但外部动作一旦错误无法回滚（已发消息、已下单）
- Zhenyu 的范式：高风险动作一律 pause 确认，低风险动作（点赞、截图）可以一路自动

**错误范式 C：记忆文件只写不读**
- 有些实现只让 skill 记录日志，但下次不读——相当于没有记忆
- Zhenyu 的范式：SKILL.md 开头明确"Before Starting"要 read 哪些文件

### 已经实践的 Skill 项目

| Skill | 用途 | 核心数据文件 |
|-------|------|-------------|
| private personal automation project (WeChat Moments interaction) | 微信朋友圈自动点赞 + 留言 | (persona file) / (examples corpus) / (blocklist file) / (safe-action file) / (memory file) |
| *(未来添加)* | | |

### 开放问题

- **Skill 之间的共享基础设施**：如果将来有多个 skill，(persona file)（用户身份）应该共享还是各自复制？
- **Skill 的版本化与回滚**：当 skill 自动更新了 blocklist / examples，如果发现某次更新有误，如何回滚？当前靠 git，是否需要更细粒度的 audit log？
- **跨 skill 的记忆迁移**：在 A skill（朋友圈）里记录的朋友近况，B skill（日程安排）如果要用，是不是应该有统一的"personal knowledge graph"层而不是各自复制？
- **Claude Skill vs Anthropic 的 Agent SDK**：什么时候用 Skill、什么时候用代码级 Agent SDK？目前 Zhenyu 偏好 Skill（低代码、可由用户本人维护），但某些需要复杂状态管理的场景可能更适合 SDK

### 来源

- private personal automation project (WeChat Moments interaction) — 第一个完整实例

### 相关页面

- [[macOS-桌面应用自动化]] — 当前 Skill 的底层自动化技术
- [[AI工具与效率提升]] — 更宏观的 AI 工具使用技能
- [[profile]]

---

## English Version

### Definition

**Claude Code Skill** is the new paradigm Anthropic released in late 2025: package complex multi-step agent workflows as a standardized, auto-discoverable "skill" loadable by Claude Code CLI. Minimum unit is a directory containing:
- One `SKILL.md` (frontmatter `name` / `description` / `allowed-tools`; body is the markdown workflow)
- Any number of auxiliary data/rule files (persona, examples, blocklists, etc.)
- Optional scripts or tools (shell, AppleScript, etc.)

On top of that baseline, Zhenyu has developed his own **preferred Skill architecture paradigm** — the core of which is not "call the API" but "**engineer a recurring task into an agent that Claude can safely, iteratively, and self-improvingly execute**."

### Core Arguments (Zhenyu's Skill Architecture Paradigm)

**1. Phased, explicit workflow**
- Split the agent's work into clear Phases in SKILL.md (e.g., "open target → loop over objects → produce summary")
- Each phase lists concrete steps (screenshot → identify → decide → execute)
- Hard-code known UI/interaction positions so the agent doesn't need to "explore"

**2. Separating data from logic**
- `SKILL.md` = workflow (How)
- (persona file) / profile files = user/scenario context (Who)
- (examples corpus) = style corpus / few-shot (What tone)
- (blocklist file) / (safe-action file) / rule files = hard rules (Must / Must-not)
- (memory file) / structured journal = long-term memory (State)
- Benefit: each dimension can evolve independently; context can be loaded selectively rather than all-at-once

**3. Human-in-the-loop + data flywheel**
- Before any high-risk action (send message, place order, truly modify external state), pause and present draft to user
- User's "ok" or edited final version is **auto-written back to examples / memory files** — this sample immediately informs the next generation
- Flywheel effect: the more the skill is used, the closer the output gets to the user's personal style; **no training needed, personalization via accumulated in-context examples**

**4. Tiered behavior rules**
- Hard rules (blocklist): skip entirely
- Semi-hard rules (like-only): degrade to a safe action
- Frequency/interval rules (e.g., "Zhang Chen motormouth rule"): time-dimension dedup
- Persona-level soft rules (e.g., "forbid 'envy' toward X"): fine-grained linguistic preference
- Auto-update triggers for each layer must be designed carefully: only "user explicitly instructs" OR "Claude recommends + user confirms" should write to the rule files, to avoid a one-off edit being learned as a long-term preference

**5. Structured long-term memory vs runtime context**
- Files like (memory file) are not logs but **entity-organized journals**: one section per person with header + background + current location + dated updates appended inside their section
- Benefit: next time a post from the same friend appears, all their existing context is one fetch away
- Contrast: a pure timeline log is O(n) to search; entity-sectioned journals are O(1)

**6. Skill = the minimum unit for "productizing" LLM capability**
- Differs from "write a Python script": skills embrace the fact that agents aren't deterministic, delegating uncertainty to the LLM's judgment + human backstop rather than hard-coding every branch
- Differs from "just chat with ChatGPT": skills persist reusable context and rules, so you don't re-explain every session

### Anti-patterns

**Anti-pattern A: Skill as "prompt template"** — Single SKILL.md stuffed with all rules/samples/persona. Maintenance nightmare, context explosion. Zhenyu's paradigm: split into multiple markdown files by dimension.

**Anti-pattern B: Full automation, no human-in-loop** — Looks efficient, but external actions once wrong can't be rolled back (message already sent, order placed). Zhenyu's paradigm: pause before high-risk actions; low-risk actions (like, screenshot) can run freely.

**Anti-pattern C: Memory files are write-only** — Some implementations log but never read back — effectively no memory. Zhenyu's paradigm: SKILL.md explicitly lists "Before Starting" files to read.

### Practiced Skill Projects

| Skill | Purpose | Core data files |
|-------|---------|-----------------|
| private personal automation project (WeChat Moments interaction) | WeChat Moments auto-like + comment | (persona file) / (examples corpus) / (blocklist file) / (safe-action file) / (memory file) |
| *(future)* | | |

### Open Questions

- **Shared infrastructure across skills**: if multiple skills exist, should (persona file) (user identity) be shared or duplicated? Plan to build a universal `~/.claude/personal-context/` referenced by all skills?
- **Skill versioning and rollback**: when a skill auto-updates blocklist/examples, how to roll back a bad update? Currently git-based — need finer-grained audit logs?
- **Cross-skill memory migration**: friend updates recorded in skill A (Moments) — should skill B (calendar) read them? Feels like a unified "personal knowledge graph" layer, not duplication
- **Claude Skill vs Anthropic Agent SDK**: when to use Skill vs code-level Agent SDK? Zhenyu currently prefers Skill (low-code, user-maintainable), but complex state management may favor SDK

### Sources

- private personal automation project (WeChat Moments interaction) — first full instance

### Related Pages

- [[macOS-桌面应用自动化]] — underlying automation tech for the current skill
- [[AI工具与效率提升]] — broader AI productivity skill
- [[profile]]
