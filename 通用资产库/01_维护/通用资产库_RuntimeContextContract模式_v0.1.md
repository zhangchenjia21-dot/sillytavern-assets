---
title: 通用资产库｜Runtime Context Contract 模式
aliases:
  - Context Contract Pattern
  - Runtime Activation Pattern
version: 0.1
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
  - EP-ORG-CORE v0.1.1
skill: tavern-asset v0.8.0
asset_spec_binding: pending-g9
---

# 通用资产库｜Runtime Context Contract 模式 v0.1

> [!abstract] 定位
> 本文件冻结 G9 前 Semantic Asset 阶段的 Runtime Context Contract 写法。
>
> 它不是最终 JSON Schema / Runtime API / token budget；它规定的是：**一个 Expansion 必须能够解释自己何时进入 Runtime、何时不进入模型、模型最少需要看到什么，以及如何通过 Handoff 保持上下文局部化。**
>
> `EP-REPUTATION-CORE v0.1` 是第一份从出生即完整遵守本模式的 Reference Implementation；`EP-ORG-CORE v0.1.1` 是第一份旧资产 Retrofit 对照样本。

---

# 1. 四层集合

所有 Runtime Expansion 必须遵守：

```text
Asset Library
!=
Game Enabled Asset Set
!=
Current Runtime Relevant Set
!=
Current Model Visible Working Set
```

进一步冻结：

```text
Full Semantic Asset
!= Model Prompt Payload
```

```text
Dependency Graph
!= Context Inclusion Graph
```

目标不是限制 Game Instance 能启用多少资产，而是确保**单次模型推理只读取完成当前职责所需的最小高信号工作集**。

---

# 2. Context Contract 标准段落

每个新 Core / 重要 Expansion 正文至少回答以下 11 项。

## 2.1 Routing Profile

给第一轮 Model-first Router 的极小目录描述。

最低包含：

- ID；
- Name；
- One-line Scope；
- 少量 Typical Semantics / routing hints。

Routing Profile 不能复制完整机制规则，也不能成为关键词白名单。

## 2.2 Immediate Activation

回答：

> 当前玩家输入在什么情况下需要本 Domain 参与“当前语义理解 / 当前处理”？

只写 immediate relevance，不要求把所有未来可能后果都预测出来。

## 2.3 State-mandatory Activation

回答：

> 即使 Router 漏掉，本 Runtime 已经存在什么 authoritative active state，会使本 Domain 必须参与？

例如 Active Combat Context。

若本 Domain 没有这类场景，可以明确写“无额外 state-mandatory condition”。

## 2.4 Downstream Activation

回答：

> 哪些后果应该通过 Formal Event / State Change → Typed Handoff 后再激活本 Domain，而不是要求 Router 预判？

这项是防止 Router 变成全世界因果预测器的关键。

## 2.5 No-load Conditions

明确列出常见“不应该因为 Enabled 就加载本资产”的场景。

No-load 是正式设计内容，不是优化备注。

## 2.6 Minimal Read Set

回答：

> 一旦激活，Runtime 最少读取哪些 Authoritative Facts / Projections？

必须优先局部：当前实体、当前关系、当前状态、当前必要历史摘要。

避免“读整表 / 全历史 / 全世界”。

## 2.7 Model-needed Semantics

只列 LLM 真正擅长且当前职责确实需要的内容：自由语言意图理解、开放式社会 /角色语义解释、非确定性候选、player-safe narrative summarization 等。

## 2.8 Program-owned Logic

明确哪些逻辑不应该占用模型注意力：ID / Ref validation、authoritative state read / write、deterministic rule、permission / formal authority validation、RNG / Dice、Formal Outcome、Atomic Commit、Save / Restore、deterministic lifecycle bookkeeping。

如果能 Program deterministic、安全、可测地处理，默认留在 Program。

## 2.9 Output Candidate

模型输出必须是 Candidate / Intent / Interpretation / Clarification Need，不得直接成为 Formal State Mutation。

## 2.10 Handoff / Information Boundary

同时回答 Incoming / Outgoing，以及哪些后台 Truth 不能进入 Player / NPC / Narrative / Router Context。

Handoff 是 Ownership Boundary，也是 Context Complexity Boundary。

## 2.11 Context Cost / Bounded Strategy

至少给出：

```text
Enabled X != X always in model context
All X State != Current X Projection
```

并说明状态规模扩大 5–10 倍时普通无关 Turn 为什么仍可保持基本稳定。

