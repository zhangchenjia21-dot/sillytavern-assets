---
title: 组织与任职核心｜Expansion Pack
aliases:
  - EP-ORG-CORE
  - Organization Core
  - 组织核心
version: 0.1
status: audited-current
created: 2026-08-17
asset_type: expansion-pack
asset_family: 通用拓展包资产库
reusability: cross-world
dependency_role: organization-core
hard_dependencies: []
creator_binding: pending-g9
asset_spec_binding: pending-g9
skill: tavern-asset v0.7.1
---

# 组织与任职核心｜Expansion Pack v0.1

> [!abstract]
> `EP-ORG-CORE` 是跨 World Pack 通用的持续组织结构事实 Owner。
>
> 它维护 Organization Identity、Membership、Formal Affiliation、Role、Rank、Branch、Internal Authority、任职生命周期，以及组织间正式关系生命周期骨架。
>
> 它不拥有私人关系、政治权力、法律状态、经济资源、战争 Formation 或人物能力。

# 1. Canonical Scope

## 负责

- Organization Definition；
- Organization Instance；
- Membership；
- Formal Affiliation；
- Role Definition；
- Role Holding；
- Rank / Grade；
- Branch / Department Structure；
- Internal Authority；
- Appointment / Removal / Resignation；
- Generic Role Succession skeleton；
- Formal Inter-Organization Relation lifecycle skeleton。

## 不负责

- Character Capability → EP-CHAR-CORE；
- Trust / Respect / Attachment → Relationship Core；
- Reputation → Reputation Core；
- Political Authority / Recognition / Control → Politics Core；
- Resources → Economy Core；
- Formation / Campaign → War Core；
- Legal Procedure → Law；
- Formal Outcome / Commit → Runtime。

# 2. Core Invariants

1. Organization != Faction Score。
2. Membership != Relationship。
3. Role != Rank。
4. Role Holding != Public Authority。
5. Internal Authority != Political Authority。
6. Standing Organization != Operational Formation。
7. Organization Relation lifecycle != Domain-specific Relation meaning。

# 3. Definition → Instance

```text
Organization Definition
↓
instantiate
↓
Named Organization Instance
↓
Runtime Membership / Role / Structure State
```

Definition 更新不得静默覆盖 Instance。

# 4. Membership

Membership 表示正式成员关系。

允许一个 Character 同时拥有多个 Membership。

Formal Affiliation 用于：

- 客卿；
- 门客；
- 长期顾问；
- 合同关系；
- 受保护对象。

Membership 与 Affiliation 均不得替代 Relationship。

# 5. Role / Rank

Role：当前承担的正式职能。

Rank：组织内部等级 / 资序。

示例：

```text
Rank:
二代弟子

Role:
执法堂副堂主
```

两者独立存在。

# 6. Internal Authority

Internal Authority 描述组织内部正式权限：

- 任命内部职位；
- 管理成员；
- 分配组织任务；
- 执行组织规则。

不得推出：

- 国家行政权；
- 法律效力；
- 战争指挥权。

# 7. Organization Relation Skeleton

ORG 提供组织间关系生命周期：

- 参与组织；
- 生效状态；
- 起止时间；
- 来源事件。

具体语义由 Domain Contribution 提供：

Politics：联盟、臣属、外交关系。

Jianghu：盟约、门派关系、互保。

Commerce：商业合作。

# 8. Open Attempt

身份和权限限制 Formal Effect，不限制 Attempt。

例如：

```text
普通弟子宣布自己成为掌门
↓
Attempt 成立
↓
无合法任命/继承
↓
Role Holding 不成立
```

# 9. Information Boundary

组织真实状态 != 玩家知识。

秘密成员、隐藏分支、内部协议必须经过 Knowledge / Clue / Event 才进入玩家安全投影。

# 10. Migration Boundary

未来 Han Politics Genericization：

迁出：

- Faction organization skeleton；
- staff / retainer；
- Office Role skeleton；
- Office Holding 基础任职事实。

保留 Politics：

- Public Authority；
- Jurisdiction；
- Recognition；
- Political Control；
- Political Claim。

# 11. G9 Boundary

不冻结：

- JSON Schema；
- Runtime API；
- Surface ID；
- Creator machine fields。

当前冻结 Semantic Ownership。
