---
title: "Linear Superposition Framework (Zhenyu 原创)"
description: "Walker Circulation 对 oceanic forcing 宽度响应的 forcing-response operator 二阶 Taylor expansion + interaction-term-drop 框架"
publish: true
lang: bilingual
---

# Linear Superposition Framework (Zhenyu 原创, 2021)

> **页面用途**: Zhenyu 在 2021 年 PKU 大四本科研究 (胡永云 / 聂绩 指导) 期间原创提出的 conceptual framework, 用于解释 Walker Circulation 在不同 oceanic forcing 距离 $D$ 下的响应。

## 中文版

### 定义

**Linear Superposition framework** 是 Zhenyu 在 2021-07-13 于 PKU 大四 [[PKU-Walker-Circulation-Research]] 项目中原创提出的 conceptual framework, 用于解释 Walker Circulation 在不同 oceanic forcing 距离下的响应。

设 $F(W, C)$ 为大气对 Warm-pool forcing $W$ 与 Cold-pool forcing $C$ 联合响应的 operator。二阶 Taylor expansion:

$$F(W, C) = F(0,0) + \frac{\partial F}{\partial W}\bigg|_0 W + \frac{\partial F}{\partial C}\bigg|_0 C + \frac{1}{2}\frac{\partial^2 F}{\partial W^2}\bigg|_0 W^2 + \frac{1}{2}\frac{\partial^2 F}{\partial C^2}\bigg|_0 C^2 + \frac{\partial^2 F}{\partial W \partial C}\bigg|_0 WC + \cdots$$

**关键简化**: 当 $W$ 和 $C$ 在空间上相距较远 (forcing distance $D$ 大) 时, 非局域 forcing 对 cross derivative 的贡献衰减 → $\partial^2 F / \partial W \partial C \to 0$ → drop interaction term:

$$\boxed{F(W, C) \approx F(W, 0) + F(0, C) = \mathrm{Response}(W) + \mathrm{Response}(C)}$$

即: 双源联合响应 ≈ Warm-only 响应 + Cold-only 响应。

### 核心论点

**1. 4-field quantitative validation (D80-D180 bulk)**

对 CAM3 aqua-planet 10 cases × 30-yr runs, 4 个 diagnostic field 的 bulk correlation (Warm+Cold 实际响应 vs Wonly+Conly 线性叠加预测):

| Field | Bulk correlation | Spatial pattern |
| --- | --- | --- |
| SST (30-yr climate) | **0.9063** | Double-pole warming, WP 侧增强 |
| Precipitation | **0.9215** | Double-peak: WP + EP |
| ω @ 500mb | **0.8282** | Walker cell clearly visible |
| Shortwave radiation | **0.9324** | Subsidence region dark |

所有 4 个 field bulk correlation **> 0.82** → linear superposition framework **quantitatively validated** at $D \geq 80°$.

**2. Emergent non-monotonic Walker strength**

Walker strength 定义为 $|\Delta \omega @ 500\mathrm{mb}|_{\mathrm{WEP-EEP}}$ (见 [[PKU-Walker-Circulation-Research]] §3.1 metric), 观察: 随 $D$ 从 60° → 180° 单调 increase 的 forcing 间距, Walker strength **非单调** — peaks at **$D \approx 80$–$100°$** 然后 decrease。

Linear superposition 解释: $D \approx 80$–$100°$ 这个 peak 恰好对应 Wonly 的 natural descending area (200-220°E) 与 cold pool 几何重合的位置 → Wonly 下沉支 + Cold pool 冷却 双重 reinforcement。**不需要 nonlinear mechanism 解释这个 emergent non-monotonicity**。

**3. Framework 失效的边界 ($D < 80°$): Low-cloud positive feedback**

当 $D < 80°$ 时, Warm pool 与 Cold pool 几何上 "too close", cross-derivative $\partial^2 F / \partial W \partial C$ 不再 negligible → linear superposition 失效。

失效的 mechanism 被 Zhenyu 诊断为 **low-cloud positive feedback loop**:

```
CP descending ↑
  → suppress convection
  → trap humidity
  → low cloud ↑
  → albedo ↑
  → SW absorption ↓
  → SST ↓
  → ΔSST ↑
  → (loop back to intensify CP descending)
```

