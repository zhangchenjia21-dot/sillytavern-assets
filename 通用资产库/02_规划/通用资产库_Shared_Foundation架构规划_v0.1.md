---
title: 通用资产库｜Shared Foundation 架构规划
aliases:
  - 通用资产库上游核心规划
  - Generic Shared Foundation Plan
version: 0.1
status: current-planning-baseline
created: 2026-08-17
updated: 2026-08-17
scope:
  - generic-asset-library
  - shared-foundation
  - canonical-ownership
  - migration-planning
skill: tavern-asset v0.7.1
asset_spec_binding: pending-g9
creator_binding: pending-g9
---

# 通用资产库｜Shared Foundation 架构规划 v0.1

> [!abstract] 规划结论
> 第三个“江湖 / 架空中国王朝”资产族触发了正式 Genericity / Shared Foundation Gate。
>
> 本轮不允许为江湖世界复制一套“江湖政治 / 江湖经济 / 江湖战争”第二 Owner；应先补齐跨世界社会结构上游，并把已经证明具有跨世界语义的汉末三国 Politics / Economy / War 从世界专用 Owner 逐步提升为 Generic Core。
>
> 当前正式生产顺序冻结为：
>
> `ORG → Reputation → Kinship → Politics → Economy → War`
>
> Governance 与 Law / Enforcement 继续登记为重要 P1 Consumer，但在其上游 Core 稳定前暂缓正文生产。

---

# 1. 触发背景

当前通用资产库已经拥有人物能力、身体状态、个人战斗、关系、生存、穿越 / 系统以及超自然领域资产，但社会结构层仍存在明显 Owner 空白。

第三个资产族要求同时表达：

- 门派、帮会、镖局、寺观、宗族、商号等持续组织；
- 官府、中央朝廷、地方衙署、正式任职与公共 Authority；
- 武林名望、恶名、地方口碑与跨圈层社会评价；
- 家族、血缘、谱系、宗族与继承资格证据；
- 财赋、人口、市场、生产与社会资源；
- 军队、Formation、Campaign、指挥与战争；
- 后续治理执行与法律 / 执法。

若直接在江湖 World Pack 或江湖专用 Expansion 内拥有这些事实，将再次造成 world-specific duplicate owner，并迫使未来其他历史世界重复开发同一上游。

---

# 2. Shared Foundation 分层

## P0-A｜Independent Foundation

### 2.1 EP-ORG-CORE｜组织与任职核心

状态：**AUDITED CURRENT / v0.1**

唯一职责：

> 持续组织实体、Membership / Formal Affiliation、Role / Rank、Branch、Internal Authority、组织结构与通用组织间正式关系生命周期。

不拥有：私人关系、社会名望、公共政治权力、经济资源、战争 Formation、法律状态。

---

### 2.2 EP-REPUTATION-CORE｜名望与社会评价核心

状态：**PLANNED**

唯一职责：

> 某对象在某 Audience / Social Scope 中因特定来源形成的持续公共评价、传播、名号、恶名、争议声誉与时效。

硬边界：

`Reputation != Relationship != Knowledge != Political Recognition != Organization Rank`

---

### 2.3 EP-KINSHIP-CORE｜亲缘与谱系核心

状态：**PLANNED**

唯一职责：

> Biological / Adoptive / Genealogical Kinship、Lineage、Branch、Generation、Disputed Genealogy 与继承资格证据。

硬边界：

- Marriage Bond 继续归 Relationship Core；
- Clan Organization 归 ORG；
- Political Succession Outcome 归 Politics；
- 法律继承结果等待 Law；
- Kinship 只提供谱系事实与资格证据。

---

## P0-B｜Large-scale Domain Core

### 2.4 EP-POLITICS-CORE｜政治与公共权力核心

状态：**PLANNED GENERICIZATION**

来源：汉末三国《政争与势力》中的可通用政治语义。

Hard Dependency：

- EP-ORG-CORE

唯一职责：

> Public Authority、Jurisdiction、Political Recognition、Political Control、Sovereignty、Political Claim、政治继承、Regime、Diplomatic Political Semantics 与政权转化。

必须从现有 Han Politics 剥离：

- Faction / Organization entity；
- Membership / staff / retainer 类 affiliation；
- Office / Role 基础结构；
- 通用组织间 Relation lifecycle。

这些迁入 / 绑定 ORG。

---

### 2.5 EP-ECONOMY-CORE｜经济与社会资源核心

状态：**PLANNED GENERICIZATION**

来源：汉末三国《财赋与治理》中的可通用经济语义。

唯一职责：

> Treasury、Bulk Resource、Production、Population、Labor、Market、Bulk Transport、经济基础设施、Livelihood Pressure 与经济损害 / 恢复。

必须继续保持：

`Economy resource availability → Survival need → Health consequence`

必须迁出：

- Local Governance Execution Capacity；
- policy implementation；
- tax / relief / corvée execution；
- administrative friction。

