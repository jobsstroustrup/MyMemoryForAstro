---
title: "L-Curve Axis-Scale Ambiguity (Hansen σ² vs σ⁴ bug catch)"
description: "Caltech DSCOVR retrieval (2022-01-08): undergraduate-stage discovery of a σ² vs σ⁴ ambiguity in Hansen's L-curve curvature formula causing 80× λ overestimate"
publish: true
lang: bilingual
---

# L-Curve Axis-Scale Ambiguity (Hansen σ² vs σ⁴ bug catch)

> **页面用途**: Caltech DSCOVR retrieval 项目 (2021.03–2022.03, Yuk Yung + King-Fai Li 指导) Zhenyu 作为本科生 2022-01-08 group meeting 上展示的技术发现 — 在 Hansen *Discrete Inverse Problems* (SIAM 2010, foundational textbook) 中发现公式级 bug 并独立识别其深层原因为 axis-scale ambiguity。

## 中文版

### 定义

**L-Curve Axis-Scale Ambiguity** 是 Zhenyu 2022-01-08 在 Caltech DSCOVR 项目 group meeting 上 formal articulate 的 structural limitation of classical L-curve method:

1. **Hansen 公式层 bug**: Hansen *Discrete Inverse Problems* (SIAM 2010) 中 log-log L-curve curvature 公式的分母应为 $\sigma_i^4$ (filter factor 导数展开的 chain-rule denominator), 但书中 **写成了 $\sigma_i^2$** — 不是 typo, 而是导致实际计算最佳 λ **80× overestimate** 的 systematic bug
2. **Axis-scale ambiguity (深层原因)**: Hansen 讨论 L-curve 的"拐角识别"时, **未讨论 x-axis 与 y-axis 单位是否应 commensurate** — "naked-eye elbow" 不是 scale-invariant (visual artifact), 即使公式写对了, 不同 axis scaling 下 computed curvature 最大值和 naked-eye elbow 会不一致

> *"Hansen didn't talk about whether we should control the units of x-axis and y-axis of L-curve to be the same. In his book, he showed two L-curve figures, but both didn't control the units to be the same."* — Zhenyu 2022-01-08 group meeting

### 80× 数值对比 (核心证据)

同一 toy model + 同一 DSCOVR PC2 real data, 同时跑 Hansen 书本公式 vs Hansen 学生 (某学生) 正确公式:

| Formula | Toy model best λ | PC2 best λ | 准确性 |
|---------|-----------------|-----------|--------|
| **Hansen 学生正确版 (分母 $\sigma_i^4$)** | **0.0251** ✓ | **0.0575** ✓ | 与 naked-eye elbow + `axis image` 下理论值一致 (Toy); 与 axis-image 下 $x = -1.337$ 一致 (PC2) |
| **Hansen 书本错误版 (分母 $\sigma_i^2$)** | **1.995** ✗ | **1.995** ✗ | **80× overestimate**, 完全失败 (PC2 上甚至**不依赖数据, 恒为 1.995**) |

**Zhenyu 的独立数学验证** (`Deductions of the curvature of log-log Lcurve.docx`, 36-paragraph 完整推导):

- 从 SVD $A = U \Sigma V^T$ + filter factors $f_i = \sigma_i^2 / (\sigma_i^2 + \lambda^2)$ 开始
- 推导 $\ln \|x_\lambda\|$ 和 $\ln \|A x_\lambda - b\|$ 关于 $\mu = \ln \lambda$ 的一阶、二阶导
- 关键一步: denominator of chain-rule expansion has $\sigma_i^4$ (原文 *"The denominator should have $\sigma_i^4$ instead of $\sigma_i^2$"*)
- 完整公式结构 (符号推导 39 paras) → Hansen 学生公式与 Zhenyu 独立推导一致

**Zhenyu 的 intuition diagnosis** (from `lcurve_test.docx`, 84 paras):

> *"Eta_u 在 u 大的时候, 相对比较小, rho_u 在 miu 大的时候, 近乎是一个不变的常数。所以如果把分母的 u⁴ 错误写成了 u², 那么在 u > 1 的区间内, 分母被低估了, 整个分式结果被高估了。但是如此高引用的文章, 居然有这样的问题"*

