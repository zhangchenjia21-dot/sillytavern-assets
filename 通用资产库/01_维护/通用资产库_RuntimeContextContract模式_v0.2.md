---
title: 通用资产库｜Runtime Context Contract 模式
aliases:
  - Context Contract Pattern
  - Runtime Activation Pattern
version: 0.2
status: current-maintenance-pattern
created: 2026-08-18
updated: 2026-08-18
scope:
  - generic-asset-library
  - runtime-context
  - retrofit
  - g9-upstream
reference_assets:
  - EP-REPUTATION-CORE v0.1
  - EP-ORG-CORE v0.1.2
skill: tavern-asset v0.8.0
asset_spec_binding: pending-g9
supersedes:
  - 通用资产库_RuntimeContextContract模式_v0.1
---

# 通用资产库｜Runtime Context Contract 模式 v0.2

> [!abstract] 定位
> 本文件冻结 G9 前 Semantic Asset 阶段的 Runtime Context Contract 写法。
>
> 它不是最终 JSON Schema / Runtime API / token budget；它规定的是：**一个 Expansion 必须能够解释自己何时进入 Runtime、何时不进入模型、模型最少需要看到什么，以及如何通过 Handoff 保持上下文局部化。**
>
> v0.2 新增 Retrofit Sidecar 规则：成熟旧资产如果 Canonical Domain Semantics 完全不变，允许用唯一 Runtime Context Contract Sidecar 补齐横切绑定元数据，避免为了 metadata 机械重写大型 audited-current 正文。

---

# 1. 四层集合

所有 Runtime Expansion 必须遵守：

```text
Asset Library
!= Game Enabled Asset Set
!= Current Runtime Relevant Set
!= Current Model Visible Working Set
```

进一步冻结：

```text
Full Semantic Asset != Model Prompt Payload
Dependency Graph != Context Inclusion Graph
```

目标不是限制 Game Instance 能启用多少资产，而是确保单次模型推理只读取完成当前职责所需的最小高信号 Working Set。

---

# 2. Context Contract 标准段落

每个新 Core / 重要 Expansion 至少回答以下 11 项：

1. Routing Profile；
2. Immediate Activation；
3. State-mandatory Activation；
4. Downstream Activation；
5. No-load Conditions；
6. Minimal Read Set；
7. Model-needed Semantics；
8. Program-owned Logic；
9. Output Candidate；
10. Handoff / Information Boundary；
11. Context Cost / Bounded Strategy。

## 2.1 Routing Profile

给第一轮 Model-first Router 的极小目录描述：ID / Name / One-line Scope / 少量 Typical Semantics。

不能复制完整机制规则，也不能成为关键词白名单。

## 2.2 Immediate Activation

只回答当前玩家输入何时需要本 Domain 参与“当前语义理解 / 当前处理”。

不要预测全部未来后果。

## 2.3 State-mandatory Activation

回答即使 Router 漏掉，什么 authoritative active state 会使本 Domain 必须成为 Runtime Relevant。

`Runtime Relevant != Model Visible`；Program 能 deterministic 处理时仍可不把完整机制交给模型。

## 2.4 Downstream Activation

说明哪些后果应通过：

```text
Formal Event / State Change
→ Typed Handoff
→ downstream activation
```

再进入本 Domain。

## 2.5 No-load Conditions

明确常见“不应该因为 Enabled 就加载本资产”的场景。No-load 是正式设计内容，不是优化备注。

## 2.6 Minimal Read Set

激活后优先读取当前实体 / 当前关系 / 当前局部状态 / 少量必要历史摘要。

禁止默认整表、全历史、全世界。

## 2.7 Model-needed Semantics

只保留 LLM 真正擅长且当前职责确实需要的：自然语言意图、开放式社会/角色语义、非确定性 Candidate、player-safe summarization。

## 2.8 Program-owned Logic

ID / Ref validation、authoritative state、deterministic rule、permission / authority、RNG / Dice、Formal Outcome、Atomic Commit、Save / Restore 等优先 Program。

## 2.9 Output Candidate

模型输出必须是 Candidate / Intent / Interpretation / Clarification Need，不得直接成为 Formal State Mutation。

## 2.10 Handoff / Information Boundary

同时回答 Incoming / Outgoing，并说明哪些后台 Truth 不能进入 Player / NPC / Narrative / Router Context。

Handoff 是 Ownership Boundary，也是 Context Complexity Boundary。

## 2.11 Context Cost

至少明确：

```text
Enabled X != X always in model context
All X State != Current X Projection
```

状态扩大 5–10 倍时，普通无关 Turn 仍应基本稳定。

---

# 3. Canonical Context Contract Location｜正文与 Sidecar

## 3.1 新资产默认正文内建

新建 Core / 重要 Expansion 默认把 Context Contract 直接写入正式资产正文。

原因：新资产从出生就应同时明确 Domain Semantics 与 Runtime Relevance Boundary。

`EP-REPUTATION-CORE v0.1` 是当前 Reference Implementation。

## 3.2 成熟旧资产允许 Sidecar Retrofit

如果旧资产已经 audited-current，且本轮审计确认：

- Canonical Owner 不变；
- Domain Semantics 不变；
- Dependency / Handoff 的业务含义不变；
- Open Attempt / Program Authority 已正确；
- 唯一缺口只是 Routing / Activation / bounded projection 等横切绑定元数据；

