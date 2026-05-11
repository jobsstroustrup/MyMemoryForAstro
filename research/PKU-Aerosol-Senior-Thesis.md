---
title: "Aerosol Joint Retrieval Senior Thesis @ PKU"
publish: true
lang: bilingual
description: "Senior thesis (2021-2022): MODIS+CALIPSO joint retrieval methodology"
---

# Aerosol Joint Retrieval Senior Thesis @ PKU

> **相关页面**: 本页是 [[PKU-Undergraduate-Research]] umbrella 下 Aerosol senior thesis project 的独立 experience page (parallel 逻辑 to [[PKU-Walker-Circulation-Research]] 拆出); source page 见 [[Aerosol-Senior-Thesis]].

## 中文版

### 基本信息
- **时间**: 2021.12 — 2022.06 (~7 months, 大四春 senior thesis period; active research 5.5 months + thesis writing 4 weeks + post-defense polish 2 weeks)
- **角色**: 本科毕业论文独立研究 (Sole author, PI-supervised)
- **组织**: 北京大学物理学院 大气与海洋科学系 ([[Jing-Li-李婧]] group)
- **指导教师**: [[Jing-Li-李婧]] (sole formal advisor, senior thesis PI)
- **地点**: 北京 / NSCC-GZ Tianhe-II (login as (undergraduate Tianhe-II account))
- **Senior thesis artifact**: `(senior thesis final docx).docx` (+ .pdf, 2022-06-03 defended, 1,350 words core content / 192 段 / 7 tables / 4 refs / 21 images)

### 核心问题

**首次 (first) 实现 MODIS + CALIPSO 迭代耦合联合反演气溶胶算法** — 通过把 CALIPSO 主动遥感反演的 aerosol extinction coefficient profile 用于替换 MODIS 被动遥感 Dark Target C5 算法中的 fixed scale-height assumption; 将 MODIS 反演得到的 column-total AOD 作为 CALIPSO 多条候选消光系数廓线的 total-mass constraint (boundary condition); 两者相互 iterate 直至 MODIS AOD 与 CALIPSO extinction profile 同时收敛, 互相 supplement 对方假设中最弱的环节.

### 🌟 Zhenyu 原创贡献

**贡献 1 — First iteratively-coupled MODIS + CALIPSO joint retrieval algorithm** (§4.2 自述):

> *"本研究**首次**实现了 MODIS 和 CALIPSO 的气溶胶联合反演算法的开发，同时该联合反演算法是将 MODIS 和 CALIOP 算法**相互迭代、相互耦合**的，不是孤立地进行改善，而是同时对于 MODIS 的反演 AOD 值和 CALIOP 的消光系数廓线进行改进，因而两卫星在联合反演的全程可以互相匹配、改善、验证。"*

→ 不是单一 satellite 产品的 ad-hoc combination, 而是 convergent iterative coupling algorithm.

**贡献 2 — CALIPSO L2 non-physical bug catch + 修正**:

| 源 | 532 nm 消光系数范围 (0-10 km) | 物理合理性 |
|---|---|---|
| 本研究联合反演 (image14) | **0 – 0.2 km⁻¹**, 全程正值 | ✅ 物理合理 |
| CALIPSO L2 官方产品 (image15) | **-5000 至 -10000 km⁻¹** 突变负值 | ❌ 严重非物理 |

→ **质的改进 (qualitative)** — 不是把小误差降低, 而是**修正 CALIPSO 官方 L2 产品的 non-physical 伪影** (从 -10⁴ km⁻¹ negative 修正到 0-0.2 km⁻¹ 合理正值范围).

**贡献 3 — 4 Beijing case study validation** (vs AERONET Beijing 站 550 nm AOD ground truth):

| # | 日期 | AERONET 基准 AOD | 误差变化 (vs MODIS-only baseline) |
|---|---|---|---|
| 1 | 2007-03-11 | 0.1430 | **abs ↓ 0.0114, rel ↓ 7.97%** |
| 2 | 2008-04-14 | 0.7051 | ⚠️ abs ↑ 0.4565, rel ↑ 64.74% (未收敛, 反向 preserved) |
| 3 | 2008-04-30 | 1.0797 | **abs ↓ 0.0322, rel ↓ 2.98%** |
| 4 | 2019-03-23 | 0.1004 | **abs ↓ 0.0196, rel ↓ 19.52%** |

→ **3/4 成功改进 MODIS-only, absolute AOD error 减小 0.011-0.032, relative error 减小 3-20%, 高 AOD 区改善更显著**. Case 2 反向结果完整保留 in thesis (not airbrushed) — 反向成为 algorithm applicability boundary 诊断 (see 贡献 4).

**贡献 4 — inconvenient evidence 独立 docx 保留**:

独立 docx (supplementary inconvenient-evidence docx) preserve 完整 table: **CALIPSO L2 柱总量 AOD 在 4/4 cases 都比 Zhenyu 联合反演的廓线积分 AOD 更接近 AERONET** — 对 thesis main narrative disadvantageous.

