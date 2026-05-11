---
title: "macOS 桌面应用自动化"
description: "macOS 上通过 AppleScript + computer-use MCP 自动化原生应用 (private personal automation: social-feed interaction)"
publish: true
lang: bilingual
---

# macOS 桌面应用自动化 (macOS Native App Automation)

## 中文版

### 熟练度
熟练

### 描述
- **两层架构**：AppleScript（把 app 唤前、切窗口）+ computer-use MCP（视觉截图 + 点击 + 键盘输入）配合使用，绕开无官方 API 的桌面应用
- **视觉驱动的 UI 操作**：基于截图定位 UI 元素（如 WeChat 的 Discover 图标、每条朋友圈的 `..` 按钮）、使用显式等待、批量动作合并（`computer_batch`）优化速度
- **Claude Code Skill 封装**：把多步骤 agent 工作流打包成标准 skill（SKILL.md + 辅助数据文件），可复用、可迭代
- **Agent 行为工程**：human-in-the-loop review、数据飞轮（自增长 few-shot 语料库）、多级行为规则（blocklist / frequency cap / per-target persona）、结构化长期记忆
- 与 [[Python-网页自动化]] 的 Selenium 脚本形成互补：前者攻浏览器 DOM，后者攻原生 macOS 应用

### 在哪些经历中用到
- 个人项目 / 日常效率工具：private personal automation project — social-feed interaction + archival workflow
- [[AI工具与效率提升]] — 把桌面重复任务交给 AI agent 的路径

---

## English Version

### Proficiency
Proficient

### Description
- **Two-layer architecture**: AppleScript (bring app to front, switch windows) + computer-use MCP (screenshot + click + keyboard) combined — works around desktop apps with no official API
- **Vision-driven UI operations**: locate UI elements from screenshots (e.g. WeChat's Discover icon, the `..` button on each post), explicit waits, `computer_batch` to combine multiple actions for speed
- **Claude Code Skill packaging**: wraps multi-step agent workflows into standard skill format (SKILL.md + supporting data files) for reuse and iteration
- **Agent behavior engineering**: human-in-the-loop review, data flywheel (self-growing few-shot corpus), multi-tier behavior rules (blocklist / frequency cap / per-target persona), structured long-term memory
- Complements [[Python-网页自动化]] Selenium scripting — one tackles browser DOM, the other tackles native macOS apps

### Used In
- Personal project / daily productivity tool: private personal automation project — social-feed interaction + archival workflow
- [[AI工具与效率提升]] — the path of delegating repetitive desktop tasks to AI agents
