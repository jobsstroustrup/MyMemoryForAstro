---
title: "GP 贝叶斯反演 (Gaussian Process Bayesian Inversion)"
description: "用高斯过程作先验 + MCMC 对超参数采样的贝叶斯反演框架，与经典 Tikhonov/正则化的对偶关系"
publish: true
lang: bilingual
---

# GP 贝叶斯反演 (Gaussian Process Bayesian Inversion)

> **页面用途**：Zhenyu 2021 年本科末期在 DSCOVR 地球反演项目中实践的贝叶斯反演方法学。和 [[反问题与正则化]] 互为对偶——后者是频率学派视角（选单一"最佳" $\lambda$），本页面是贝叶斯视角（$\lambda$ 是概率变量，用 MCMC 积出来）。

## 中文版

### 定义

**贝叶斯反演 (Bayesian Inversion)**：把反问题 $d = Ax + \epsilon$ 转化为后验分布推断：

$$p(x \mid d) \propto p(d \mid x) \cdot p(x)$$

- **似然** $p(d \mid x)$：由观测模型决定，通常取 $\mathcal{N}(Ax, \Sigma_d)$
- **先验** $p(x)$：表达我们对解的"合理性"期望
- **后验** $p(x \mid d)$：我们真正想要的结果——不只是一个 $\hat{x}$ 的点估计，而是对解的不确定性的完整刻画

**高斯过程先验 (GP Prior)**：$x \sim \mathcal{GP}(0, K(\cdot, \cdot))$。把未知量 $x$ 视作索引在某空间（如球面、时空网格）上的随机函数，核函数 $K$ 编码"相邻点之间应该多相似"的假设。

**共轭性的好处**：若似然是高斯、先验是 GP，则后验也是高斯，均值和协方差有闭式：

$$\hat{x} = K_{xy} (K_{yy} + \Sigma_d)^{-1} d$$
$$\text{Cov}(x \mid d) = K_{xx} - K_{xy}(K_{yy} + \Sigma_d)^{-1} K_{yx}$$

这个闭式后验均值在形式上等价于 Tikhonov 解 $x_\lambda = (A^T A + \lambda I)^{-1} A^T d$（当 $K = \alpha^{-1} I$ 时）——**这是贝叶斯视角与经典正则化的对偶**。

### 核心论点

**1. Tikhonov ≡ 共轭高斯先验下的后验均值**

设 $x \sim \mathcal{N}(0, \alpha^{-1} I)$（各向同性高斯先验），$d \mid x \sim \mathcal{N}(Ax, \sigma^2 I)$。后验均值：
$$\hat{x} = (A^T A + \frac{\sigma^2}{\alpha^{-1}} I)^{-1} A^T d$$
正则化参数 $\lambda = \sigma^2 \alpha$ = **噪声精度 / 先验精度**。这揭示：选 $\lambda$ = 选先验强度。

**2. GP 核函数就是"结构化先验"**

各向同性高斯先验是最弱的结构。换上 RBF kernel $K(p, q) = \exp(-\|p-q\|^2 / 2\ell^2)$ 立刻获得"空间平滑"的强先验——相邻点应该相似。在 Zhenyu 的 DSCOVR 反演里：
- **空间**：在 HEALPix 球面网格上用 RBF，$\ell$ 控制"相信 Earth 的陆海分布有多大尺度的结构"
- **时间**：另一个 RBF kernel $K_T$ 控制"同一地点在时间上变化应该多慢"
- **联合**：用 **separable kernel** $K = K_S \otimes K_T$ 避免全联合协方差的 $O(N^3)$ 计算

**3. 层级贝叶斯：超参数也当成随机变量**

核函数里的超参数（RBF 的 $\ell$ / $\alpha$ / $\sigma$）本身也不确定。两种处理方式：

- **Type-II MLE / Empirical Bayes**：最大化 $p(d \mid \theta) = \int p(d \mid x, \theta) p(x \mid \theta) dx$（边缘似然），取单点 $\hat\theta$
- **Fully Bayesian**：对超参数积分 $p(x \mid d) = \int p(x \mid d, \theta) p(\theta \mid d) d\theta$，用 **MCMC over $\theta$** 近似——Zhenyu 在 [[MCMC-Mapping-GitHub]] 里选了这条路

