---
title: "About — Zhenyu He · Jobs Stroustrup"
publish: true
private: false
lang: bilingual
description: "Physicist-turned-builder. UC Berkeley EPS (2022–2026) and Peking University (2018–2022). Climate dynamics, inverse problems, AI engineering."
---

# Zhenyu He · Jobs Stroustrup

## English Version

### Who I Am

I am Zhenyu He, a physicist-turned-builder working at the intersection of climate physics, inverse problems, and AI-augmented engineering. After completing my Master's degree at UC Berkeley in Spring 2026 in the Department of Earth and Planetary Science, I am transitioning from academic refinement to industry-scale infrastructure work.

Online I also go by the pen name **Jobs Stroustrup** — a small, deliberate homage to two builders whose work shaped my taste: Steve Jobs (product aesthetics, end-to-end ownership of the user experience) and Bjarne Stroustrup (the patient, decade-spanning craftsmanship that produced C++). The dual identity is a compass, not a costume: ship things people can actually use, but build them on foundations meant to last.

### Education

- **UC Berkeley** — Department of Earth and Planetary Science (Aug 2022 – Feb 2026). Completed Master's degree at UC Berkeley in Spring 2026, transitioning to entrepreneurship. Primary advisor: **David Romps**; secondary advisor: **Inez Fung**. Focus: high-resolution fluid dynamics simulations and climate physics.
- **Peking University** — School of Physics, Department of Atmospheric and Oceanic Sciences (Sep 2018 – Jun 2022). Concurrent double degree in Economics at the National School of Development (NSD).

### Current Positioning

I am a **Co-Founder of TerraByte Intelligence (YC Spring 2026)**, a robotics data-collection startup I co-founded in December 2025. As founding CEO I led the team to a Y Combinator Spring 2026 offer. The team chose not to join the batch after weighing the program timing and the company's decision to base operations in China, and I remain a Co-Founder responsible for the U.S. side. Early partnerships included an enterprise agreement with Wanda Group (January 2026). My day-to-day energy is now on **AI safety and AI policy**, alongside the long-running ONE-AGI thread on AI-powered personal effectiveness: how a single technically-fluent person, paired with modern AI tools, can credibly take on what used to require a team. I also continue the climate-physics technical stack as a personal research interest.

In an earlier business-development phase I worked with corporate counterparties whose names appear in this section only because they have explicitly consented to public reference. To honor the company-secret boundary policy, specifics about deal terms, internal team composition, and any non-consented counterparty are out of scope for this page. For TerraByte product or commercial inquiries, please contact the company through its own channels.

### Research Identity (4 Dimensions)

Across roughly seven years (2019–2026), my research record clusters into four threads:

1. **Climate dynamics & high-resolution fluid simulation.** Tropical Walker circulation work in the Ji Nie group at Peking University; a 3,663-word draft paper (eight weeks, nine versions, two advisor passes) preserved in my archive but never submitted. Later, multi-year work with David Romps on nuclear-winter simulations using the DAM 3-D large-eddy-simulation framework, including 8 production runs at ~46k core-hours each, a hydrostatic-balance closure diagnostic that drove residuals from ~85 J/kg down to machine precision (3.58e-5 J/kg), and a "less than 20 lines of new physics" microphysics methodology workshop.
2. **Inverse problems & MCMC retrieval.** From March 2021 to March 2022, I worked with **Yuk Yung** at Caltech and **King-Fai Li** at UC Riverside on the DSCOVR satellite Bayesian retrieval. Highlights: catching a textbook σ² vs σ⁴ scaling bug in Hansen's standard reference (an ~80× overestimate), a pre-whitened L-curve regularization variant, and a "direction of the noise vector" diagnostic I pursued after a literature search returned nothing on the topic. I held the line on the methodology rather than tuning priors to engineer a target λ — a small but load-bearing personal precedent.
3. **Satellite remote sensing & methane MRV.** Work with **Inez Fung** on Sentinel-5P TROPOMI methane anomaly mapping, including a "vernier-caliper" aggregation that pushes effective precision from native 5.5×3.5 km down to ~10.87 m, plus a regression-inversion diagnosis that turned a stubborn 12-month negative slope into a Nebraska-region positive R² ≈ 0.633. Earlier senior thesis with **Jing Li** on first-generation iteratively-coupled MODIS + CALIPSO aerosol retrieval, with lab collaborators on Fernald inversion, MODIS, and tutorials, bridged by **Yuk Yung**. The thesis caught a non-physical CALIPSO L2 bug (negative extinctions on the order of -10⁴ km⁻¹) and improved Beijing-case AOD by 3–20% relative.
4. **Nuclear safety & AI engineering.** In October 2024, I gave an invited talk at Princeton SGS — *"Constraining the Dynamics of Extreme Convection in the Case of Hiroshima"* — to **Frank von Hippel** and a small group of nuclear-security researchers. The Princeton work, plus the cross-cutting Fortran/Python/HPC stack, is being redirected from academic refinement toward industry-scale engineering. Alongside this, I write tools — Selenium scrapers, scientific-computing pipelines, automation scripts — and treat AI tooling as a force multiplier rather than a separate discipline.

