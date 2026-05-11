---
title: "游戏开发 pygame"
description: "本科时期 pygame 全栈 2D 游戏开发 — sprite/scene/asset/audio/input + DSL 设计 + 游戏化教育"
publish: true
lang: bilingual
---

# 游戏开发 pygame (Game Development with pygame)

## 中文版

### 熟练度
熟练



### 描述

**pygame 框架全栈**
- `pygame.sprite.Sprite` 基类 + 继承树（9 种 Enemy 子类；4 种 Bar 子类）
- `pygame.sprite.Group` 按类型分组管理（`enemies` 总集 + `ord_enemies` / `heal_enemies` / `split_enemies` 按敌人类型分组，支持批量碰撞检测/批量更新）
- `pygame.Surface` / `pygame.image.load` / `convert_alpha` 资产加载 + 双缓冲绘制
- `pygame.mixer` 音频引擎：`music.load + play(-1)` 循环背景乐 + `mixer.Sound` 触发式音效
- `pygame.font` 自定义字体加载（Futura.ttc）+ 文本渲染
- `pygame.time.Clock` FPS 控制（60 FPS，60 秒/局）
- `pygame.event` 事件循环：KEYDOWN/KEYUP + QUIT + 多事件分支

**场景与状态机管理**
- 多 mode 状态机（主菜单 / 战斗 / 故事剧情 / 暂停 / 结束 / 教程 —— 6 种场景）
- 资产 pre-load 到 Surface 缓存，避免运行时磁盘 I/O
- 暂停/结束 overlay + 双层菜单（`pause_option` / `end_option` 各自管理）

**自定义 DSL（Domain-Specific Language）设计**
- Token stream 数据结构（双端 deque）支持 `L_` prepend / `R_` append 的双向构造
- 键盘输入 → token 映射（`KEYDICT` 查表）
- 实时求值（`calc(x)` 按 token 顺序应用到输入）
- 符号化简规则引擎（互逆操作对自动抵消：`a·s`、`l·e`、`d·d`、`-·-`、`/·*`）—— 简化版计算机代数系统的 normalize
- 表达式 pretty-print（token stream → 人类可读字符串如 `sin(e(x/2))`）
- 自定义异常作为游戏机制（`out_of_domain` 在 log(负)/arcsin(|x|>1)/1/0 时抛出，触发"函数无效"反馈）

**游戏平衡性与 incentive design**
- 非线性费用函数：`cost = f(linear, A, d, e, l)`，用**指数复合** `pow(2+linear, 1.5+A)` 惩罚 nested 操作 —— 让"简洁表达式"成为 dominant 策略
- 把数学严格性（exception）转化为 gameplay feedback —— 玩错的方式即学到的地方

**坐标系抽象**
- 四个双向映射函数（`lof` / `tof` / `xof` / `yof`）解耦物理坐标和屏幕坐标
- `pygame.sprite.Sprite.rect.center` 和自定义 (x, y) 双坐标系同步

**游戏化教育设计（educational game design）**
- 11 关教程模式按数学难度递进：单 ln → 单 exp → 单 sin → 2sin → sin×2 → sin÷2 → …
- 每关固定目标点（e.g. `[(0,-4), (1,0), (3,1), (7,2)]` 对应 ln），玩家要构造出经过这些点的函数——**问题到答案的 inverse 练习**
- Knowledge sequencing：先单操作、再组合、最后复合，覆盖课程设计的基本原理
- 这个能力与 profile 里讨论过的 **Exam-centric AI Coaching**（主动式 AI 备考教练）方向直接相关

**引擎反向工程（跨项目）**
- 在 [[Osmo-GameAI-GitHub]] 里为了写 rollout simulator，完整反向工程了陈斌教授的对战平台 `kernel.py`（eject 物理/absorb 多体碰撞/collision grouping）——对外部游戏引擎做白盒建模的能力

### 与其他 skill 的关系

- 与 [[游戏AI与控制架构]] **互补**：一个开发游戏本身、一个开发能玩游戏的 AI
- 与 [[算法与数据结构]] **承载**：pygame 实现里的 OOP 继承树、deque 式 stream、规则引擎化简都是本 skill 的载体
- 与 [[前端与网页开发]] **思想共鸣**：都是"交互式应用开发"（一个是 pygame Surface，另一个是 DOM）；产品审美 + 工程细节的同一份偏好
- 与 [[Claude-Skill开发方法论]] **思想共鸣**：DSL 设计（键盘 → 数学函数）与 SKILL.md + persona + examples 的"Skill 即用户自定义行为"有同构的 DSL 设计思维