则允许：

> **WORKSPACE / METADATA ONLY → Runtime Context Contract Sidecar。**

Sidecar 必须：

- 绑定精确 `asset_id + asset_version`；
- 明确 `canonical_domain_ownership: none`；
- 不复制整份资产正文；
- 不新增该资产原本没有的业务能力；
- 不改变 Formal Outcome / Owner；
- 不声明任意 state path / selector / expression DSL；
- 只有一份 current canonical sidecar。

## 3.3 什么时候不能用 Sidecar

如果 Context Audit 暴露：

- Owner 边界错误；
- 依赖拓扑需要改变；
- Handoff 缺失导致业务语义不成立；
- Prompt-owned mechanic 应迁回 Program；
- Open Attempt / Information Boundary 有实质错误；
- 新 Activation 规则会改变正式玩法结果；

则必须回到正式资产正文做 Patch / Minor / Major Rewrite。

Sidecar 不得成为绕开资产修订的兼容层。

## 3.4 冲突优先级

```text
Canonical Asset Domain Semantics
>
Context Sidecar Binding Metadata
```

如果二者冲突：Sidecar 必须修订；不能用 Sidecar 反向覆盖 Domain Owner。

## 3.5 Context Contract Index

通用库维护一份唯一索引，记录每个资产的 current Context Contract 位于：

- embedded-in-asset；或
- sidecar。

禁止同一 `asset_id + version` 同时存在两个 active Context Contract truth source。

---

# 4. Model-first Routing 标准链

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
↓
Semantic reasoning / Program resolution / Narrative
```

Program 不重复自然语言语义 Router，只做返回 ID 是否真实、是否 Enabled、结构是否合法，以及 authoritative active state 是否要求补充必然 Domain。

Router miss 不能成为玩家行为白名单。

---

# 5. Router 不负责全部后果

错误：

```text
Player Input
→ Router 一次预测 Combat + Health + Law + Reputation + Politics + Relationship
→ 全量加载
```

推荐：

```text
Player Input
→ immediate domains
→ Formal Outcome / Event
→ Typed Handoff
→ downstream activation
```

例如公开决斗：Combat immediate；Health / Reputation 在正式后果形成后按需进入。

---

# 6. Context Pattern 审核问题

Asset Audit 至少检查：

1. Routing Profile 是否足够短且能区分邻近 Domain？
2. Activation 是否只写 immediate relevance？
3. State-mandatory 是否来自 authoritative state？
4. 是否误把 Dependency 当 Context Inclusion？
5. No-load 是否真实存在？
6. Minimal Read 是否可能退化成全量状态？
7. Program-owned Logic 是否仍被 Prompt-owned？
8. Handoff 是否会触发 transitive full-context explosion？
9. 是否通过 player-safe / npc-safe information boundary？
10. Enabled Asset / Session History 增长时普通无关 Turn 是否保持稳定？
11. Router miss 是否会错误禁止 Open Attempt？
12. Context Contract 的 canonical location 是否唯一？
13. Sidecar 是否偷偷新增 Domain Semantics？

---

# 7. Reference Implementation

## EP-REPUTATION-CORE v0.1

验证 born-compliant embedded contract：immediate social routing、Event-driven downstream activation、Target × Audience 局部 read、Provenance summary、Reputation / Relationship / ORG / Politics / Law Context Boundary。

## EP-ORG-CORE v0.1.2

验证 embedded retrofit：旧资产可在不改变 Owner 的情况下补齐 State-mandatory / Downstream / Information Boundary。

## Wave 1 Sidecar Retrofit

Character / Relationship / Health / Combat 验证：当 Domain Semantics 已成熟、缺口仅是横切 Context Binding 时，可使用唯一 Sidecar 避免无意义正文 churn。

---

# 8. Existing Expansion Retrofit Waves

```text
Wave 1 COMPLETE
Character / Relationship / Health / Combat / ORG recheck

Wave 2 NEXT
Survival / Traveler-System

Wave 3
Magic / Divine

Wave 4
Combat Magic
```

旧资产先审计，再分类：ALREADY COMPLIANT / PATCH / MINOR / MAJOR / WORKSPACE-METADATA ONLY。

---

# 9. Cluster / Library Context Convergence

每个 Wave 结束做 Cluster Audit；全部 Retrofit 结束做 Generic Library Context Convergence。

至少测试 Typical / Heavy / Worst Reasonable Valid 组合：普通无关 Turn、单 Domain、2–3 Domain 联动、高耦合 Event、长期 Session。

核心趋势：

```text
Enabled Assets ↑↑↑
ordinary unrelated Turn model context ≈ stable
```

```text
Session Length ↑↑↑
ordinary Turn model context ≈ bounded
```

---

# 10. Host-first / G9 Boundary

当前 G8 仍在 Final Host Convergence；G9 machine contract / compiler / Context Router implementation 仍被 G8 Exit Gate 阻塞。

本 Pattern 允许继续进行 **Semantic Retrofit**，但不冻结 Schema 字段、Router API、Context Compiler、Retrieval Algorithm、token budget、模型调用次数、Provider-specific prompt layout，也不通过资产反向发明 Host Capability。