这些等待 Governance。

---

### 2.6 EP-WAR-CORE｜战争与军事核心

状态：**PLANNED GENERICIZATION**

来源：汉末三国《军略与战争》v0.2 的大部分上层机制。

Hard Dependency：

- EP-ORG-CORE

Optional / Handoff：

- EP-CHAR-CORE；
- EP-COMBAT-CORE；
- EP-HEALTH-CORE；
- EP-ECONOMY-CORE；
- EP-POLITICS-CORE。

唯一职责：

> War Theater、Campaign、Operational Formation、Operational Command、Military Order、War Fog、March、Formation Battle、Siege、Formation aggregate state 与 Military Occupation。

关键边界：

`Standing Military Organization != Operational Formation`

`Named Character Health != Formation Casualty Aggregate`

`Military Occupation != Political Control`

---

# 3. 暂缓的 P1 重要 Consumer

## 3.1 Governance｜治理与行政执行

暂不生产正文。

预期 Hard Dependency：

- ORG；
- Politics；
- Economy。

唯一问题：

> 有合法 Authority 且存在可用资源以后，行政网络实际能把公共政策执行到什么程度？

Governance 未来拥有行政执行过程，不拥有 Politics Authority，也不拥有 Economy Resource Truth。

## 3.2 Law / Enforcement｜法律、司法与执法

暂不生产正文。

预期主要上游：

- ORG；
- Politics；
- World OS Event / Knowledge / Clue。

唯一问题：

> 法律规范、案件状态、通缉 / 判决与合法执法程序怎样成立和演化？

Law 不拥有 Event Truth、Character Health、Item Placement、Position 或 Public Political Authority。

---

# 4. Canonical Ownership Registry｜目标态

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

# 5. 关键 Semantic Namespace

以下词禁止在后续资产中无 namespace 混用：

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

```text
Economy Infrastructure State
!= Place / Building authoritative identity
```

---

# 6. 汉末三国 Migration Strategy

只有对应 Generic Core 完成 Asset Audit / Cluster Gate 后，才迁移现有 Han-specific Consumer。

禁止现在批量改 37 张 Character Card 或四个 Han-specific Expansion 去引用 provisional owner。

## Politics Migration

- Faction organization skeleton → SPLIT / REBIND ORG；
- staff / retainer / formal service → SPLIT / REBIND ORG；
- Office role skeleton / holding → SPLIT / REBIND ORG；
- Public Authority / Jurisdiction → KEEP then GENERICIZE Politics；
- Recognition / Control / Claim / Regime Succession → KEEP then GENERICIZE Politics；
- Organization relation lifecycle → SPLIT / REBIND ORG；
- political semantics → KEEP Politics。

## Economy Migration

- Treasury / Bulk Stock / Population / Labor / Market / Production → GENERICIZE Economy；
- Governance Execution Capacity / policy execution → SPLIT to future Governance；
- Han-specific fiscal institutions / taxes / historical definitions → KEEP Han Theme / World Definition。

## War Migration

- Formation / Campaign / Command / War Fog / March / Siege / Occupation → GENERICIZE War；
- standing military organization → REBIND ORG；
- Han-specific military system / units / offices / doctrine → KEEP Han Theme / Definition。

历史参照与分歧继续 Han-specific，不 genericize。

---

# 7. 江湖资产族进入条件

江湖资产族的专用 Expansion 暂定：

1. 江湖｜武学与内功；
2. 江湖｜武林生态；
3. 江湖｜朝廷与江湖。

在以下上游至少完成语义稳定前，不正式批量生产 World Pack / Character Cards：

- ORG；
- Reputation；
- Kinship；
- Politics；
- Economy；
- War。

Governance / Law 可以在江湖 Theme 初步设计后继续补齐，但在最终“历史拟真 Full Profile”收口前必须重新评估是否为 Hard Requirement。

---

# 8. 正式生产顺序

```text
SF-01  EP-ORG-CORE                         AUDITED CURRENT
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

`正式创作 → Asset Audit → Consumer Stress Test / Cluster Gate → 必要修订 → 更新库级 current source → 再进入下一项`

---

# 9. 止损

当前不继续抽：

- 商业 Core；
- 科举 Core；
- 教育 Core；
- 宗教组织 Core；
- 地产 Core；
- 犯罪 Core；
- 情报 Core；
- 工程 Core；
- 派系 Core。

除非未来 Domain Survey 证明现有 Owner 无法承载，优先将其作为 Economy / Politics / ORG / Law / Character / Knowledge 的 Downstream 或 Definition Contribution。

---

# 10. G9 边界

本规划冻结 Semantic Ownership 与生产顺序，不冻结：

- JSON Schema；
- Machine Manifest；
- Runtime API；
- Creator machine field；
- Surface ID；
- Bundle machine contract。

所有 Frontmatter 仅用于当前人工仓库治理。
