---
title: "Hardened Balancing Principle (HBP)"
description: "Caltech DSCOVR retrieval (2021-2022): Zhenyu's generalization of Bauer 2007 Balancing Principle for automatic Tikhonov regularization-parameter selection"
publish: true
lang: bilingual
---

# Hardened Balancing Principle (HBP)

> **页面用途**: Caltech DSCOVR retrieval 项目 (2021.03–2022.03, with Yuk Yung and UCR co-advisor) Zhenyu 自己在 Bauer 2007 framework 基础上 generalize + 系统 benchmark 的 automatic regularization-parameter selector. 

## 中文版

### 定义

**Hardened Balancing Principle (HBP)** 是 Bauer 2007 在 Bauer & Hohage 2005 的 Balancing Principle (BP) 基础上提出的 **自动 Tikhonov 正则化参数 $\lambda$ 选择方法**, Zhenyu 在 Caltech DSCOVR 项目中 (1) 从 $\psi^+ = 1$ (Tikhonov) 起始做完整符号推导, (2) generalize 到 exponential concentration assumption, (3) 在 4 个 benchmark 上系统 stress-test 与 L-curve / GCV / Morozov discrepancy / Kawahara Bayesian 对比, (4) 采用为 DSCOVR automatic pipeline 的主 selector。

**HBP 相对 BP 的核心优势**: BP 的 Lepskij-type stopping rule 需要 (i) prior knowledge of noise level $\delta$, (ii) tuning constant $\kappa$; HBP 通过 "minimum difference regularization parameter" 构造, **两者都不需要**。

**Bauer 2007 Definition 5.1** (HBP 构造骨架):

- "minimum difference regularization parameter":
  $$n^+ = \min\{ n \in [0, N] : D(n, k) > D(n-1, k) \text{ for some } k \}$$
- Balancing functional (简化):
  $$b(n, m) = \frac{\|x_n - x_m\|}{\Phi(N, m) - \Phi(N, n)}$$
- HBP 选 $\lambda_{n^+}$

### 核心论点

**1. 从 $\psi^+ = 1$ (Tikhonov) 起始的 exponential concentration 推导**

Zhenyu 从 Tikhonov 情形 $\psi^+ = 1$ 出发, 用 Bauer 的 exponential concentration assumption, 推导出 HBP 的 $\lambda_{n^+}$ 自动选择公式。完整 90 段 derivation 含:

- Lepskij-type stopping rule 的 generalization
- Mathé-Pereverzev 2003 geometric framework
- Tikhonov → BP → HBP 的 逐步 simplification
- Exponential concentration assumption 的 verification 方法 (difference function 的 minimum selection)

**[Future expansion]** Full mathematical derivation reserved for a follow-up post; this page captures the methodology skeleton only.

**2. 系统 stress test 结果**

Zhenyu 在 **4 个 benchmark** 上同时跑 HBP 与 4 个传统方法 (L-curve / GCV / Morozov discrepancy / Kawahara Bayesian cost):

| Benchmark | 配置 | HBP 表现 |
|---|---|---|
| **Hansen gravity problem** | 500-instance randomization | Automatic, 最 robust, 稳定 converge |
| **Golub 1979 Laplace** | Condition number **2.88e28** (Zhenyu 实测) vs paper 原 **1.54e5** — 比原论文更 ill-conditioned 的 stress test | Automatic, 仍然 work |
| **3-point linear regression** | Prof. King-Fai Li × Zhenyu Bayesian 化闭式解交叉验证 | 一致 |
| **DSCOVR real PC2 time series** | 2-year EPIC PC2, 实际 viewing geometry W (DSCOVR 轨道 + Earth rotation + pixelation + sun-illumination) | **HBP automatic λ** 收敛范围与 Siteng Fan 的 manual $\lambda \approx 10^{-3}$ benchmark 匹配 |

**3. Pipeline 主 selector 决策 logic** (经过 4 方法 stress-test 后的 motivated decision)

