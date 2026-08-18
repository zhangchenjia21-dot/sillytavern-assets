---
title: 通用资产库｜Shared Foundation 架构规划
aliases:
  - 通用资产库上游核心规划
  - Generic Shared Foundation Plan
version: 0.2
status: current-planning-baseline
created: 2026-08-17
updated: 2026-08-18
scope:
  - generic-asset-library
  - shared-foundation
  - canonical-ownership
  - migration-planning
  - runtime-context
skill: tavern-asset v0.8.0
asset_spec_binding: pending-g9
creator_binding: pending-g9
supersedes:
  - 通用资产库_Shared_Foundation架构规划_v0.1
---

# 通用资产库｜Shared Foundation 架构规划 v0.2

> [!abstract] 规划结论
> 第三个“江湖 / 架空中国王朝”资产族触发了正式 Genericity / Shared Foundation Gate。
>
> 本轮不允许为江湖世界复制一套“江湖政治 / 江湖经济 / 江湖战争”第二 Owner；应先补齐跨世界社会结构上游，并把已经证明具有跨世界语义的汉末三国 Politics / Economy / War 从世界专用 Owner 逐步提升为 Generic Core。
>
> 同时，本轮架构审计确认：**资产模块化必须配套 Runtime Context 模块化。** Enabled Expansion 不得自动进入每 Turn Prompt；后续所有 Shared Foundation Core 必须带 Runtime Activation / Context Contract。
>
> 当前正式生产顺序冻结为：
>
> `ORG → Reputation → Kinship → Politics → Economy → War`
>
> Governance 与 Law / Enforcement 继续登记为重要 P1 Consumer，但在其上游 Core 稳定前暂缓正文生产。

---

# 1. Shared Foundation 分层

## P0-A｜Independent Foundation

### EP-ORG-CORE｜组织与任职核心

状态：**AUDITED CURRENT / v0.1.1**

唯一职责：持续组织实体、Membership / Formal Affiliation、Role / Rank、Branch、Internal Authority、组织结构与通用组织间正式关系生命周期。

### EP-REPUTATION-CORE｜名望与社会评价核心

状态：**NEXT / DISCUSSION FROZEN**

唯一职责：某对象在某 Audience / Social Scope 中因特定来源形成的持续公共评价、传播、名号、恶名、争议声誉与时效。

硬边界：

`Reputation != Relationship != Knowledge != Political Recognition != Organization Rank`

### EP-KINSHIP-CORE｜亲缘与谱系核心

状态：**PLANNED**

唯一职责：Biological / Adoptive / Genealogical Kinship、Lineage、Branch、Generation、Disputed Genealogy 与继承资格证据。

硬边界：

- Marriage Bond → Relationship Core；
- Clan Organization → ORG；
- Political Succession Outcome → Politics；
- 法律继承结果 → future Law；
- Kinship 只提供谱系事实与资格证据。

---

## P0-B｜Large-scale Domain Core

### EP-POLITICS-CORE｜政治与公共权力核心

状态：**PLANNED GENERICIZATION**

Hard Dependency：EP-ORG-CORE。

拥有 Public Authority、Jurisdiction、Political Recognition、Political Control、Sovereignty、Political Claim、政治继承、Regime、Diplomatic Political Semantics 与政权转化。

现有 Han Politics 的 Faction / Membership / Office skeleton / generic organization-relation lifecycle 迁出并绑定 ORG。

### EP-ECONOMY-CORE｜经济与社会资源核心

状态：**PLANNED GENERICIZATION**

拥有 Treasury、Bulk Resource、Production、Population、Labor、Market、Bulk Transport、经济基础设施、Livelihood Pressure 与经济损害 / 恢复。

继续保持：

`Economy resource availability → Survival need → Health consequence`

Governance Execution Capacity、policy / tax / relief / corvée execution、administrative friction 迁出到 future Governance。

### EP-WAR-CORE｜战争与军事核心

状态：**PLANNED GENERICIZATION**

Hard Dependency：EP-ORG-CORE。