**4-term energy budget (SW + LH dominate)**:
- $\Delta SW$ at $D = 60°$ = **$-66.5141$ W/m²** → at $D = 180°$ = **$-110.6316$ W/m²** (magnitude monotonically increasing with $D$)
- $\Delta LH$, $\Delta LW$, $\Delta SH$ 相对小

这是 paper v6 abstract Key Point 3, verbatim:

> *"Low-cloud positive feedback dominates Walker suppression at small forcing widths (D<80°), diagnosed via 4-term energy budget with SW and LH as leading terms."*

### 不同观点 / 与其他 framework 的对比

**vs Nonlinear Walker mechanism literature**

- 传统 literature (e.g., Cessi & Young 1992, Dijkstra 2005) 常把 Walker strength 的 spatial dependence 归因于 nonlinear feedback (e.g., Bjerknes feedback, ocean-atmosphere coupling nonlinearity)
- Linear Superposition framework 说: **大部分 parameter regime ($D \geq 80°$) 的 emergent behavior 可以只用 linear superposition 解释**, 不需要 nonlinear; nonlinear mechanism 只在 $D \in [60°, 80°]$ boundary regime 才 kick in (low-cloud feedback)
- 这是一个 **conceptual simplification** 而非 extension — 减少 explanatory burden

**vs Perturbation theory in general**

- 任何 small-signal regime 都可以用 Taylor expansion + drop high-order term; 但通常 interaction term 是主导 (e.g., climate sensitivity feedback)
- Walker/width 问题的特殊性: forcing 是**空间分隔的** (W 在 WP, C 在 EP), cross-derivative 是 spatial-integrated $\partial^2 F / \partial W(x_W) \partial C(x_C)$, decay 随 $|x_W - x_C|$ (non-local operator 性质)

**vs atmospheric general circulation model sensitivity literature**

- Held & Soden 2006, Neelin 2011 等经典综述强调 feedback coupling 的 global integration
- Linear Superposition 是 **spatial-decomposition** perspective — forcing 可以按空间 split, response 也可以 split, under the "forcings far apart" assumption

### 开放问题 (待 Zhenyu 深入或未来 research extension 时补充)

- **Forcing shape generalization**: 目前只 test Gaussian-shape Warm pool + Gaussian-shape Cold pool; 非 Gaussian forcing (如 real-world 地形 + land-sea contrast) 下 linear superposition 是否仍然成立?
- **Coupled vs atmosphere-only**: 目前 aqua-planet CAM3 是 "slab ocean + fixed SST" framework; coupled ocean model 下 ocean dynamics 会 introduce additional nonlinearity — linear superposition 的适用边界缩小多少?
- **Application to ENSO**: Walker circulation 的 ENSO variability 是否也可以 decompose 为 "mean + linear superposition + residual nonlinear" 3-term?
- **Non-equilibrium state**: 所有 validation 是 30-yr climate average; transient response (如 abrupt CO2 increase) 下 linear superposition 还 hold 吗?

### 应用场景

**Zhenyu 已用的场景**:

- CAM3 aqua-planet 10 cases × 30-yr runs 验证 (Walker paper v6)

**可迁移的场景**:

- Hadley circulation 对 meridional forcing 的 response
- Madden-Julian Oscillation 的 superposition decomposition
- 北极 amplification 的 spatial source attribution (Arctic warming 的 tropics vs high-lat forcing decomposition)
- Tropical cyclone track forcing decomposition
- 更广: 任何 "multiple forcings spatially separated" 的 GCM diagnostic experiment

`[待补充]` 未来 Hadley / ENSO decomposition 具体 case studies 可在此扩充 (Berkeley Romps Lab 或 future research extension 中若应用此 framework, 应回填实际 case + 数值验证)

### 开发历史 (breakthrough timeline — 7-month intuition accumulation)