当前不冻结统一 token 上限。

---

# 3. Model-first Routing 标准链

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

Program 不重复实现自然语言语义 Router，只做返回 ID 是否真实存在、是否属于当前 Enabled Set、输出结构是否合法，以及 authoritative active state 是否要求补充必然 Domain。

Router 未命中某 Domain 不能成为玩家行为白名单。

---

# 4. Router 不负责全部后果

错误模式：Player Input → Router 一次预测 Combat + Health + Law + Reputation + Politics + Relationship → 一次性加载全部。

推荐模式：Player Input → immediate domains → Formal Outcome / Event → Typed Handoff → downstream domain activation。

例如公开决斗：Combat 是 immediate；Reputation 是战后公开 Event 的 downstream consumer。

---

# 5. Context Pattern 审核问题

Asset Audit 时额外检查：

1. Routing Profile 是否足够短且能区分邻近 Domain？
2. Activation 是否只写 immediate relevance？
3. 是否误把 Dependency 当 Context Inclusion？
4. No-load 是否真实存在，而不是空话？
5. Minimal Read 是否可能退化成“全量状态”？
6. Program-owned Logic 是否仍被 Prompt-owned？
7. Handoff 是否会触发 transitive full-context explosion？
8. 是否通过 player-safe / NPC-safe information boundary？
9. Enabled Asset 数量增长时普通无关 Turn 是否保持稳定？
10. 长期 Event / State 历史增长时是否只读取 bounded relevant summary？
11. Router miss 是否会错误禁止 Open Attempt？

---

# 6. Reference Implementation 结论

## EP-REPUTATION-CORE v0.1

验证了 immediate social-reputation routing、Event-driven downstream activation、Target × Audience 的局部 Minimal Read、Provenance summary 而非完整 source history，以及 Reputation / Relationship / ORG / Politics / Law 的 Context Boundary。

## EP-ORG-CORE v0.1.1

验证了旧资产可以通过 Patch 加入 Context Contract 而不改变 Canonical Owner；ORG / Reputation 同时 Enabled 不代表共同常驻 Prompt；organization facts 可以 bounded projection 被读取。

---

# 7. Existing Expansion Retrofit Waves

## Wave 1｜Always-common Foundation

- EP-CHAR-CORE；
- EP-RELATIONSHIP-ROMANCE-CORE；
- EP-HEALTH-CORE；
- EP-COMBAT-CORE；
- EP-ORG-CORE 复审。

重点：避免“上游很常用”被错误翻译成“上游全文永驻 Prompt”。

## Wave 2｜Common Gameplay / Framework

- EP-SURVIVAL；
- EP-TRAVELER-SYSTEM。

Traveler/System 重点验证：`Package Enabled != Module Active != Model Visible`。

## Wave 3｜Supernatural Core

- EP-MAGIC-CORE；
- EP-DIVINE-CORE。

## Wave 4｜Theme

- EP-MAGIC-COMBAT。

Theme 只增加增量语义；不得因为 Theme 激活就机械包含全部 Hard Providers 全文。

---

# 8. Retrofit 审核结果分类

每个旧 Expansion 先审计，再决定是否改文件：

- ALREADY COMPLIANT；
- PATCH REQUIRED；
- MINOR REQUIRED；
- MAJOR REWRITE REQUIRED；
- METADATA / WORKSPACE ONLY。

禁止为了“所有版本都变整齐”机械升级资产。

---

# 9. Cluster / Library Context Convergence

Wave 1 完成后执行一次 Context Cluster Audit。

全部 Retrofit 完成后执行 Generic Library Context Convergence Audit，至少用 Typical Valid Bundle / Heavy Valid Bundle / Worst Reasonable Valid Bundle 测试普通无关 Turn、单 Domain、2–3 Domain 联动、高耦合 Event、长期 Session。

核心趋势：

```text
Enabled Assets ↑↑↑
ordinary unrelated Turn model context ≈ stable
```

```text
Session Length ↑↑↑
ordinary Turn model context ≈ bounded
```

具体 token budget 等待 G9 / G11 真实 Provider Benchmark。

---

# 10. G9 Boundary

本 Pattern 冻结 Semantic Contract，不冻结 Schema 字段、Router API、Context Compiler 实现、Retrieval Algorithm、Embedding / search 方案、token budget、模型调用次数、Provider-specific prompt layout。

G9 应根据真实 Host / Runtime 能力，把本 Pattern 编译成可验证 Machine Contract。