A common theme across all four: **multi-method comparison** (running 3+ independent approaches against the same problem), preserving inconvenient evidence next to convenient evidence in the repository, and a preference for catching one's own mistakes in code review before they reach a paper.

### Publications and Preprints

**Agents' Last Exam (ALE)**. Co-author (Data Contributors group). A 1,000+-task agent benchmark spanning 55 specialized domains, from UC Berkeley RDI (Dawn Song lab). I built and evaluated agent tasks in the natural-science domain. Submission under review, NeurIPS 2026 Evaluations and Datasets (E&D) Track. arXiv:2606.05405 (https://arxiv.org/abs/2606.05405).

### Manuscripts Under Review

These are listed with title, author position, and journal only, pending peer review.

- "A cloud-resolving simulation of the Hiroshima firestorm plume." First author. Corresponding author David Romps. Under review at JGR-Atmospheres, 2026.
- "A lower bound on the altitude of the Hiroshima firestorm plume from ray optics." Third author. Corresponding author David Romps. Under review at Geophysical Research Letters (GRL), 2026.

### Mentor Influences

I am openly grateful to the following advisors and collaborators for shaping how I think:

- **Ji Nie (聂绩)** — Peking University, climate dynamics. My first research advisor; the lab where I learned what "research" means, and where I drafted my first long-form paper.
- **Jing Li (李婧)** — Peking University, atmospheric remote sensing. Senior thesis advisor; taught me to keep the inconvenient evidence in the same folder as the favorable evidence.
- **Yuk Yung** — Caltech, planetary atmospheres. Collaborator and bridge across the Caltech / UCR / PKU triangle from 2021–2022.
- **King-Fai Li** — UC Riverside, DSCOVR retrieval. Day-to-day collaborator on the MCMC inverse-problem work.
- **David Romps** — UC Berkeley, atmospheric convection. PhD primary advisor; the source of the "less than 20 lines of new physics" discipline.
- **Inez Fung** — UC Berkeley, biogeochemistry. PhD secondary advisor; the methane MRV work is hers.
- **Frank von Hippel** — Princeton SGS, nuclear security. Host of the October 2024 invited talk.
- Lab collaborators on the PKU aerosol senior thesis (acknowledged with explicit consent in the original thesis).
- **Lixiang Gu (顾理想)** — collaborator on an earlier research line.

Other lab mates and collaborators are deliberately not named here — names appear on this page only with explicit personal consent.

### Languages & Contact

