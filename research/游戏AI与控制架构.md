---
title: "游戏 AI 与控制架构"
description: "2019 年 Osmo AI 项目 — reactive+deliberative 混合架构, 状态机, 自适应超参数, 引擎反向工程"
publish: true
lang: bilingual
---

# 游戏 AI 与控制架构 (Game AI & Control Architecture)

## 中文版

### 熟练度
熟练

### 描述

**多层决策架构（reactive + deliberative 混合）**
- 威胁检测层 → 立即反应式避险（reactive）
- 无威胁时 → 规划-验证-执行管线（deliberative）
- 对应经典 AI 行为架构：Brooks subsumption / Boyd OODA loop
- 应用：从高频避险到低频长程追击的平滑切换

**有状态 AI 控制器**
- 状态机 + 持久化计划 + 外部条件触发的 abort/reset
- 区别于 memoryless reactive 控制：agent 有记忆、能多帧执行一个计划、同时保留 abort 通道
- 应用：既不"每帧重新思考"浪费算力，也不"无脑走完已定死路线"变成 brittle

**自适应超参数（adaptive hyperparameters）**
- 密度自适应搜索半径：环境状态 → 动态 FOV（拥挤时聚焦、空旷时广视野）
- 失败触发的探索扩展（`searchtime` 机制）：反复无解时自动扩大搜索空间，避免近视导致的局部极小值
- 对标思想：RL 中的 adaptive exploration / temperature annealing

**候选过滤的双侧阈值（cost-benefit pruning）**
- 不只有上界（"能吃的猎物"），还有下界（"追这个猎物花费 > 收益就不追"）
- 从经济学视角剪枝决策空间——每个动作算 ROI，不值得的直接丢弃
- 可迁移到：交易策略、预算受限的 agent 规划、资源有限的任务调度

**引擎反向工程与白盒建模**
- 对外部系统（游戏引擎、外部 API、第三方库）做**完整反向工程**，得到一个可在 agent 内部复现的白盒模型
- 这是精确 rollout 仿真、模拟决策后果、预训练 agent 的基础
- 具体例：在 agent 内部重现 `kernel.py` 的 eject/absorb 物理公式，使前向仿真结果与真实引擎帧帧一致

**Forward simulation / rollout verification**
- 不依赖启发式得分，而是实打实跑 N 帧游戏引擎仿真，检查计划是否会中途失败
- 思想血缘：Monte-Carlo tree search、AlphaGo/MuZero 的 rollout、model-based RL
- 当前朴素版：200 帧顺序仿真；未来可扩展到 MCTS 并行 rollout

**OOP 游戏实体建模**
- 标准 game-object 数据模型：pos / veloc / radius / id / dead / collide_group
- 配套方法：move / distance_from / area / collide / stay_in_bounds / limit_speed
- 可迁移到：物理仿真、机器人仿真、多体物理系统

**对手建模与 meta-game**
- 读对手的策略代码 → 理解其决策模式 → 设计针对性反制
- 博弈论二阶思维：不只"我要怎么最优"，还考虑"对手知道我这么想之后会怎么调整"
- 可迁移到：对抗性 ML（adversarial robustness）、商业竞争分析、博弈论应用

**Benchmark 文化**
- 构建 baseline 梯度：brownian motion（最弱）→ 简单启发式 → 完整 AI（最强）
- "能打败哪些 baseline 才算合格"的工程纪律
- 迁移：所有需要评估 agent/model 性能的场景

### 与其他 skill 的关系

- 底层依赖 [[算法与数据结构]]（数据结构、搜索、几何计算）——这些是具体实现手段
- 本 skill 是**架构/架构思想**层——关心"怎么组合这些算法成一个能实时决策的 agent"
- 与 [[Claude-Skill开发方法论]] 有深刻的思想共鸣：
  - 两者都是 human-in-the-loop + 数据飞轮 + 多层规则 + 结构化记忆的某种变体
  - Osmo AI（2019）→ Claude Skill agent 设计（2026）的思想传承
  - 都强调"规划-验证-执行"管线而非单步 reactive

