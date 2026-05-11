---
title: "MCMC 与贝叶斯反演"
description: "Caltech DSCOVR (2021-2022) 研究级能力 + 4 原创贡献 (Hansen σ² vs σ⁴ bug catch + Pre-whitening L-curve + HBP)"
publish: true
lang: bilingual
---

# MCMC 与贝叶斯反演 (MCMC & Bayesian Inversion)

## 中文版

### 熟练度
熟练

### 描述

**MCMC 采样**
- 使用 `emcee` (affine-invariant ensemble sampler, Foreman-Mackey 2013) 做真实问题上的后验采样
- 处理 log-space 重参数化（`log10_alpha` / `log10_sigma`）避免尺度跨度问题
- Trace plot + corner plot 做链诊断
- MCMC 多进程与 BLAS 线程冲突的工程处理（`OMP_NUM_THREADS=1` 等 8 个环境变量）

**高斯过程回归 (GP)**
- RBF kernel + 超参数 MCMC 层级化处理（超参数 alpha、sigma 通过 MCMC 采样）
- Spatial × Temporal separable kernel `KS ⊗ KT` 避免 O(N³) 全联合协方差
- HEALPix 球面网格作为 GP 的 spatial grid（healpy）
- Snapshot-level 与 pixelwise 两种后验协方差的手写闭式实现

**反问题正则化参数选择**
- L-Curve method
- L-Curve Curvature method
- Generalized Cross Validation (GCV) —— 手写 Golub 1979 定义的目标函数
- Morozov discrepancy principle
- 在 Hansen 书 gravity problem 例子和真实 DSCOVR 数据上都做过四种方法的对比

**Numerical Linear Algebra**
- `scipy.linalg.solve(..., assume_a="pos")` Cholesky 求解避免显式 inv
- `np.linalg.slogdet` 代替 `log(det)` 防下溢
- SVD 分解 + Tikhonov 正则化（MATLAB `csvd` 等）
- 大矩阵的条件数分析

**工具链**
- Python：emcee、scipy、numpy、healpy、astropy、pandas
- MATLAB：方法验证 + Hansen 书数值复现
- Mathematica：符号推导 / 概率形式化验算

### 自学路径（值得强调）
2021 年独立读完 **Hansen《Discrete Inverse Problems》** + **Bishop PRML** + **Golub 1979 原始 GCV 论文**，并在 repo 中逐步复现教科书和原始论文里的数值实验——"教科书 → 原始论文 → 复现 → 应用到新问题"的链路。

### 🌟 Caltech DSCOVR 4 原创贡献 (2021-2022, Yuk Yung + King-Fai Li 指导)

#### 🌟 贡献 (c): 发现并修正 Hansen 教科书公式错误 (σ² vs σ⁴, 80× 偏差)

**核心成就**: 作为本科生, 用独立 SVD + filter factor 推导, 在 Hansen classic 的 *Discrete Inverse Problems* (SIAM 2010) 这种 foundational textbook 中发现**公式级 bug** — 不是 typo, 而是导致**数值结果相差 ~80× 的实质错误**。

**数值对比** (同样 toy model + PC2 数据):

| Formula | Toy model λ | PC2 λ | 准确性 |
|---------|------------|-------|--------|
| **Hansen 学生正确版 (σ⁴)** | **0.0251** ✓ | **0.0575** ✓ | 与 naked-eye elbow + axis-image 下理论值一致 |
| **Hansen 书本错误版 (σ²)** | **1.995** ✗ | **1.995** ✗ | **80× overestimate, 完全失败** |

**创新发现**: 独立发现 Hansen 未讨论的 **L-curve axis-scale ambiguity**:

> *"Hansen didn't talk about whether we should control the units of x-axis and y-axis of L-curve to be the same. In his book, he showed two L-curve figures, but both didn't control the units to be the same."* (2022-01-08 发现)

**3-step self-correction cycle** (11/29 → 12/06 → 01/08): 自己发现公式错 → 假设 accumulation of errors → refute + 正确归因为 axis-scale ambiguity — 体现 intellectual honesty + iteration

**物理证据纪律**: 同时保留 **Hansen 原版 PDF (分母 σ²) + Hansen 学生正确版 PDF (分母 σ⁴) 并列在 `LCurve_HansenMistake_WeRectify_Test/` 目录** — "inconvenient-evidence retention" 精神, 对应 [[inconvenient-evidence retention discipline (private)]]

**社区贡献**: 向学术社区提出 **3 个 open questions** — (1) 应否 control L-curve axes 等单位? (2) a senior collaborator 的 elbow λ=1e-3 结论是否为 scale-artifact? (3) 应用 L-curve 时在哪些情况下调节, 如何调?