| 实验 | L2 vs AERONET abs err | 联合 vs AERONET abs err | 谁更接近基准 |
|---|---|---|---|
| 1 (2007-03-11) | 0.0694 | 0.1942 | **L2 更近** ⚠️ |
| 2 (2008-04-14) | 0.0917 | 1.6959 | **L2 更近** ⚠️ |
| 3 (2008-04-30) | 0.3226 | 0.3044 | 联合稍近 (持平) |
| 4 (2019-03-23) | 0.0519 | 0.1541 | **L2 更近** ⚠️ |

→ Zhenyu 没有把这个 comparison dimension 从 thesis 中 omit, 而是**独立 docx full table preserve**, 接受 defense 时可能被 point out 的 risk. 详见 Evidence Preservation Discipline (private companion) Instance 4.

**贡献 5 — Failed-approach physical preservation (Instance 5 of Disadvantageous discipline)**:

CALIPSO_Retrieval_Changliang/ 25 versions 中 2 个 failed approaches 完整 preserved + explicit annotation:
- `try1_useH/` (2.5 GB, 早期 "useH" approach abandoned)
- `_之前错误的Cdistance版本/` (920 MB, C_distance.mlx bug 版本, 对应 2022-03-21 weekly PPT 中 "球面距离函数 bug + 前半周工作重做" 的 pre-fix 版本)
- 顶层 txt 标注: `除了try_1_useH和_之前错误的Cdistance版本_其他文件夹中都是正确的函数.txt`

→ 2 级冗余 annotation (folder name 自带"之前错误的" + 顶层 txt 显式列出错误 folders). **失败 approach 物理证据 preserved + explicit annotation, 不删除**.

### 关键成就

1. **First iteratively-coupled MODIS + CALIPSO joint retrieval algorithm** (本科毕业论文级别的 novel algorithm)
2. **CALIPSO L2 -10⁴ km⁻¹ non-physical bug catch + fix** (0-10 km 高度 negative spike → 修正到 0-0.2 km⁻¹ 合理正值范围)
3. **4 Beijing case AOD improvement** (abs ↓ 0.011-0.032, rel ↓ 3-20%, vs MODIS-only baseline, AERONET ground truth)
4. **inconvenient evidence 独立 docx preservation** ((supplementary inconvenient-evidence docx), 4/4 cases L2 柱总量更近 AERONET)
5. **9-version thesis auto-diff** (316 → 1,350 words in 27 days / 9 versions / 2 轮 李婧 edit pass / 9 条 substantive annotations); 316→1137 words in 3 天 (+821 words / +270 words/day = fastest content fill)
6. **22 weekly group meeting PPTs** sustained 6 月 (Dec 2021 - May 2022) at ~1 PPT/周 cadence; 含 Apr 11 dual-version (forme self-track + forteacher present) discipline


8. **4-person lab scaffolding under [[Jing-Li-李婧]] PI**:
   - a lab senior collaborator — Fernald 1984 math pedagogy (`Formula_derivation.docx` 24 段) + lidar-ratio LUT (a 2020 AGU Fall Meeting paper, thesis ref [10]) + CALIPSO base code
   - [[Li-Chong-李充]] 师姐 — MODIS retrieval matlab code + 1 km 标高误差 → 30% AOD 误差 quantification + **critical Caltech bridge** (Li, C., Li, J., Dubovik, O., Zeng, Z. C., **Yung, Y. L.** 2020 *Remote Sensing* 12(9), 1524 paper 一作; 与 Zhenyu 同期 Caltech DSCOVR 项目 PI [[Yuk-Yung]] co-author)
   - [[Dong-Yueming-董悦明]] — LAADS DAAC + wget MODIS L1B 下载 13-slide PPT (2020-09-04 onboarding tutorial)
9. **Mid-term commitment → final delivery 完整闭环**: 2021-12-14 mid-term answer 预 commit 4 features (相关系数提升 + RMSE 降低 + 拟合斜率 → 1 + 廓线 smoother no negative), May 2022 final 全部 confirmed + 加 1 新 (CALIPSO L2 -10⁴ 非物理修正)

### 5.5-month trajectory 关键 milestones

| 日期 | 事件 | 状态 |
|---|---|---|
| 2021-12-10 | 第 1 个正式 progress PPT | MODIS code 跑 NaN + 主动 ask 学长学姐 (honest assessment) |
| 2021-12-14 | 中期答辩 PPT (12 slides) + 讲稿 | "Replace MODIS LUT entirely" ambitious framework + 4 features pre-commit |
| 2021-12-17 | 李充讨论 PPT (7 slides) | line-level + path-level MODIS NaN demonstration to 师姐 |
| 2022-01-17 | weekly report | **MODIS NaN 1-month debug closure** (root cause: 暗像元算法 + 云雪亮地表 automatic NaN = expected behavior; diagnostic: cross-validate via MODIS L2 `Mean_Reflectance_Land`) |
| 2022-02-21 | weekly report | **CALIPSO single-stack closure** — "反演代码中已读通, 测试中的 bug 已解决. Sigma_532, Sigma_1064, 雷达比廓线均可以得到" |
| 2022-03-14 | weekly report (374 KB) | **联合算法 first 实例** (2019-08-01 北京 case) + 2 关键 questions: (Q1) CALIPSO vs MODIS 量级差异, (Q2) AOD 对 scale height 是否敏感 = "假迭代平衡" seed |
| 2022-03-21 | weekly report | **🌟 C_distance.mlx bug fix** — "球面距离函数 bug, 前半周工作重做" (对应 P3 `_之前错误的Cdistance版本/` preserved folder) |
| 2022-03-28 | weekly report (17 slides) | AERONET 9 组合 methodology + self-reject 2_2 (早-晚 13 小时差) |
| 2022-04-04 | weekly report (15 slides) | **log-linear 全廓线拟合 vs 1/e 法 multi-method comparison 加入** (见 [[Multi-Method-Comparison-Spine]]); 2019-08-01 case 两种方法 0.66 km vs 4.1 km = **6× 差异** |
| 2022-04-11 | **dual-version** forme (35 slides) + forteacher (34 slides) | **8 cases (2007 Jan-Apr) systematic sweep**: 5 舍弃 + 1 不收敛 + 2 success, 每 rejection 有 documented reason (CALIPSO NaN / 单廓线 / 与 MODIS 差距过大 / AERONET 缺测) |
| 2022-05-02 | weekly report (28 slides) | **AERONET 验证完全加入 + 4 final cases lock** (3_6 / 2_1 / 4_8 / 4_9) = thesis Section 3.4 source-of-truth |
| 2022-05-07 | thesis writing 起步 | 0507 模板版 (316 words) |
| 2022-06-03 | **defense + 终稿** | 1,350 words / 192 段 / 7 tables / 4 refs / 21 images |

