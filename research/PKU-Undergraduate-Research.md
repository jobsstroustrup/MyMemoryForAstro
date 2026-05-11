---
title: "Undergraduate Research @ Peking University & Caltech/UCR"
publish: true
lang: bilingual
description: "Undergraduate research overview (2018-2022): 4 independent projects across 3 labs / 3 institutions"
---

# Undergraduate Research @ Peking University & Caltech/UCR

> **相关页面**: 本页只记录科研项目 (umbrella pointer page)。本科期间的 **班长 / 学生会 / 支教 / 爱心社 / 棒垒队** 等 leadership & service 经历见 [[PKU-Leadership-and-Service]]; **所有奖项荣誉** 见 [[Academic-Honors-PKU]]。

## 中文版

### 基本信息
- **时间**: 2018.09 — 2022.06 (本科 4 年)
- **角色**: 本科独立研究 (4 independent projects across 3 labs / 3 institutions)
- **组织**: 北京大学物理学院 (李婧 / 胡永云 / 聂绩 教授) + Caltech / UC Riverside (Yuk Yung / King-Fai Li)
- **地点**: 北京 / 远程
- **资助**: PKU President Fellowship + 本科生科研训练项目

### 4 Projects Overview (按时间顺序, 每个独立 page 见 pointer)

**1. Walker/Hadley Circulation Response Under Global Warming** (2019.10 — 2020.05, [[Ji-Nie-聂绩]])
→ 独立页面: [[PKU-Walker-Hadley-Response-Research]]
→ **TL;DR**: 本科大二秋季 first project, 计算不同 CO₂ level 下 Walker/Hadley 强度变化 + 贡献分解。2019-11-04 first long report 43 slides 已 demonstrate **3-method Walker strength 并列对比** (velocity potential / integral / precip+850hPa) — 是 Zhenyu multi-method comparison discipline 的 **earliest evidence** (比 PhD SWTG 早 6 年)。包含 Ji Nie 组 onboarding + 4-advisor evaluation selection ([four PKU faculty across quantitative-biology / optics / quantum-materials / climate]) + 2 个 reading club 跨 monsoon/BL/Walker/Hadley/ENSO ~30+ papers in 2 months + 2020-09 全员大组会 Walker metric (ω@500mb WEP-EEP diff) = Walker paper v6 §3.1 metric 完全 identical, 早 1 年 7 个月 already articulated。

**2. Walker Circulation Width Dependence** (2020.11 — 2021.10, [[Ji-Nie-聂绩]] + [[Yongyun-Hu-胡永云]])
→ 独立页面: [[PKU-Walker-Circulation-Research]]
→ **TL;DR**: 本科大三秋到大四秋 (12 months), CAM3 aqua-planet 10 cases × 30-yr runs (D60-D180 step 20° + Wonly/Conly/Aqua)。**2021-07-13 breakthrough** Zhenyu 自己提出 **Linear Superposition framework** + Ji Nie 当场 endorsement (4-field corr 0.83-0.93 validation); paper draft v6 (3663 words, 11 refs, 2021-10-22) **未投稿** (Ji Nie 当时 private context (held until 2026-06-10))。27,882 MATLAB+NCL lines + 20 NCAR CAM3 .F90 source mods (含 `somoce` MLDANN 50→30m key dep) + Tianhe-II (undergraduate Tianhe-II account) 48-PE 并行 + 5-stage HPC pipeline。

**3. MCMC Retrieval Methods** (2021.03 — 2022.03, [[Yuk-Yung]] + [[King-Fai-Li]], Caltech / UCR 远程)
→ 独立页面: [[Caltech-DSCOVR-Research]]
→ **TL;DR**: 本科大三春到大四春, DSCOVR 单点光曲线反演地球陆海分布。4 项原创贡献: (a) **Hansen σ² vs σ⁴ 80× bug catch** (Hansen 教材数值实现 bug); (b) **Pre-whitening L-curve** (L-Curve Curvature / GCV / Morozov 4 方法系统对比); (c) **Hardened Balancing Principle 90-paragraph writeup** (Sep 2021 被 Siteng Fan 点名); (d) **Direction of Noise Vector discovery** (Sep 2021 Zhenyu 自己发现的 ill-posed structure)。5 种 programming languages (IDL / MATLAB / Python / Mathematica / R) + 29 group_meeting pptx。自学 Hansen *Discrete Inverse Problems* + Bishop PRML + Golub 1979 GCV 原始论文并逐一复现数值实验。Repo: [[MCMC-Mapping-GitHub]]。