#### 🌟 贡献 (b): Pre-whitening L-curve 创新 + 拒绝 methodological-engineering pressure 的诚实决策

**技术创新**: 在 RBF kernel (non-diagonal covariance $S_a$) 下, 变换到白化空间:
$$x_1 = S_a^{-1/2}x, \quad y_1 = S_e^{-1/2}y, \quad A_1 = S_e^{-1/2}A S_a^{1/2}$$

**问题诊断**: 发现 **L-curve 在非对角 $S_a$ 下 x/y 值不单调** → structural limit: L-curve 对应 pure Tikhonov, non-diagonal $S_a$ 不能 derive 到 Tikhonov form; "modified L-curve" 对 $S_a, S_e$ priors 过度敏感。

**独立判断 — methodological restraint (2022-01-23 group meeting verbatim)**:



(Declined to tune $S_a$, $S_e$ priors to engineer a target λ — methodological commitment.)

**Methodology maturity 证据**: "我自己提议的方法, 我自己系统诊断它的 limitation" — 本科生拒绝 advisor 隐含 preference 来凑 λ 数值, research integrity signature。与 [[Independent Judgment narrative (private)]] Moment 3 对应。

#### 贡献 (a): Hardened Balancing Principle (HBP) 90-段数学展开

**理论框架**: 从 $\psi^+=1$ (Tikhonov) 出发, 经 Bauer 2007 exponential concentration assumption → 自动 parameter selection 的 HBP `λ_{n+}` 公式。

**系统 stress test**:
- Hansen gravity problem (500-instance, 条件数 ~2.88e28 vs reported ~1.54e5)
- Golub 1979 Laplace (条件数达 2.88e28)
- 3-point linear regression (Prof. King-Fai Li × Zhenyu Bayesian 化闭式解交叉验证)
- DSCOVR real PC2 time series

**结论**: HBP 表现最好, 不需 prior knowledge of noise level δ 或 tuning constant κ

**输出**: `internal-only manuscript` 的 **90-段数学 section writeup** — 相当于独立技术笔记/教程规模, 含从 Tikhonov 到 HBP 的完整推导。

#### 贡献 (d): Noise Vector 方向影响正则化方法性能 (独创发现)

**原始发现 (2021-09-20 verbatim)**:

> *"When I did numerical tests on L-Curve, GCV etc., **I found out the direction of the noise vector plays a big role** in the performance of statistical criteria. **I did a literature search and it seems nobody has studied this topic.**"*

**4-method failure-mode catalog**:

| Method | 失效条件 |
|--------|---------|
| L-curve | \|x_sol\| 大, 或 $dd$ 近 EV1 |
| Kawahara Bayesian | \|x_sol\| 大 (5/5 fail for x_sol=[10,1]) |
| GCV | $d$ 近 EV1 且 $dd$ 近 EV2 |
| Discrepancy principle | 总 work, 但引入 systematic error |

**源头偶然发现**: Golub 1979 GCV 复现 (condition 2.88e28) 时, 5 instance 中第 4 个 λ_GCV 完全不同 → Hansen gravity 500-instance 验证汇聚 → 系统化为贡献 (d)。**独立发现 + literature gap awareness** (与 HBP later extended by a subsequent collaborator to PC1/PC4 clouds 形成方法影响力链)。

**跨语言 fluency** (本单个 11-month 项目):

| Language | 承担任务 |
|----------|---------|
| **IDL** | OOP MCMC class (继承 Yuk Yung lab convention) |
| **MATLAB** | Hansen 书 gravity problem replication + csvd |
| **Python** | Kawahara CUDA library bootstrap (remote workstation, Anaconda) + emcee + healpy |
| **Mathematica** | symbolic curvature 推导 (calculation_4_cal_deriva.nb + calculation_5_cal_deriva.nb) |
| **R** | Metropolis-Hastings baseline for cross-validation |

**29 group_meeting pptx** sustained trajectory (Mar 2021 → Mar 2022), 与 Walker paper v3→v6 drafting (Sep-Oct 2021) + nwp_hw 4 作业 (Oct-Dec 2021) 构成 [[Independent Judgment narrative (private)]] Moment 4 的 "3-track parallel Sep-Dec 2021" evidence。

### 在哪些经历中用到
- [[PKU-Undergraduate-Research]] — MCMC Retrieval Methods 项目 (2021.03—2022.03), Caltech PI Yuk Yung + UCR King-Fai Li 合作; **29 group_meeting pptx / 5 种编程语言** (IDL + MATLAB + Python + Mathematica + R)
- [[Caltech-DSCOVR-Research]] — 从 PKU-Undergraduate-Research.md 拆出的独立 35k words project experience page, 含 4 原创贡献 deep-dive
- [[MCMC-Mapping-GitHub]] — 完整研究代码 + 学习笔记 repo (2021-09-13 last commit, pre-Caltech 4 贡献 finalization)
- 可以迁移到: 任何 ill-posed inverse problem (气候反演 / 医学成像 / 地球物理 / 系外行星 spin-mapping)

