---
title: "DSCOVR Inverse Problem + Regularization Methods @ Caltech / UCR"
publish: true
role_framing: sole-author
project_status: completed
year: 2021
lang: bilingual
description: "Caltech / UCR remote undergraduate research on the DSCOVR inverse problem with novel regularization methods (HBP, Pre-whitening L-curve)"
---

# DSCOVR Inverse Problem + Regularization Methods @ Caltech / UCR

## 中文版

### 基本信息
- **时间**: 2021.03 — 2022.03 (~11 months active work, 含最集中的 4 个月原创贡献窗口)
- **角色**: 本科远程研究 (Undergraduate remote research)
- **组织**: Caltech (Division of Geological and Planetary Sciences) + UC Riverside (Environmental Sciences)
- **指导教师**: [[Yuk-Yung]] (primary PI, Caltech) + [[King-Fai-Li]] (co-supervisor, UCR)
- **Paper draft corresponding author**: [[Siteng-Fan-范思腾]] (LMD Paris, former Yuk Yung postdoc)
- **地点**: 远程 (Zhenyu 在北大, Caltech / UCR teamwork remote)
- **项目入口**: via [[Li-Chong-李充]] (北大师兄, Yuk Yung co-author on Li C 2020 RS paper)

### 核心问题
DSCOVR 单点地球光曲线 inverse problem — 从 DSCOVR/EPIC 卫星在 Sun-Earth L1 Lagrange point 观测到的 Earth 单点 reflectance time series, 反演 Earth 陆海分布 (land-ocean map retrieval), 作为未来 exoplanet characterization 的 "validation exoplanet" benchmark。方法上以 MCMC 扩展 Rodgers 传统反演, 并系统研究 ill-conditioned inverse problem ($A x = b$, condition number ~$10^6$, DSCOVR $W$ matrix Picard plot 衰减远快于 Kawahara toy) 的 regularization-parameter selection。

**Paper draft** (未发表): *"An automatic pipeline for retrieval from DSCOVR data"*, co-authors co-authors (anonymized in public version), **Zhenyu He¹**, [[Siteng-Fan-范思腾]]\* (corresponding), King-Fai Li³, Yuk L. Yung⁴,⁵, Yongyun Hu¹ (multiple institutions)。90-paragraph HBP mathematical section 由 Zhenyu 主笔。

---

### 🌟 Zhenyu 4 原创贡献 (按 proposal Example 6 的 4 原创 narrative)

#### 🌟 贡献 (c): Hansen σ² vs σ⁴ textbook bug catch (2022-01-08, **80× 偏差**)

**核心成就**: 作为本科生, 用独立 SVD + filter factor 推导, 在 Hansen classic *Discrete Inverse Problems* (SIAM 2010) 这种 foundational textbook 中发现 **公式级 bug** — 不是 typo, 而是导致 **数值结果相差 ~80×** 的实质错误。

**数值对比** (同一 toy model + PC2 数据):

| Formula | Toy model λ | PC2 λ | 准确性 |
|---------|------------|-------|--------|
| **Hansen 学生正确版 (σ⁴)** | **0.0251** ✓ | **0.0575** ✓ | 与 naked-eye elbow + axis-image 下理论值一致 |
| **Hansen 书本错误版 (σ²)** | **1.995** ✗ | **1.995** ✗ | **80× overestimate, 完全失败** (λ 卡在上界, 不依赖数据) |

**创新发现** — 独立识破 Hansen 未讨论的 **L-curve axis-scale ambiguity** (2022-01-08 发现):

> *"Hansen didn't talk about whether we should control the units of x-axis and y-axis of L-curve to be the same. In his book, he showed two L-curve figures, but both didn't control the units to be the same."*

**3-step self-correction cycle** (11/29 → 12/06 → 01/08, 整个 trajectory 保留):
1. **11/29** 发现自己公式错 (group-meeting slide 4)
2. **12/06** 假设 "accumulation of errors" — 归因错误 (slide 6)
3. **01/08** refute 该假设, **正确归因 axis-scale ambiguity** — slide 7-10 原话: *"What if our naked eyes are wrong, but the calculated curvature is right?"* (5-cell 手算演示, 加 matlab `axis image` 强制等单位后, curvature elbow at $x=-1.337$ 就真正对上了)