**4. MODIS+CALIPSO Joint Aerosol Retrieval (Senior Thesis)** (2021.12 — 2022.06, [[Jing-Li-李婧]])
→ 独立页面: [[PKU-Aerosol-Senior-Thesis]]
→ **TL;DR**: 本科大四春 senior thesis。**First iteratively-coupled MODIS+CALIPSO joint retrieval** (用 CALIPSO 反演 aerosol extinction 廓线替换 MODIS lookup table + MODIS AOD 作 CALIPSO 反演 boundary condition, 迭代直至收敛)。CALIPSO L2 **-10⁴ non-physical bug catch** + **4 Beijing case study** (abs ↓ 0.011-0.032, rel ↓ 3-20%) + **9-version thesis auto-diff** (316→1350 words in 27 days) + **4-person lab scaffolding** ([[Jing-Li-李婧]] + [[Chang-Liang-常亮]] + [[Li-Chong-李充]] + [[Dong-Yueming-董悦明]] + Caltech bridge)。

### Early Exploration Prequel Phase (2019.04 — 2019.10, 前 Ji Nie onboarding)

本科 research 并非从 2019.10 Ji Nie first project 启动就开始, 前面有 18 个月 prequel phase:
- **Phase 0.A**: 2019-03-17 物理学院本研分享会 (7 senior PPTs covering HEP / Quantum / Biology / ML / Galaxy / **Planetary Climate**) + 4-advisor candidate evaluation across quantitative-biology / optics / quantum-materials / climate, 最终 selected Ji Nie ([Moment 1 of Independent Judgment narrative — held until 2026-06-10])
- **Phase 0.B**: 2019 春期间撰写的关于本科生科研体制的 critical reflection note (private)，影响后续 advisor 选择 (selected 李婧 + 聂绩 都属于主动 deemphasize 自己 credit 的 minority)。


- **Phase 0.C-G**: 2 group reading club (BL 8 papers + monsoon 6 papers) + 首次 CAM5 aqua-planet 实验 (2020-04 → 2020-05, `data_summary_big_picture.pptx` 22 slides) + 2020-09 全员大组会 Walker/Hadley metric establish (Walker paper v6 metric 早 1 年 7 个月 source-of-truth) + 2020-09-27 Zhenyu first appearance in Hu group (28 slides)

### 使用的技能
- [[Python-科学计算]]
- [[气候物理与大气科学]]
- [[卫星遥感与数据处理]]
- [[MCMC-贝叶斯反演]]
- [[数值模式源代码修改]] (Walker 20 NCAR CAM3 .F90 mods, aggregate)
- [[高性能计算-HPC]] (Tianhe-II (undergraduate Tianhe-II account) → (undergraduate Tianhe-II account) → (undergraduate Tianhe-II account) 跨 3 个 lab account)

### 相关页面
- [[PKU-Walker-Hadley-Response-Research]] — Project 1 独立 page
- [[PKU-Walker-Circulation-Research]] — Project 2 独立 page
- [[Caltech-DSCOVR-Research]] — Project 3 独立 page
- [[PKU-Aerosol-Senior-Thesis]] — Project 4 独立 page
- [[PKU-Leadership-and-Service]] — 非科研 leadership/service experiences
- [[Academic-Honors-PKU]] — 本科奖项荣誉
- [[Ji-Nie-聂绩]] + [[Yongyun-Hu-胡永云]] + [[Jing-Li-李婧]] + [[Yuk-Yung]] + [[King-Fai-Li]] — 本科 advisors
- Independent Judgment narrative (held until 2026-06-10) — Moment 1 + 2 (4-advisor + 18 岁 critical reflection)
- PKU advisor methodology companion (private) — 李婧 + 聂绩 advisor methodology (private) narrative spine
- [[Multi-Method-Comparison-Spine]] — 3-method Walker strength 并列对比 root evidence (2019-11-04)
- 2019 critical reflection note (private) — 大二春季 critical reflection source