### 方法论 concept 页
- [[反问题与正则化]] — 频率学派视角
- [[GP-贝叶斯反演]] — 贝叶斯视角
- [[Hardened-Balancing-Principle]] — HBP 90-段独立 concept, 从 Bauer 2007 出发的 automatic regularization parameter selection
- [[L-Curve-Axis-Scale-Ambiguity]] — Hansen σ²/σ⁴ 80× bug 独立 concept, L-curve axis-scale 单位处理的 open question

---

## English Version

### Proficiency
Proficient

### Description

**MCMC sampling**
- `emcee` (affine-invariant ensemble sampler, Foreman-Mackey 2013) on real problems
- Log-space reparameterization for scale-spanning parameters
- Trace + corner plots for chain diagnostics
- Practical handling of MCMC multi-process × BLAS thread collision (`OMP_NUM_THREADS=1` + 7 other env vars)

**Gaussian Process regression**
- RBF kernel + hierarchical MCMC sampling of hyperparameters
- Spatial × Temporal separable kernel `KS ⊗ KT` to avoid O(N³) joint covariance
- HEALPix spherical grid as GP spatial support (healpy)
- Snapshot-level and pixelwise posterior covariances implemented in closed form

**Regularization parameter selection for inverse problems**
- L-Curve method
- L-Curve Curvature method
- Generalized Cross Validation (GCV) — hand-implemented from Golub 1979
- Morozov discrepancy principle
- All four compared on Hansen gravity-problem example and on real DSCOVR data

**Numerical linear algebra**
- `scipy.linalg.solve(..., assume_a="pos")` Cholesky instead of explicit inverse
- `np.linalg.slogdet` vs `log(det)` for underflow safety
- SVD + Tikhonov regularization (MATLAB `csvd`, etc.)
- Matrix condition number analysis

**Toolchain**
- Python: emcee, scipy, numpy, healpy, astropy, pandas
- MATLAB: method verification + Hansen-book reproductions
- Mathematica: symbolic derivations / probability formalism checks

### Self-study path (worth highlighting)
In 2021 self-studied **Hansen's *Discrete Inverse Problems*** + **Bishop's PRML** + **Golub 1979 original GCV paper**, progressively reproducing textbook and original-paper numerical experiments — the "textbook → original paper → reproduction → applied to new problem" chain.

### Used In
- [[PKU-Undergraduate-Research]] — MCMC Retrieval Methods project (Mar 2021 — Mar 2022)
- [[MCMC-Mapping-GitHub]] — full research-code + study-notes repo
- Transferable to: any ill-posed inverse problem (climate retrieval, medical imaging, geophysical inversion, exoplanet spin-mapping)

### Methodology Concept Pages
- [[反问题与正则化]] — frequentist view
- [[GP-贝叶斯反演]] — Bayesian view
- [[Hardened-Balancing-Principle]] — HBP automatic regularization parameter selection
- [[L-Curve-Axis-Scale-Ambiguity]] — Hansen σ²/σ⁴ 80× bug open question

### Caltech DSCOVR 4 Original Contributions (2021-2022, Advised by Yuk Yung + King-Fai Li)

#### Contribution (c): Hansen Textbook σ² vs σ⁴ Bug Catch (80× Deviation)

**Core achievement**: As an undergraduate, using independent SVD + filter-factor derivation, found a **formula-level bug** in Hansen's classic *Discrete Inverse Problems* (SIAM 2010) — a foundational textbook — not a typo, but a substantive error causing **numerical results to differ by ~80×**.

**Numerical comparison** (same toy model + PC2 data):

| Formula | Toy model λ | PC2 λ | Accuracy |
|---|---|---|---|
| **Hansen-student correct version (σ⁴)** | **0.0251** ✓ | **0.0575** ✓ | Consistent with naked-eye elbow + theoretical value under axis-image |
| **Hansen-book erroneous version (σ²)** | **1.995** ✗ | **1.995** ✗ | **80× overestimate, complete failure** |

**Innovative discovery**: independently identified an **L-curve axis-scale ambiguity** not discussed by Hansen:

> *"Hansen didn't talk about whether we should control the units of x-axis and y-axis of L-curve to be the same. In his book, he showed two L-curve figures, but both didn't control the units to be the same."* (discovered 2022-01-08)

**3-step self-correction cycle** (11/29 → 12/06 → 01/08): self-discovered the formula error → hypothesized accumulation of errors → refuted that and correctly attributed it to axis-scale ambiguity — demonstrates intellectual honesty + iteration.