- **Languages**: native Mandarin Chinese; fluent professional English (research writing, technical talks, and day-to-day collaboration); reading-level scientific French as a side interest.
- **Contact**: `zhenyuhe@berkeley.edu` is the right inbox for substantive email. I prefer asynchronous email over real-time channels for first contact — it gives me time to give a real answer instead of a fast one. For research correspondence, please put a one-line summary at the top; I read and reply faster when the ask is in the first paragraph.
- **Methodology for getting a useful reply**: tell me what you have already tried, what specific question you want me to answer, and what would constitute a "good" response. This is the same discipline I apply when emailing senior collaborators — it is the cheapest possible courtesy and it works.
- **Profiles**: ORCID 0009-0005-1942-9469 (https://orcid.org/0009-0005-1942-9469); Google Scholar (https://scholar.google.com/citations?user=OK6sAb0AAAAJ).

### What I Am Not Doing

To keep this page honest about scope: I am not currently taking consulting work, and I am not advertising specific services. The climate-physics work continues as a personal interest. For TerraByte product details or current commercial inquiries, please contact the company directly through its own channels.

### Looking for the 2021 version of this site?

This is the 2026 rebuild. The original site (2020–2021, ~33 undergraduate-era posts and a Portraits / Sceneries photo gallery) is preserved verbatim at **[`/archive/`](/archive/)** as a frozen snapshot — content stopped updating 2021-10-31. The archive includes the photo galleries, AV (classical-music samples), and the personal narrative I was working through as an undergraduate. The downloadable resume in the archive `/about/` has been updated to the current version; everything else is the 2021 incarnation.

---

## 中文版

### 关于我

我是贺震昱（Zhenyu He），一个从物理学转向工程与建造的人，在气候物理、反演问题、AI 增强工程的交叉地带做事。2026 年春季于 UC Berkeley Earth and Planetary Science Department 完成 Master 学位，正在从学术雕琢转向产业级基础设施。

我同时使用笔名 **Jobs Stroustrup**，是对两位塑造了我审美的人的小小致敬：Steve Jobs（产品美学，对用户体验端到端的所有权）和 Bjarne Stroustrup（耐心、跨越数十年磨成 C++ 的工艺）。这个双名是罗盘而不是戏服：做出真正能用的东西，但要把它建在长久的基础上。

### 教育背景

- **UC Berkeley** — Earth and Planetary Science Department（2022 年 8 月 – 2026 年 2 月）。2026 年春季于 UC Berkeley 完成 Master 学位，转向创业实践。主导师 **David Romps**，副导师 **Inez Fung**。方向：高分辨率流体动力学模拟与气候物理。
- **北京大学** — 物理学院大气与海洋科学系（2018 年 9 月 – 2022 年 6 月）。同时在国家发展研究院（NSD）修读经济学双学位。

### 当前定位

我是 **TerraByte Intelligence 联合创始人（YC Spring 2026）**。这家机器人数据采集创业公司由我在 2025 年 12 月联合创办。作为创始 CEO，我带领团队拿到 Y Combinator Spring 2026 offer。团队在权衡 program timing 与公司将主体运营设在中国之后，选择不加入该批次，我仍作为联合创始人负责美国一侧。早期合作包括与万达集团达成的企业合作（2026 年 1 月）。我目前的主要精力放在 **AI 安全与 AI 政策** 上，同时延续长期跟进的 ONE-AGI 主线（AI 赋能的个人效率）：一个技术上有发言权的人，结合现代 AI 工具，能否可信地承担过去需要一个团队才能做的事。我也把气候物理这套技术栈作为个人研究兴趣继续往下走。

在更早的商务拓展阶段，我与企业对手方有过数据合作。这些公司的名字仅在已获得明确公开同意的前提下才会出现。出于商业机密边界政策的考虑，具体的合作条款、内部团队结构、以及未经同意的任何对手方都不在本页讨论范围内。TerraByte 的产品与商务咨询请通过公司官方渠道联系。

### 研究身份（4 个维度）

在大约 7 年（2019–2026）的研究记录里，我的工作集中在四条线索上：

1. **气候动力学与高分辨率流体模拟。** 在北京大学聂绩（Ji Nie）组做热带 Walker 环流，写出了一篇 3663 词、8 周、9 版、两轮导师审阅的长文，留作个人存档但未投稿。之后在 David Romps 组做核冬天模拟，使用 DAM 3-D 大涡模拟框架，完成 8 次 production runs（每次约 46k core-hours），开发了静力平衡闭合诊断（残差从 ~85 J/kg 收敛到机器精度 3.58e-5 J/kg），并完成了一次"小于 20 行新物理"的微物理方法论 workshop。
2. **反演问题与 MCMC 检索。** 2021 年 3 月到 2022 年 3 月，与 Caltech 的 **Yuk Yung** 和 UC Riverside 的 **King-Fai Li** 一起做 DSCOVR 卫星贝叶斯检索。亮点：在 Hansen 教科书参考公式中抓出 σ² vs σ⁴ 数量级 bug（约 80 倍过估）、做了一种 pre-whitened L 曲线正则化变体、从零开始研究"噪声向量方向"这一文献中无人涉足的诊断角度。我坚持方法论原则，没有为达到某个目标 λ 而调超参 —— 一个虽小但承重的个人先例。
3. **卫星遥感与甲烷 MRV。** 与 **Inez Fung** 一起做 Sentinel-5P TROPOMI 甲烷异常制图，包括"游标卡尺"聚合（把原生 5.5×3.5 km 精度推到约 10.87 m）和回归反演诊断（把固执的 12 月负斜率扭转为 Nebraska 区域正向 R² ≈ 0.633）。更早在 **Jing Li**（李婧）组做的本科毕业论文是首批迭代耦合的 MODIS + CALIPSO 气溶胶反演工作，由实验室合作者在 Fernald 反演、MODIS、教学方面提供支持，由 **Yuk Yung** 桥接。论文捕捉到 CALIPSO L2 一个非物理 bug（量级 -10⁴ km⁻¹ 的负消光），并将北京案例 AOD 相对改进 3–20%。
4. **核安全与 AI 工程。** 2024 年 10 月，受邀在 Princeton SGS 做演讲 —— *"Constraining the Dynamics of Extreme Convection in the Case of Hiroshima"* —— 听众是 **Frank von Hippel** 和一群核安全研究者。这条 Princeton 主线，加上跨越 Fortran/Python/HPC 的技术栈，正在从学术雕琢转向产业级工程。与此同时我写工具 —— Selenium 抓取脚本、科学计算 pipeline、自动化脚本 —— 把 AI 工具当作放大器而不是另一个独立学科。我也曾参与 **顾理想（Lixiang Gu）** 的研究线。

四条线的共同主题：**多方法比较**（同一问题用 3+ 种独立方法跑一遍）、**保留不利证据**（在 repo 里把不方便的结果文件留在方便的旁边）、并且偏爱在自己代码评审里抓出错误而不是让它进入论文。

### 论文与预印本

**Agents' Last Exam (ALE)**。共同作者（Data Contributors 组）。一个覆盖 55 个专业领域、超过 1,000 项任务的 agent benchmark，出自 UC Berkeley RDI（Dawn Song 实验室）。我负责构建并评估自然科学领域的 agent 任务。论文投稿，审稿中，NeurIPS 2026 Evaluations and Datasets (E&D) Track。arXiv:2606.05405（https://arxiv.org/abs/2606.05405）。

### 审稿中的手稿

以下仅列出标题、作者位次与期刊，论文尚在同行评审中。

- "A cloud-resolving simulation of the Hiroshima firestorm plume"。第一作者。通讯作者 David Romps。审稿中，JGR-Atmospheres，2026。
- "A lower bound on the altitude of the Hiroshima firestorm plume from ray optics"。第三作者。通讯作者 David Romps。审稿中，Geophysical Research Letters (GRL)，2026。

### 导师影响

我对以下导师与合作者公开表达感谢，他们塑造了我思考的方式：

- **聂绩（Ji Nie）** —— 北京大学，气候动力学。我的第一位研究导师，让我学会了"研究"是什么，也是我写第一篇长文的实验室。
- **李婧（Jing Li）** —— 北京大学，大气遥感。本科毕业论文导师，教会我把不利证据和有利证据放在同一个文件夹里。
- **Yuk Yung** —— Caltech，行星大气。2021–2022 年间桥接 Caltech / UCR / PKU 三角的合作者。
- **King-Fai Li** —— UC Riverside，DSCOVR 检索。MCMC 反演工作的日常合作者。
- **David Romps** —— UC Berkeley，大气对流。博士主导师，"小于 20 行新物理"这条纪律的来源。
- **Inez Fung** —— UC Berkeley，生物地球化学。博士副导师，甲烷 MRV 工作的源头。
- **Frank von Hippel** —— Princeton SGS，核安全。2024 年 10 月受邀演讲的主持人。
- 北大气溶胶毕设的实验室合作者（致谢已在原毕设中列出）。
- **顾理想（Lixiang Gu）** —— 一条更早研究线上的合作者。

其他实验室同事和合作者刻意没有列在本页 —— 名字出现在这一页的前提是已获得明确的个人同意。

### 语言与联系方式

- **语言**：母语普通话；流利的专业英语（研究写作、技术演讲、日常协作）；阅读级科学法语作为业余兴趣。
- **联系方式**：`zhenyuhe@berkeley.edu` 是处理实质邮件的正确收件箱。首次联系我偏好异步邮件而不是即时通讯 —— 这给我足够时间给你一个真正的回答，而不是一个快速的回答。研究类邮件请把一行摘要放在最上面；问题在第一段时我读得快、回得快。
- **如何让我给出有用回复的方法论**：告诉我你已经试过什么、希望我具体回答什么问题、什么样的回答对你算"好"。这是我在写信给资深合作者时同样会用的纪律 —— 是最便宜的礼貌，也是最管用的。
- **学术主页**：ORCID 0009-0005-1942-9469（https://orcid.org/0009-0005-1942-9469）；Google Scholar（https://scholar.google.com/citations?user=OK6sAb0AAAAJ）。

### 我不在做什么

为了让本页对自己的范围保持诚实：我目前不接咨询工作，也不在本页推销具体服务。气候物理工作以个人兴趣的形式继续。TerraByte 的产品信息或当前商务合作请通过公司自己的渠道联系。

### 想看 2021 版本的网站？

这是 2026 年的重建版。原版网站（2020–2021，约 33 篇本科期间博文 + Portraits / Sceneries 摄影画廊）以冻结快照的形式完整保留在 **[`/archive/`](/archive/)** —— 内容停留在 2021-10-31。archive 包括摄影画廊、AV（古典音乐曲选）、本科期间正在思考的个人叙事。archive 中 `/about/` 的可下载简历已更新到当前版本；其他所有内容仍是 2021 年的形态。