---

## English Version

> **Related pages**: This page only indexes research projects (umbrella pointer page). For **class monitor / student union / teaching support / love society / softball team** leadership & service, see [[PKU-Leadership-and-Service]]; for **all awards and honors**, see [[Academic-Honors-PKU]].

### Basic Info
- **Period**: Sep 2018 — Jun 2022 (4 years undergraduate)
- **Role**: Undergraduate Independent Researcher (4 independent projects across 3 labs / 3 institutions)
- **Organizations**: Peking University (Prof. Jing Li, Prof. Yongyun Hu, Prof. Ji Nie) + Caltech / UC Riverside (Prof. Yuk Yung / Prof. King-Fai Li)
- **Location**: Beijing / Remote
- **Support**: PKU President Fellowship + undergraduate research training program

### 4 Projects Overview (Chronological — see dedicated pages via pointers)

**1. Walker/Hadley Circulation Response Under Global Warming** (Oct 2019 — May 2020, [[Ji-Nie-聂绩]])
→ Dedicated page: [[PKU-Walker-Hadley-Response-Research]]
→ **TL;DR**: Sophomore-autumn first project under Ji Nie. Quantified Walker/Hadley intensity changes under different CO₂ levels and decomposed contributions to total tropical mass flux. 2019-11-04 first long report (43 slides) already demonstrated **3-method comparison on Walker strength** (velocity potential / integral / precip+850hPa wind) — **earliest evidence** of Zhenyu's multi-method comparison discipline (6 years before PhD SWTG "failed cancellation"). Includes Ji Nie lab onboarding + 4-advisor candidate evaluation + 2 reading clubs (~30+ papers across monsoon/BL/Walker/Hadley/ENSO in 2 months) + 2020-09 lab-wide meeting establishing Walker metric (ω@500mb WEP-EEP diff) identical to Walker paper v6 §3.1 — 1 year 7 months ahead.

**2. Walker Circulation Width Dependence** (Nov 2020 — Oct 2021, [[Ji-Nie-聂绩]] + [[Yongyun-Hu-胡永云]])
→ Dedicated page: [[PKU-Walker-Circulation-Research]]
→ **TL;DR**: Junior-autumn through senior-autumn (12 months). CAM3 aqua-planet 10 cases × 30-yr runs (D60-D180 step 20° + Wonly/Conly/Aqua). **2021-07-13 breakthrough**: Zhenyu proposed the **Linear Superposition framework**, endorsed on-the-spot by Ji Nie (4-field correlations 0.83-0.93). Paper draft v6 (3663 words, 11 refs, 2021-10-22) **not submitted** due to Ji Nie's private context (held until 2026-06-10). 27,882 MATLAB+NCL lines + 20 NCAR CAM3 .F90 source mods (including `somoce` MLDANN 50→30m key dep) + Tianhe-II (undergraduate Tianhe-II account) 48-PE parallel + 5-stage HPC pipeline.

