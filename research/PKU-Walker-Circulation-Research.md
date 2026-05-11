---
title: "Walker Circulation Dynamics @ PKU"
publish: true
lang: bilingual
description: "Walker Circulation Dynamics @ PKU (2020-2021), independent undergraduate research project"
---

# Walker Circulation Dynamics @ PKU

## 中文版

### 基本信息
- **时间**: 2020.11 — 2021.10 (~12 months active research; paper draft v6 finalized 2021-10-22)
- **角色**: 本科独立研究 (First author)
- **组织**: 北京大学物理学院大气与海洋科学系
- **指导教师**: [[Ji-Nie-聂绩]] (primary PI) + [[Yongyun-Hu-胡永云]] (co-advisor, 胡组讨论平台)
- **地点**: 北京 / Tianhe-II 国家超算广州中心 (NSCC-GZ)
- **资助**: PKU President Fellowship (undergraduate research)

### 核心问题
Walker Circulation 对 oceanic forcing **宽度** 的 systematic 响应: 在 CAM3 aqua-planet 里把海洋热源 (Warm Pool) 与冷源 (Cold Pool) 的距离 D 从 60° 变化到 180° (step 20°), 加上 Warm-only / Cold-only / Aqua baseline, 共 **10 cases × 30 年 runs**, 探索 Walker 强度 + 大尺度 SST/precip/ω/SW 响应的规律。

### 🌟 Zhenyu 核心原创贡献 (2021-07-13 breakthrough)

**Linear Superposition framework** — 用 forcing-response operator 的 2nd-order Taylor expansion 在 forcing 距离较远时 drop interaction term, 得到:

$$\mathrm{Response}(W + C) \approx \mathrm{Response}(W) + \mathrm{Response}(C)$$

**4-field quantitative validation** (D80-D180 bulk):
- **SST corr 0.9063**
- **Precip corr 0.9215**
- **ω@500mb corr 0.8282**
- **SW corr 0.9324** (all > 0.82)

**2021-07-13 breakthrough 现场 verbatim** (见 [[2021-07-13-Breakthrough-PPT]] slide 24):


After advisor discussion, the linear superposition framework proposed by Zhenyu provided a satisfactory explanation, and was endorsed.

**Emergent prediction**: Walker strength 非单调 peaks at D80-100° — 这个 peak 恰好对应 Wonly 的 natural descending area (200-220°E) 与 cold pool 几何重合的位置。**不需要 nonlinear mechanism 解释**。

**Linear superposition 失效的边界 (D60-D80)**: low-cloud positive feedback loop —— CP descending↑ → suppress convection → trap humidity → low cloud↑ → albedo↑ → SW absorption↓ → SST↓ → ΔSST↑ → loop; 4-term energy budget diagnosed (SW+LH dominate, ΔSW D60: -66.5141 W/m² → D180: -110.6316 W/m²)。

### 7-Month Intuition Accumulation Trajectory (从 framing 到 breakthrough)

| 时间 | 事件 | 累积状态 |
|------|------|---------|
| 2020-12-29 slide 5 | **Walker 左右非对称 framing** (7-width sweep) | 早期 framework seed |
| 2021-04-26 master PPT 295 slides | **拼贴萌芽 slides 32-65** (3 个月 BEFORE breakthrough) | first systematic superposition attempt |
| 2021-05-16 胡组 15 slides | **D180 self-consistent linear superposition explicit** | 3 个月前 explicit |
| 2021-05-26 / 5-28 / 6-2 进展报告 | **84 figure groups systematic** (5-28 拼贴系统化到 6 fields) | 2 个月前接近成形 |
| **2021-07-13 进展报告 29 slides** | ⭐ **breakthrough** — Zhenyu 当场提出 linear superposition + Ji Nie endorsement | "之后就可以开始写论文" |
| 2021-07-16 胡组 28 slides | Post-breakthrough 给 Hu group 的 echo (slide 20 "线性叠加可以解释 Q1") | multi-advisor platform delivery |

### 关键成就

1. **Linear Superposition framework 提出 + 4-field 0.83-0.93 correlation 验证** (framework-level 贡献, 非 incremental), 详见 [[Linear-Superposition-Framework]]
2. **Emergent non-monotonic Walker strength 解释** (D80-100° peak = natural descending 与 cold pool 重合)
3. **Low-cloud feedback failure-boundary 诊断** (4-term energy budget SW+LH dominate)
4. **ω-based vs u-based methodology bug catch** (4-26 slide 26 发现 omega 不满足 "无散"; 两 NCL module 并列 preserved: `msf_top2bottom_u2_Walker.ncl` 61 lines + `msf_top2bottom_omega2_WalkerStream.ncl` 63 lines) — engineering rigor signature, 归于 [[Multi-Method-Comparison-Spine]]
5. **Paper draft v6 (3663 words, 11 refs, 2021-10-22)**: **Zhenyu He¹, Ji Nie¹\***, supported by the PKU President Fellowship — **未投稿**:

   
Project not submitted by mutual decision.

   非 research failure, 是合作者的 publishing decision。paper 草稿存档见 [[Walker-Paper-v6-Unpublished]]。
