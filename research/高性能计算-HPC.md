---
title: "高性能计算 HPC"
description: "HPC — proficient (uncommon for an undergraduate), Tianhe-II SLURM + CAM3 aqua-planet, Lawrencium 46k core-hours"
publish: true
lang: bilingual
---

# 高性能计算 HPC (High Performance Computing)

## 中文版

### 熟练度
熟练

### 描述
- 大涡模拟 (LES) 运行与调试（DAM 模型），单次运行约 46k core-hours
- 代码扩展：添加诊断输出变量、新的 forcing 逻辑、I/O 节奏优化
- 计算资源规划：在算力预算内设计可执行的敏感性实验方案
- 理想化水球模拟 (aquaplanet simulations)

### 🌟 研究级 signature capabilities

**PKU 本科 HPC infra mastery (2020-2021)**
- **Tianhe-II NSCC-GZ**: 3 accounts ((undergraduate Tianhe-II account) primary + 2 更多 Walker variants) `yhrun -p work -n 48` 48-PE SLURM (~本科生少见)
- **CAM3 aqua-planet 30-yr spin-up runs × 10 cases** (D60-180 + Wonly + Conly + Aqua, 每 case 30 year integration)
- **27,882 MATLAB+NCL analysis lines** + 5-stage HPC pipeline architecture (CAM3 aqua-planet → Tianhe-II runs → 25 cal_X MATLAB diagnostic → NCL stream function + ω analysis → Python figure polish)

**UC Berkeley PhD HPC mastery (2022-2025)**
- **Lawrencium LBNL cluster**: 8 production runs × ~46k core-hours each ≈ 44 days HPC wall time 工程规划
- **DAM quasi-2D arrays Lx 20km-50000km** scan (Phase 4.5 killer figure convergence)
- **115,363 Jupyter notebook lines / 62 ipynb / 3,793 code cells** aggregate (PhD analysis code)

**Cross-language HPC tooling**
- **Fortran 77/90**: NCAR CAM3 v3.1 source tree (615 .F90 files) + DAM LES source (40+ modules) 级 source code 理解
- **Python/MATLAB/R/NCL/IDL/Mathematica**: 跨语言 scientific computing (Caltech DSCOVR 5-language fluency)
- **remote workstation CUDA bootstrap** (Caltech, Windows CUDA incompatibility → manual CUDA driver + Anaconda bootstrap)

### 方法论 concept 页

- [[数值模式源代码修改]]
- [[Multi-Method-Comparison-Spine]]

### 在哪些经历中用到
- [[UCBerkeley-Romps-Lab]] — DAM 模型 3D LES，46k core-hours/run
- [[PKU-Undergraduate-Research]] — 理想化水球模拟
- [[PKU-Walker-Circulation-Research]] — Tianhe-II 48-PE + CAM3 aqua-planet
- [[Caltech-DSCOVR-Research]] — (remote workstation) bootstrap + 5-language
- [[Nuclear-Winter-Phase-4p5-Methodology-Workshop]] — Lawrencium production runs

---

## English Version

### Proficiency
Proficient

### Description
- Large Eddy Simulation (LES) execution and debugging (DAM model), ~46k core-hours per run
- Code extension: adding diagnostic output variables, new forcing logic, I/O cadence optimization
- Compute resource planning: designing tractable sensitivity plans within compute budgets
- Idealized aquaplanet simulations

### Used In
- [[UCBerkeley-Romps-Lab]] — DAM model 3D LES, 46k core-hours/run
- [[PKU-Undergraduate-Research]] — idealized aquaplanet simulations
- [[PKU-Walker-Circulation-Research]] — Tianhe-II 48-PE + CAM3 aqua-planet
- [[Caltech-DSCOVR-Research]] — (remote workstation) bootstrap + 5-language
- [[Nuclear-Winter-Phase-4p5-Methodology-Workshop]] — Lawrencium production runs

### Research-grade signature capabilities

**PKU undergraduate HPC infra mastery (2020-2021)**
- **Tianhe-II NSCC-GZ**: 3 accounts ((undergraduate Tianhe-II account) primary + 2 more Walker variants); `yhrun -p work -n 48` 48-PE SLURM (rare for an undergraduate)
- **CAM3 aqua-planet 30-yr spin-up runs × 10 cases** (D60-180 + Wonly + Conly + Aqua, each case a 30-year integration)
- **27,882 MATLAB+NCL analysis lines** + 5-stage HPC pipeline architecture (CAM3 aqua-planet → Tianhe-II runs → 25 cal_X MATLAB diagnostics → NCL stream function + ω analysis → Python figure polish)

**UC Berkeley PhD HPC mastery (2022-2025)**
- **Lawrencium LBNL cluster**: 8 production runs × ~46k core-hours each ≈ 44 days HPC wall time engineering plan
- **DAM quasi-2D arrays Lx 20km-50000km** scan (Phase 4.5 killer-figure convergence)
- **115,363 Jupyter notebook lines / 62 ipynb / 3,793 code cells** aggregate (PhD analysis code)

**Cross-language HPC tooling**
- **Fortran 77/90**: source-code-level understanding of NCAR CAM3 v3.1 source tree (615 .F90 files) + DAM LES source (40+ modules)
- **Python/MATLAB/R/NCL/IDL/Mathematica**: cross-language scientific computing (Caltech DSCOVR 5-language fluency)
- **remote workstation CUDA bootstrap** (Caltech, Windows CUDA incompatibility → manual CUDA driver + Anaconda bootstrap)

### Methodology concept pages

- [[数值模式源代码修改]]
- [[Multi-Method-Comparison-Spine]]