Optional / Handoff：Character / Combat / Health / Economy / Politics。

拥有 War Theater、Campaign、Operational Formation、Operational Command、Military Order、War Fog、March、Formation Battle、Siege、Formation aggregate state 与 Military Occupation。

硬边界：

`Standing Military Organization != Operational Formation`

`Named Character Health != Formation Casualty Aggregate`

`Military Occupation != Political Control`

---

# 2. 暂缓的 P1 重要 Consumer

## Governance｜治理与行政执行

预期 Hard Dependency：ORG + Politics + Economy。

唯一问题：有合法 Authority 且存在可用资源以后，行政网络实际能把公共政策执行到什么程度？

## Law / Enforcement｜法律、司法与执法

预期主要上游：ORG + Politics + World OS Event / Knowledge / Clue。

唯一问题：法律规范、案件状态、通缉 / 判决与合法执法程序怎样成立和演化？

---

# 3. Canonical Ownership Registry｜目标态

| Domain | Canonical Owner |
|---|---|
| Character Long-term Capability | EP-CHAR-CORE |
| Persistent Bodily State | EP-HEALTH-CORE |
| Character-scale Direct Combat | EP-COMBAT-CORE |
| Relationship / Romance Truth | EP-RELATIONSHIP-ROMANCE-CORE |
| Survival Need / Exposure | EP-SURVIVAL |
| Organization / Membership / Role / Rank / Internal Authority | EP-ORG-CORE |
| Public Social Reputation | EP-REPUTATION-CORE |
| Kinship / Genealogy / Lineage | EP-KINSHIP-CORE |
| Public Political Authority / Recognition / Control / Claim | EP-POLITICS-CORE |
| Economy / Bulk Resource / Population / Market / Production | EP-ECONOMY-CORE |
| War / Formation / Campaign / Operational Command / Occupation | EP-WAR-CORE |
| Governance Execution | future Governance |
| Legal Case / Wanted / Judgment / Procedure | future Law / Enforcement |
| Current World State / Time / Position / Item / Knowledge / Task / Commitment / Event | World OS / Runtime |
| RNG / Dice / Program Judge / Formal Outcome / Atomic Commit | Runtime |

---

# 4. Runtime Relevance / Context Gate

正式冻结：

```text
Asset Library
!= Game Enabled Asset Set
!= Current Runtime Relevant Set
!= Current Model Visible Working Set
```

以及：

```text
Full Semantic Asset
!= Model Prompt Payload
```

```text
Dependency Graph
!= Context Inclusion Graph
```

每个 Shared Foundation Core 从 v0.2 起必须在正文中回答 Context Contract：

1. Routing Profile；
2. Activation；
3. No-load Conditions；
4. Minimal Read Set；
5. Model-needed Semantics；
6. Program-owned Logic；
7. Output Candidate；
8. Handoff；
9. Information Boundary；
10. Context Cost / bounded strategy。

## Model-first Semantic Routing

正式方向：

```text
Player Input
+
Enabled Expansion Routing Profiles
+
minimal current scene / active context
↓
Router Model
↓
immediate Domain / Intent candidates
↓
Program structural validation
+
state-mandatory augmentation
↓
JIT bounded runtime projections
```

Program 不重复自然语言语义路由；Program 只验证 ID / enabled / output 合法性，并根据 authoritative active state 补充必然参与的 Domain。

Router 只判断 immediate semantic relevance。Health / Law / Reputation / Politics 等后续影响通过 Formal Event / Typed Handoff 再激活，不要求第一轮 Router 预测全部后果。

## 长期成本目标

```text
Game State / Event History / Enabled Assets ↑↑↑
不应导致
ordinary unrelated Turn Model Context 同比例 ↑↑↑
```

成本主要由 Current Relevant Complexity 决定。

---

# 5. 关键 Semantic Namespace

```text
Organization Internal Authority
!= Politics Public Authority
!= Law Procedural Authority
!= War Operational Command Authority
```

```text
Organization Rank
!= Reputation Standing
!= Political Recognition
!= Character Capability
```