### 技术深度 (resume-grade specifics)

- **5 种语言 integrated**: MATLAB (CALIPSO + MODIS retrieval 主 stack) + Python (MODIS data + plotting, MPL_Extinction ref) + Bash (batch processing) + R + NCL
- **~6,400 MATLAB lines across hzy_experi* folders (aggregate)**: 33 个 MODIS hzy_experi* folders (each ~1,057-1,606 lines, 4-6 .m files) + 24 个 CALIPSO hzy_experi* folders (each ~14 mlx files) = 大部分 copy-paste per-experiment, 真正 unique ~1,500-2,000 lines core code + hardcoded path/data adjust per folder
- **48 GB Modis_scripts + 5.7 GB CALIPSO_Retrieval_Changliang** (aggregate storage) — 含 raw HDF data + per-experiment cached .mat; `贺震昱_code_整理/` final clean reproducible version 仅 56 MB (source + 18 LUT + 2 instruction txt)
- **22 weekly PPTs / Dec 2021 - May 2022 / ~1 PPT/周** sustained cadence (PPT size 演化反映 work intensity: Jan-Feb 30-70 KB code debug → Mar-Apr 400-900 KB experiment 图 → Apr 11 dual-version peak)
- **9-stage experimental-design selection cascade**: CALIPSO 数据质量 / 50 km 距离 / 35 min 时间差 / MODIS-CALIPSO AOD range overlap / MODIS 预反演 30 km 平均 / CALIPSO 沿轨 28 km (~163 profiles, ~8 s 飞行) 平均 / AERONET 同时段 availability / 吸收型主导 regime (Jan-Apr) / log-linear 全廓线拟合 (而非 2-point 1/e 法) — 多年 satellite dataset distilled down to **4 rigorously-validated successful experiments**
- **18 LUT .mat files** (3 bands × 6 aerosol types = MODIS Dark Target C5 forward RT pre-computed tables, earlier lab production) + **12 chinaha_X.mat** (1-12 月 China monthly scale height LUT) + **Table.mat** (Angstrom ↔ lidar ratio LUT (earlier lab production))
- **NSCC-GZ Tianhe-II HPC** (login as (undergraduate Tianhe-II account), 李婧 lab account) — 与 Walker 项目 (undergraduate Tianhe-II account) (Ji Nie lab account) 同 物理 infrastructure + 不同 lab account (cross-project HPC continuity)
- **2 次 PaperPass 旗舰版 查重 trial + 1 次知网正式查重** (post-knowledge-graph plagiarism check discipline) + 2 份 PKU 官方 forms (导师评阅表 + 审查表, 5-3 created 1 个月 buffer ahead of 6-3 defense) = PKU 本科毕业论文 administrative discipline
- **2 GB 北京 + 中国 OpenStreetMap shapefile** (over-prepared for BOUNT_line.shp Beijing boundary subset 仅用; preservation of future-work data) + 李万彪 *大气物理 教材* 自批注扫描版 24 MB (本科课堂教材 carry-over 到 senior thesis 阶段 reference)

### 学术 / 职业意义