### 3-step self-correction cycle (11/29 → 12/06 → 01/08)

体现 Zhenyu 的 intellectual honesty + research iteration:

**Step 1 — 2021-11-29 group meeting (slide 4)**: 发现自己公式算出的 curvature 最大值不在 naked-eye elbow 位置 — 承认"自己公式错" 作为初步 hypothesis

**Step 2 — 2021-12-06 group meeting (slide 6)**: 假设 "accumulation of numerical errors during 9600×3200 matrix computation" 是 root cause — 这是一个 **physically reasonable 但其实 wrong 的 hypothesis**, 在 PPT 上 explicit 写出

**Step 3 — 2022-01-08 group meeting (breakthrough)**: Refute Step 2 的 "accumulation of errors" hypothesis, 正确归因为 **axis-scale ambiguity** — naked-eye elbow 本身不是 scale-invariant

> *"What if our naked eyes are wrong, but the calculated curvature is right?"*

**5-cell 手算演示** (2022-01-08 PPT): Zhenyu 给出一个手算示例, 明确 demonstrate 同一 L-curve 在不同 axis scaling 下 (matplotlib 默认 vs matlab `axis image`) "naked-eye elbow" 位置不同, 但真实 curvature maximum (公式正确版计算) 不变 → 证明 **naked-eye elbow IS NOT scale-invariant**。

### inconvenient-evidence retention (物理证据纪律)

Zhenyu 在 `LCurve_HansenMistake_WeRectify_Test/` 子目录 **同时保留两个 PDF 文件并列**:

- `Hansen自己文章_仍然mu二次方.pdf` — Hansen 自己书中公式 (分母 $\sigma^2$, **Zhenyu 判定错误**)
- `hansen学生mu四次方.pdf` — Hansen 学生 (某 Student Formula) 版本 (分母 $\sigma^4$, **Zhenyu 判定正确**)

这是 **"inconvenient-evidence retention"** 精神: 不把 Hansen 书本的错误 PDF 删掉, 而是与修正版并列保存 — 为后续读者提供直接 visual diff 的 raw material。同一目录还有:

- 5 个嵌套 test 子目录 (toy model / PC2 / 2 prior-whitening variants / DSCOVR stress test)
- 每个 test 含 `cal_curv_bydata_PC2.m` + `knee_pt.m` + `spline_test.m` MATLAB 代码 + .mat 数据 + .png plot
- `lcurve_test.docx` (84 paras) + `Deductions of the curvature of log-log Lcurve.docx` (36 paras) 两份学习笔记

### 3 open questions to community (Zhenyu 提出)

在 2022-01-08 PPT 结尾, Zhenyu 明确向 L-curve community 提出 3 个 open questions, 明示 Hansen 未讨论的 structural boundary:

1. **应否 control L-curve axes 等单位?** — matplotlib / matlab 默认不 enforce same axis scale, 但 curvature 是 scale-dependent; 应否 standardize?
2. **a senior collaborator 的 elbow $\lambda = 10^{-3}$ 结论是否为 scale-artifact?** — DSCOVR PC2 case 和 Kawahara's toy 的 elbow $\approx 10^{-3}$, **可能只是巧合** (因为 naked-eye judgment 对 scale 敏感) — 不应 over-trust
3. **应用 L-curve 时在哪些情况下调节, 如何调?** — 提供 guideline 让未来使用者知道何时 naked-eye OK, 何时必须校正 axis-scale

→ 这是**指出成名方法的未讨论边界**的 research maturity — 一般的本科生或硕士生不会意识到这种问题。

### 开放问题

`[待补充]` 未来如 L-curve community 回复这 3 个 open questions, 或 Zhenyu 将"axis-scale ambiguity" 的 full 数学论证 submit arxiv / 发信给 Hansen 本人, 回填 community reaction + 正式论证 PDF

- **Generalization to other regularization methods**: L-curve 的 axis-scale 问题是否也存在于 other log-log graphical diagnostics (e.g., Picard plot, filter factor plot)?
- **Curvature formula canonical form**: `Deductions of the curvature of log-log Lcurve.docx` 36-paragraph 推导的"正确" curvature formula 是否 community 已有 published correction? 若无, 是否值得 Zhenyu 独立写短文 submit?