**物理证据 discipline**: `LCurve_HansenMistake_WeRectify_Test/` 目录同时保留
- `Hansen自己文章_仍然mu二次方.pdf` (Hansen 原版, 分母 σ²)
- `hansen学生mu四次方.pdf` (Hansen 学生正确版, 分母 σ⁴)

并列纪录为 reproducible numerical-science best practice — 见 Evidence Preservation Discipline (private companion)。

**独立数学验证**: `Deductions of the curvature of log-log Lcurve.docx` 36-paragraph 符号推导, 从 SVD $A = U\Sigma V^T$ + filter factors $f_i = \sigma_i^2 / (\sigma_i^2 + \lambda^2)$ 推导 $\ln|x_\lambda|$ 与 $\ln|Ax_\lambda - b|$ 关于 $\mu = \ln\lambda$ 的二阶导, 关键一步: "**The denominator should have σ_i^4 instead of σ_i^2**"。

**社区贡献 (3 open questions)**: (1) 应否 control L-curve axes 等单位? (2) a senior collaborator 的 elbow λ=1e-3 结论是否 scale-artifact? (3) 应用 L-curve 时什么情况下调节, 如何调?

详见 [[L-Curve-Axis-Scale-Ambiguity]] concept page。

---

#### 🌟 贡献 (b): Pre-whitening L-curve 创新 + methodological restraint (2022-01-23)

**技术创新**: 在 RBF kernel (non-diagonal prior covariance $S_a$) 下, 变换到白化空间:

$$x_1 = S_a^{-1/2}x, \quad y_1 = S_e^{-1/2}y, \quad A_1 = S_e^{-1/2}A S_a^{1/2}$$

在 whitened space 绘 $\ln|x_1|$ vs $\ln|y_1 - A_1 x_1|$ → "modified L-curve"。

**问题诊断**: 发现 L-curve 在非对角 $S_a$ 下 **x/y 值不单调变化** → structural limit: L-curve 对应 pure Tikhonov, non-diagonal $S_a$ 不能 derive 到 Tikhonov form; "modified L-curve" 结果对 $S_a, S_e$ priors 过度敏感 — how well you know the priors 直接影响结果。

**独立判断 — 2022-01-23 group meeting verbatim (methodological restraint)**:


Held to the methodology rather than tuning $S_a$, $S_e$ priors to engineer a target λ.

**意义**: 21 岁本科生**当场拒绝 advisor [[Siteng-Fan-范思腾]] 隐含 preference** (tune $S_a, S_e$ 来凑 λ=1e-3 的 paper benchmark) — 不投机取巧, 诚实承认 "我自己提议的方法, 只在 Tikhonov-equivalent covariance 下能 work"。**"我自己诊断自己方法的 limitation"** 是 methodology maturity 的稀有 discipline。

与 Independent Judgment narrative (held until 2026-06-10) Moment 3 对应。

---

#### 贡献 (a): Hardened Balancing Principle (HBP) 90-段数学展开

**理论框架**: 从 Bauer 2007 Definition 5.1 的 $\psi^+ = 1$ (Tikhonov) 起始, 推导:
- minimum-difference regularization parameter: $n^+ = \min\{n \in [0,N] : D(n,k) > D(n-1,k) \text{ for some } k\}$
- balancing functional $b(n,m) = \|x_n - x_m\| / [\Phi(N,m) - \Phi(N,n)]$
- exponential concentration → HBP `λ_{n+}` 自动 parameter selection

**系统 stress test** (4 benchmark):

| Benchmark | 条件数 / 数据 | HBP 表现 |
|-----------|-------------|---------|
| Hansen gravity problem (500-instance) | ~2.88e28 vs Hansen 书 reported ~1.54e5 | 稳健 |
| Golub 1979 Laplace | 2.88e28 (比 Golub 原 paper 1.54e5 更 ill-conditioned) | 稳健 |
| 3-point linear regression | King-Fai Li Bayesian 闭式解 cross-validate | α=9.57, σ=0.023, λ 解析 vs MCMC 差 18% ✓ |
| DSCOVR real PC2 time series | Kawahara Bayesian cost 失效的 W | 收敛到 Siteng λ≈1e-3 近似范围 |

**结论**: HBP 不需 prior knowledge of noise level δ 或 tuning constant κ (BP 都需要), 多 benchmark 最稳健。

**输出**: `internal-only manuscript` 的 **90-paragraph mathematical section writeup** — 从 Tikhonov 到 HBP 全部推导, 相当于独立技术笔记 / 教程规模。

