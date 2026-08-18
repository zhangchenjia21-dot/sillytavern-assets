---
title: 组织与任职核心｜Expansion Pack
aliases:
  - EP-ORG-CORE
  - Organization Core
  - 组织核心
version: 0.1.1
status: audited-current
created: 2026-08-17
updated: 2026-08-18
asset_type: expansion-pack
asset_family: 通用拓展包资产库
reusability: cross-world
dependency_role: organization-core
hard_dependencies: []
creator_binding: pending-g9
asset_spec_binding: pending-g9
skill: tavern-asset v0.8.0
supersedes:
  - 组织与任职核心_Expansion_Pack_v0.1
---

# 组织与任职核心｜Expansion Pack v0.1.1

> [!abstract]
> `EP-ORG-CORE` 是跨 World Pack 通用的持续组织结构事实 Owner。
>
> 它维护 Organization Identity、Membership、Formal Affiliation、Role、Rank、Branch、Internal Authority、任职生命周期，以及组织间正式关系生命周期骨架。
>
> 它不拥有私人关系、政治权力、法律状态、经济资源、战争 Formation 或人物能力。
>
> v0.1.1 不改变 Canonical Ownership；本 Patch 新增 Runtime Activation / Context Contract，使本 Core 可在大型多 Expansion 游戏中按需进入有界 Working Set，而不是成为常驻 Prompt。

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
8. Enabled ORG != ORG always visible to model。
9. ORG Dependency != full ORG prompt inclusion。

# 3. Definition → Instance

```text
Organization Definition
↓ instantiate
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

```text
Rank: 二代弟子
Role: 执法堂副堂主
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

- Politics：联盟、臣属、外交关系；
- Jianghu：盟约、门派关系、互保；
- Commerce：商业合作。

# 8. Open Attempt

身份和权限限制 Formal Effect，不限制 Attempt。

```text
普通弟子宣布自己成为掌门
↓
Attempt 成立
↓
无合法任命 / 继承
↓
Role Holding 不成立
```

Context Router 未命中 ORG，也不能因此判定玩家关于组织的自由表达非法；必要时可以 generic interpretation / clarification。

# 9. Information Boundary

组织真实状态 != 玩家知识。

秘密成员、隐藏分支、内部协议必须经过 Knowledge / Clue / Event 才进入玩家安全投影。

# 10. Runtime Activation / Context Contract

## 10.1 Routing Profile

Router 级最小描述：

```text
ID: EP-ORG-CORE
Scope: 组织身份、成员关系、任职、等级、分支、内部权限、任命/辞任与正式组织关系生命周期
Typical semantics: 加入 / 退出组织、任职 / 撤职、职位 / 等级、内部命令、分支结构、组织间正式关系
```

Routing Profile 只用于语义路由，不替代本资产完整 Definition。

## 10.2 Activation

典型 immediate activation：

- 加入 / 退出某组织；
- 接受 / 拒绝正式任职；
- 任命 / 撤任 / 辞任；
- 查询或使用某角色的组织 Role / Rank；
- 组织内部权限是否成立；
- 分支 / 部门 / 上下级组织结构发生变化；
- 建立 / 终止一项正式组织关系；
- 其他 Domain 需要读取 authoritative organization facts。

## 10.3 No-load Conditions

以下普通场景通常不应因为本局启用了 ORG 就自动加载 ORG 详细上下文：

- 与组织身份无关的私人闲聊；
- 普通 Character-scale Combat；
- 单纯 Health / Survival 更新；
- 与任何组织事实无关的移动、观察、物品操作。

若其他 Domain 只需要一个确定性 ORG Fact，优先由 Runtime 读取并形成最小 projection，而不是加载 ORG 全部语义。

## 10.4 Minimal Read Set

根据当前 Intent，只读取直接相关的：

- target Organization；
- relevant Membership / Formal Affiliation；
- relevant Role / Rank；
- relevant Branch；
- relevant Internal Authority；
- directly relevant formal organization relation；
- 必要的来源 Event / effective state。

不得为了一个局部任职问题加载全部组织、全部成员或完整组织历史。

## 10.5 Model-needed Semantics

模型主要用于：

- 理解玩家自由语言中的加入、辞任、任命、冒充、内部命令等意图；
- 解释非标准组织互动；
- 在有歧义时提出结构化 Candidate / clarification；
- 结合人物和上下文生成 NPC 对组织行为的语义回应候选。

## 10.6 Program-owned Logic

Program / authoritative state 负责：

- Ref / organization identity validation；
- Membership / Role 当前状态读取；
- 当前正式任职是否存在；
- Internal Authority 的确定性范围校验；
- Formal Outcome / Atomic Commit；
- 更新时间、生效 / 终止状态；
- Save / Restore。

模型不得直接写 Membership / Role Holding。

## 10.7 Output Candidate

模型最多提出：

- organization intent；
- candidate membership / affiliation change；
- candidate appointment / resignation / removal；
- candidate organization-relation action；
- candidate internal-authority use；
- clarification need。

最终正式变化由 Program Judge / Runtime Owner 决定。

## 10.8 Handoff

ORG 可以向：

- Politics：提供 Organization / Role / internal structure facts；
- War：提供 standing military organization / role source；
- Reputation：提供 target / audience organization context；
- Law：提供 agency / role / internal-organization facts；
- Relationship：提供 Context，但不修改私人关系。

Handoff 不要求把 ORG 完整正文放进对方模型上下文。

## 10.9 Context Cost

正式原则：

```text
Enabled ORG
!=
ORG always in model context
```

```text
Full ORG Definition
!=
Turn-level ORG Projection
```

大量组织 / 成员存在于 Game State 时，普通无关 Turn 的模型上下文应保持基本稳定。

# 11. Migration Boundary

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

# 12. G9 Boundary

当前冻结：

- Semantic Ownership；
- Routing / Activation / Context Contract 语义。

不冻结：

- JSON Schema；
- Runtime API；
- Router API；
- token budget；
- Surface ID；
- Creator machine fields。