- **本科 portfolio 3-track parallel Sep-Dec 2021** 组成部分: Aerosol thesis drafting + [[PKU-Walker-Circulation-Research]] paper v3→v6 + [[Caltech-DSCOVR-Research]] MCMC 反演 + `nwp_hw` 4 道作业 ≈ **3-4 deliverable/week sustained** (与 Caltech DSCOVR 项目 Feb 2022 paper draft 终止后 Aerosol 单项目 full focus 不同 cadence pattern, 但同 sustained discipline)
- **Caltech institutional bridge via [[Li-Chong-李充]]**: 李充 2020 *Remote Sensing* paper co-author 包含 [[Yuk-Yung]] — 这是 Zhenyu 在 2021.03 进入 Caltech DSCOVR 项目的 **institutional pathway 之一**. **PKU 李婧 group → 李充 paper → Caltech Yuk Yung group** 是 2021.03 Zhenyu 与 Caltech onboarding 的 co-author chain.
- **Senior thesis 2022-06-03 defense → 2022-08 UC Berkeley 入学** timeline: 毕业论文 Jun 3 defended, 9 月 start Berkeley Romps lab PhD (详见 [[UCBerkeley-Romps-Lab]])
- **Aerosol research → [[UCBerkeley-Fung-Lab]] Inez Fung methane mapping (2023.12 — 2024.06) preparation training**: satellite remote sensing discipline 一脉相承 (CALIPSO L1/L2 处理 → Sentinel-5P TROPOMI CH₄ 处理; iterative coupled algorithm 方法论 → emission inventory matching)
- **致谢段 cross-project 确认 mentorship sequence**: thesis 终稿致谢 (paragraph 178-186) 列出全部 mentorship 网络 — **李婧老师 (4th, Aerosol PI)** *[detailed mentorship]* → **聂绩老师 + 胡永云老师 (5th, Walker)** *"本科生科研期间指导我的聂绩老师、胡永云老师"* — **explicit 确认**: Zhenyu 本科生科研 = Walker 项目 (Nov 2020 - Oct 2021), 与 thesis = Aerosol (Dec 2021 - Jun 2022) 是 **sequential 而非 parallel**

### 使用的技能

- [[卫星遥感与数据处理]] (MODIS L1B Dark Target C5 + CALIPSO L1 Fernald 方法 + AERONET L2 插值; NASA LAADS/LARC/AERONET 三 data center; 5 种插值 methodology comparison)
- [[气候物理与大气科学]] (Fernald 1984 雷达方程 + Angstrom 指数与 lidar ratio 物理约束 + Kaufman & Tanré 1998 Dark Target + Twomey/Albrecht 间接辐射强迫; 吸收型 aerosol scale-height 敏感性物理 motivation)
- [[Python-科学计算]] (MODIS data 下载 + AERONET 插值 plotting + MPL ref code)
- **MATLAB** — 未 separate skill page, 但 **~6,400 lines across hzy_experi* folders (aggregate)** + CALIPSO + MODIS 双 stack 主要 implementation 是 capability evidence; 可在 [[Python-科学计算]] skill page 补充 MATLAB 技能 sub-section

### 相关页面

- [[PKU-Undergraduate-Research]] — 本科研究 umbrella (Aerosol section 缩成 cross-link to 本页)
- [[Jing-Li-李婧]] — sole formal advisor, reference methodology signature source
- a senior lab collaborator — 师兄, Fernald 1984 math pedagogy + CALIPSO base code
- [[Li-Chong-李充]] — 师姐, MODIS code + 1km 标高 quantification + **critical Caltech bridge via Yuk Yung co-author**
- [[Dong-Yueming-董悦明]] — 师姐/师兄, MODIS download tutorial (2020-09-04)
- [[Yuk-Yung]] — Caltech PI, 与李婧通过李充 paper paper attribution connected (bridge context for [[Caltech-DSCOVR-Research]])
- PKU advisor methodology companion (private) — 李婧 reference methodology signature (mirror with [[Ji-Nie-聂绩]] Walker project (private context))
- Evidence Preservation Discipline (private companion) — Instance 4 (`难以解释.docx`) + Instance 5 (`try1_useH/` + `_之前错误的Cdistance版本/`) + Instance 6 (8-case rejection cascade)
- [[Multi-Method-Comparison-Spine]] — log-linear 全廓线拟合 vs 1/e 法 2-point multi-method; 5 个 numerical method (linear 外插 + pchip 外插 + log 拟合 + 1/e 法 + multi-AOD_c 平均) 并列 active
- Independent Judgment narrative (held until 2026-06-10) — Moment 5 artifact (Aerosol 难以解释 docx)
- [[Aerosol-Senior-Thesis]] — thesis source page (终稿 docx + .pdf)
- [[Academic-Honors-PKU]] — 本科毕业论文 archive
- [[PKU-Walker-Circulation-Research]] — parallel Walker experience page (sequential predecessor; 致谢段 explicit 确认 sequence)
- [[Caltech-DSCOVR-Research]] — 同期 Caltech 项目 (2021.03 - 2022.03 MCMC 反演; bridge via 李充 Yuk Yung co-author)
- [[UCBerkeley-Fung-Lab]] — Aerosol satellite remote sensing → methane mapping successor PhD 项目

### 来源

- `research_wiki/projects/aerosol_retrieval/overview.md` (~46k words 完整, P1-P5 deep-dive 全)
- `research_wiki/resume_angles/problem_solving.md` §Project 4 Aerosol (若 mention)
- `research_wiki/resume_angles/cross_disciplinary.md` §Section 9 李婧 methodology (private)
- raw artifact: `raw/pku项目文件/pku_research/Lijing/毕业论文写作/(senior thesis final docx).docx` (+ .pdf)
- raw artifact: `raw/pku项目文件/pku_research/Lijing/毕业论文写作/supplementary inconvenient-evidence section.docx` (inconvenient evidence independent docx)
- raw artifact: `raw/pku项目文件/pku_research/Lijing/code/` (48 GB Modis_scripts + 5.7 GB CALIPSO_Retrieval_Changliang + 56 MB 贺震昱_code_整理 final clean)
- raw artifact: `raw/pku项目文件/pku_research/Lijing/毕业论文写作/ppt_pre合集/` (22 weekly PPTs, Dec 2021 - May 2022)