**Downstream impact**: HBP 被 co-author a subsequent collaborator 扩展到 PC1 (low clouds) / PC4 (high clouds) retrieval (不同于 Zhenyu 的 PC2 = land/ocean) — 方法学影响力延伸到合作者工作。

详见 [[Hardened-Balancing-Principle]] concept page。

---

#### 贡献 (d): Direction of Noise Vector discovery (2021-09-20)

**原始发现 (2021-09-20 verbatim)**:

> *"When I did numerical tests on L-Curve, GCV etc., **I found out the direction of the noise vector plays a big role** in the performance of statistical criteria. **I did a literature search and it seems nobody has studied this topic.**"*

**Geometric decomposition**: $A = [A_1, A_2]$ 的 column space 中, $d = A x_{sol}$, 噪声 $dd$ 分解为 perpendicular + parallel; parallel component 沿 eigenvector 分解后 **EV2 方向分量会被放大**。

**4-method failure-mode catalog**:

| Method | 失效条件 |
|--------|---------|
| L-curve | $\|x_{sol}\|$ 大, 或 $dd$ 近 EV1 |
| Kawahara Bayesian | $\|x_{sol}\|$ 大 (5/5 fail for $x_{sol}=[10,1]$, negative component) |
| GCV | $d$ 近 EV1 且 $dd$ 近 EV2 (long flat cost region) |
| Discrepancy principle | 总 work, 但引入 systematic error (underestimates $\|x\|$) |

**源头偶然发现 → systematic discovery**: Golub 1979 GCV paper 复现 (Zhenyu condition 2.88e28, 比 paper 1.54e5 更 ill-conditioned) 时, 5 instances 中第 4 个 λ_GCV 与其他 4 个完全不同 → Hansen gravity 500-instance 再次独立发现 → 两独立 evidence 汇聚 → 系统化为 contribution (d)。**文献检索确认 literature gap ("nobody has studied")** 是 signature of independent problem-formulation ability。

详见 [[Multi-Method-Comparison-Spine]]。

---

### 关键成就

1. **Hansen textbook bug catch (80× overestimate, 公式级错误 in foundational classic)** — 本科生在 SIAM 2010 classic 发现公式 bug + inconvenient evidence 并列保留
2. **Pre-whitening L-curve 创新 + 2022-01-23 methodological restraint verbatim** — research integrity signature
3. **HBP 90-段数学展开 + 4-benchmark stress test + subsequent collaborator's PC1/PC4 extension** — 方法学影响力链
4. **Direction of Noise Vector independent discovery + literature gap awareness** — problem-formulation 原创性
5. **跨语言 fluency**: 单 11-month 项目内 **5 种编程语言**:

| Language | 承担任务 |
|----------|---------|
| **IDL** | OOP MCMC class (继承 Yuk Yung lab convention, 向李婧 PKU group 学 scripts) |
| **MATLAB** | Hansen gravity problem replication + csvd + 5 `LCurve_HansenMistake_WeRectify_Test` 嵌套子目录 |
| **Python** | Kawahara CUDA library bootstrap (remote workstation) + emcee + healpy + scipy |
| **Mathematica** | symbolic curvature 推导 (`calculation_4_cal_deriva.nb` + `calculation_5_cal_deriva.nb`) |
| **R** | Metropolis-Hastings baseline for cross-validation |

6. **29 group_meeting pptx** sustained trajectory (Mar 2021 → Mar 2022, ~1 PPT / 2 周) — 本科生 ~12 个月单项目 29 次正式 group-meeting 报告
7. **Self-study rigor**: 三本 classic 全部复现 — Hansen *Discrete Inverse Problems* (SIAM 2010) + Bishop PRML + Golub 1979 original GCV paper, 数值实验逐一 replicate

---

### 技术深度 (resume-grade specifics)