**4. MCMC 超参数采样的实践要点**
- Affine-invariant ensemble sampler (`emcee`, Foreman-Mackey 2013) 适合中等维度超参数
- **Log-space 重参数化**：`log10_alpha`, `log10_sigma` —— 避免"alpha 跨六个数量级"的采样灾难
- **混合积分**：给定一个 $\theta$ 样本，$x \mid d, \theta$ 是高斯闭式；所以只需要 MCMC 采 $\theta$，然后 for each $\theta^{(k)}$ 取高斯解析 $\hat x_k$ + $\text{Cov}_k$，最后做 Gaussian Mixture approximation —— **这是 rao-blackwell 的思想**
- **数值稳定性**：$K_{yy} + \Sigma_d$ 大且病态，用 Cholesky（`scipy.linalg.solve(..., assume_a="pos")`）而非显式 `inv`；log-determinant 用 `np.linalg.slogdet`

### 不同观点

**频率学派 vs 贝叶斯**
- 频率派选单一 $\lambda$（见 [[反问题与正则化]]）——快、对小问题够用
- 贝叶斯 MCMC 出整个后验分布——慢、但不确定性量化更诚实

**MCMC vs Variational Inference**
- MCMC：收敛到真后验，但慢
- VI：近似后验（mean-field 或 structured），快但偏差不可控
- Zhenyu 当前用 MCMC（问题维度不大，emcee 够用）；VI 若要上生产环境可以考虑

**GP 的计算瓶颈**
- $O(N^3)$ 的 Cholesky 是标准 GP 对 $N \geq 10^4$ 的致命伤
- Separable kernel (`KS ⊗ KT`) 是 Kawahara/Aizawa 脉络下的实用突破
- 更现代：inducing points (SGPR)、random features、KISS-GP、GPyTorch 的 LazyTensor —— 未来扩展方向

### Kawahara / Aizawa 系外行星 Spin-Mapping 脉络（学术谱系）

Zhenyu 的 DSCOVR 地球反演直接借鉴了一条系外行星研究的方法论：
- **Cowan & Agol 2008**：从系外行星总亮度光曲线反演表面纹理可行性分析
- **Kawahara & Fujii 2010** / **Kawahara 2016**：SOT (Spin-Orbit Tomography) 方法提出——把行星自转的光变曲线逆推为表面 albedo map
- **Aizawa 2020 ApJ 896 22** (repo 里有 PDF)：Dynamic SOT 扩展——允许 map 随时间变化（考虑云/季节）
- **Zhenyu 的迁移**：把 SOT 从"观测系外行星"反用到"观测地球"【在Siteng Fan的方法上更进一步】——DSCOVR 在 L1 点看到的地球是个"从外部观测的行星"，完美的方法迁移靶场

这条脉络贴合 Zhenyu PhD 方向（气候 / 行星大气），也是他在 Caltech / UCR 合作里的核心贡献。

### 应用场景

- 从光曲线反演系外行星 / 地球表面图
- 遥感大气反演中的多参数联合不确定性量化
- 气候模拟输出与观测的 data assimilation
- 任何需要"平滑解 + 不确定性量化"的问题

### 开放问题

- **非共轭似然**：若噪声非高斯（如 Poisson 光子计数、Student-t 重尾），闭式后验不可得，需要更复杂的 MCMC 方案
- **实时反演**：DSCOVR 每小时有新观测，是否需要 sequential Bayesian update（Kalman 类方法）而非每次重跑 MCMC？

### 来源

- [[MCMC-Mapping-GitHub]] — 完整代码实现 + 复现 Kawahara/Aizawa 方法 + DSCOVR 真实数据实验
- [[PKU-Undergraduate-Research]] — MCMC Retrieval Methods 项目背景（Yuk Yung / King-Fai Li 指导）
- **教科书**（raw）：Bishop《Pattern Recognition and Machine Learning》2006 — 第 6 章 GP
- **论文**（raw）：Aizawa 2020 ApJ 896 22 — Dynamic SOT
- **隐含论文**：Kawahara & Fujii 2010、Cowan & Agol 2008（本 repo 未直接存但方法被继承）
- **[Future expansion]** Kawahara 系列论文、具体推导细节、Zhenyu 自己写的 Chinese `.docx` 学习笔记

### 相关页面

- [[反问题与正则化]] — 频率学派对偶视角
- [[MCMC-贝叶斯反演]] — skill 页
- [[Python-科学计算]] — emcee / scipy / healpy 实现
- [[卫星遥感与数据处理]] — DSCOVR 数据处理
- [[气候物理与大气科学]] — 应用领域
- [[profile]]

---

## English Version

### Definition

**Bayesian Inversion** recasts the inverse problem as posterior inference:
$$p(x \mid d) \propto p(d \mid x) \cdot p(x)$$
with likelihood $p(d \mid x)$, prior $p(x)$, and the posterior $p(x \mid d)$ as the deliverable (not a point estimate, but full uncertainty quantification).

**Gaussian Process Prior**: $x \sim \mathcal{GP}(0, K)$. Treat the unknown as a random function over some index space (sphere, space-time grid); the kernel $K$ encodes "how similar neighboring points should be."