**3. MCMC Retrieval Methods** (Mar 2021 — Mar 2022, [[Yuk-Yung]] + [[King-Fai-Li]], Caltech / UCR remote)
→ Dedicated page: [[Caltech-DSCOVR-Research]]
→ **TL;DR**: Junior-spring through senior-spring. Attempted to retrieve Earth's land-ocean distribution from DSCOVR single-point light curve. 4 original contributions: (a) **Hansen σ² vs σ⁴ 80× bug catch** (numerical-implementation bug in Hansen's textbook); (b) **Pre-whitening L-curve** (systematic comparison of L-Curve / L-Curve Curvature / GCV / Morozov discrepancy); (c) **Hardened Balancing Principle 90-paragraph writeup** (recognized by Siteng Fan, Sep 2021); (d) **Direction of Noise Vector discovery** (Zhenyu's own discovery of ill-posed structure, Sep 2021). 5 programming languages (IDL / MATLAB / Python / Mathematica / R) + 29 group_meeting pptx. Self-studied Hansen *Discrete Inverse Problems* + Bishop PRML + Golub 1979 original GCV paper, reproducing each numerical experiment. Repo: [[MCMC-Mapping-GitHub]].

**4. MODIS+CALIPSO Joint Aerosol Retrieval (Senior Thesis)** (Dec 2021 — Jun 2022, [[Jing-Li-李婧]])
→ Dedicated page: [[PKU-Aerosol-Senior-Thesis]]
→ **TL;DR**: Senior-spring senior thesis. **First iteratively-coupled MODIS+CALIPSO joint retrieval** (replaced MODIS lookup tables with CALIPSO-retrieved aerosol extinction profiles + added MODIS AOD as boundary condition for CALIPSO, iterating until convergence). **CALIPSO L2 -10⁴ non-physical bug catch** + **4 Beijing case studies** (absolute ↓ 0.011-0.032, relative ↓ 3-20%) + **9-version thesis auto-diff** (316→1350 words in 27 days) + **4-person lab scaffolding** ([[Jing-Li-李婧]] + [[Chang-Liang-常亮]] + [[Li-Chong-李充]] + [[Dong-Yueming-董悦明]] + Caltech bridge).

### Early Exploration Prequel Phase (Apr 2019 — Oct 2019, pre-Ji Nie onboarding)

Undergraduate research did not start when the Ji Nie first project launched in Oct 2019; an 18-month prequel came before:
- **Phase 0.A**: 2019-03-17 Physics Dept. undergraduate research sharing event (7 senior talks covering HEP / Quantum / Biology / ML / Galaxy / **Planetary Climate**) + 4-advisor candidate evaluation across quantitative-biology / optics / quantum-materials / climate; ultimately selected Ji Nie ([Moment 1 of Independent Judgment narrative — held until 2026-06-10])
- **Phase 0.B**: Spring 2019 — drafted a private critical reflection note on undergraduate research, which informed subsequent advisor selection (Li Jing + Ji Nie chosen partly because they belong to the minority who proactively deemphasize their own credit).


- **Phase 0.C-G**: 2 group reading clubs (BL 8 papers + monsoon 6 papers) + first CAM5 aqua-planet experiment (Apr-May 2020, `data_summary_big_picture.pptx` 22 slides) + 2020-09 lab-wide meeting establishing Walker/Hadley metric (Walker paper v6 metric source-of-truth 1 year 7 months ahead) + 2020-09-27 Zhenyu's first appearance in Hu group (28 slides)

### Skills Used
- [[Python-科学计算]]
- [[气候物理与大气科学]]
- [[卫星遥感与数据处理]]
- [[MCMC-贝叶斯反演]]
- [[数值模式源代码修改]] (Walker 20 NCAR CAM3 .F90 mods, aggregate)
- [[高性能计算-HPC]] (Tianhe-II (undergraduate Tianhe-II account) → (undergraduate Tianhe-II account) → (undergraduate Tianhe-II account) across 3 lab accounts)

### Related Pages
- [[PKU-Walker-Hadley-Response-Research]] — Project 1 dedicated page
- [[PKU-Walker-Circulation-Research]] — Project 2 dedicated page
- [[Caltech-DSCOVR-Research]] — Project 3 dedicated page
- [[PKU-Aerosol-Senior-Thesis]] — Project 4 dedicated page
- [[PKU-Leadership-and-Service]] — non-research leadership/service experiences
- [[Academic-Honors-PKU]] — undergraduate awards
- [[Ji-Nie-聂绩]] + [[Yongyun-Hu-胡永云]] + [[Jing-Li-李婧]] + [[Yuk-Yung]] + [[King-Fai-Li]] — undergraduate advisors
- Independent Judgment narrative (held until 2026-06-10) — Moments 1 + 2 (4-advisor + 18-year-old reflection)
- PKU advisor methodology companion (private) — Li Jing + Ji Nie advisor-methodology arc spine
- [[Multi-Method-Comparison-Spine]] — 2019-11-04 3-method Walker strength comparison root evidence
- 2019 critical reflection note (private) — Spring 2019 critical reflection source
