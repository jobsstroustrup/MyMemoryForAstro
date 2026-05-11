---
title: "Department Head @ ONE-AGI"
publish: true
role_framing: team-project
project_status: active
year: 2025
description: "Department Head of the AGI division at UC Berkeley BETA (Berkeley Emerging Technology Association)"
---

# Department Head @ ONE-AGI

## 中文版

### 基本信息
- **时间**: 2025 — 至今
- **角色**: Department Head（AGI 分部负责人）
- **组织**: ONE-AGI; UC Berkeley BETA (Berkeley Emerging Technology Association) 下属的 AGI 分部
- **地点**: UC Berkeley

### 角色概述
ONE-AGI 是 Zhenyu 在 UC Berkeley 期间发起并主持的"个人 AI 效率部门"实践，定位是一种"一人份的 department"：把每一项反复出现的任务工程化为可被 AGI 安全完成的工作流，把"用 LLM 提升个人产出"从口号落到日常 artifact。同时它是 UC Berkeley BETA 下的 AGI 分部，每周组织 AGI 安全、政策、人机共存方向的跨学科 seminar。

### 主要工作产出（具体 artifact）

1. **Claude Code Skill 开发范式**: 在 2025 年底 Anthropic 推出 Claude Code Skill 后，独立摸索出一套"工作流分阶段 + 数据/逻辑分层 + human-in-the-loop + 数据飞轮 + 结构化长期记忆"的 Skill 架构方法论；写成方法论 wiki 页，作为后续每个新 Skill 项目的复用范式。
2. **private personal automation**: 该方法论的第一个完整实例，把"日常浏览微信朋友圈、点赞、留言"封装成一个 Claude Skill。技术栈结合 AppleScript（唤起桌面 app）+ computer-use MCP（截图/点击）+ Claude 视觉与中文生成，再叠加 persona / examples / blocklist / friends 五个分层数据文件。每次留言提交前由 user 确认，确认后样本自动回写到 examples，形成个性化飞轮。
3. **MyMemory wiki**: 受 Karpathy 风格 LLM Wiki 启发，2026 年 4 月启动的个人结构化知识库；维护者是 LLM，人类 review/approve；目录分为 sources / entities / concepts / experience / skills / meta / raw 等模块；通过 frontmatter `publish` 字段控制公开范围。
4. **三层 fail-closed 公开管线**: 当前这个个人网站的整套 MyMemory → MyMemoryForAstro → Astro 物理 + 逻辑隔离架构本身就是 ONE-AGI 的工程实践案例，由 19 个 Opus subagent research brief 收敛而成。
5. **AGI 议题 seminar**: 每周组织 BETA 同学讨论 AGI 安全、AI 政策、法律框架、人机共存；同时面向更广受众做 AI 工具上手与 prompt 设计的工作坊。

### 与个人研究/创业身份的连接
ONE-AGI 与 Zhenyu 在 Romps Lab 的气候动力研究、与早期具身 AI 数据公司 (passive shareholder) 的实践之间不是平行三条线，而是同一个"研究者 + 工程师 + 系统设计者"身份在不同 surface 的展开：研究关注用 LES + 反问题工具理解物理系统，创业把方法落到数据飞轮，ONE-AGI 把同样的工程纪律折叠回个人生产力本身。

### 时间线
2025 年发起；持续到当前（2026-05），seminar 与个人 Skill 库均在持续维护。

### 使用的技能
- [[AI工具与效率提升]]
- [[Claude-Skill开发方法论]]
- [[macOS-桌面应用自动化]]

---

## English Version

### Basic Info
- **Period**: 2025 — Present
- **Role**: Department Head (AGI Division Lead)
- **Organization**: ONE-AGI; the AGI Division of UC Berkeley BETA (Berkeley Emerging Technology Association)
- **Location**: UC Berkeley

### Role Summary
ONE-AGI is Zhenyu's "department-of-one for AI-powered personal effectiveness," initiated at UC Berkeley in 2025. The framing is literal: treat the practice of using AGI for individual productivity as a department with its own discipline, artifacts, and review cadence; engineer every recurring task into a workflow an agent can complete safely; turn "10x productivity through LLMs" from a slogan into shipped artifacts. The same role doubles as convener of UC Berkeley BETA's AGI Division, running weekly cross-disciplinary seminars on AGI safety, AI policy, and human-AGI coexistence.

### Concrete Artifacts

1. **A Claude Code Skill authoring methodology**. After Anthropic released Claude Code Skill in late 2025, Zhenyu independently developed a paradigm built on five tenets: phased explicit workflows, data-and-logic separation, human-in-the-loop on high-risk actions, an examples-write-back data flywheel, and entity-organized long-term memory. Captured as a reusable methodology page that grows with each new skill.
2. **private personal automation**. The first full instance of that methodology: a Claude Skill that automates browsing, liking, and commenting on WeChat Moments. Combines AppleScript (bring the desktop app forward), the computer-use MCP (screenshot and click), and Claude's vision plus Chinese generation, layered over five data files (persona, examples, blocklist, like-only, friends). Every comment is presented as a draft for user confirmation; the confirmed final form is appended to the examples corpus, producing a personalization flywheel without any model fine-tuning.
3. **MyMemory wiki**. A Karpathy-style LLM Wiki launched in April 2026 as the canonical store for the writer's personal record: sources, entities, concepts, experience, skills, meta. The LLM is the maintainer; the human reviews and approves; per-page `publish` flags govern what ever leaves the local store.
4. **A three-layer fail-closed publishing pipeline**. The very website you are reading is itself an ONE-AGI artifact: a MyMemory canonical layer, an auto-generated MyMemoryForAstro middle layer with hard exclusions and section-level redaction, and an Astro-rendered public layer with schema-level fallback. Architecture distilled from nineteen Opus subagent research briefs and a Wave-based decision protocol.
5. **AGI-issue seminars**. Weekly Berkeley discussions on AGI safety, policy, legal frameworks, and human-AGI coexistence; occasional public workshops on practical AI tooling and prompt design for newcomers.

### Connection to the Broader Research and Builder Identity
ONE-AGI is not a separate track from the climate-physics research at Romps Lab or the embodied-data company (now passive shareholder). They are the same identity expressed on three surfaces: research treats large physical systems with LES and inverse methods, the startup folds those methods into a data flywheel, and ONE-AGI folds the same engineering discipline back onto the practitioner's own productivity surface.

### Timeline
Began 2025; ongoing as of 2026-05; both the BETA seminar cadence and the personal skill library remain active.

### Skills Used
- [[AI工具与效率提升]]
- [[Claude-Skill开发方法论]]
- [[macOS-桌面应用自动化]]