| Method | DSCOVR 上表现 | 选 / 不选 | 理由 |
|--------|-------------|--------|------|
| L-curve | 视觉 elbow 与理论 curvature 不一致 (**axis-scale bug**, 见 [[L-Curve-Axis-Scale-Ambiguity]]) | ❌ | unreliable 除非 axis-scale 校正 |
| Kawahara Bayesian cost | Hansen toy 上 case-by-case 不稳定 (5/5 失败于 $x_{sol} = [10, 1]$) + DSCOVR W 下 fail | ❌ | not robust for arbitrary W |
| GCV | long flat region → sensitive to noise direction + underestimates best λ | ❌ | statistical bias |
| Morozov discrepancy | systematic error (always biased to right of L-curve elbow) + 需要 $\delta$ | ❌ | systematic bias + prior info requirement |
| **HBP** | Automatic, 不需要 $\delta$ / $\kappa$, 在 DSCOVR 上表现可与 Siteng manual 结果匹配 | ✅ | **最 robust 且 automatic** |

→ **HBP 的采用不是任意 choice, 而是经过 Hansen textbook 4 方法的系统 stress-test 后的 motivated decision**。

### 与其他 regularization 方法对比

**vs L-curve** ([[反问题与正则化]] 所述经典方法):

- L-curve 需要 "拐角识别" — 要么 naked-eye (scale-dependent artifact, 见 [[L-Curve-Axis-Scale-Ambiguity]]), 要么计算 curvature (对 noise 敏感 + axis-scale 依赖)
- HBP 不需要 geometric interpretation, 完全 algebraic → 更适合 pipeline

**vs GCV** (Golub 1979):

- GCV 在 Golub 1979 原论文 example (condition 1.54e5) 上 work, 但 Zhenyu 复现时 condition 推到 2.88e28, 首次发现 **noise-direction dependence** (5 instance 中第 4 个 $\lambda_{GCV}$ 完全不同) → 后来系统化为 DSCOVR contribution (d) "Direction of Noise Vector Influences Regularization"
- HBP 对这个 geometry-dependence 更 robust

**vs Morozov Discrepancy Principle**:

- Discrepancy 要求 $\|A x_\lambda - d\| = \delta$, **必须预先知道 $\delta$**; HBP 完全 data-driven, $\delta$ 不需要

**vs Kawahara 2016 Bayesian cost**:

- Kawahara 的 evidence maximization 在特定 toy model work, 但 `|x_{sol}|` 大时 (e.g., $[10, 1]$) 在 Hansen toy 上 5/5 fail; DSCOVR 的 W 下也 fail
- HBP 在 Zhenyu 的 benchmark 中 **唯一在所有 4 benchmark 都 work** 的方法

### Downstream influence (方法学影响力)



Subsequent collaborators applied HBP to extended regimes (low / high clouds), demonstrating methodology transfer beyond the original PC2 land/ocean retrieval.

### 开放问题

- **非线性 forward operator** 下 HBP 是否仍然 valid? Bauer 2007 原 framework 是 linear Tikhonov, 非线性拓展需要重新推导 exponential concentration 性质
- **高维 regime** (n > 10000) 下 HBP 的 computational cost vs. GCV (需要 trace of hat matrix) 的实际对比
- **Bayesian 解释**: HBP 在 Bayesian framework 下是否对应某 specific hyperprior? 与 [[GP-贝叶斯反演]] 的 Type-II MLE 是否可 unify?

**[Future expansion]** Full math derivations, Bauer 2007 reading notes, and Mathé-Pereverzev 2003 geometric framework details reserved for a follow-up post.

### 来源

- `research_wiki/projects/mcmc_retrieval/overview.md` §贡献 (a) Hardened Balancing Principle (HBP) 应用 + 数学展开 (2021-09-27 + paper draft 90-paragraph section)
- `research_wiki/projects/mcmc_retrieval/overview.md` §🌟 贡献 (a) 扩展: HBP 在 DSCOVR case 上的系统测试
- `research_wiki/projects/mcmc_retrieval/overview.md` §贡献 (a) 扩展 Table (L-curve / Kawahara / GCV / Discrepancy / HBP 决策 logic)

- HBP mathematical writeup with collaborator acknowledgments (working manuscript, not publicly submitted).
- Bauer 2007 — HBP 方法源论文 (Definition 5.1)
- Bauer & Hohage 2005 — Balancing Principle 前身
- Mathé & Pereverzev 2003 — geometric framework
- `[待补充]` Zhenyu research-angle 独立 wiki 中的 HBP 学习笔记 (合并后此页扩展到 full derivation depth)

### 相关页面

