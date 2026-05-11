---
title: "Multi-Method Comparison Spine (2019-2025)"
description: "Zhenyu 跨 7 年至少 8 instances 的 systematic multi-method comparison methodology backbone"
publish: true
lang: bilingual
---

# Multi-Method Comparison Spine (2019-2025)

## 中文版

### 页面用途

本页 articulate Zhenyu 跨 7 年至少 8 个 instances 的 **systematic multi-method comparison** pattern — 而非 single-method + 事后 sanity check 的 ad-hoc pattern. 这条 spine 是 cross-project methodology backbone, 从 2019 年 11 月大二 first long report (earliest evidence) 到 2025 ongoing methane regressions, 在完全独立的 domain (climate dynamics / quantitative finance / inverse problem theory / aerosol retrieval / spectral methods) 都 consistently 出现.

### 定义

**Multi-method comparison** = **对同一 scientific question, 从一开始就 set up ≥ 2 个 independent methods 并列执行 + 全部 preserve result, 不是 "1 method + 事后 sanity check" 的 ad-hoc pattern**. 关键 distinguishing features:

1. **Methods 独立** (不共享 core assumption 或 subroutine)
2. **并列执行** (不是 fallback from failed method)
3. **所有结果 preserved** (即使某方法 disadvantageous to narrative)
4. **Cross-validate 作为 discovery mechanism** (不仅是 robustness check)

### 跨 7 年 ≥ 8 instances 总表

| Year | Context | Methods compared | Outcome |
|------|---------|-----------------|---------|
| **2019-11-04** | PKU Zhenyu 大二 first long report 43 slides `the impact on the strength of tropical circulations 2.pptx` | **3 Walker strength 度量方式** (Tanaka 2004 velocity potential + ω-based + u-based / equivalent) | Earliest multi-method evidence — capability spine 起源 |
| **2020-2021** | Walker paper v6 (PKU Ji Nie) | **ω-based vs u-based stream function** (`msf_top2bottom_omega2_WalkerStream.ncl` 63 lines + `msf_top2bottom_u2_Walker.ncl` 61 lines) 两 NCL module 并列 preserved | Methodology bug catch: ω-based 对"无散"条件满足不好 → switch to u-based for paper v6, 但 ω-based module 保留作为 failed approach evidence |
| **Summer 2021** | QLBS self-study + NSD Summer School Final Project (joint course project) | **DP backward Bellman + FQI off-policy RL ($\eta=0.5$) + Black-Scholes closed-form benchmark** — 3 solutions in single 780-line notebook + 1606-line Coursera independent path | 780 lines of independent verification — earliest numerical multi-method instance, Summer 2021 (比 Caltech 早 3 月, 比 PhD 早 4 年) |
| **2021-11** | Caltech DSCOVR (Yuk Yung + King-Fai Li) | **Pre-whitening L-curve + L-curve + GCV + Morozov + Hardened Balancing Principle + Tikhonov + TSVD + Kawahara Bayesian cost + discrepancy principle** (7+ methods) | Structural limits diagnosed: Hansen σ² vs σ⁴ bug (80×) + Method B/C failure + axis-scale ambiguity + non-diagonal $S_a$ self-limit |
| **2022-01** | Phase 1 T,q vs h,q closure (PhD Nuclear Winter) | **h-based RK4 + h-based forward Euler + T,q separate integrate + h_adj + T,q + cp_adj** (4 Method variants) + **conserved potential temperature 3rd-party ground truth** | Root cause isolation (85 J/kg → 3 J/kg → 3.58e-5 J/kg), diagnosed hydrostatic balance violation as mechanism |
| **2022-02** | Aerosol joint retrieval (PKU 李婧 senior thesis) | **Log scale height regression vs 1/e decay method** — 两种 scale height 推算方法 + 系统 comparison across 12-month China LUT | Convention harmonization: log-linear full-profile regression chosen as primary method, 1/e preserved; test case 2019-08-01 Beijing (0.66 km vs 4.1 km) based on physical sanity check |
| **2025-09** | Phase 4.5 SWTG (PhD Nuclear Winter) | **Spectral modes (Sturm-Liouville eigendecomposition)** vs **DAM 3-D LES ground truth** + sanity-check experiments isolating mode evolution | 1-D model 显著高估高度诊断: "failed cancellation" mechanism identified through multi-experiment comparison |
| **Ongoing (2024-)** | Methane mapping (UC Berkeley Inez Fung Lab) | **Multiple regression types**: quantile (upper 50% filter) + density (AvgHeadPer100Acres) + raw linear (MillionHeads) | Texas puzzle reformulation — recover positive slope in Nebraska/Idaho after density + quantile; raw linear preserved to show original negative slope artifact |