### 在哪些经历中用到
- [[Osmo-GameAI-GitHub]] — 完整实例，5 层架构（搜索机制 / 参数调优 / 战略编排 / 引擎反向工程 / 对手谱系）

---

## English Version

### Proficiency
Proficient

### Description

**Multi-layer decision architecture (reactive + deliberative hybrid)**
- Threat detection → immediate reactive avoidance
- No-threat → plan-validate-execute pipeline (deliberative)
- Maps to classical AI architectures: Brooks subsumption / Boyd OODA
- Smooth switching between high-frequency avoidance and low-frequency long-horizon pursuit

**Stateful AI controller**
- State machine + plan persistence + external-condition-triggered abort/reset
- Distinct from memoryless reactive control: the agent has memory, executes multi-frame plans, yet retains an abort channel
- Avoids both "rethink every frame" (compute-wasteful) and "mindlessly run the locked plan" (brittle)

**Adaptive hyperparameters**
- Density-adaptive search radius: environment state → dynamic FOV (focus in crowded areas, wide lens when sparse)
- Failure-triggered exploration expansion (`searchtime`): when repeatedly no feasible plan, auto-widen the search space to escape near-sighted local minima
- Kindred idea: adaptive exploration / temperature annealing in RL

**Two-sided candidate filtering (cost-benefit pruning)**
- Not just an upper bound ("targets I can eat") but also a lower bound ("chasing this costs more than the payoff")
- Economic pruning — each action is scored by ROI; unworthy ones dropped
- Transferable to: trading strategies, budget-limited agent planning, resource-constrained scheduling

**Engine reverse-engineering and white-box modeling**
- Fully reverse-engineer external systems (game engines, external APIs, third-party libs) into an internally-reproducible white-box model
- Foundation for precise rollout simulation, consequence modeling, agent pretraining
- Example: reproducing `kernel.py`'s eject/absorb physics inside the agent so forward simulation matches the real engine frame-by-frame

**Forward simulation / rollout verification**
- No reliance on heuristic scores — actually run N frames of engine simulation and check whether the plan fails mid-flight
- Lineage: Monte-Carlo tree search, AlphaGo/MuZero rollout, model-based RL
- Current naive form: 200-frame sequential simulation; extensible to MCTS parallel rollout

**OOP game-entity modeling**
- Standard game-object model: pos / veloc / radius / id / dead / collide_group
- Companion methods: move / distance_from / area / collide / stay_in_bounds / limit_speed
- Transferable to: physics simulation, robotics simulation, multi-body systems

**Opponent modeling & meta-game**
- Read the opponent's strategy code → understand decision pattern → design targeted counter-play
- Game-theoretic second-order thinking: not just "my optimal move" but "how the opponent adapts after anticipating my move"
- Transferable to: adversarial ML (robustness), competitive business analysis, game-theory applications

**Benchmark culture**
- Construct baseline gradients: brownian motion (weakest) → simple heuristics → full AI (strongest)
- The engineering discipline of "passes which baselines to count as decent"
- Transfers to every situation needing agent/model evaluation

### Relationship to Other Skills

- Depends on [[算法与数据结构]] (data structures, search, geometry) — those are the concrete implementation tools
- This skill operates at the **architecture / thinking** level — "how do we compose these algorithms into a real-time decision agent?"
- Strong resonance with [[Claude-Skill开发方法论]]:
  - Both are variants of human-in-the-loop + data flywheel + tiered rules + structured memory
  - A line of thought: Osmo AI (2019) → Claude Skill agent design (2026)
  - Both emphasize "plan-validate-execute" pipelines over single-step reactive logic

### Used In
- [[Osmo-GameAI-GitHub]] — full instance, 5-layer architecture (search mechanics / parameter tuning / strategy orchestration / engine RE / opponent spectrum)