- **2020-12-29** slide 5 (W1.001 seed): "Walker 左右非对称 framing" — 早期 framework seed
- **2021-04-26** master PPT slides 32-65 (W1.034 拼贴萌芽): first systematic superposition attempt
- **2021-05-16** 胡组 15 slides slide 15: D180 self-consistent linear superposition explicit
- **2021-05-26 / 5-28 / 6-2** 进展报告: 84 figure groups systematic (5-28 拼贴系统化到 6 fields)
- **🌟 2021-07-13** 进展报告 29 slides slide 24 (breakthrough):

  
  After advisor discussion, the linear superposition framework proposed by Zhenyu provided a satisfactory explanation, and was endorsed.

- Prof. [[Ji-Nie-聂绩]] 当场 endorsement "之后就可以开始写论文"
- **2021-07-16** Hu group (胡组) 28 slides: post-breakthrough 给 Hu group 的 echo, slide 20 "线性叠加可以解释 Q1"

**7-month intuition accumulation**: 从 2020-12 framing 到 2021-07-13 breakthrough, breakthrough 是 weekly-writeup articulate 的 accumulate 出来, **不是 lucky inspiration**。

### 来源

- `research_wiki/projects/walker_hadley/overview.md` §Linear Superposition (math derivation + 4-field corr table + emergent prediction + low-cloud feedback failure boundary)
- `research_wiki/projects/walker_hadley/overview.md` §Authorship + §Paper v6 Key Points + §9-version auto-diff table
- `research_wiki/resume_angles/problem_solving.md` §Project 5
- `research_wiki/resume_angles/technical_depth.md` §Section 9 Walker 5-stage HPC pipeline
- `research_wiki/resume_angles/independent_judgment.md` — 此 framework 是 "本科生提框架 + advisor 当场 endorse" 的独立判断时刻
- Paper draft: internal-only manuscript draft (not submitted) (Oct 22, 2021, 3663 words, 11 refs, **未投稿**)
- Breakthrough artifact: 2021-07-13 breakthrough PPT (private artifact)
- `[待补充]` 进一步的 Walker 项目 `.docx` 学习笔记 + 数值实验 artifact (Wonly / Conly case individual run log + 4-term energy budget breakdown PPT)

### 相关页面

- [[PKU-Walker-Circulation-Research]] — 项目 experience page
- [[Ji-Nie-聂绩]] — 项目 PI
- 2021-07-13 breakthrough PPT (private artifact) — breakthrough artifact
- [[气候物理与大气科学]] — skill 页 (本 framework 是其 capability expansion)
- cross-project "breakthrough = 积累 articulate" pattern
- Independent Judgment narrative (held until 2026-06-10) — 本 framework proposal 是本科生原创提框架 + advisor 当场 endorsement 的 pivotal moment
- [[profile]]

---

## English Version

### Definition

**Linear Superposition framework** is a conceptual framework Zhenyu originated on 2021-07-13 during his PKU senior-year [[PKU-Walker-Circulation-Research]] project, used to explain Walker Circulation response under different oceanic forcing distances.

Let $F(W, C)$ be the operator describing the atmospheric joint response to Warm-pool forcing $W$ and Cold-pool forcing $C$. Second-order Taylor expansion:

$$F(W, C) = F(0,0) + \frac{\partial F}{\partial W}\bigg|_0 W + \frac{\partial F}{\partial C}\bigg|_0 C + \frac{1}{2}\frac{\partial^2 F}{\partial W^2}\bigg|_0 W^2 + \frac{1}{2}\frac{\partial^2 F}{\partial C^2}\bigg|_0 C^2 + \frac{\partial^2 F}{\partial W \partial C}\bigg|_0 WC + \cdots$$

**Key simplification**: when $W$ and $C$ are spatially well-separated (forcing distance $D$ large), the contribution of non-local forcing to the cross derivative decays → $\partial^2 F / \partial W \partial C \to 0$ → drop interaction term:

$$\boxed{F(W, C) \approx F(W, 0) + F(0, C) = \mathrm{Response}(W) + \mathrm{Response}(C)}$$

That is: dual-source joint response ≈ Warm-only response + Cold-only response.

### Core Arguments

**1. 4-field quantitative validation (D80-D180 bulk)**

For CAM3 aqua-planet 10 cases × 30-yr runs, bulk correlation between actual joint response (Warm+Cold) and linear superposition prediction (Wonly+Conly) across 4 diagnostic fields:

| Field | Bulk correlation | Spatial pattern |
| --- | --- | --- |
| SST (30-yr climate) | **0.9063** | Double-pole warming, enhanced on WP side |
| Precipitation | **0.9215** | Double-peak: WP + EP |
| ω @ 500mb | **0.8282** | Walker cell clearly visible |
| Shortwave radiation | **0.9324** | Subsidence region dark |

All 4 fields' bulk correlation **> 0.82** → linear superposition framework **quantitatively validated** at $D \geq 80°$.

**2. Emergent non-monotonic Walker strength**

Walker strength is defined as $|\Delta \omega @ 500\mathrm{mb}|_{\mathrm{WEP-EEP}}$ (see [[PKU-Walker-Circulation-Research]] §3.1 metric). Observation: as $D$ monotonically increases from 60° → 180°, Walker strength is **non-monotonic** — peaks at **$D \approx 80$–$100°$** and then decreases.

Linear superposition explanation: the $D \approx 80$–$100°$ peak corresponds to the geometric overlap between the Wonly natural descending area (200-220°E) and the cold pool location → Wonly descending branch + cold pool cooling reinforce each other. **No nonlinear mechanism is needed to explain this emergent non-monotonicity**.

**3. Framework breakdown boundary ($D < 80°$): Low-cloud positive feedback**

When $D < 80°$, Warm pool and Cold pool are geometrically "too close", the cross-derivative $\partial^2 F / \partial W \partial C$ is no longer negligible → linear superposition fails.

The breakdown mechanism is diagnosed by Zhenyu as a **low-cloud positive feedback loop**:

```
CP descending ↑
  → suppress convection
  → trap humidity
  → low cloud ↑
  → albedo ↑
  → SW absorption ↓
  → SST ↓
  → ΔSST ↑
  → (loop back to intensify CP descending)
```

**4-term energy budget (SW + LH dominate)**:
- $\Delta SW$ at $D = 60°$ = **$-66.5141$ W/m²** → at $D = 180°$ = **$-110.6316$ W/m²** (magnitude monotonically increasing with $D$)
- $\Delta LH$, $\Delta LW$, $\Delta SH$ relatively small

This is paper v6 abstract Key Point 3, verbatim:

> *"Low-cloud positive feedback dominates Walker suppression at small forcing widths (D<80°), diagnosed via 4-term energy budget with SW and LH as leading terms."*

### Different Perspectives / Comparison with other frameworks

**vs Nonlinear Walker mechanism literature**

- Traditional literature (e.g., Cessi & Young 1992, Dijkstra 2005) often attributes the spatial dependence of Walker strength to nonlinear feedback (e.g., Bjerknes feedback, ocean-atmosphere coupling nonlinearity)
- The Linear Superposition framework says: **most parameter regimes ($D \geq 80°$) of emergent behavior can be explained using only linear superposition**, no nonlinearity needed; nonlinear mechanism only kicks in within the $D \in [60°, 80°]$ boundary regime (low-cloud feedback)
- This is a **conceptual simplification** rather than extension — it reduces the explanatory burden

**vs Perturbation theory in general**

- Any small-signal regime can use Taylor expansion + drop high-order term; but typically the interaction term dominates (e.g., climate sensitivity feedback)
- Walker/width problem's particularity: forcing is **spatially separated** (W on WP, C on EP), the cross-derivative is the spatial-integrated $\partial^2 F / \partial W(x_W) \partial C(x_C)$, which decays with $|x_W - x_C|$ (non-local operator property)

**vs atmospheric general circulation model sensitivity literature**

- Classical reviews like Held & Soden 2006, Neelin 2011 emphasize the global integration of feedback coupling
- Linear Superposition is a **spatial-decomposition** perspective — forcing can be split spatially, response can be split, under the "forcings far apart" assumption

### Open Questions (to be added when Zhenyu deepens or in future research extensions)