**Conjugacy**: with Gaussian likelihood + GP prior, the posterior is Gaussian with closed-form mean and covariance:
$$\hat{x} = K_{xy}(K_{yy} + \Sigma_d)^{-1} d, \quad \text{Cov}(x \mid d) = K_{xx} - K_{xy}(K_{yy} + \Sigma_d)^{-1} K_{yx}$$
This closed-form posterior mean is equivalent to the Tikhonov solution when $K = \alpha^{-1} I$ — **the Bayesian dual of classical regularization**.

### Core Arguments

**1. Tikhonov ≡ posterior mean under isotropic Gaussian prior**. $\lambda = \sigma^2 \alpha$ = noise precision / prior precision. Choosing $\lambda$ = choosing prior strength.

**2. GP kernels = structured priors**. Isotropic Gaussian is the weakest. RBF kernel $K(p,q) = \exp(-\|p-q\|^2/2\ell^2)$ gives "spatial smoothness." In DSCOVR retrieval:
- Spatial: RBF on HEALPix sphere, $\ell$ = "how large a scale of structure do we expect on Earth"
- Temporal: separate RBF $K_T$
- **Separable** $K = K_S \otimes K_T$ to avoid $O(N^3)$

**3. Hierarchical Bayes — hyperparameters as random variables**. Either Type-II MLE (marginal likelihood point estimate) or **Fully Bayesian: MCMC over $\theta$**. Zhenyu chose MCMC in [[MCMC-Mapping-GitHub]].

**4. Practical notes on MCMC over hyperparameters**
- Affine-invariant ensemble (`emcee`) for moderate dims
- **Log-space reparameterization** (`log10_alpha`, `log10_sigma`) for scale-spanning params
- **Mixed integration** (Rao-Blackwell): MCMC samples $\theta^{(k)}$; given each, $x \mid d, \theta^{(k)}$ is closed-form Gaussian — mixture approximation for final posterior
- Numerical stability: Cholesky (`scipy.linalg.solve(..., assume_a="pos")`), not `inv`; `slogdet`, not `log(det)`

### Different Perspectives

- **Frequentist vs Bayesian**: point $\lambda$ (fast) vs full posterior (slow, honest UQ)
- **MCMC vs VI**: true posterior slowly vs approximate posterior quickly
- **GP scaling**: $O(N^3)$ Cholesky is the ceiling. Separable kernel is one escape; inducing points / random features / KISS-GP / GPyTorch LazyTensor are modern directions

### Kawahara / Aizawa Exoplanet Spin-Mapping Lineage

Zhenyu's DSCOVR Earth retrieval borrows directly from the exoplanet line:
- **Cowan & Agol 2008**: feasibility of retrieving surface texture from exoplanet light curves
- **Kawahara & Fujii 2010 / Kawahara 2016**: SOT (Spin-Orbit Tomography)
- **Aizawa 2020 ApJ 896 22** (PDF in repo): Dynamic SOT — time-varying maps
- **Zhenyu's transfer**: apply SOT to Earth viewed from L1 (DSCOVR) — a perfect testbed

### Applications

Light-curve → exoplanet/Earth surface maps; multi-parameter atmospheric retrieval UQ; climate-observation data assimilation; any problem needing smooth solution + UQ.

### Open Questions

- Non-conjugate likelihoods (Poisson photon counts, Student-t heavy tails) — no closed-form posterior, need more involved MCMC
- Prior sensitivity: how much does a wrong $\ell$ distort results? Systematic sensitivity study?
- Deep-learning integration: NTK view — infinite-width NN ≡ GP; deep structured GP priors?
- Real-time retrieval: sequential Bayesian update (Kalman-family) rather than batch MCMC each hour?

### Sources

- [[MCMC-Mapping-GitHub]] — code + Kawahara/Aizawa reproduction + DSCOVR experiments
- [[PKU-Undergraduate-Research]] — project background (Yuk Yung / King-Fai Li)
- Textbook (raw): Bishop PRML 2006 — Ch. 6 GP
- Paper (raw): Aizawa 2020 ApJ 896 22 — Dynamic SOT
- Implied papers: Kawahara & Fujii 2010, Cowan & Agol 2008
- **[Future expansion]** Kawahara series papers, derivation details, Zhenyu's own Chinese `.docx` study notes

### Related Pages

- [[反问题与正则化]] — frequentist dual view
- [[MCMC-贝叶斯反演]] — skill page
- [[Python-科学计算]] — emcee / scipy / healpy
- [[卫星遥感与数据处理]] — DSCOVR data pipeline
- [[气候物理与大气科学]] — application domain
- [[profile]]