**Physical-evidence discipline**: simultaneously preserved **Hansen original-version PDF (denominator σ²) + Hansen-student correct-version PDF (denominator σ⁴) side-by-side under `LCurve_HansenMistake_WeRectify_Test/` directory** — "inconvenient-evidence retention" spirit, corresponding to [[inconvenient-evidence retention discipline (private)]].

**Community contribution**: posed **3 open questions** to the academic community — (1) Should L-curve axes be controlled to the same units? (2) Is a senior collaborator's elbow λ=1e-3 conclusion a scale artifact? (3) When applying L-curve, in which cases should one tune, and how?

#### Contribution (b): Pre-whitening L-curve Innovation + Methodological Restraint

**Technical innovation**: under RBF kernel (non-diagonal covariance $S_a$), transform into the whitened space:
$$x_1 = S_a^{-1/2}x, \quad y_1 = S_e^{-1/2}y, \quad A_1 = S_e^{-1/2}A S_a^{1/2}$$

**Problem diagnosis**: discovered that **L-curve x/y values become non-monotonic under non-diagonal $S_a$** → structural limit: L-curve corresponds to pure Tikhonov, and non-diagonal $S_a$ cannot derive into Tikhonov form; "modified L-curve" is overly sensitive to $S_a, S_e$ priors.

**Independent judgment — methodological restraint (2022-01-23 group meeting verbatim)**:



(Declined to tune $S_a$, $S_e$ priors to engineer a target λ — methodological commitment.)

**Methodology-maturity evidence**: "I systematically diagnose the limitations of a method I myself proposed" — an undergraduate refusing the advisor's implicit preference to engineer the desired λ value, a research-integrity signature. Corresponds to [[Independent Judgment narrative (private)]] Moment 3.

#### Contribution (a): Hardened Balancing Principle (HBP) 90-paragraph Writeup

**Theoretical framework**: starting from $\psi^+=1$ (Tikhonov), via Bauer 2007 exponential concentration assumption → automatic parameter-selection HBP `λ_{n+}` formula.

**Systematic stress test**:
- Hansen gravity problem (500-instance, condition number ~2.88e28 vs reported ~1.54e5)
- Golub 1979 Laplace (condition number reaching 2.88e28)
- 3-point linear regression (Prof. King-Fai Li × Zhenyu Bayesian-form closed-solution cross-validation)
- DSCOVR real PC2 time series

**Conclusion**: HBP performs the best, requiring no prior knowledge of noise level δ or tuning constant κ.

**Output**: the **90-paragraph math section writeup** in `internal-only manuscript` — equivalent in scale to a standalone technical note/tutorial, containing the full derivation from Tikhonov to HBP.

#### Contribution (d): Direction of Noise Vector Influences Regularization (Original Discovery)

**Original discovery (2021-09-20 verbatim)**:

> *"When I did numerical tests on L-Curve, GCV etc., **I found out the direction of the noise vector plays a big role** in the performance of statistical criteria. **I did a literature search and it seems nobody has studied this topic.**"*

**4-method failure-mode catalog**:

| Method | Failure condition |
|---|---|
| L-curve | \|x_sol\| large, or $dd$ near EV1 |
| Kawahara Bayesian | \|x_sol\| large (5/5 fail for x_sol=[10,1]) |
| GCV | $d$ near EV1 and $dd$ near EV2 |
| Discrepancy principle | Always works, but introduces systematic error |

**Origin — accidental discovery**: when reproducing Golub 1979 GCV (condition 2.88e28), the 4th of 5 instances had a completely different λ_GCV → Hansen-gravity 500-instance validation aggregated → systematized into contribution (d). **Independent discovery + literature-gap awareness** (with HBP later extended by a subsequent collaborator to PC1/PC4 clouds, forming a methodology-influence chain).

**Cross-language fluency** (within this single 11-month project):

| Language | Task taken |
|---|---|
| **IDL** | OOP MCMC class (inheriting Yuk Yung lab convention) |
| **MATLAB** | Hansen-book gravity problem replication + csvd |
| **Python** | Kawahara CUDA library bootstrap (remote workstation, Anaconda) + emcee + healpy |
| **Mathematica** | Symbolic curvature derivations (calculation_4_cal_deriva.nb + calculation_5_cal_deriva.nb) |
| **R** | Metropolis-Hastings baseline for cross-validation |

**29 group_meeting pptx** sustained trajectory (Mar 2021 → Mar 2022), together with Walker paper v3→v6 drafting (Sep-Oct 2021) + nwp_hw 4 assignments (Oct-Dec 2021) constitutes the "3-track parallel Sep-Dec 2021" evidence of [[Independent Judgment narrative (private)]] Moment 4.