---

## English Version

### Basic Info
- **Period**: Dec 2021 — Jun 2022 (~7 months, senior-spring senior-thesis period; ~5.5 months active research + 4 weeks of thesis writing + 2 weeks of post-defense polish)
- **Role**: Senior-thesis independent research (sole author, PI-supervised)
- **Organization**: Department of Atmospheric and Oceanic Sciences, School of Physics, Peking University ([[Jing-Li-李婧]] group)
- **Advisor**: [[Jing-Li-李婧]] (sole formal advisor, senior-thesis PI)
- **Location**: Beijing / NSCC-GZ Tianhe-II (login as (undergraduate Tianhe-II account))
- **Senior-thesis artifact**: `(senior thesis final docx).docx` (+ .pdf, defended 2022-06-03; 1,350 words core content / 192 paragraphs / 7 tables / 4 refs / 21 images)

### Core Problem

**First** implementation of an iteratively coupled MODIS + CALIPSO joint aerosol-retrieval algorithm — using the aerosol extinction-coefficient profile from CALIPSO active remote sensing to replace the fixed scale-height assumption in MODIS Dark Target C5 passive remote sensing; using the column-total AOD retrieved by MODIS as a total-mass constraint (boundary condition) on CALIPSO's multiple candidate extinction profiles; iterating until both MODIS AOD and CALIPSO extinction profile converge, supplementing each other's weakest assumptions.

### Zhenyu's Original Contributions

**Contribution 1 — First iteratively-coupled MODIS + CALIPSO joint retrieval algorithm** (§4.2 self-statement):

> *"本研究**首次**实现了 MODIS 和 CALIPSO 的气溶胶联合反演算法的开发，同时该联合反演算法是将 MODIS 和 CALIOP 算法**相互迭代、相互耦合**的，不是孤立地进行改善，而是同时对于 MODIS 的反演 AOD 值和 CALIOP 的消光系数廓线进行改进，因而两卫星在联合反演的全程可以互相匹配、改善、验证。"*
>
> (English gloss: This study, **for the first time**, develops a joint MODIS + CALIPSO aerosol-retrieval algorithm. The joint algorithm **mutually iterates and mutually couples** MODIS and CALIOP, rather than improving them in isolation: it simultaneously improves both MODIS-retrieved AOD and CALIOP extinction profile, so the two satellites can match, improve, and validate each other throughout the joint retrieval.)

→ Not an ad-hoc combination of single-satellite products, but a convergent iterative-coupling algorithm.

**Contribution 2 — CALIPSO L2 non-physical bug catch + correction**:

| Source | 532 nm extinction range (0-10 km) | Physical plausibility |
|---|---|---|
| Joint retrieval here (image14) | **0 – 0.2 km⁻¹**, all positive | OK — physically plausible |
| CALIPSO L2 official product (image15) | **-5000 to -10000 km⁻¹** abrupt negatives | NOT plausible — strongly non-physical |

→ **Qualitative improvement** — not just reducing small errors, but **correcting non-physical artifacts in the official CALIPSO L2 product** (from -10⁴ km⁻¹ negatives to a plausible 0-0.2 km⁻¹ positive range).

**Contribution 3 — 4 Beijing-case validation** (vs AERONET Beijing site 550 nm AOD ground truth):

| # | Date | AERONET reference AOD | Error change (vs MODIS-only baseline) |
|---|---|---|---|
| 1 | 2007-03-11 | 0.1430 | **abs ↓ 0.0114, rel ↓ 7.97%** |
| 2 | 2008-04-14 | 0.7051 | abs ↑ 0.4565, rel ↑ 64.74% (did not converge; reverse case preserved) |
| 3 | 2008-04-30 | 1.0797 | **abs ↓ 0.0322, rel ↓ 2.98%** |
| 4 | 2019-03-23 | 0.1004 | **abs ↓ 0.0196, rel ↓ 19.52%** |

→ **3/4 cases successfully improve over MODIS-only**: absolute AOD error reduced by 0.011-0.032; relative error reduced by 3-20%; improvement more pronounced in higher-AOD regimes. Case 2 reverse result is fully preserved in the thesis (not airbrushed) — the reverse becomes algorithm-applicability-boundary diagnosis (see Contribution 4).

**Contribution 4 — inconvenient evidence preserved as a separate docx**:

A separate docx (supplementary inconvenient-evidence docx) (filename gloss: "Hard-to-Explain or inconvenient evidence Section.docx") preserves the full table: **the CALIPSO L2 column-total AOD is closer to AERONET than the joint-retrieval profile-integrated AOD in 4/4 cases** — disadvantageous to the thesis's main narrative.

| Experiment | L2 vs AERONET abs err | Joint vs AERONET abs err | Closer to reference |
|---|---|---|---|
| 1 (2007-03-11) | 0.0694 | 0.1942 | **L2 closer** |
| 2 (2008-04-14) | 0.0917 | 1.6959 | **L2 closer** |
| 3 (2008-04-30) | 0.3226 | 0.3044 | Joint slightly closer (tied) |
| 4 (2019-03-23) | 0.0519 | 0.1541 | **L2 closer** |