- **Forcing shape generalization**: only Gaussian-shape Warm pool + Gaussian-shape Cold pool tested currently; does linear superposition still hold for non-Gaussian forcing (e.g., real-world topography + land-sea contrast)?
- **Coupled vs atmosphere-only**: aqua-planet CAM3 currently uses a "slab ocean + fixed SST" framework; under coupled ocean models, ocean dynamics will introduce additional nonlinearity — by how much does the applicability boundary of linear superposition shrink?
- **Application to ENSO**: can ENSO variability of Walker circulation also be decomposed into the 3-term "mean + linear superposition + residual nonlinear"?
- **Non-equilibrium state**: all validation is on 30-yr climate average; does linear superposition still hold under transient response (e.g., abrupt CO2 increase)?

### Application Scenarios

**Scenarios Zhenyu has applied**:

- CAM3 aqua-planet 10 cases × 30-yr runs validation (Walker paper v6)

**Transferable scenarios**:

- Hadley circulation response to meridional forcing
- Madden-Julian Oscillation superposition decomposition
- Spatial source attribution of Arctic amplification (decomposing tropics vs high-lat forcing for Arctic warming)
- Tropical cyclone track forcing decomposition
- More broadly: any GCM diagnostic experiment with "multiple forcings spatially separated"

`[to be added]` Specific case studies of future Hadley / ENSO decomposition can be expanded here (if this framework is applied at Berkeley Romps Lab or future research extension, the actual case + numerical validation should be backfilled)

### Development History (breakthrough timeline — 7-month intuition accumulation)

- **2020-12-29** slide 5 (W1.001 seed): "Walker left-right asymmetry framing" — early framework seed
- **2021-04-26** master PPT slides 32-65 (W1.034 collage embryo): first systematic superposition attempt
- **2021-05-16** Hu group 15 slides slide 15: D180 self-consistent linear superposition explicit
- **2021-05-26 / 5-28 / 6-2** progress reports: 84 figure groups systematic (5-28 collage systematized to 6 fields)
- **🌟 2021-07-13** progress report 29 slides slide 24 (breakthrough):

  
  After advisor discussion, the linear superposition framework proposed by Zhenyu provided a satisfactory explanation, and was endorsed.
  >
  > (English gloss: After discussion, there were indeed those weak points on the left side [referring to the previous MSE budget explanation]... Later I proposed the **linear explanation theory** myself, which could explain things well, and the advisor agreed.)

- Prof. [[Ji-Nie-聂绩]] on-the-spot endorsement: "you can start writing the paper now"
- **2021-07-16** Hu group (胡组) 28 slides: post-breakthrough echo to Hu group, slide 20 "linear superposition can explain Q1"

**7-month intuition accumulation**: from 2020-12 framing to 2021-07-13 breakthrough, the breakthrough was accumulated through weekly-writeup articulation, **not lucky inspiration**.

### Sources

- `research_wiki/projects/walker_hadley/overview.md` §Linear Superposition (math derivation + 4-field corr table + emergent prediction + low-cloud feedback failure boundary)
- `research_wiki/projects/walker_hadley/overview.md` §Authorship + §Paper v6 Key Points + §9-version auto-diff table
- `research_wiki/resume_angles/problem_solving.md` §Project 5
- `research_wiki/resume_angles/technical_depth.md` §Section 9 Walker 5-stage HPC pipeline
- `research_wiki/resume_angles/independent_judgment.md` — this framework is a moment of independent judgment with "undergrad proposes framework + advisor on-the-spot endorsement"
- Paper draft: internal-only manuscript draft (not submitted) (Oct 22, 2021, 3663 words, 11 refs, **not submitted**)
- Breakthrough artifact: 2021-07-13 breakthrough PPT (private artifact)
- `[to be added]` Further Walker project `.docx` study notes + numerical experiment artifacts (Wonly / Conly individual case run logs + 4-term energy budget breakdown PPT)

### Related Pages

- [[PKU-Walker-Circulation-Research]] — project experience page
- [[Ji-Nie-聂绩]] — project PI
- 2021-07-13 breakthrough PPT (private artifact) — breakthrough artifact
- [[气候物理与大气科学]] — skill page (this framework is a capability expansion thereof)
- cross-project "breakthrough = accumulation articulated" pattern
- Independent Judgment narrative (held until 2026-06-10) — proposal of this framework is a pivotal moment of undergrad-originated framework + advisor on-the-spot endorsement
- [[profile]]