### 来源

- `research_wiki/projects/mcmc_retrieval/overview.md` §贡献 (c) "Find Maximum Curvature only by the data" (2022-01-08, theoretical + numerical)
- `research_wiki/projects/mcmc_retrieval/overview.md` §💎 P3 新发现 1: Zhenyu 直接发现 Hansen 教科书里的公式错误 (σ² vs σ⁴)
- `research_wiki/projects/mcmc_retrieval/overview.md` §2021-11-29 → 2021-12-06 catch own bug + self-audit (3-step cycle)
- `research_wiki/projects/mcmc_retrieval/overview.md` §3 open questions to community
- `LCurve_HansenMistake_WeRectify_Test/` — 物理证据并列目录 (Hansen 原版 PDF + Hansen 学生 PDF + 5 test 子目录 + `lcurve_test.docx` 84 paras + `Deductions of the curvature of log-log Lcurve.docx` 36 paras)
- Hansen, P. C. *Discrete Inverse Problems: Insight and Algorithms* (SIAM 2010) — 原教科书, Zhenyu 发现其公式 bug 的 source
- 2022-01-08 group meeting PPT (P2) "Find Max Curvature only by data" — axis-scale 发现 + 3 open questions 正式 present
- `[待补充]` Zhenyu research-angle 独立 wiki 中 `Deductions of the curvature of log-log Lcurve.docx` 完整 36-段 SVD + filter factor chain-rule 推导 (合并后此页可贴出 full symbolic derivation)
- `[待补充]` 如 Zhenyu 未来 submit 正式论证 (arxiv preprint or letter to Hansen), 回填 artifact link

### 相关页面

- [[MCMC-贝叶斯反演]] — skill 页 (含 Caltech DSCOVR 4 原创贡献 subsection, 本 concept 对应贡献 (c))
- [[反问题与正则化]] — parent concept (L-curve 是其 4 个 regularization parameter selection 方法之一, axis-scale ambiguity 是其 未讨论 structural limitation)
- [[Hardened-Balancing-Principle]] — sibling concept (同 batch 建立的 DSCOVR 技术发现, HBP 避开了 L-curve 的 axis-scale 问题)
- [[Caltech-DSCOVR-Research]] — 项目 experience page (从 PKU-Undergraduate-Research 拆出)
- [[Independent Judgment narrative (private)]] — 这是 technical-level judgment moment: 本科生挑战 published textbook + 3-step self-correction + 正式 articulate open questions
- [[Yuk-Yung]] — PI (Caltech)
- [[King-Fai-Li]] — co-advisor (UCR)
- [[profile]]

---

## English Version

### Definition

**L-Curve Axis-Scale Ambiguity** is a structural limitation of the classical L-curve method, formally articulated by Zhenyu at the Caltech DSCOVR project's 2022-01-08 group meeting:

1. **Hansen formula-level bug**: in Hansen's *Discrete Inverse Problems* (SIAM 2010), the denominator of the log-log L-curve curvature formula should be $\sigma_i^4$ (the chain-rule denominator from the filter-factor derivative expansion), but the book **writes it as $\sigma_i^2$** — not a typo, but a systematic bug that causes the actual computed best λ to be **80× overestimated**
2. **Axis-scale ambiguity (deeper cause)**: when discussing "corner identification" of L-curve, Hansen **does not discuss whether the units of x-axis and y-axis should be commensurate** — the "naked-eye elbow" is not scale-invariant (a visual artifact); even if the formula is correct, under different axis scaling the maximum of the computed curvature and the naked-eye elbow will not agree

> *"Hansen didn't talk about whether we should control the units of x-axis and y-axis of L-curve to be the same. In his book, he showed two L-curve figures, but both didn't control the units to be the same."* — Zhenyu 2022-01-08 group meeting

### 80× Numerical Comparison (core evidence)

For the same toy model + same DSCOVR PC2 real data, simultaneously running Hansen's textbook formula vs Hansen's student's correct formula:

| Formula | Toy model best λ | PC2 best λ | Accuracy |
|---------|-----------------|-----------|--------|
| **Hansen student correct version (denominator $\sigma_i^4$)** | **0.0251** ✓ | **0.0575** ✓ | Consistent with naked-eye elbow + theoretical value under `axis image` (Toy); consistent with $x = -1.337$ under axis-image (PC2) |
| **Hansen book wrong version (denominator $\sigma_i^2$)** | **1.995** ✗ | **1.995** ✗ | **80× overestimate**, completely fails (on PC2 even **independent of data, constantly 1.995**) |

**Zhenyu's independent mathematical verification** (`Deductions of the curvature of log-log Lcurve.docx`, 36-paragraph complete derivation):

- Starting from SVD $A = U \Sigma V^T$ + filter factors $f_i = \sigma_i^2 / (\sigma_i^2 + \lambda^2)$
- Deriving first- and second-order derivatives of $\ln \|x_\lambda\|$ and $\ln \|A x_\lambda - b\|$ with respect to $\mu = \ln \lambda$
- Key step: denominator of chain-rule expansion has $\sigma_i^4$ (verbatim *"The denominator should have $\sigma_i^4$ instead of $\sigma_i^2$"*)
- Complete formula structure (39-paragraph symbolic derivation) → Hansen student's formula is consistent with Zhenyu's independent derivation

**Zhenyu's intuition diagnosis** (from `lcurve_test.docx`, 84 paragraphs):

> *"Eta_u 在 u 大的时候, 相对比较小, rho_u 在 miu 大的时候, 近乎是一个不变的常数。所以如果把分母的 u⁴ 错误写成了 u², 那么在 u > 1 的区间内, 分母被低估了, 整个分式结果被高估了。但是如此高引用的文章, 居然有这样的问题"*
>
> (English gloss: When u is large, Eta_u is relatively small; when miu is large, rho_u is nearly a constant. So if the u⁴ in the denominator is mistakenly written as u², then in the u > 1 interval the denominator is underestimated and the whole fraction result is overestimated. Yet such a highly cited paper has this kind of issue.)

### 3-step self-correction cycle (11/29 → 12/06 → 01/08)

Embodies Zhenyu's intellectual honesty + research iteration:

**Step 1 — 2021-11-29 group meeting (slide 4)**: discovered that the curvature maximum computed by his own formula was not at the naked-eye elbow location — admitted "my formula is wrong" as an initial hypothesis

**Step 2 — 2021-12-06 group meeting (slide 6)**: hypothesized that "accumulation of numerical errors during 9600×3200 matrix computation" was the root cause — this was a **physically reasonable but actually wrong hypothesis**, written explicitly on the PPT

**Step 3 — 2022-01-08 group meeting (breakthrough)**: refuted the "accumulation of errors" hypothesis from Step 2, correctly attributing it to **axis-scale ambiguity** — the naked-eye elbow itself is not scale-invariant

> *"What if our naked eyes are wrong, but the calculated curvature is right?"*

**5-cell hand-calculation demo** (2022-01-08 PPT): Zhenyu provided a hand-calculation example explicitly demonstrating that the same L-curve under different axis scalings (matplotlib default vs matlab `axis image`) has different "naked-eye elbow" positions, but the true curvature maximum (computed with the correct formula) is unchanged → proving **the naked-eye elbow IS NOT scale-invariant**.

### inconvenient-evidence retention (physical evidence discipline)

In the `LCurve_HansenMistake_WeRectify_Test/` subdirectory, Zhenyu **preserves both PDF files side by side**:

- `Hansen自己文章_仍然mu二次方.pdf` (filename gloss: "Hansen's own article — still mu squared.pdf") — Hansen's own book formula (denominator $\sigma^2$, **judged wrong by Zhenyu**)
- `hansen学生mu四次方.pdf` (filename gloss: "Hansen student — mu fourth power.pdf") — Hansen's student (a Student Formula) version (denominator $\sigma^4$, **judged correct by Zhenyu**)

This is the **"inconvenient-evidence retention"** spirit: not deleting the wrong PDF from Hansen's book but preserving it side by side with the corrected version — providing direct visual-diff raw material for subsequent readers. The same directory also contains:

- 5 nested test subdirectories (toy model / PC2 / 2 prior-whitening variants / DSCOVR stress test)
- Each test contains `cal_curv_bydata_PC2.m` + `knee_pt.m` + `spline_test.m` MATLAB code + .mat data + .png plots
- `lcurve_test.docx` (84 paragraphs) + `Deductions of the curvature of log-log Lcurve.docx` (36 paragraphs), two study notes