- [[MCMC-贝叶斯反演]] — skill 页 (含 Caltech DSCOVR 4 原创贡献 subsection)
- [[反问题与正则化]] — parent concept (HBP 是其 automatic parameter selection 分支)
- [[L-Curve-Axis-Scale-Ambiguity]] — sibling concept (同 batch 建立的 DSCOVR 技术发现)
- [[GP-贝叶斯反演]] — Bayesian 对偶视角 (HBP 的 Bayesian interpretation 是开放问题)
- [[Caltech-DSCOVR-Research]] — 项目 experience page (从 PKU-Undergraduate-Research 拆出)
- [[Yuk-Yung]] — PI (Caltech)
- [[King-Fai-Li]] — co-advisor (UCR)
- [[Independent Judgment narrative (private)]] — HBP 采用决策是 motivated stress-test 的 pivotal moment
- [[profile]]

---

## English Version

### Definition

**Hardened Balancing Principle (HBP)** is an **automatic Tikhonov regularization parameter $\lambda$ selection method** proposed by Bauer 2007 on top of the Balancing Principle (BP) of Bauer & Hohage 2005. In the Caltech DSCOVR project, Zhenyu (1) carried out a complete symbolic derivation starting from $\psi^+ = 1$ (Tikhonov), (2) generalized to the exponential concentration assumption, (3) systematically stress-tested HBP on 4 benchmarks against L-curve / GCV / Morozov discrepancy / Kawahara Bayesian, and (4) adopted it as the primary selector for the DSCOVR automatic pipeline.

**HBP's core advantage over BP**: BP's Lepskij-type stopping rule requires (i) prior knowledge of noise level $\delta$, (ii) tuning constant $\kappa$; HBP, via the construction of "minimum difference regularization parameter", **needs neither**.

**Bauer 2007 Definition 5.1** (HBP construction skeleton):

- "minimum difference regularization parameter":
  $$n^+ = \min\{ n \in [0, N] : D(n, k) > D(n-1, k) \text{ for some } k \}$$
- Balancing functional (simplified):
  $$b(n, m) = \frac{\|x_n - x_m\|}{\Phi(N, m) - \Phi(N, n)}$$
- HBP picks $\lambda_{n^+}$

### Core Arguments

**1. Exponential concentration derivation starting from $\psi^+ = 1$ (Tikhonov)**

Zhenyu starts from the Tikhonov case $\psi^+ = 1$ and uses Bauer's exponential concentration assumption to derive the HBP $\lambda_{n^+}$ automatic selection formula. The complete 90-paragraph derivation contains:

- Generalization of the Lepskij-type stopping rule
- Mathé-Pereverzev 2003 geometric framework
- Step-by-step simplification from Tikhonov → BP → HBP
- Verification method for the exponential concentration assumption (minimum selection of the difference function)

**[Future expansion]** Full mathematical derivation (formula-level depth) reserved for a follow-up post.

**2. Systematic stress-test results**

Zhenyu ran HBP simultaneously with 4 traditional methods (L-curve / GCV / Morozov discrepancy / Kawahara Bayesian cost) on **4 benchmarks**:

| Benchmark | Configuration | HBP performance |
|---|---|---|
| **Hansen gravity problem** | 500-instance randomization | Automatic, most robust, stably converges |
| **Golub 1979 Laplace** | Condition number **2.88e28** (Zhenyu's measurement) vs the paper's original **1.54e5** — a stress test more ill-conditioned than the original paper | Automatic, still works |
| **3-point linear regression** | Cross-validated via Prof. King-Fai Li × Zhenyu Bayesian closed-form solution | Consistent |
| **DSCOVR real PC2 time series** | 2-year EPIC PC2, real viewing geometry W (DSCOVR orbit + Earth rotation + pixelation + sun-illumination) | **HBP automatic λ** convergence range matches Siteng Fan's manual $\lambda \approx 10^{-3}$ benchmark |

**3. Pipeline primary selector decision logic** (motivated decision after 4-method stress-test)

| Method | DSCOVR performance | Selected? | Reason |
|--------|-------------|--------|------|
| L-curve | Visual elbow inconsistent with theoretical curvature (**axis-scale bug**, see [[L-Curve-Axis-Scale-Ambiguity]]) | ❌ | Unreliable unless axis-scale corrected |
| Kawahara Bayesian cost | Case-by-case unstable on Hansen toy (5/5 fail at $x_{sol} = [10, 1]$) + fail under DSCOVR W | ❌ | Not robust for arbitrary W |
| GCV | Long flat region → sensitive to noise direction + underestimates best λ | ❌ | Statistical bias |
| Morozov discrepancy | Systematic error (always biased to right of L-curve elbow) + requires $\delta$ | ❌ | Systematic bias + prior info requirement |
| **HBP** | Automatic, requires neither $\delta$ nor $\kappa$, performance on DSCOVR matches Siteng's manual result | ✅ | **Most robust and automatic** |

→ **HBP's adoption is not an arbitrary choice but a motivated decision after systematic stress-testing of 4 textbook methods from Hansen**.

### Different Perspectives / Comparison with other regularization methods

**vs L-curve** (the classical method described in [[反问题与正则化]]):

- L-curve requires "corner identification" — either by naked-eye (a scale-dependent artifact, see [[L-Curve-Axis-Scale-Ambiguity]]) or by computing curvature (sensitive to noise + axis-scale dependent)
- HBP requires no geometric interpretation, is fully algebraic → better suited for pipelines

**vs GCV** (Golub 1979):

- GCV works on the original paper example of Golub 1979 (condition 1.54e5), but when Zhenyu reproduced it pushing condition number to 2.88e28, **noise-direction dependence** was first discovered (the 4th of 5 instances had a completely different $\lambda_{GCV}$) → later systematized as DSCOVR contribution (d) "Direction of Noise Vector Influences Regularization"
- HBP is more robust against this geometry-dependence

**vs Morozov Discrepancy Principle**:

- Discrepancy requires $\|A x_\lambda - d\| = \delta$, **which requires $\delta$ known a priori**; HBP is fully data-driven, no $\delta$ needed

**vs Kawahara 2016 Bayesian cost**:

- Kawahara's evidence maximization works on specific toy models, but when `|x_{sol}|` is large (e.g., $[10, 1]$), it fails 5/5 on Hansen toy; also fails under the DSCOVR W
- HBP is the **only method in Zhenyu's benchmarks that works on all 4 benchmarks**

### Downstream influence (methodological influence)



Subsequent collaborators applied HBP to extended regimes (low / high clouds), demonstrating methodology transfer beyond the original PC2 land/ocean retrieval.

### Open Questions

- Does HBP remain valid under **nonlinear forward operators**? Bauer 2007's original framework is linear Tikhonov; nonlinear extension would require re-deriving the exponential concentration property
- Practical comparison of HBP's **computational cost in high-dimensional regimes** (n > 10000) vs. GCV (which requires the trace of the hat matrix)
- **Bayesian interpretation**: does HBP correspond to a specific hyperprior in the Bayesian framework? Can it be unified with the Type-II MLE in [[GP-贝叶斯反演]]?

**[Future expansion]** HBP study notes (full math, Bauer 2007 reading notes, Mathé-Pereverzev 2003 framework derivation) reserved for a follow-up post.

### Sources

- `research_wiki/projects/mcmc_retrieval/overview.md` §Contribution (a) Hardened Balancing Principle (HBP) application + math expansion (2021-09-27 + paper draft 90-paragraph section)
- `research_wiki/projects/mcmc_retrieval/overview.md` §🌟 Contribution (a) extension: HBP systematic test on the DSCOVR case
- `research_wiki/projects/mcmc_retrieval/overview.md` §Contribution (a) extension Table (L-curve / Kawahara / GCV / Discrepancy / HBP decision logic)

- HBP mathematical writeup with collaborator acknowledgments (working manuscript, not publicly submitted).
- Bauer 2007 — original HBP method paper (Definition 5.1)
- Bauer & Hohage 2005 — Balancing Principle predecessor
- Mathé & Pereverzev 2003 — geometric framework
- `[to be added]` HBP study notes in Zhenyu's research-angle independent wiki (after merge, this page can be expanded to full derivation depth)

### Related Pages

- [[MCMC-贝叶斯反演]] — skill page (contains 4 original Caltech DSCOVR contributions subsection)
- [[反问题与正则化]] — parent concept (HBP is its automatic parameter selection branch)
- [[L-Curve-Axis-Scale-Ambiguity]] — sibling concept (DSCOVR technical discoveries established in the same batch)
- [[GP-贝叶斯反演]] — Bayesian dual perspective (HBP's Bayesian interpretation is an open question)
- [[Caltech-DSCOVR-Research]] — project experience page (split off from PKU-Undergraduate-Research)
- [[Yuk-Yung]] — PI (Caltech)
- [[King-Fai-Li]] — co-advisor (UCR)
- [[Independent Judgment narrative (private)]] — HBP adoption decision is a pivotal moment of motivated stress-testing
- [[profile]]
