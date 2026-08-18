---
title: 通用资产库｜Shared Foundation 架构规划
aliases:
  - 通用资产库上游核心规划
  - Generic Shared Foundation Plan
version: 0.5
status: current-planning-baseline
created: 2026-08-17
updated: 2026-08-18
scope:
  - generic-asset-library
  - shared-foundation
  - canonical-ownership
  - migration-planning
  - runtime-context
skill: tavern-asset v0.8.1
asset_spec_binding: pending-g9
creator_binding: pending-g9
supersedes:
  - 通用资产库_Shared_Foundation架构规划_v0.4
---

# 通用资产库｜Shared Foundation 架构规划 v0.5

> [!abstract] 当前裁定
> 社会结构 Shared Foundation 已完成前两项：`ORG v0.1.2 → Reputation v0.1`。
>
> 二者已经通过 Ownership + Runtime Context Cluster Audit，并冻结 `Runtime Context Contract Pattern v0.3`。
>
> **现在暂停继续生产 Kinship；先对既有 Runtime Expansion 做分波次 Context Retrofit。** Retrofit 收敛后再恢复 `Kinship → Politics → Economy → War`。

---

# 1. P0-A Independent Foundation

## EP-ORG-CORE｜组织与任职核心

状态：AUDITED CURRENT v0.1.2。

Owner：Organization / Membership / Formal Affiliation / Role / Rank / Branch / Internal Authority / generic organization relation lifecycle。

Context：retrofit reference / PASS。

## EP-REPUTATION-CORE｜名望与社会评价核心

状态：AUDITED CURRENT v0.1。

Owner：Target × Audience 公共社会评价、传播、显著性、争议、时效与 Social Epithet。

Hard：无。Optional：ORG / Relationship / Character / future Politics / Law。

Context：born-compliant Reference Implementation / PASS。

关键边界：

```text
Reputation != Relationship
Reputation != Knowledge
Reputation != Organization Rank
Reputation != Political Recognition
Reputation != Legal Status
Reputation != Character Capability
```

## EP-KINSHIP-CORE｜亲缘与谱系核心

状态：PLANNED / PAUSED FOR CONTEXT RETROFIT。

Owner：Biological / Adoptive / Genealogical Kinship、Lineage、Branch、Generation、Disputed Genealogy 与继承资格证据。

---

# 2. P0-B Large-scale Domain Core

EP-POLITICS-CORE：PLANNED GENERICIZATION，Hard ORG。

EP-ECONOMY-CORE：PLANNED GENERICIZATION。

EP-WAR-CORE：PLANNED GENERICIZATION，Hard ORG。

Governance / Law 继续 DEFERRED P1。

---

# 3. Canonical Ownership Registry｜目标态

| Domain | Canonical Owner |
|---|---|
| Character Capability | EP-CHAR-CORE |
| Bodily State | EP-HEALTH-CORE |
| Direct Combat | EP-COMBAT-CORE |
| Relationship / Romance | EP-RELATIONSHIP-ROMANCE-CORE |
| Survival | EP-SURVIVAL |
| Organization / Role / Rank / Membership | EP-ORG-CORE |
| Public Social Reputation | EP-REPUTATION-CORE |
| Kinship / Genealogy | future EP-KINSHIP-CORE |
| Public Political Authority / Recognition / Control | future EP-POLITICS-CORE |
| Economy / Bulk Resources / Population / Market | future EP-ECONOMY-CORE |
| War / Formation / Campaign / Occupation | future EP-WAR-CORE |
| Governance Execution | future Governance |
| Legal Case / Wanted / Judgment / Procedure | future Law |
| Game State / Time / Position / Item / Knowledge / Task / Commitment / Event | World OS / Runtime |
| RNG / Dice / Formal Outcome / Atomic Commit | Runtime |

---

# 4. Runtime Context Gate

冻结：