### 3 open questions to community (proposed by Zhenyu)

At the end of the 2022-01-08 PPT, Zhenyu explicitly raised 3 open questions to the L-curve community, making explicit Hansen's undiscussed structural boundary:

1. **Should L-curve axes be of commensurate units?** — matplotlib / matlab default does not enforce same axis scale, yet curvature is scale-dependent; should this be standardized?
2. **Is a senior collaborator's elbow $\lambda = 10^{-3}$ conclusion a scale artifact?** — the elbow $\approx 10^{-3}$ in DSCOVR PC2 case and Kawahara's toy **may be merely coincidence** (since naked-eye judgment is sensitive to scale) — should not be over-trusted
3. **Under what conditions and how should L-curve be tuned in application?** — provide guidelines so that future users know when naked-eye is OK and when axis-scale must be corrected

→ This is the research maturity of **pointing out the undiscussed boundaries of an established method** — typical undergrads or master's students would not realize this kind of issue.

### Open Questions

`[to be added]` In the future, if the L-curve community responds to these 3 open questions, or if Zhenyu submits the full mathematical argument for "axis-scale ambiguity" as an arxiv preprint or sends a letter to Hansen himself, backfill the community reaction + formal argument PDF.

- **Generalization to other regularization methods**: does the L-curve axis-scale problem also exist in other log-log graphical diagnostics (e.g., Picard plot, filter factor plot)?
- **Curvature formula canonical form**: does the "correct" curvature formula derived in `Deductions of the curvature of log-log Lcurve.docx` 36-paragraph have a published correction in the community? If not, is it worth Zhenyu writing an independent short note for submission?

### Sources

- `research_wiki/projects/mcmc_retrieval/overview.md` §Contribution (c) "Find Maximum Curvature only by the data" (2022-01-08, theoretical + numerical)
- `research_wiki/projects/mcmc_retrieval/overview.md` §💎 P3 New discovery 1: Zhenyu directly found the textbook formula error in Hansen (σ² vs σ⁴)
- `research_wiki/projects/mcmc_retrieval/overview.md` §2021-11-29 → 2021-12-06 catch own bug + self-audit (3-step cycle)
- `research_wiki/projects/mcmc_retrieval/overview.md` §3 open questions to community
- `LCurve_HansenMistake_WeRectify_Test/` — physical evidence side-by-side directory (Hansen original PDF + Hansen student PDF + 5 test subdirectories + `lcurve_test.docx` 84 paras + `Deductions of the curvature of log-log Lcurve.docx` 36 paras)
- Hansen, P. C. *Discrete Inverse Problems: Insight and Algorithms* (SIAM 2010) — the original textbook, the source where Zhenyu found the formula bug
- 2022-01-08 group meeting PPT (P2) "Find Max Curvature only by data" — formal presentation of axis-scale discovery + 3 open questions
- `[to be added]` Full 36-paragraph SVD + filter factor chain-rule derivation in `Deductions of the curvature of log-log Lcurve.docx` from Zhenyu's research-angle independent wiki (after merge this page can post the full symbolic derivation)
- `[to be added]` If Zhenyu submits a formal argument in the future (arxiv preprint or letter to Hansen), backfill artifact link

### Related Pages

- [[MCMC-贝叶斯反演]] — skill page (contains the 4-original-contribution Caltech DSCOVR subsection; this concept corresponds to contribution (c))
- [[反问题与正则化]] — parent concept (L-curve is one of its 4 regularization parameter selection methods; axis-scale ambiguity is its undiscussed structural limitation)
- [[Hardened-Balancing-Principle]] — sibling concept (DSCOVR technical discoveries established in the same batch; HBP avoids the L-curve axis-scale problem)
- [[Caltech-DSCOVR-Research]] — project experience page (split off from PKU-Undergraduate-Research)
- [[Independent Judgment narrative (private)]] — this is a technical-level judgment moment: undergrad challenges a published textbook + 3-step self-correction + formal articulation of open questions
- [[Yuk-Yung]] — PI (Caltech)
- [[King-Fai-Li]] — co-advisor (UCR)
- [[profile]]