- **Self-study 三本教材全复现**: Hansen *Discrete Inverse Problems* + Bishop PRML + Golub 1979 GCV paper — 不是阅读, 是 replicate Fig 5.9 gravity 500-instance histogram + Laplace condition 2.88e28 stress test + Ch 5.6 shaw test problem, 得到与原图几乎重合的 histogram
- **~3,000+ lines of code + study notes** on [[MCMC-Mapping-GitHub]] repo (与 Caltech 4 贡献 parallel, pre-finalization commit 2021-09-13, 后续 research-wiki 文件已不在此 repo 但概念统一)
- **remote workstation bootstrap**: Caltech Anaconda + CUDA 11.2 + Kawahara library (Windows 下 CUDA library 不 support → Zhenyu manual 诊断 + driver setup), 2021-08-09 group meeting "Finished Setting up Environments for Running codes on (remote workstation)" — 非 trivial 的 devops skill
- **5 个 nested stress test 子目录** (`LCurve_HansenMistake_WeRectify_Test/`): 测试1 Hansen公式_失败于上界_toy / 测试2 学生公式_成功_toy / 测试3 PC2 / 测试4 SaSe白化_自己估计 / 测试5 SaSe白化_Kawahara后验 — 每目录含 Hansen原版 + 学生正确版 L-curve + curvature-vs-λ figure, 便于视觉 diff
- **Mathematica symbolic ↔ MCMC 交叉验证**: 3-point regression 闭式解 (α=9.57, σ=0.023, λ=5.73e-5) vs MCMC (λ=6.76e-5) 差 18% — double-check discipline
- **5×4 failure-mode matrix** (5 $x_{sol}$ geometry × 4 regularization method): [1,1] / [3,1] / [5,1] / [7,1] / [10,1] 每个 case 对 L-curve / Kawahara / GCV / Discrepancy 给出 best λ + retrieved x, 结构性识别每方法 fail 的 geometric condition — 不是 "4 方法并列" 而是 "4 方法在 5 geometry 下的 capability diagnosis"

---

### 学术 / 职业意义

- **Moment 4 (Caltech → Berkeley cross-paradigm switch, 2022-08)**: 放弃 11 个月 IDL / MATLAB / Python / Mathematica / R tooling + 4 原创贡献 momentum, 跨 paradigm 到 David Romps DAM LES Fortran (single-point remote sensing → 3-D LES moist convection);  External factor 是 key external factor, 但核心是 Zhenyu **主动** 选择 switch 应用方向 (exoplanet habitability → nuclear winter policy) — 详见 Independent Judgment narrative (held until 2026-06-10) Moment 4
- **Moment 3 (methodological restraint, 2022-01-23)**: DSCOVR pre-whitening 验证失败时本科生当场拒绝 self-discipline call (declined to engineer target λ) — 见 Independent Judgment narrative (held until 2026-06-10) Moment 3
- **3-track parallel Sep-Dec 2021 本科大四上**: Caltech DSCOVR HBP 成熟 + Walker paper v3→v6 drafting (见 [[PKU-Walker-Circulation-Research]]) + PKU Aerosol thesis drafting (见 [[PKU-Aerosol-Senior-Thesis]]) + nwp_hw 4 个作业 ≈ 3-4 deliverable/week sustained intensity

---

### 使用的技能
- [[MCMC-贝叶斯反演]] (Round 3 update 加 Caltech 4 贡献)
- [[反问题与正则化]] (Hansen bug catch + pre-whitening; concept scaffold)
- [[GP-贝叶斯反演]] (Kawahara SOT 方法)
- [[Python-科学计算]]
- [[高性能计算-HPC]] ((remote workstation) CUDA bootstrap)

---

### 相关页面
- [[PKU-Undergraduate-Research]] (umbrella page)
- [[Yuk-Yung]] (Caltech primary PI)
- [[King-Fai-Li]] (UCR co-supervisor)
- [[Siteng-Fan-范思腾]] (LMD Paris, paper draft corresponding author)
- [[Li-Chong-李充]] (Caltech bridge via Li C 2020 RS paper)
- [[Hardened-Balancing-Principle]] (贡献 a)
- [[L-Curve-Axis-Scale-Ambiguity]] (贡献 c)
- Evidence Preservation Discipline (private companion) (Hansen PDF 并列保留)
- [[Multi-Method-Comparison-Spine]] (4-method 5-geometry failure-mode matrix)
- Independent Judgment narrative (held until 2026-06-10) (Moment 3 + 4)
- [[PKU-Walker-Circulation-Research]] (3-track parallel Sep-Dec 2021)
- [[PKU-Aerosol-Senior-Thesis]]
- [[MCMC-Mapping-GitHub]]
- [[反问题与正则化]]
- [[GP-贝叶斯反演]]