```text
Asset Library != Game Enabled != Runtime Relevant != Model Visible
Full Semantic Asset != Model Prompt Payload
Dependency Graph != Context Inclusion Graph
```

Pattern：`[[通用资产库_RuntimeContextContract模式_v0.3]]`；Contract location：`[[通用资产库_RuntimeContextContract索引_v0.2]]`。

Model-first Router：Player Input + Enabled Routing Profiles + minimal active context → immediate Domain / Intent candidates；Program 只做 structural validation + state-mandatory augmentation；后续由 Event / Handoff 再激活。

Wave 2 增量：

```text
Background deterministic progression != Model Activation
Package Included != Feature Enabled != Module Enabled != Runtime Relevant != Model Visible
```

---

# 5. Reference Implementation / Cluster 结论

Reputation 验证短 Routing Profile、immediate/downstream 分离、Target × Audience Minimal Read、Provenance summary 与 Knowledge boundary。

ORG + Reputation 验证 bounded projection、Handoff 替代 state mirroring、Role/Rank 与社会 Standing 无 duplicate owner。

Wave 1 / Wave 2 将这些证据收敛为 current Context Pattern v0.3。

---

# 6. Existing Expansion Context Retrofit｜当前最高优先级

```text
Wave 1
Character → Relationship → Health → Combat → ORG recheck
✓ PASS / CLOSED

Wave 2
Survival → Traveler/System
✓ PASS / CLOSED

Wave 3
Magic → Divine
NEXT

Wave 4
Combat Magic
↓ Generic Library Context Convergence
```

Wave 1：Character / Relationship / Health / Combat 使用 Sidecar；ORG v0.1.2 embedded。

Wave 2：Survival / Traveler-System 使用 Sidecar；新增 Background Program Progression 与 Feature / Module Activation Hierarchy。

Sidecar 只拥有 Context Binding Metadata，不获得 Domain Ownership。

---

# 7. Retrofit 后恢复 Shared Foundation

```text
Context Retrofit Convergence
↓
EP-KINSHIP-CORE
↓
EP-POLITICS-CORE + Han migration
↓
EP-ECONOMY-CORE + Han migration
↓
EP-WAR-CORE + Han migration
↓
Generic Library Convergence
↓
Governance / Law re-evaluation
↓
Jianghu-specific assets
```

---

# 8. 汉末三国 Migration Strategy

对应 Generic Core 未 audited-current 前，不批量迁移 Han Character Cards / World Pack。

Politics：Faction / staff / Office skeleton → ORG；Authority / Recognition / Control / Claim → Politics。

Economy：Treasury / Bulk / Population / Market / Production → generic Economy；Governance execution → future Governance。

War：Formation / Campaign / Command / Siege / Occupation → generic War；standing military organization → ORG。

History Reference / Divergence 继续 Han-specific。

---

# 9. 江湖资产族进入条件

江湖专用：Martial Arts → Jianghu Ecology → Court-Jianghu。

在 Shared Foundation 与 Context Retrofit 至少达到可组合稳定前，不批量生产 World Pack / Character Cards。

---

# 10. Periodic Architecture Audit

每形成高耦合 Cluster 检查：规模 5–10 倍、duplicate owner / state mirroring、pairwise / transitive context explosion、over-modularization、Prompt-owned deterministic mechanics、成本 / 延迟与后台 model-call explosion。

必要时邀请用户做 Owner Reflection。

---

# 11. G9 Boundary

不冻结 JSON / Schema / Router API / token budget / retrieval algorithm / Creator machine fields / Bundle contract。

WEB-04 Final Host Convergence 已 PASS / CLOSED；G9 machine protocol 仍必须等待 G8 Exit。Semantic Retrofit 可继续，并为 G9-02 提供 handwritten runtime profile requirements，但不能反向定义 Host。

当前冻结 Semantic Ownership、Context Contract Pattern 与生产 / Retrofit 顺序。