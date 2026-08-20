# 通用资产库｜Generic Asset Library Workspace

本目录管理跨 World Pack 可复用 Expansion 的库级 Blueprint、Version、Ownership、Dependency、Consumer、Runtime Context Contract、维护规范与审核资料。

正式 Expansion 正文仍只保存在：`../拓展包/通用拓展包/`。本目录不是 Bundle，也不复制 Expansion 正文。

## Current

- Existing Reusable Expansion：**13**
- Stable Semantic Baseline：**10**
- Generic Supernatural Candidate：**3**
- Context Contract Coverage：**13 / 13 PASS**
- Existing Expansion Retrofit：**CLOSED**
- Generic Library Context Convergence：**PASS / CLOSED**
- `EP-KINSHIP-CORE｜家族与亲缘核心 v0.1`：**PASS / AUDITED CURRENT**
- `EP-POLITICS-CORE｜政治与公共权力核心 v0.1`：**PASS / AUDITED CURRENT**
- Han Politics Migration Plan：**COMPLETE / NOT YET EXECUTED**

当前维护源：

- `通用拓展包资产库总蓝图_v1.0`
- `通用资产库_当前版本矩阵_v0.9`
- `通用资产库_RuntimeContextContract模式_v0.6`
- `通用资产库_RuntimeContextContract索引_v0.6`
- `通用资产库_维护规范_v0.8`
- `通用资产库_Shared_Foundation架构规划_v0.9`
- `通用资产库_后续发展路线_v0.9`
- `tavern-asset v1.0`

## Politics 关键结论

```text
Regime / Political Order != Government Organization
Role Holding != Public Authority
Claim != Recognition != Control != Occupation != Jurisdiction
Public Reputation != Political Recognition
Kinship != Succession Outcome
Political Agreement != Commitment Promise Lifecycle
```

Politics 不建立通用 loyalty / legitimacy / stability / control score。

## Large Relation Graph

Kinship + Politics 已形成两份独立证据，正式提升为通用 Context Rule：

```text
Large Relation Graph
→ canonical primary relations / source facts
→ Program deterministic current-relevant path / subgraph
→ owner-safe + player-safe bounded projection
→ Model only for open semantic work
```

```text
Whole Relation Graph != Model Prompt
Derived Pairwise Projection != Canonical Truth
```

## Current Next

资产语义维护线自身仍可继续执行已计划的真实消费者迁移：

> **汉末三国《政争与势力》对 `EP-POLITICS-CORE` / ORG / Kinship 的迁移。**

迁移收口后：Economy → War → Shared Foundation Convergence。

这条资产维护路线与游戏项目 G9-04 Adapter / Compiler Gate 并行但不可混淆：资产正文仍是 canonical semantic source，G9-04 负责 deterministic machine adapter，不允许借机反向重写资产语义 owner。

## Archive

同一维护文档族 superseded 版本进入：`99_归档/版本历史/`。`90_审核/` 保留历史审核证据，不与 current 事实源竞争。

## Game / G9

当前游戏项目权威状态以 `Vibe-Coding/main/sillytavern/` 为准；本段只做资产工作台导航同步。

```text
G9-02                         PASS / CLOSED
G9-03 Unified Protocol       PASS / CLOSED
G9-04 Adapter / Compiler     AUTHORIZED / NEXT
G9-05 Creator                BLOCKED BY G9-04
```

G9-03 current protocol authority：

- `Vibe-Coding/main/sillytavern/G9-03_UnifiedAssetReferenceProtocol规格_v1.0_2026-08-20.md`
- `Vibe-Coding/main/sillytavern/G9-03A_RuntimeModuleBinding与TypedConfig增量裁定_v1.0_2026-08-20.md`
- `Vibe-Coding/main/sillytavern/G9-03_IndependentReview_最终收口_v1.0_2026-08-20.md`

G9-04 将从本仓库 current canonical samples 中读取真实：

- World Pack；
- Character Card；
- Expansion Pack；
- Library 最小协议样本 / reference material；

并通过 AI-independent adapter / parser 转成已冻结 `TavernAssetV1`，再证明 `TavernGameAssetManifestV1 → G9-02 Source Binding / Game-local lineage`。

现有 Semantic Assets 不需要因为 G9-03 PASS 而手工改写为 JSON；adapter/compiler 承担 authoring format → canonical machine object 的转换。

继续禁止资产线自行提前实现：

- Creator fields / chat transport；
- Runtime Library retrieval；
- arbitrary relation query DSL；
- executable asset/plugin；
- 第二套 Source / Game-local / Runtime identity；
- 为适配器方便而私自发明 `tavern.asset.v1` 之外的 hidden machine truth。