### 来源
- `research_wiki/projects/mcmc_retrieval/overview.md` (~35k words, 全 1329 行)
- `research_wiki/resume_angles/problem_solving.md` §Project 3 DSCOVR
- `research_wiki/resume_angles/independent_judgment.md` §Moment 3 + 4
- `raw/Caltech_task/` 1.5 GB folder (1,364 files / 126 dirs, 29 group_meeting pptx + `internal-only manuscript` + 10 technical docx + `LCurve_HansenMistake_WeRectify_Test/` 子目录)

---

## English Version

### Basic Info
- **Period**: Mar 2021 — Mar 2022 (~11 months active work, with the most concentrated 4-month original-contribution window)
- **Role**: Undergraduate remote research
- **Organization**: Caltech (Division of Geological and Planetary Sciences) + UC Riverside (Environmental Sciences)
- **Advisors**: [[Yuk-Yung]] (primary PI, Caltech) + [[King-Fai-Li]] (co-supervisor, UCR)
- **Paper draft corresponding author**: [[Siteng-Fan-范思腾]] (LMD Paris, former Yuk Yung postdoc)
- **Location**: Remote (Zhenyu at PKU; Caltech / UCR teamwork remote)
- **Project entry**: via [[Li-Chong-李充]] (PKU older labmate, Yuk Yung co-author on the Li C 2020 RS paper)

### Core Problem

DSCOVR single-point Earth lightcurve inverse problem — from Earth single-pixel reflectance time series observed by DSCOVR/EPIC at the Sun-Earth L1 Lagrange point, retrieve the land-ocean distribution map, serving as a "validation exoplanet" benchmark for future exoplanet characterization. Methodologically extends the traditional Rodgers retrieval with MCMC, and systematically studies regularization-parameter selection in ill-conditioned inverse problems ($A x = b$, condition number ~$10^6$, DSCOVR $W$ matrix Picard plot decays much faster than the Kawahara toy).

**Paper draft** (unpublished): *"An automatic pipeline for retrieval from DSCOVR data"*, co-authors co-authors (anonymized in public version), **Zhenyu He¹**, [[Siteng-Fan-范思腾]]\* (corresponding), King-Fai Li³, Yuk L. Yung⁴,⁵, Yongyun Hu¹ (multiple institutions). The 90-paragraph HBP mathematical section was authored primarily by Zhenyu.

---

### Zhenyu's 4 Original Contributions (per the proposal Example-6 4-original narrative)

#### Contribution (c): Hansen σ² vs σ⁴ textbook bug catch (2022-01-08, **80× deviation**)

**Core achievement**: as an undergraduate, using independent SVD + filter-factor derivation, Zhenyu identified a **formula-level bug** in Hansen's classic *Discrete Inverse Problems* (SIAM 2010), a foundational textbook — not a typo, but a substantive error that produces **~80× different numerical results**.

**Numerical comparison** (same toy model + PC2 data):

| Formula | Toy model λ | PC2 λ | Accuracy |
|---------|------------|-------|--------|
| **Hansen-student correct version (σ⁴)** | **0.0251** | **0.0575** | Consistent with naked-eye elbow + axis-image theoretical value |
| **Hansen-textbook erroneous version (σ²)** | **1.995** (fail) | **1.995** (fail) | **80× overestimate, complete failure** (λ pinned at upper bound, data-independent) |

**Innovative discovery** — independently identified an **L-curve axis-scale ambiguity** that Hansen did not discuss (found 2022-01-08):

> *"Hansen didn't talk about whether we should control the units of x-axis and y-axis of L-curve to be the same. In his book, he showed two L-curve figures, but both didn't control the units to be the same."*

**3-step self-correction cycle** (11/29 → 12/06 → 01/08, the entire trajectory preserved):
1. **11/29** discovered own formula was wrong (group-meeting slide 4)
2. **12/06** hypothesized "accumulation of errors" — wrong attribution (slide 6)
3. **01/08** refuted that hypothesis, **correctly attributed to axis-scale ambiguity** — slides 7-10 verbatim: *"What if our naked eyes are wrong, but the calculated curvature is right?"* (5-cell hand-computation demo; after MATLAB `axis image` forces equal units, the curvature elbow at $x=-1.337$ truly aligns)

