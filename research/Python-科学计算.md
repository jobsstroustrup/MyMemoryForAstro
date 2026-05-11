---
title: "Python 科学计算"
description: "Python 科学计算 — 精通级, cross-project scientific code, emcee+healpy+scipy+xarray, 5-language fluency"
publish: true
lang: bilingual
---

# Python 科学计算 (Python Scientific Computing)

## 中文版

### 熟练度
精通

### 描述
以 Python 为主要工具进行科学计算和数据分析。具体能力包括：
- 数值模拟数据的处理与可视化（netCDF、HDF5 格式）
- 数据管线构建（QA 过滤、空间重映射、时间聚合）
- 空间数据加速处理（KD-tree 索引、网格化聚合）
- 统计分析与敏感性实验设计
- MCMC 等反演方法实现

### 🌟 研究级 signature capabilities

**Aggregate scale signature**
- **~175k+ lines total aggregated** 跨 7 年 research (PKU Walker 27,882 MATLAB+NCL lines + PKU Aerosol ~6,400 MATLAB lines + Caltech DSCOVR ~3,000+ lines + PhD 115,363 lines / 62 ipynb / 3,793 code cells — Python 主 + 跨语言 auxiliary)
- **62 ipynb notebooks** in PhD research notebook (UC Berkeley Romps Lab aggregate)

**Multi-language fluency (context-switch discipline)**
- **Caltech DSCOVR 11-month 项目内 5 种语言 fluency**: IDL (Yuk Yung lab OOP MCMC class) + MATLAB (Hansen csvd) + Python (Kawahara CUDA + emcee + healpy) + Mathematica (symbolic 推导) + R (Metropolis-Hastings)
- **PhD 阶段 Fortran 77/90** (NCAR CAM3 + DAM LES source mods, 见 [[数值模式源代码修改]])

**Filename-as-version-control discipline**
- Jupyter notebook 用 filename 编码 methodology version (e.g., `enforceEpsilon_z_iteration_v3.ipynb` — filename encoding methodology iteration)
- Aerosol 代码目录: `hzy_experi1_package_collaborator_revised_now_no_error_above_height_4` (filename 编码 collaboration history)
- 见 Inconvenient Evidence Retention Discipline (private)

**Research-grade Python libraries**
- `emcee` (Foreman-Mackey 2013) MCMC
- `healpy` HEALPix 球面网格
- `scipy.linalg` Cholesky (`assume_a="pos"`) + `slogdet` + SVD
- `KDTree` spatial indexing (TROPOMI 大规模 coordinate match)
- `pandas` / `xarray` / `netCDF4` / `h5py`
- `matplotlib` / `cartopy` geographic plotting

### 在哪些经历中用到
- [[UCBerkeley-Romps-Lab]] — 烟羽动力学诊断管线、敏感性扫描
- [[UCBerkeley-Fung-Lab]] — Sentinel-5P CH4 处理管线、KD-tree 加速
- [[PKU-Undergraduate-Research]] — MCMC 反演、气候模拟分析
- [[PKU-Walker-Circulation-Research]] — figure polishing + diagnostic
- [[PKU-Aerosol-Senior-Thesis]] — MATLAB auxiliary
- [[Caltech-DSCOVR-Research]] — 5-language context switch
- [[Nuclear-Winter-Phase-4p5-Methodology-Workshop]] — 62 ipynb aggregate

---

## English Version

### Proficiency
Expert

### Description
Python as primary tool for scientific computing and data analysis:
- Processing and visualization of numerical simulation data (netCDF, HDF5)
- Data pipeline construction (QA filtering, spatial remapping, temporal aggregation)
- Spatial data acceleration (KD-tree indexing, gridded aggregation)
- Statistical analysis and sensitivity experiment design
- Implementation of inversion methods (MCMC, etc.)

### Used In
- [[UCBerkeley-Romps-Lab]] — plume dynamics diagnostic pipeline, sensitivity sweeps
- [[UCBerkeley-Fung-Lab]] — Sentinel-5P CH4 pipeline, KD-tree acceleration
- [[PKU-Undergraduate-Research]] — MCMC retrieval, climate simulation analysis
- [[PKU-Walker-Circulation-Research]] — figure polishing + diagnostic
- [[PKU-Aerosol-Senior-Thesis]] — MATLAB auxiliary
- [[Caltech-DSCOVR-Research]] — 5-language context switch
- [[Nuclear-Winter-Phase-4p5-Methodology-Workshop]] — 62 ipynb aggregate

### Research-grade signature capabilities

**Aggregate scale signature**
- **~175k+ lines total aggregated** across 7 years of research (PKU Walker 27,882 MATLAB+NCL lines + PKU Aerosol ~6,400 MATLAB lines + Caltech DSCOVR ~3,000+ lines + PhD 115,363 lines / 62 ipynb / 3,793 code cells — Python primary + cross-language auxiliary)
- **62 ipynb notebooks** in PhD research notebook (UC Berkeley Romps Lab aggregate)

**Multi-language fluency (context-switch discipline)**
- **5-language fluency within the 11-month Caltech DSCOVR project**: IDL (Yuk Yung lab OOP MCMC class) + MATLAB (Hansen csvd) + Python (Kawahara CUDA + emcee + healpy) + Mathematica (symbolic derivations) + R (Metropolis-Hastings)
- **Fortran 77/90 in PhD stage** (NCAR CAM3 + DAM LES source mods, see [[数值模式源代码修改]])

**Filename-as-version-control discipline**
- Jupyter notebooks use filename to encode methodology version (e.g., `enforceEpsilon_z_iteration_v3.ipynb` — filename encoding methodology iteration)
- Aerosol code directory: `hzy_experi1_package_collaborator_revised_now_no_error_above_height_4` (filename gloss: "hzy_experi1_package_handed-to-collaborator_revised_now-no-error-when-elevation-over-4"; filename encodes collaboration history)
- See Inconvenient Evidence Retention Discipline (private)

**Research-grade Python libraries**
- `emcee` (Foreman-Mackey 2013) MCMC
- `healpy` HEALPix spherical grid
- `scipy.linalg` Cholesky (`assume_a="pos"`) + `slogdet` + SVD
- `KDTree` spatial indexing (TROPOMI large-scale coordinate match)
- `pandas` / `xarray` / `netCDF4` / `h5py`
- `matplotlib` / `cartopy` geographic plotting