### 在哪些经历中用到
- [[FunctionsGame-GitHub]] — Math Kills Monsters Alpha 4.0（~1300 行 pygame + 9 敌人 + 11 关教程 + 完整 UI + 音画资产）
- [[Osmo-GameAI-GitHub]] — 对战平台 kernel.py / world.py / cell.py 的引擎内部理解（白盒建模）
- 可能的未来应用：interactive components for educational/visualization products

---

## English Version

### Proficiency
Proficient



### Description

**pygame framework (full stack)**
- `pygame.sprite.Sprite` base class + inheritance tree (9 Enemy subclasses; 4 Bar subclasses)
- `pygame.sprite.Group` organized by type (`enemies` full set + `ord_enemies` / `heal_enemies` / `split_enemies` subset for per-type batch collision/update)
- `pygame.Surface` / `pygame.image.load` / `convert_alpha` + double-buffered drawing
- `pygame.mixer`: `music.load + play(-1)` for looping BGM + `mixer.Sound` for triggered SFX
- `pygame.font` with custom font (Futura.ttc) + text rendering
- `pygame.time.Clock` FPS control (60 FPS, 60s per match)
- `pygame.event` event loop: KEYDOWN/KEYUP + QUIT + multi-branch

**Scene + state management**
- Multi-mode state machine (main menu / battle / story / pause / end / tutorial — 6 scenes)
- Assets pre-loaded into Surface caches to avoid runtime disk I/O
- Pause/end overlays + per-menu option state

**Custom DSL (Domain-Specific Language) design**
- Token-stream data structure (double-ended deque) supporting both `L_` prepend and `R_` append
- Key-to-token mapping (`KEYDICT` lookup)
- Real-time evaluation (`calc(x)` applies tokens in order)
- Symbolic simplification rule engine (inverse pair cancellation: `a·s`, `l·e`, `d·d`, `-·-`, `/·*`) — lite computer-algebra normalize
- Expression pretty-print (token stream → readable string like `sin(e(x/2))`)
- Custom exceptions as gameplay mechanic (`out_of_domain` on log(neg)/arcsin(|x|>1)/1/0 triggers "function invalid" feedback)

**Game balance & incentive design**
- Non-linear cost function: `cost = f(linear, A, d, e, l)` with **exponential composition** `pow(2+linear, 1.5+A)` penalizing nested operations — making elegant expressions the dominant strategy
- Converting mathematical rigor (exceptions) into gameplay feedback — getting it wrong is how you learn

**Coordinate abstraction**
- Four bidirectional mapping functions (`lof` / `tof` / `xof` / `yof`) decouple physics and screen coords
- `pygame.sprite.Sprite.rect.center` and custom (x, y) coord systems kept in sync

**Gamified educational design**
- 11-level tutorial with increasing math difficulty: single ln → single exp → single sin → 2sin → sin×2 → sin÷2 → ...
- Each level has fixed target points (e.g. `[(0,-4), (1,0), (3,1), (7,2)]` for ln) — player must construct a function through them — an **inverse problem-to-answer practice**
- Knowledge sequencing: single ops first, then composition, then deep nesting — core curriculum-design principle
- Directly relevant to the **Exam-centric AI Coaching** idea in [[profile]]

**Engine reverse-engineering (cross-project)**
- In [[Osmo-GameAI-GitHub]], to build the rollout simulator, Zhenyu fully reverse-engineered Prof. Chen's `kernel.py` (eject physics / multi-body absorb / collision grouping) — white-box modeling of external game engines

### Relationships to Other Skills

- **Complementary** to [[游戏AI与控制架构]]: one develops the game, the other develops AI that plays games
- **Carried by** [[算法与数据结构]]: OOP inheritance, deque streams, rule-engine simplification — all vehicles of this skill
- **Resonates with** [[前端与网页开发]]: both are "interactive application development" (pygame Surface vs DOM); same product-aesthetics + engineering-detail preference
- **Resonates with** [[Claude-Skill开发方法论]]: DSL design (keyboard → math function) is isomorphic to SKILL.md + persona + examples design thinking (Skills as user-defined behavior)

### Used In
- [[FunctionsGame-GitHub]] — Math Kills Monsters Alpha 4.0 (~1300 lines pygame + 9 enemies + 11 tutorial levels + full UI + audio/visual assets)
- [[Osmo-GameAI-GitHub]] — white-box understanding of the kernel.py / world.py / cell.py game engine internals
- Potential future use: interactive components for educational/visualization products