6. **8 周 / 9-version paper auto-diff**: v1 → v2_2 → v2_2-nj (Ji Nie 第 1 轮 +13 中文 inline comments) → v3 (Zhenyu 实施 +3 equation tables) → v4 (+465 words / +8 refs in 2 days, 大扩充) → v5 → v5-nj (Ji Nie 第 2 轮) → v6 (+3 refs, 最终)
7. **Ji Nie methodology arc arc signature**: 
Project paper draft retained internally; advisor and student arrived at a mutual decision not to submit.

### 技术深度 (Resume-grade specifics)

- **5-stage HPC pipeline architecture**: (1) CAM3 aqua-planet with prescribed Q-flux → (2) 30-year spin-up on Tianhe-II (undergraduate Tianhe-II account) account (`yhrun -p work -n 48` 48-PE SLURM) → (3) 25 `cal_X/` MATLAB diagnostic folders → (4) NCL stream function + ω analysis → (5) paper figure refinement MATLAB + Python
- **27,882 MATLAB+NCL lines / 5 languages**: MATLAB (main diagnostic) + NCL (stream function) + Fortran (namelist + CAM3 source mods) + Bash (SLURM runscripts) + Python (paper figure polish)
- **14 Q-flux variants** preserved (D60 / D80 / D100 / D120 / D140 / D160 / D180 + Wonly + Conly + Aqua + variations)
- **20 NCAR CAM3 .F90 source mods** (`SourceMods.zip` 143 KB in Walker `cam3_task/`), aggregate: cldinti / cldsav / cloud_fraction / comctl / ghg_defaults / hb_diff / history / hycoef / ice_constants / inidat / initext / ocn_srf / physpkg / radiation / radlw / runtime_opts / **somoce** (MLDANN 50→30m slab ocean, key dep) / stratiform / tphysbc — 本科生 source-code 级别的 GCM 修改

### 学术 / 职业 意义
- 与 [[PKU-Aerosol-Senior-Thesis]] + [[Caltech-DSCOVR-Research]] 共同构成 **3-track parallel Sep-Dec 2021 本科大四上** (Walker paper v3→v6 + DSCOVR HBP + nwp_hw 4 个作业 ≈ 3-4 deliverable/week)
- 是 [[PKU-Walker-Hadley-Response-Research]] (2019.10 — 2020.05, Ji Nie 组 first project) 的 successor + 是 [[UCBerkeley-Romps-Lab]] PhD 阶段 3D LES + 1-D DSE+SWTG quasi-2D 等 multi-model 工作的 competence foundation
- Walker paper v6 的 research-grade specificity 被 Zhenyu 后续用于 UC Berkeley PhD 申请 + Caltech/UCR Yuk Yung/King-Fai Li 合作 + Princeton SGS 邀请的底色
- Moment 2 of Independent Judgment narrative (held until 2026-06-10) spine (2021-07-13 在导师 MSE budget 解释失败后, 自己提出 linear superposition 并 defend 到 Ji Nie endorsement)

### 使用的技能
- [[气候物理与大气科学]] (Walker/Hadley + 4-term energy budget + low-cloud feedback)
- [[高性能计算-HPC]] (Tianhe-II (undergraduate Tianhe-II account) 48-PE + CAM3 aqua-planet 30-yr)
- [[Python-科学计算]] (paper figure + 部分 diagnostic)
- [[数值模式源代码修改]] (20 NCAR CAM3 .F90 mods)

### 相关页面
- [[PKU-Undergraduate-Research]] — 本科研究 umbrella page
- [[PKU-Walker-Hadley-Response-Research]] — 前序 Ji Nie 组 project (2019.10 — 2020.05)
- [[Ji-Nie-聂绩]] — Walker 项目 primary PI
- [[Yongyun-Hu-胡永云]] — Walker co-advisor, 胡组讨论平台
- [[Linear-Superposition-Framework]] — Zhenyu 原创 framework concept 页
- [[2021-07-13-Breakthrough-PPT]] — breakthrough artifact source page
- [[Walker-Paper-v6-Unpublished]] — paper draft source page
- PKU advisor methodology companion (private) — acknowledgment 改写 arc, 与 [[Jing-Li-李婧]] 共同构成
- [[Multi-Method-Comparison-Spine]] — ω-vs-u methodology rigor 归入此 spine
- Independent Judgment narrative (held until 2026-06-10) — Moment 2 (meta-level)
- [[Academic-Honors-PKU]] — supported by the PKU President Fellowship