### Meta pattern (what makes this distinct from ad-hoc sanity check)

**Characteristic 1: Upfront design, 不是 fallback**
- 每 instance 的 methods **从一开始就是 parallel design**, 不是 "method A 失败了 → 试 method B"
- Evidence: QLBS single notebook 同时实现 3 solutions; Phase 1 4 method variants 并列从项目第一 phase 就存在

**Characteristic 2: Independent methods (不 share core assumption)**
- DP + FQI + BS closed-form: 完全不同 mathematical framework (backward recursion / off-policy RL / analytical stochastic calculus)
- ω-based vs u-based stream function: 不同 momentum variable + 不同 integration path
- Phase 1: h-based vs T,q-based 是不同 state-variable choice

**Characteristic 3: All results preserved, even disadvantageous**
- Walker v6 preserve ω-based NCL module 即使 methodology bug caught
- Caltech preserve Hansen 原版 (σ²) 错误 PDF 并列 Hansen 学生正确版 (σ⁴) PDF
- Phase 1+2 `enforceEpsilon_z_iteration_v3.ipynb` filename-as-failure-marker
- Aerosol (supplementary inconvenient-evidence docx) preserve CALIPSO L2 4/4 优势

**Characteristic 4: Cross-validate as discovery mechanism, 不只是 robustness**
- Caltech 7+ method comparison → Hansen textbook bug catch (80× overestimation)
- Phase 1 T,q vs h,q comparison → hydrostatic balance violation mechanism identified
- Methane density vs raw count → Texas free-range grazing hypothesis (Inez's contribution)

### 与其他 cross-project patterns 的关系

#### 与 Evidence Preservation Discipline (private companion) 的关系

- Multi-method comparison 生成 inconvenient evidence 的 "source pool" (1 method "wins", others 是 "losers" or "fails") — Characteristic 3 与 inconvenient evidence 的 preservation discipline 直接 overlap
- 但 multi-method comparison focus 是 **design-time upfront parallelism**; inconvenient-evidence retention focus 是 **result-time honest retention**. 两个 pattern 是 complementary (前者 upstream, 后者 downstream)

#### 与 PKU advisor methodology companion (private) 的关系

- 两者 都是 **methodology integrity** 层面的 capability. methodology arc 是 advisor-level (credit honesty), multi-method spine 是 student-level (methodology honesty) — 两个 independent 证据 in same integrity cluster

#### 与 Independent Judgment narrative (held until 2026-06-10) 的关系

- Moment 3 (2022-01-23 refuse methodological-engineering pressure) 直接 rooted in multi-method comparison Characteristic 4: pre-whitening L-curve method 在 RBF kernel 下 showed non-monotonic behavior → Zhenyu articulate method self-limit, refuse tune 多 Sa/Se bundles. **Multi-method discipline 使 Zhenyu able to diagnose method-level limit, 进而 refuse methodological-engineering pressure at methodology-integrity level**.

### Distinct signature: 大二 earliest evidence

**Critical observation**: capability spine 起源不是 PhD, 不是 Caltech, 也不是 senior thesis — **是大二 first long report (2019-11-04)**. 这意味着:

- **多 method comparison 不是 研究 training 的 learned skill**, 而是 Zhenyu **personal epistemic habit** — 从 entering 领域之初就存在
- 与 PhD-level multi-method training (通常 1-2 年 literature exposure 后 develop) 的 timeline 完全不 match
- 可以解释为什么 PhD 阶段 Caltech DSCOVR 7-method comparison 在本科 senior fall 就 emerge — 不是 "突然学会" 而是 "capability 已存在, domain 准备好才 fully expressed"



### 来源

- research_wiki `resume_angles/problem_solving.md` 整页 (350+ 行, 所有 multi-method stories 完整 documented)
- research_wiki `resume_angles/technical_depth.md` §1 Numerical Methods (7+ regularization methods + QLBS 3-way + Phase 1 4-method variants)
- research_wiki `projects/walker_hadley/overview.md` §ω-based vs u-based 流函数 + 大二 2019-11-04 first long report
- research_wiki `projects/mcmc_retrieval/overview.md` §Caltech DSCOVR 7-method systematic comparison
- research_wiki `projects/aerosol_retrieval/overview.md` §log 拟合 vs 1/e 法 scale height
- research_wiki `projects/nuclear_winter/overview.md` §Phase 1 T,q vs h,q + Phase 4.5 SWTG spectral modes
- research_wiki `projects/methane_mapping/overview.md` §regression reformulation (density + quantile)
- research_wiki `projects/early_exploration/overview.md` §2019-11-04 first long report 43 slides

### 相关页面

- Evidence Preservation Discipline (private companion) — downstream honesty discipline (companion concept)
- PKU advisor methodology companion (private) — methodology integrity companion
- Independent Judgment narrative (held until 2026-06-10) — Moment 3 refuse methodological-engineering pressure 直接 rooted in multi-method spine
- [[PKU-Walker-Circulation-Research]] — ω-vs-u 流函数 module preserved
- [[Caltech-DSCOVR-Research]] — 7+ regularization method comparison
- [[PKU-Aerosol-Senior-Thesis]] — log vs 1/e scale height
- [[L-Curve-Axis-Scale-Ambiguity]] — Caltech multi-method outcome (axis-scale diagnosis)
- [[Linear-Superposition-Framework]] — Walker 4-field validation cross-method
- [[反问题与正则化]] — technical methodology reference
- [[profile]]

---

## English Version

### Page Purpose

This page articulates Zhenyu's pattern of **systematic multi-method comparison** across at least 8 instances over 7 years — rather than the ad-hoc pattern of "single-method + post-hoc sanity check". This spine is the cross-project methodology backbone, from sophomore first long report in November 2019 (earliest evidence) to ongoing 2025 methane regressions, consistently appearing across completely independent domains (climate dynamics / quantitative finance / inverse problem theory / aerosol retrieval / spectral methods).

### Definition

**Multi-method comparison** = **for the same scientific question, set up ≥ 2 independent methods in parallel from the start + preserve all results, not the "1 method + post-hoc sanity check" ad-hoc pattern**. Key distinguishing features:

1. **Methods are independent** (not sharing core assumptions or subroutines)
2. **Parallel execution** (not a fallback from a failed method)
3. **All results preserved** (even if some methods are disadvantageous to the narrative)
4. **Cross-validation as discovery mechanism** (not just robustness check)

### Cross-7-year ≥ 8 instances overview table

| Year | Context | Methods compared | Outcome |
|------|---------|-----------------|---------|
| **2019-11-04** | PKU Zhenyu sophomore first long report 43 slides `the impact on the strength of tropical circulations 2.pptx` | **3 Walker strength metrics** (Tanaka 2004 velocity potential + ω-based + u-based / equivalent) | Earliest multi-method evidence — origin of the capability spine |
| **2020-2021** | Walker paper v6 (PKU Ji Nie) | **ω-based vs u-based stream function** (`msf_top2bottom_omega2_WalkerStream.ncl` 63 lines + `msf_top2bottom_u2_Walker.ncl` 61 lines) two NCL modules preserved in parallel | Methodology bug catch: ω-based does not satisfy "non-divergence" condition well → switch to u-based for paper v6, but ω-based module preserved as failed-approach evidence |
| **Summer 2021** | QLBS self-study + NSD Summer School Final Project (joint course project) | **DP backward Bellman + FQI off-policy RL ($\eta=0.5$) + Black-Scholes closed-form benchmark** — 3 solutions in single 780-line notebook + 1606-line Coursera independent path | 780 lines of independent verification — earliest numerical multi-method instance, Summer 2021 (3 months earlier than Caltech, 4 years earlier than PhD) |
| **2021-11** | Caltech DSCOVR (Yuk Yung + King-Fai Li) | **Pre-whitening L-curve + L-curve + GCV + Morozov + Hardened Balancing Principle + Tikhonov + TSVD + Kawahara Bayesian cost + discrepancy principle** (7+ methods) | Structural limits diagnosed: Hansen σ² vs σ⁴ bug (80×) + Method B/C failure + axis-scale ambiguity + non-diagonal $S_a$ self-limit |
| **2022-01** | Phase 1 T,q vs h,q closure (PhD Nuclear Winter) | **h-based RK4 + h-based forward Euler + T,q separate integrate + h_adj + T,q + cp_adj** (4 Method variants) + **conserved potential temperature 3rd-party ground truth** | Root cause isolation (85 J/kg → 3 J/kg → 3.58e-5 J/kg), diagnosed hydrostatic balance violation as mechanism |
| **2022-02** | Aerosol joint retrieval (PKU Jing Li senior thesis) | **Log scale height regression vs 1/e decay method** — two scale height inference methods + systematic comparison across 12-month China LUT | Convention harmonization: log-linear full-profile regression chosen as primary method, 1/e preserved; test case 2019-08-01 Beijing (0.66 km vs 4.1 km) based on physical sanity check |
| **2025-09** | Phase 4.5 SWTG (PhD Nuclear Winter) | **Spectral modes (Sturm-Liouville eigendecomposition)** vs **DAM 3-D LES ground truth** + sanity-check experiments isolating mode evolution | 1-D model significantly overestimates height diagnostic: "failed cancellation" mechanism identified through multi-experiment comparison |
| **Ongoing (2024-)** | Methane mapping (UC Berkeley Inez Fung Lab) | **Multiple regression types**: quantile (upper 50% filter) + density (AvgHeadPer100Acres) + raw linear (MillionHeads) | Texas puzzle reformulation — recovered positive slope in Nebraska/Idaho after density + quantile; raw linear preserved to show original negative slope artifact |

### Meta pattern (what makes this distinct from ad-hoc sanity check)

**Characteristic 1: Upfront design, not fallback**
- Methods in each instance are **parallel by design from the beginning**, not "method A failed → try method B"
- Evidence: QLBS single notebook simultaneously implements 3 solutions; Phase 1 4 method variants existed in parallel from the project's first phase

**Characteristic 2: Independent methods (not sharing core assumptions)**
- DP + FQI + BS closed-form: completely different mathematical frameworks (backward recursion / off-policy RL / analytical stochastic calculus)
- ω-based vs u-based stream function: different momentum variable + different integration path
- Phase 1: h-based vs T,q-based are different state-variable choices

**Characteristic 3: All results preserved, even disadvantageous**
- Walker v6 preserves ω-based NCL module even though methodology bug was caught
- Caltech preserves Hansen original (σ²) wrong PDF side-by-side with Hansen student correct (σ⁴) PDF
- Phase 1+2 `enforceEpsilon_z_iteration_v3.ipynb` filename-as-failure-marker
- Aerosol (supplementary inconvenient-evidence docx) (filename gloss: "Hard-to-Explain or inconvenient evidence Section.docx") preserves CALIPSO L2 4/4 advantage

**Characteristic 4: Cross-validate as discovery mechanism, not just robustness**
- Caltech 7+ method comparison → Hansen textbook bug catch (80× overestimation)
- Phase 1 T,q vs h,q comparison → hydrostatic balance violation mechanism identified
- Methane density vs raw count → Texas free-range grazing hypothesis (Inez's contribution)

### Relationships to other cross-project patterns

#### Relation to Evidence Preservation Discipline (private companion)

- Multi-method comparison generates the "source pool" of inconvenient evidence (1 method "wins", others are "losers" or "fails") — Characteristic 3 directly overlaps with the inconvenient-evidence retention discipline
- However, multi-method comparison's focus is **design-time upfront parallelism**; inconvenient-evidence retention's focus is **result-time honest retention**. The two patterns are complementary (the former upstream, the latter downstream)

#### Relation to PKU advisor methodology companion (private)

- Both are capabilities at the **methodology integrity** layer. The methodology arc is advisor-level (credit honesty), the multi-method spine is student-level (methodology honesty) — two independent pieces of evidence in the same integrity cluster

#### Relation to Independent Judgment narrative (held until 2026-06-10)

- Moment 3 (2022-01-23 refuse methodological-engineering pressure) is directly rooted in multi-method comparison Characteristic 4: pre-whitening L-curve method showed non-monotonic behavior under RBF kernel → Zhenyu articulates method self-limit, refuses to tune multiple Sa/Se bundles. **Multi-method discipline enables Zhenyu to diagnose method-level limits and thus refuse methodological-engineering pressure at the methodology-integrity level**.

### Distinct signature: sophomore earliest evidence

**Critical observation**: the origin of the capability spine is not PhD, not Caltech, not the senior thesis — **it is the sophomore first long report (2019-11-04)**. This means:

- **Multi-method comparison is not a learned skill from research training** but is Zhenyu's **personal epistemic habit** — present from his entry into the field
- It does not match the timeline of PhD-level multi-method training (typically developed after 1-2 years of literature exposure)
- This explains why the Caltech DSCOVR 7-method comparison emerged in undergrad senior fall — not "suddenly learned" but "the capability already existed, fully expressed when the domain was ready"



### Sources

- research_wiki `resume_angles/problem_solving.md` whole page (350+ lines, all multi-method stories fully documented)
- research_wiki `resume_angles/technical_depth.md` §1 Numerical Methods (7+ regularization methods + QLBS 3-way + Phase 1 4-method variants)
- research_wiki `projects/walker_hadley/overview.md` §ω-based vs u-based stream function + sophomore 2019-11-04 first long report
- research_wiki `projects/mcmc_retrieval/overview.md` §Caltech DSCOVR 7-method systematic comparison
- research_wiki `projects/aerosol_retrieval/overview.md` §log fit vs 1/e method scale height
- research_wiki `projects/nuclear_winter/overview.md` §Phase 1 T,q vs h,q + Phase 4.5 SWTG spectral modes
- research_wiki `projects/methane_mapping/overview.md` §regression reformulation (density + quantile)
- research_wiki `projects/early_exploration/overview.md` §2019-11-04 first long report 43 slides

### Related Pages

- Evidence Preservation Discipline (private companion) — downstream honesty discipline (companion concept)
- PKU advisor methodology companion (private) — methodology integrity companion
- Independent Judgment narrative (held until 2026-06-10) — Moment 3 refuse methodological-engineering pressure directly rooted in multi-method spine
- [[PKU-Walker-Circulation-Research]] — ω-vs-u stream function module preserved
- [[Caltech-DSCOVR-Research]] — 7+ regularization method comparison
- [[PKU-Aerosol-Senior-Thesis]] — log vs 1/e scale height
- [[L-Curve-Axis-Scale-Ambiguity]] — Caltech multi-method outcome (axis-scale diagnosis)
- [[Linear-Superposition-Framework]] — Walker 4-field validation cross-method
- [[反问题与正则化]] — technical methodology reference
- [[profile]]