→ Zhenyu did not omit this comparison dimension from the thesis but instead **fully preserved the table in a separate docx**, accepting the risk of being pointed out at defense. See Evidence Preservation Discipline (private companion) Instance 4.

**Contribution 5 — Failed-approach physical preservation (Instance 5 of the disadvantageous discipline)**:

Within `CALIPSO_Retrieval_Changliang/`'s 25 versions, 2 failed approaches are fully preserved + explicitly annotated:
- `try1_useH/` (2.5 GB, early "useH" approach abandoned)
- `_之前错误的Cdistance版本/` (920 MB, C_distance.mlx bug version, corresponding to the 2022-03-21 weekly PPT's "spherical distance function bug + first-half-week work redo" pre-fix version) (folder gloss: "previous_incorrect_Cdistance_version/")
- Top-level txt annotation: `除了try_1_useH和_之前错误的Cdistance版本_其他文件夹中都是正确的函数.txt` (filename gloss: "Except for try_1_useH and previous_incorrect_Cdistance_version, all other folders contain correct functions.txt")

→ Two-level redundant annotation (folder name itself includes "previous incorrect" + top-level txt explicitly lists wrong folders). **Failed-approach physical evidence preserved + explicitly annotated; not deleted**.

### Key Achievements

1. **First iteratively-coupled MODIS + CALIPSO joint retrieval algorithm** (novel-algorithm-level senior thesis)
2. **CALIPSO L2 -10⁴ km⁻¹ non-physical bug catch + fix** (0-10 km altitude negative spike → corrected to 0-0.2 km⁻¹ plausible positive range)
3. **4-Beijing-case AOD improvement** (abs ↓ 0.011-0.032, rel ↓ 3-20% vs MODIS-only baseline, AERONET ground truth)
4. **inconvenient evidence preserved in a separate docx** ((supplementary inconvenient-evidence docx), 4/4 cases L2 column-total closer to AERONET)
5. **9-version thesis auto-diff** (316 → 1,350 words in 27 days / 9 versions / 2 rounds of Jing Li edit pass / 9 substantive annotations); 316 → 1,137 words in 3 days (+821 words / +270 words/day = fastest content fill)
6. **22 weekly group-meeting PPTs** sustained over 6 months (Dec 2021 - May 2022) at ~1 PPT/week cadence; including the Apr 11 dual-version (forme self-track + forteacher present) discipline

8. **4-person lab scaffolding under [[Jing-Li-李婧]] PI**:
   - a senior lab collaborator (older labmate) — Fernald 1984 math pedagogy (`Formula_derivation.docx` 24 paragraphs) + lidar-ratio LUT (a 2020 AGU Fall Meeting paper, thesis ref [10]) + CALIPSO base code
   - [[Li-Chong-李充]] (older labmate) — MODIS retrieval MATLAB code + 1 km scale-height error → 30% AOD-error quantification + **critical Caltech bridge** (Li, C., Li, J., Dubovik, O., Zeng, Z. C., **Yung, Y. L.** 2020 *Remote Sensing* 12(9), 1524 paper first author; co-author with Zhenyu's contemporaneous Caltech DSCOVR PI [[Yuk-Yung]])
   - [[Dong-Yueming-董悦明]] — LAADS DAAC + wget MODIS L1B download 13-slide PPT (2020-09-04 onboarding tutorial)
9. **Mid-term commitment → final delivery full closure**: at the 2021-12-14 mid-term answer Zhenyu pre-committed 4 features (correlation-coefficient improvement + RMSE reduction + fitted slope → 1 + smoother profile with no negatives), and by May 2022 the final delivery confirmed all 4 + added 1 new (CALIPSO L2 -10⁴ non-physical correction)

### 5.5-month Trajectory Key Milestones

| Date | Event | Status |
|---|---|---|
| 2021-12-10 | First formal progress PPT | MODIS code returns NaN + proactively asked older labmates (honest assessment) |
| 2021-12-14 | Mid-term defense PPT (12 slides) + script | "Replace MODIS LUT entirely" ambitious framework + 4 features pre-committed |
| 2021-12-17 | Discussion PPT with Li Chong (7 slides) | Line-level + path-level MODIS NaN demonstration to older labmate |
| 2022-01-17 | Weekly report | **MODIS NaN 1-month debug closure** (root cause: dark-pixel algorithm + cloud/snow bright surface auto-NaN = expected behavior; diagnostic: cross-validate via MODIS L2 `Mean_Reflectance_Land`) |
| 2022-02-21 | Weekly report | **CALIPSO single-stack closure** — "Retrieval code now reads correctly; bug under testing resolved. Sigma_532, Sigma_1064, lidar-ratio profiles all obtainable" |
| 2022-03-14 | Weekly report (374 KB) | **First instance of joint algorithm** (2019-08-01 Beijing case) + 2 key questions: (Q1) CALIPSO vs MODIS magnitude difference, (Q2) AOD sensitivity to scale height = "false iterative equilibrium" seed |
| 2022-03-21 | Weekly report | **C_distance.mlx bug fix** — "spherical-distance function bug, first-half-week work redone" (corresponds to the P3 `_之前错误的Cdistance版本/` preserved folder) |
| 2022-03-28 | Weekly report (17 slides) | AERONET 9-combination methodology + self-rejecting 2_2 (early-late 13-hour gap) |
| 2022-04-04 | Weekly report (15 slides) | **Log-linear full-profile fitting vs 1/e method multi-method comparison added** (see [[Multi-Method-Comparison-Spine]]); 2019-08-01 case two methods give 0.66 km vs 4.1 km = **6× difference** |
| 2022-04-11 | **Dual-version**: forme (35 slides) + forteacher (34 slides) | **8-case (2007 Jan-Apr) systematic sweep**: 5 rejected + 1 non-converged + 2 successful, each rejection has a documented reason (CALIPSO NaN / single profile / too far from MODIS / AERONET missing) |
| 2022-05-02 | Weekly report (28 slides) | **AERONET validation fully integrated + 4 final cases locked** (3_6 / 2_1 / 4_8 / 4_9) = thesis Section 3.4 source-of-truth |
| 2022-05-07 | Thesis writing kickoff | 0507 template version (316 words) |
| 2022-06-03 | **Defense + final draft** | 1,350 words / 192 paragraphs / 7 tables / 4 refs / 21 images |

### Technical Depth (resume-grade specifics)

- **5 languages integrated**: MATLAB (CALIPSO + MODIS retrieval main stack) + Python (MODIS data + plotting, MPL_Extinction ref) + Bash (batch processing) + R + NCL
- **~6,400 MATLAB lines across hzy_experi* folders (aggregate)**: 33 MODIS hzy_experi* folders (each ~1,057-1,606 lines, 4-6 .m files) + 24 CALIPSO hzy_experi* folders (each ~14 mlx files) = mostly copy-paste per-experiment, ~1,500-2,000 truly unique core lines + hardcoded per-folder path/data adjustments
- **48 GB Modis_scripts + 5.7 GB CALIPSO_Retrieval_Changliang** (aggregate storage) — including raw HDF data + per-experiment cached .mat; the `贺震昱_code_整理/` final clean reproducible version is only 56 MB (source + 18 LUT + 2 instruction txt)
- **22 weekly PPTs / Dec 2021 - May 2022 / ~1 PPT/week** sustained cadence (PPT size evolution reflects work intensity: Jan-Feb 30-70 KB code debug → Mar-Apr 400-900 KB experiment plots → Apr 11 dual-version peak)
- **9-stage experimental-design selection cascade**: CALIPSO data quality / 50 km distance / 35 min time gap / MODIS-CALIPSO AOD-range overlap / 30 km MODIS pre-retrieval averaging / 28 km along-track CALIPSO (~163 profiles, ~8 s flight) averaging / AERONET availability in same time window / absorption-dominant regime (Jan-Apr) / log-linear full-profile fitting (instead of 2-point 1/e method) — multi-year satellite dataset distilled down to **4 rigorously validated successful experiments**
- **18 LUT .mat files** (3 bands × 6 aerosol types = MODIS Dark Target C5 forward-RT pre-computed tables, prior production by Li Chong / Chang Liang) + **12 chinaha_X.mat** (months 1-12 China monthly scale-height LUT) + **Table.mat** (Chang Liang Angstrom ↔ lidar-ratio LUT)
- **NSCC-GZ Tianhe-II HPC** (login as (undergraduate Tianhe-II account), Jing Li lab account) — same physical infrastructure as the Walker project's (undergraduate Tianhe-II account) (Ji Nie lab account) but a different lab account (cross-project HPC continuity)
- **2 PaperPass flagship trials + 1 official CNKI plagiarism check** (post-knowledge-graph plagiarism-check discipline) + 2 PKU official forms (advisor review form + audit form, both created on 5-3, 1-month buffer ahead of the 6-3 defense) = senior-thesis administrative discipline at PKU
- **2 GB Beijing + China OpenStreetMap shapefiles** (over-prepared for `BOUNT_line.shp` Beijing-boundary subset use only; future-work data preservation) + Li Wanbiao *Atmospheric Physics textbook* with Zhenyu's annotations, scanned 24 MB (undergraduate-classroom textbook carry-over to senior-thesis-stage reference)

### Academic / Career Significance

- Component of the **3-track parallel Sep-Dec 2021 senior portfolio**: Aerosol thesis drafting + [[PKU-Walker-Circulation-Research]] paper v3→v6 + [[Caltech-DSCOVR-Research]] MCMC retrieval + `nwp_hw` 4 assignments ≈ **3-4 deliverable/week sustained** (different cadence pattern from the Caltech DSCOVR Feb-2022 paper-draft termination → Aerosol-only full-focus phase, but the same sustained discipline)
- **Caltech institutional bridge via [[Li-Chong-李充]]**: Li Chong's 2020 *Remote Sensing* paper co-author list includes [[Yuk-Yung]] — **one of the institutional pathways** for Zhenyu's Mar 2021 Caltech DSCOVR onboarding. **PKU Jing Li group → Li Chong paper → Caltech Yuk Yung group** is the co-author chain for Zhenyu's Caltech onboarding in Mar 2021.
- **Senior thesis 2022-06-03 defense → 2022-08 UC Berkeley enrollment** timeline: thesis defended Jun 3, started PhD at the Berkeley Romps lab in September (see [[UCBerkeley-Romps-Lab]])
- **Aerosol research → [[UCBerkeley-Fung-Lab]] Inez Fung methane mapping (Dec 2023 — Jun 2024) preparation training**: satellite-remote-sensing discipline carries over (CALIPSO L1/L2 processing → Sentinel-5P TROPOMI CH₄ processing; iteratively coupled algorithm methodology → emission-inventory matching)
- **Acknowledgments cross-project mentorship-sequence confirmation**: the final-draft acknowledgments (paragraphs 178-186) list the entire mentorship network — **Prof. Jing Li (4th, Aerosol PI)** *[detailed mentorship]* (gloss: very conscientious and responsible — guided every weekly work report and patiently, in detail, answered my questions) → **Prof. Ji Nie + Prof. Yongyun Hu (5th, Walker)** *"本科生科研期间指导我的聂绩老师、胡永云老师"* (gloss: Prof. Ji Nie and Prof. Yongyun Hu who advised me during the undergraduate-research period) — **explicitly confirms**: Zhenyu's undergraduate-research = the Walker project (Nov 2020 - Oct 2021), and the thesis = Aerosol (Dec 2021 - Jun 2022) are **sequential rather than parallel**

### Skills Used

- [[卫星遥感与数据处理]] (MODIS L1B Dark Target C5 + CALIPSO L1 Fernald method + AERONET L2 interpolation; NASA LAADS / LARC / AERONET 3 data centers; comparison of 5 interpolation methodologies)
- [[气候物理与大气科学]] (Fernald 1984 lidar equation + Angstrom exponent and lidar-ratio physical constraint + Kaufman & Tanré 1998 Dark Target + Twomey/Albrecht indirect radiative forcing; absorbing-aerosol scale-height sensitivity physical motivation)
- [[Python-科学计算]] (MODIS data download + AERONET interpolation plotting + MPL ref code)
- **MATLAB** — no separate skill page yet, but **~6,400 lines across hzy_experi* folders (aggregate)** + CALIPSO + MODIS dual-stack as the main implementation language is capability evidence; can be added as a MATLAB sub-section under the [[Python-科学计算]] skill page

### Related Pages

- [[PKU-Undergraduate-Research]] — undergraduate-research umbrella (Aerosol section condensed to a cross-link to this page)
- [[Jing-Li-李婧]] — sole formal advisor, source of reference-methodology signature
- a senior lab collaborator — older labmate, Fernald 1984 math pedagogy + CALIPSO base code
- [[Li-Chong-李充]] — older labmate, MODIS code + 1 km scale-height quantification + **critical Caltech bridge via Yuk Yung paper attribution**
- [[Dong-Yueming-董悦明]] — older labmate, MODIS download tutorial (2020-09-04)
- [[Yuk-Yung]] — Caltech PI, connected with Jing Li via Li Chong's paper paper attribution (bridge context for [[Caltech-DSCOVR-Research]])
- PKU advisor methodology companion (private) — Jing Li reference-methodology signature (mirror with [[Ji-Nie-聂绩]] Walker project (private context))
- Evidence Preservation Discipline (private companion) — Instance 4 (`难以解释.docx`) + Instance 5 (`try1_useH/` + `_之前错误的Cdistance版本/`) + Instance 6 (8-case rejection cascade)
- [[Multi-Method-Comparison-Spine]] — log-linear full-profile fitting vs 1/e 2-point multi-method; 5 numerical methods (linear extrapolation + pchip extrapolation + log fit + 1/e method + multi-AOD_c averaging) actively in parallel
- Independent Judgment narrative (held until 2026-06-10) — Moment 5 artifact (Aerosol disadvantageous-evidence docx)
- [[Aerosol-Senior-Thesis]] — thesis source page (final docx + .pdf)
- [[Academic-Honors-PKU]] — senior-thesis archive
- [[PKU-Walker-Circulation-Research]] — parallel Walker experience page (sequential predecessor; acknowledgments explicitly confirm sequence)
- [[Caltech-DSCOVR-Research]] — contemporaneous Caltech project (2021.03 - 2022.03 MCMC retrieval; bridge via Li Chong / Yuk Yung paper attribution)
- [[UCBerkeley-Fung-Lab]] — Aerosol satellite remote sensing → methane mapping successor PhD project

### Sources

- `research_wiki/projects/aerosol_retrieval/overview.md` (~46k words complete, full P1-P5 deep-dive)
- `research_wiki/resume_angles/problem_solving.md` §Project 4 Aerosol (if mentioned)
- `research_wiki/resume_angles/cross_disciplinary.md` §Section 9 Jing Li methodology (private)
- raw artifact: `raw/pku项目文件/pku_research/Lijing/毕业论文写作/(senior thesis final docx).docx` (+ .pdf)
- raw artifact: `raw/pku项目文件/pku_research/Lijing/毕业论文写作/supplementary inconvenient-evidence section.docx` (disadvantageous-evidence independent docx)
- raw artifact: `raw/pku项目文件/pku_research/Lijing/code/` (48 GB Modis_scripts + 5.7 GB CALIPSO_Retrieval_Changliang + 56 MB 贺震昱_code_整理 final clean)
- raw artifact: `raw/pku项目文件/pku_research/Lijing/毕业论文写作/ppt_pre合集/` (22 weekly PPTs, Dec 2021 - May 2022)