### 来源
- `research_wiki/projects/walker_hadley/overview.md` (~55k words / 1303 行)
- `research_wiki/resume_angles/problem_solving.md` §Project 5
- `research_wiki/resume_angles/technical_depth.md` §Section 9

---

## English Version

### Basic Info
- **Period**: Nov 2020 — Oct 2021 (~12 months active research; paper draft v6 finalized 2021-10-22)
- **Role**: Undergraduate independent research (First author)
- **Organization**: School of Physics, Department of Atmospheric and Oceanic Sciences, Peking University
- **Advisors**: [[Ji-Nie-聂绩]] (primary PI) + [[Yongyun-Hu-胡永云]] (co-advisor, Hu-group discussion platform)
- **Location**: Beijing / Tianhe-II NSCC-GZ
- **Support**: PKU President Fellowship (undergraduate research)

### Core Problem

Systematic response of the Walker Circulation to oceanic-forcing **width**: in CAM3 aqua-planet, vary the distance D between the warm-pool source and cold-pool sink from 60° to 180° (step 20°), plus Warm-only / Cold-only / Aqua baseline — **10 cases × 30-year runs** total — exploring the regularities of Walker strength + large-scale SST/precip/ω/SW responses.

### Zhenyu's Core Original Contribution (2021-07-13 breakthrough)

**Linear Superposition framework** — apply a 2nd-order Taylor expansion to the forcing-response operator, drop the interaction term when the forcings are far apart, yielding:

$$\mathrm{Response}(W + C) \approx \mathrm{Response}(W) + \mathrm{Response}(C)$$

**4-field quantitative validation** (D80-D180 bulk):
- **SST corr 0.9063**
- **Precip corr 0.9215**
- **ω@500mb corr 0.8282**
- **SW corr 0.9324** (all > 0.82)

**2021-07-13 breakthrough verbatim** (see [[2021-07-13-Breakthrough-PPT]] slide 24):


After advisor discussion, the linear superposition framework proposed by Zhenyu provided a satisfactory explanation, and was endorsed.
>
> 

**Emergent prediction**: Walker strength is non-monotonic and peaks at D80-100° — that peak corresponds exactly to the location where Wonly's natural descending area (200-220°E) geometrically overlaps with the cold pool. **No nonlinear mechanism is needed to explain it**.

**Linear-superposition failure boundary (D60-D80)**: low-cloud positive-feedback loop — CP descending↑ → suppress convection → trap humidity → low cloud↑ → albedo↑ → SW absorption↓ → SST↓ → ΔSST↑ → loop; 4-term energy budget diagnosed (SW + LH dominate; ΔSW D60: -66.5141 W/m² → D180: -110.6316 W/m²).

### 7-Month Intuition Accumulation Trajectory (from framing to breakthrough)

| Time | Event | Cumulative state |
|------|------|---------|
| 2020-12-29 slide 5 | **Walker left-right asymmetry framing** (7-width sweep) | Early framework seed |
| 2021-04-26 master PPT 295 slides | **Collage seedlings slides 32-65** (3 months BEFORE breakthrough) | First systematic superposition attempt |
| 2021-05-16 Hu group 15 slides | **D180 self-consistent linear superposition explicit** | Explicit 3 months before |
| 2021-05-26 / 5-28 / 6-2 progress reports | **84 figure groups systematic** (5-28 collage systematized to 6 fields) | Near-complete 2 months before |
| **2021-07-13 progress report 29 slides** | **breakthrough** — Zhenyu proposed linear superposition on the spot + Ji Nie endorsement | "Then we can start writing the paper" |
| 2021-07-16 Hu group 28 slides | Post-breakthrough echo to Hu group (slide 20 "linear superposition can explain Q1") | Multi-advisor platform delivery |

### Key Achievements

1. **Linear Superposition framework proposal + 4-field 0.83-0.93 correlation validation** (framework-level contribution, not incremental); see [[Linear-Superposition-Framework]]
2. **Emergent non-monotonic Walker-strength explanation** (D80-100° peak = natural-descending and cold-pool overlap)
3. **Low-cloud feedback failure-boundary diagnosis** (4-term energy budget, SW + LH dominate)
4. **ω-based vs u-based methodology bug catch** (4-26 slide 26 found ω does not satisfy "non-divergence"; both NCL modules preserved side by side: `msf_top2bottom_u2_Walker.ncl` 61 lines + `msf_top2bottom_omega2_WalkerStream.ncl` 63 lines) — engineering-rigor signature, attributed to [[Multi-Method-Comparison-Spine]]
5. **Paper draft v6 (3,663 words, 11 refs, 2021-10-22)**: **Zhenyu He¹, Ji Nie¹\***, supported by the PKU President Fellowship — **unpublished**:

   
Project not submitted by mutual decision.
   >


   Not a research failure but a co-author publishing decision. The paper-draft archive is at [[Walker-Paper-v6-Unpublished]].