```text
Standing Military Organization
!= War Operational Formation
```

```text
Kinship Lineage
!= Clan Organization
!= Relationship Bond
```

---

# 6. 汉末三国 Migration Strategy

只有对应 Generic Core 完成 Asset Audit / Cluster Gate 后，才迁移现有 Han-specific Consumer。

禁止现在批量改 37 张 Character Card 或四个 Han-specific Expansion 去引用 provisional owner。

## Politics

- Faction organization skeleton → SPLIT / REBIND ORG；
- staff / retainer / formal service → SPLIT / REBIND ORG；
- Office role skeleton / holding → SPLIT / REBIND ORG；
- Public Authority / Jurisdiction → KEEP then GENERICIZE Politics；
- Recognition / Control / Claim / Regime Succession → KEEP then GENERICIZE Politics；
- Organization relation lifecycle → SPLIT / REBIND ORG；
- political semantics → KEEP Politics。

## Economy

- Treasury / Bulk Stock / Population / Labor / Market / Production → GENERICIZE Economy；
- Governance Execution Capacity / policy execution → SPLIT to future Governance；
- Han-specific fiscal definitions → KEEP Han Theme / World Definition。

## War

- Formation / Campaign / Command / War Fog / March / Siege / Occupation → GENERICIZE War；
- standing military organization → REBIND ORG；
- Han-specific military system / units / offices / doctrine → KEEP Han Theme / Definition。

历史参照与分歧继续 Han-specific。

---

# 7. 江湖资产族进入条件

江湖资产族专用 Expansion 暂定：

1. 江湖｜武学与内功；
2. 江湖｜武林生态；
3. 江湖｜朝廷与江湖。

在 ORG / Reputation / Kinship / Politics / Economy / War 至少完成语义稳定前，不批量生产 World Pack / Character Cards。

Governance / Law 在最终历史拟真 Full Profile 收口前必须重新评估 Hard Requirement。

---

# 8. 正式生产顺序

```text
SF-01  EP-ORG-CORE                         AUDITED CURRENT v0.1.1
SF-02  EP-REPUTATION-CORE                  NEXT
SF-03  EP-KINSHIP-CORE                     PLANNED
SF-04  EP-POLITICS-CORE + Han Migration    PLANNED
SF-05  EP-ECONOMY-CORE + Han Migration     PLANNED
SF-06  EP-WAR-CORE + Han Migration         PLANNED

↓ Generic Library Convergence

P1-GOV  Governance                         DEFERRED
P1-LAW  Law / Enforcement                  DEFERRED

↓
J1 Martial Arts
J2 Jianghu Ecology
J3 Court ↔ Jianghu
J4 World Pack
J5 Character Cards
```

每一项 Core：

`讨论 → 正式创作 → Asset Audit → Context Contract Audit → Consumer Stress Test / Cluster Gate → 必要修订 → 更新库级 current source → 再进入下一项`

---

# 9. Periodic Architecture Audit / User Reflection

Shared Foundation 每形成一个明显高耦合簇，必须做一次 Future Explosion Review：

- 规模扩大 5–10 倍后是否仍成立；
- 是否有 duplicate owner / state mirroring / dual path；
- 是否有 transitive context / pairwise integration explosion；
- 是否过度模块化导致 shotgun change；
- 是否把未来想象当真实需求提前平台化；
- 成本 / 延迟 / 模型上下文是否会随无关资产数量增长。

若问题涉及产品体验、长期维护偏好、成本权衡或不可逆架构，先给事实 / 风险 / 推荐，再邀请用户做项目所有者视角反思。

---

# 10. 止损与 G9 边界

当前不继续抽商业、科举、教育、宗教组织、地产、犯罪、情报、工程、派系等 Core，除非真实 Consumer 证明现有 Owner 无法承载。

当前只冻结 Semantic Ownership、Context Contract 语义与生产顺序，不冻结：

- JSON Schema；
- Machine Manifest；
- Runtime API；
- Creator machine field；
- Surface ID；
- Router API；
- Context token budget；
- Bundle machine contract。