**Physical-evidence discipline**: the `LCurve_HansenMistake_WeRectify_Test/` directory simultaneously preserves
- `Hansen自己文章_仍然mu二次方.pdf` (Hansen's own version, denominator σ²) (filename gloss: "Hansen own paper still mu squared.pdf")
- `hansen学生mu四次方.pdf` (Hansen-student correct version, denominator σ⁴) (filename gloss: "hansen student mu fourth power.pdf")

Recorded side-by-side as reproducible numerical-science best practice — see Evidence Preservation Discipline (private companion).

**Independent mathematical verification**: `Deductions of the curvature of log-log Lcurve.docx`, a 36-paragraph symbolic derivation from SVD $A = U\Sigma V^T$ + filter factors $f_i = \sigma_i^2 / (\sigma_i^2 + \lambda^2)$ to the second derivatives of $\ln|x_\lambda|$ and $\ln|Ax_\lambda - b|$ with respect to $\mu = \ln\lambda$; key step: "**The denominator should have σ_i^4 instead of σ_i^2**".

**Community contribution (3 open questions)**: (1) Should L-curve axes be controlled to equal units? (2) Is Siteng's elbow λ=1e-3 result a scale artifact? (3) When applying L-curve, under what conditions should one tune, and how?

See the [[L-Curve-Axis-Scale-Ambiguity]] concept page.

---

#### Contribution (b): Pre-whitening L-curve innovation + refusing methodological-engineering pressure (2022-01-23)

**Technical innovation**: under an RBF kernel (non-diagonal prior covariance $S_a$), transform to whitened space:

$$x_1 = S_a^{-1/2}x, \quad y_1 = S_e^{-1/2}y, \quad A_1 = S_e^{-1/2}A S_a^{1/2}$$

In the whitened space, plot $\ln|x_1|$ vs $\ln|y_1 - A_1 x_1|$ → "modified L-curve".

**Problem diagnosis**: discovered that under non-diagonal $S_a$, the L-curve's x/y values do not vary monotonically → structural limit: the L-curve corresponds to pure Tikhonov, and a non-diagonal $S_a$ cannot be reduced to Tikhonov form; the "modified L-curve" results are oversensitive to the $S_a, S_e$ priors — how well you know the priors directly influences the result.

**Independent judgment — 2022-01-23 group-meeting verbatim (refusing methodological-engineering pressure)**:


Held to the methodology rather than tuning $S_a$, $S_e$ priors to engineer a target λ.

**Significance**: a 21-year-old undergraduate **refused on the spot** the  self-discipline call (declined to engineer a target λ) — no opportunism; honest admission that "the method I myself proposed only works under Tikhonov-equivalent covariance". **"I diagnose my own method's limitation"** is a rare discipline of methodology maturity.

Corresponds to Moment 3 of Independent Judgment narrative (held until 2026-06-10).

---

#### Contribution (a): 90-paragraph mathematical exposition of the Hardened Balancing Principle (HBP)

**Theoretical framework**: starting from Bauer 2007 Definition 5.1's $\psi^+ = 1$ (Tikhonov), derive:
- minimum-difference regularization parameter: $n^+ = \min\{n \in [0,N] : D(n,k) > D(n-1,k) \text{ for some } k\}$
- balancing functional $b(n,m) = \|x_n - x_m\| / [\Phi(N,m) - \Phi(N,n)]$
- exponential concentration → HBP `λ_{n+}` automatic parameter selection

**Systematic stress test** (4 benchmarks):

| Benchmark | Condition number / data | HBP performance |
|-----------|-------------|---------|
| Hansen gravity problem (500-instance) | ~2.88e28 vs Hansen-textbook reported ~1.54e5 | Robust |
| Golub 1979 Laplace | 2.88e28 (more ill-conditioned than Golub's original 1.54e5) | Robust |
| 3-point linear regression | Cross-validated against King-Fai Li's Bayesian closed-form | α=9.57, σ=0.023, λ analytical vs MCMC differ by 18% (OK) |
| DSCOVR real PC2 time series | The W where Kawahara Bayesian cost fails | Converges to a range close to Siteng λ≈1e-3 |

**Conclusion**: HBP requires no prior knowledge of noise level δ or tuning constant κ (BP needs both); most robust across benchmarks.

**Output**: the **90-paragraph mathematical-section writeup** in `internal-only manuscript` — full derivation from Tikhonov to HBP, equivalent in scope to an independent technical note / tutorial.

**Downstream impact**: HBP was extended by co-author a subsequent collaborator to PC1 (low clouds) / PC4 (high clouds) retrievals (different from Zhenyu's PC2 = land/ocean) — methodological influence reaches the collaborator's work.

See the [[Hardened-Balancing-Principle]] concept page.

---

#### Contribution (d): Direction of Noise Vector discovery (2021-09-20)

**Original finding (2021-09-20 verbatim)**:

> *"When I did numerical tests on L-Curve, GCV etc., **I found out the direction of the noise vector plays a big role** in the performance of statistical criteria. **I did a literature search and it seems nobody has studied this topic.**"*

**Geometric decomposition**: in the column space of $A = [A_1, A_2]$, with $d = A x_{sol}$, decompose noise $dd$ into perpendicular + parallel; after decomposing the parallel component along eigenvectors, the **EV2-direction component is amplified**.

**4-method failure-mode catalog**:

| Method | Failure condition |
|--------|---------|
| L-curve | $\|x_{sol}\|$ large, or $dd$ near EV1 |
| Kawahara Bayesian | $\|x_{sol}\|$ large (5/5 fail for $x_{sol}=[10,1]$, negative component) |
| GCV | $d$ near EV1 and $dd$ near EV2 (long flat cost region) |
| Discrepancy principle | Always works, but introduces systematic error (underestimates $\|x\|$) |

**Source: incidental discovery → systematic discovery**: when reproducing the Golub 1979 GCV paper (Zhenyu's condition 2.88e28, more ill-conditioned than the paper's 1.54e5), the 4th of 5 instances yielded a λ_GCV completely different from the other 4 → the Hansen gravity 500-instance independently rediscovered the same → two independent pieces of evidence converged → systematized as Contribution (d). **Literature search confirmed the literature gap ("nobody has studied")** — signature of independent problem-formulation ability.

See [[Multi-Method-Comparison-Spine]].

---

### Key Achievements

1. **Hansen textbook bug catch (80× overestimate, formula-level error in a foundational classic)** — undergraduate finds a formula bug in a SIAM 2010 classic + side-by-side inconvenient-evidence retention
2. **Pre-whitening L-curve innovation + 2022-01-23 refuse-methodological-engineering pressure verbatim** — research-integrity signature
3. **HBP 90-paragraph mathematical exposition + 4-benchmark stress test + subsequent collaborator's PC1/PC4 extension** — methodology-influence chain
4. **Independent discovery of the Direction-of-Noise-Vector + literature-gap awareness** — problem-formulation originality
5. **Cross-language fluency**: within a single 11-month project, **5 programming languages**:

| Language | Role |
|----------|---------|
| **IDL** | OOP MCMC class (inheriting Yuk Yung lab convention; learned scripts from Jing Li's PKU group) |
| **MATLAB** | Hansen gravity replication + csvd + 5 nested `LCurve_HansenMistake_WeRectify_Test` subdirectories |
| **Python** | Kawahara CUDA library bootstrap (remote workstation) + emcee + healpy + scipy |
| **Mathematica** | Symbolic-curvature derivation (`calculation_4_cal_deriva.nb` + `calculation_5_cal_deriva.nb`) |
| **R** | Metropolis-Hastings baseline for cross-validation |

6. **29 group_meeting pptx** sustained trajectory (Mar 2021 → Mar 2022, ~1 PPT / 2 weeks) — undergraduate, ~12 months, single project, 29 formal group-meeting reports
7. **Self-study rigor**: full reproduction of three classics — Hansen *Discrete Inverse Problems* (SIAM 2010) + Bishop PRML + Golub 1979 original GCV paper, with numerical experiments replicated one by one

---

### Technical Depth (resume-grade specifics)

- **Self-study, full reproduction of 3 textbooks**: Hansen *Discrete Inverse Problems* + Bishop PRML + Golub 1979 GCV paper — not just reading, but replicating Fig 5.9 gravity 500-instance histogram + Laplace condition 2.88e28 stress test + Ch 5.6 shaw test problem, obtaining histograms that nearly overlap with the originals
- **~3,000+ lines of code + study notes** on the [[MCMC-Mapping-GitHub]] repo (parallel to the 4 Caltech contributions; pre-finalization commit 2021-09-13; subsequent research-wiki files no longer in this repo but conceptually unified)
- **remote workstation bootstrap**: Caltech Anaconda + CUDA 11.2 + Kawahara library (CUDA library not supported under Windows → Zhenyu manually diagnosed + driver setup); 2021-08-09 group meeting "Finished Setting up Environments for Running codes on (remote workstation)" — non-trivial devops skill
- **5 nested stress-test subdirectories** (`LCurve_HansenMistake_WeRectify_Test/`): test 1 Hansen formula failed at upper bound on toy / test 2 student formula success on toy / test 3 PC2 / test 4 Sa, Se whitening with own estimate / test 5 Sa, Se whitening with Kawahara posterior — each directory contains Hansen original + student-correct L-curve + curvature-vs-λ figure for visual diff
- **Mathematica symbolic ↔ MCMC cross-validation**: 3-point regression closed-form (α=9.57, σ=0.023, λ=5.73e-5) vs MCMC (λ=6.76e-5) differ by 18% — double-check discipline
- **5×4 failure-mode matrix** (5 $x_{sol}$ geometries × 4 regularization methods): [1,1] / [3,1] / [5,1] / [7,1] / [10,1] — for each case, give the best λ + retrieved x for L-curve / Kawahara / GCV / Discrepancy, structurally identifying the geometric condition under which each method fails — not "4 methods in parallel" but "4 methods' capability diagnosis under 5 geometries"

---

### Academic / Career Significance

- **Moment 4 (Caltech → Berkeley cross-paradigm switch, Aug 2022)**: gave up 11 months of IDL / MATLAB / Python / Mathematica / R tooling + 4 original-contribution momentum, switched paradigm to David Romps DAM LES Fortran (single-point remote sensing → 3-D LES moist convection);  External factor is a key external factor, but the core is Zhenyu's **proactive** choice to switch application direction (exoplanet habitability → nuclear-winter policy) — see Independent Judgment narrative (held until 2026-06-10) Moment 4
- **Moment 3 (methodological restraint, 2022-01-23)**: when DSCOVR pre-whitening verification failed, the undergraduate refused the self-discipline call on the spot — see Independent Judgment narrative (held until 2026-06-10) Moment 3
- **3-track parallel Sep-Dec 2021 senior fall**: Caltech DSCOVR HBP maturation + Walker paper v3→v6 drafting (see [[PKU-Walker-Circulation-Research]]) + PKU Aerosol thesis drafting (see [[PKU-Aerosol-Senior-Thesis]]) + nwp_hw 4 assignments ≈ 3-4 deliverable/week sustained intensity

---

### Skills Used
- [[MCMC-贝叶斯反演]] (Round 3 update adding the Caltech 4 contributions)
- [[反问题与正则化]] (Hansen bug catch + pre-whitening; concept scaffold)
- [[GP-贝叶斯反演]] (Kawahara SOT method)
- [[Python-科学计算]]
- [[高性能计算-HPC]] ((remote workstation) CUDA bootstrap)

---

### Related Pages
- [[PKU-Undergraduate-Research]] (umbrella page)
- [[Yuk-Yung]] (Caltech primary PI)
- [[King-Fai-Li]] (UCR co-supervisor)
- [[Siteng-Fan-范思腾]] (LMD Paris, paper-draft corresponding author)
- [[Li-Chong-李充]] (Caltech bridge via Li C 2020 RS paper)
- [[Hardened-Balancing-Principle]] (contribution a)
- [[L-Curve-Axis-Scale-Ambiguity]] (contribution c)
- Evidence Preservation Discipline (private companion) (Hansen PDFs preserved side by side)
- [[Multi-Method-Comparison-Spine]] (4-method, 5-geometry failure-mode matrix)
- Independent Judgment narrative (held until 2026-06-10) (Moments 3 + 4)
- [[PKU-Walker-Circulation-Research]] (3-track parallel Sep-Dec 2021)
- [[PKU-Aerosol-Senior-Thesis]]
- [[MCMC-Mapping-GitHub]]
- [[反问题与正则化]]
- [[GP-贝叶斯反演]]

### Sources
- `research_wiki/projects/mcmc_retrieval/overview.md` (~35k words, full 1329 lines)
- `research_wiki/resume_angles/problem_solving.md` §Project 3 DSCOVR
- `research_wiki/resume_angles/independent_judgment.md` §Moments 3 + 4
- `raw/Caltech_task/` 1.5 GB folder (1,364 files / 126 dirs, 29 group_meeting pptx + `internal-only manuscript` + 10 technical docx + `LCurve_HansenMistake_WeRectify_Test/` subdirectories)