6. **8-week / 9-version paper auto-diff**: v1 → v2_2 → v2_2-nj (Ji Nie round 1, +13 Chinese inline comments) → v3 (Zhenyu implements +3 equation tables) → v4 (+465 words / +8 refs in 2 days, big expansion) → v5 → v5-nj (Ji Nie round 2) → v6 (+3 refs, final)
7. **Ji Nie methodology arc arc signature**: 
Project paper draft retained internally; advisor and student arrived at a mutual decision not to submit.

### Technical Depth (resume-grade specifics)

- **5-stage HPC pipeline architecture**: (1) CAM3 aqua-planet with prescribed Q-flux → (2) 30-year spin-up on Tianhe-II (undergraduate Tianhe-II account) account (`yhrun -p work -n 48` 48-PE SLURM) → (3) 25 `cal_X/` MATLAB diagnostic folders → (4) NCL stream function + ω analysis → (5) paper figure refinement in MATLAB + Python
- **27,882 MATLAB+NCL lines / 5 languages**: MATLAB (main diagnostics) + NCL (stream function) + Fortran (namelist + CAM3 source mods) + Bash (SLURM runscripts) + Python (paper figure polish)
- **14 Q-flux variants** preserved (D60 / D80 / D100 / D120 / D140 / D160 / D180 + Wonly + Conly + Aqua + variations)
- **20 NCAR CAM3 .F90 source mods** (`SourceMods.zip` 143 KB in Walker `cam3_task/`), aggregate: cldinti / cldsav / cloud_fraction / comctl / ghg_defaults / hb_diff / history / hycoef / ice_constants / inidat / initext / ocn_srf / physpkg / radiation / radlw / runtime_opts / **somoce** (MLDANN 50→30m slab ocean, key dep) / stratiform / tphysbc — undergraduate-level source-code modifications to a GCM

### Academic / Career Significance
- Together with [[PKU-Aerosol-Senior-Thesis]] + [[Caltech-DSCOVR-Research]], constitutes a **3-track parallel Sep-Dec 2021 senior fall** (Walker paper v3→v6 + DSCOVR HBP + nwp_hw 4 assignments ≈ 3-4 deliverable/week)
- Successor to [[PKU-Walker-Hadley-Response-Research]] (Oct 2019 — May 2020, the first project in Ji Nie's group), and competence foundation for the multi-model work in [[UCBerkeley-Romps-Lab]] PhD phase (3-D LES + 1-D DSE+SWTG quasi-2D etc.)
- The research-grade specificity of Walker paper v6 became the bedrock of Zhenyu's later UC Berkeley PhD application + Caltech/UCR Yuk Yung/King-Fai Li collaboration + Princeton SGS invitation
- Moment 2 of the Independent Judgment narrative (held until 2026-06-10) spine (2021-07-13: after the advisor's MSE-budget explanation failed, Zhenyu proposed linear superposition and defended it to Ji Nie's endorsement)

### Skills Used
- [[气候物理与大气科学]] (Walker/Hadley + 4-term energy budget + low-cloud feedback)
- [[高性能计算-HPC]] (Tianhe-II (undergraduate Tianhe-II account) 48-PE + CAM3 aqua-planet 30-yr)
- [[Python-科学计算]] (paper figures + part of the diagnostics)
- [[数值模式源代码修改]] (20 NCAR CAM3 .F90 mods)

### Related Pages
- [[PKU-Undergraduate-Research]] — undergraduate-research umbrella page
- [[PKU-Walker-Hadley-Response-Research]] — predecessor Ji Nie group project (Oct 2019 — May 2020)
- [[Ji-Nie-聂绩]] — Walker project primary PI
- [[Yongyun-Hu-胡永云]] — Walker co-advisor, Hu-group discussion platform
- [[Linear-Superposition-Framework]] — Zhenyu's original framework concept page
- [[2021-07-13-Breakthrough-PPT]] — breakthrough artifact source page
- [[Walker-Paper-v6-Unpublished]] — paper-draft source page
- PKU advisor methodology companion (private) — acknowledgment-edit arc, paired with [[Jing-Li-李婧]]
- [[Multi-Method-Comparison-Spine]] — ω-vs-u methodology rigor attributed to this spine
- Independent Judgment narrative (held until 2026-06-10) — Moment 2 (meta-level)
- [[Academic-Honors-PKU]] — supported by the PKU President Fellowship

### Sources
- `research_wiki/projects/walker_hadley/overview.md` (~55k words / 1303 lines)
- `research_wiki/resume_angles/problem_solving.md` §Project 5
- `research_wiki/resume_angles/technical_depth.md` §Section 9
