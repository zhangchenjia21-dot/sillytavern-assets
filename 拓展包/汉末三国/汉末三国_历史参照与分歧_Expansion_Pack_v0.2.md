---
title: 汉末三国：历史参照与分歧｜Expansion Pack
aliases:
  - 汉末三国：历史演化与分歧
  - 三国历史分歧机制拓展包
  - Han Late Three Kingdoms Historical Reference and Divergence Expansion
created: 2026-08-16
updated: 2026-08-16
status: candidate
version: 0.2
workflow_mode: light-asset
operation_mode: revise
asset_type: expansion-pack
output_profile: obsidian-markdown
asset_family: 汉末三国：天下未定
world_pack: "[[汉末三国_天下未定_World_Pack_v0.2.2]]"
politics_expansion: "[[汉末三国_政争与势力_Expansion_Pack_v0.2.1]]"
economy_expansion: "[[汉末三国_财赋与治理_Expansion_Pack_v0.2]]"
war_expansion: "[[汉末三国_军略与战争_Expansion_Pack_v0.2]]"
character_core: "[[人物能力与技艺_Expansion_Pack_v0.1.5]]"
traveler_system: "[[穿越与系统_Expansion_Pack_v0.2]]"
creator_binding: pending
asset_spec_binding: pending
runtime_asset: true
language: zh-CN
tags:
  - 三国
  - ExpansionPack
  - 历史参照
  - 历史分歧
  - Reference
  - Divergence
  - T0
  - HistoricalKnowledge
---

# 汉末三国：历史参照与分歧｜Expansion Pack v0.2

> [!abstract] 一句话定位
> **本包保存现实历史的“参照”，解释当前世界中的正式 Event 使哪些原历史前提失效，以及某段原历史未来知识现在还有多少参考价值。**
>
> 它永远不拥有：
>
> **当前世界如何继续演化。**
>
> T0 后：
>
> **Game State > Original History Reference。**

> [!important] v0.2 重构摘要
> - `Structural Historical Pressure State` 不再作为独立当前世界 State；
> - 改成 `Historical Structural Pressure Reference / Derived Context`；
> - Divergence Record 只引用正式 Game Event，不复制第二份事件历史；
> - 更新 Politics / Economy / War v0.2 read-only 接口；
> - Traveler/System 的 Historical Assistance Module 条件依赖本包，而不是本包依赖 System；
> - 普通 UI 贡献到 Core `信息`；
> - System ON + Historical Assistance 时可贡献到 `系统 > 历史参照`；
> - “历史已经改变！”仍由 System / Global Notice 决定如何显示；
> - 不建立历史偏离百分比、修正力或隐藏剧情推动器。

---

# 1. Scope Lock

## 本包拥有

- Original History Reference；
- Historical Reference Node；
- Reference Preconditions；
- Reference source / dispute；
- Reference dependency / related graph；
- Reference Validity；
- Divergence Annotation / Record；
- Historical Knowledge Relevance；
- T0 authority boundary；
- event-driven local re-evaluation；
- Significant Historical Divergence Signal；
- Historical Structural Pressure Reference / Derived Context。

## 本包不拥有

- Current World Trend；
- NPC Plan；
- Political Outcome；
- Economy Outcome；
- War Outcome；
- Character Capability progression；
- World OS Event history；
- Traveler identity / System State；
- RNG / Dice / Commit；
- 当前世界未来预测。

---

# 2. Authority Boundary

## T0 之前

World Pack + Historical Baseline Resolver：

> 可以把已经发生的历史锁入 Game Bootstrap。

## T0 之后

现实历史：

> 只作为 Original History Reference。

如果 Reference 与当前 Game State 冲突：

> 当前 Game State 胜出。

---

# 3. Original History Reference

一个 Reference 至少语义上包含：

- topic；
- time window；
- relevant people / organization / place；
- historical outcome；
- high-value preconditions；
- source；
- dispute；
- related references；
- current validity。

Reference：

> 不是 Future Event。

---

# 4. Preconditions

只保存：

> 对原历史结果真正有重要解释力的少量条件。

例如：

- key character alive；
- political position；
- territory control；
- alliance；
- previous campaign result；
- major economic condition。

不复制整个 Game State。

---

# 5. Divergence Record Is Annotation, Not Event

Divergence Record 必须绑定：

> 正式 Game Event。

它只保存：

- source Event；
- affected Reference；
- precondition changed；
- why；
- evaluation time。

不能保存第二份：

> “实际上发生了什么”。

真正历史仍在 World OS Event / Game State。

---

# 6. Historical Structural Pressure Reference

这是本版最大修订。

旧 `Structural Pressure State` 容易成为第二 World Trend。

新版改为：

> **Historical Structural Pressure Reference / Derived Context**

它回答：

> **“现实历史中的某类结构性压力，在当前正式世界条件下是否仍具有解释 / 参照价值？”**

例如：

- 北方统一政权向长江流域扩张；
- succession pressure；
- 地缘边界竞争；
- major fiscal strain；
- strategic resource conflict。

## 6.1 Derived Only

它的当前判断只能来自：

```text
Politics / Economy / War / World current facts
↓ read-only
Historical Reference
↓
Derived Pressure Relevance
```

## 6.2 Not a World Driver

禁止：

```text
History Pressure State
→ 自动创建 War / Politics Event
```

它没有：

- Action authority；
- RNG authority；
- Current State mutation authority。

即使 Runtime 为性能缓存它：

> 缓存也必须可从当前正式 Owners 重新计算，不是独立世界真相。

---

# 7. Reference Validity

推荐语义状态：

- unassessed；
- highly relevant；
- partially relevant；
- transformed；
- key preconditions invalidated；
- approximately realized；
- differently realized；
- no longer useful。

它回答：

> **参照价值**

不是：

> 发生概率。

---

# 8. Historical Knowledge Relevance

Character 可以记得：

> 原历史某事件。

即使世界已经改变：

> 这段记忆不会自动删除。

变化的是：

> **它对当前世界未来的参考价值。**

例如：

```text
Character memory:
219 年关羽失荆州

Current world:
关羽已不在荆州
↓
Relevance:
key preconditions invalidated
```

---

# 9. No Fate / No Correction Force

禁止：

- year == 208 → trigger Chibi；
- 现实历史失败方暗减骰；
- key character 必须按史死亡；
- 世界线稳定度；
- 历史修正力；
- 全局偏离百分比；
- “命运自动找替代者复现同一结果”。

如果 Structural Pressure 仍存在：

> 当前世界自己根据现实条件产生新的可能 Event。

History 不生成它。

---

# 10. Event-driven Local Re-evaluation

高影响触发：

- key character death / survival beyond anchor；
- succession change；
- regime formation / collapse；
- major recognition / control change；
- major alliance change；
- major campaign result；
- major occupation；
- major economic collapse / recovery；
- other explicitly high-impact Event。

只重评估：

> 直接关联 Reference + 有限邻域。

喝酒、普通交易、闲聊：

> 不全局重算历史。

---

# 11. Politics / Economy / War Read-only Integration

## Politics

读取：

- Regime；
- Succession；
- Recognition；
- Political Control；
- Alliance；
- Claim。

## Economy

读取高影响：

- major famine；
- migration；
- production collapse / recovery；
- major fiscal / grain change；
- infrastructure transformation。

## War

读取：

- major campaign outcome；
- occupation；
- key commander death / capture；
- formation destruction；
- strategic result。

History：

> 只做 Reference 重评估。

绝不回写这些 Owners。

---

# 12. Historical Resolver Boundary

Historical Reference Resolver 可以：

- 查询现实历史资料；
- 记录来源；
- 记录争议；
- 形成 Reference Candidate。

严格禁止：

- 修改 NPC plan；
- 修改 Game State；
- 修改 current politics；
- 修改 war result；
- 修改 character location。

联网历史资料：

> 永远只能进入 Reference layer。

---

# 13. Traveler / System Handoff

依赖方向：

```text
EP-TRAVELER-SYSTEM
Historical Assistance Module
→ conditional requires
汉末三国：历史参照与分歧
```

本包：

> 不 Hard Depend System。

没有 System：

- 仍可后台维护 Reference Validity；
- 仍可防止剧本锁；
- OOC / GM 可以查看参照。

有 System：

- 可以读取 player-safe Reference；
- 可以查询 Historical Knowledge Relevance；
- 可以消费 Significant Divergence Signal。

---

# 14. “历史已经改变！” Signal

本包只负责：

> `Significant Historical Divergence Signal`

触发条件：

- Major Divergence 已正式 Commit；
- important Reference 的 Validity 显著改变；
- current player/system 拥有合法 historical access。

本包不直接决定最终 UI 文案。

System 可以显示：

> **历史已经改变！**

并附：

- confirmed changed fact；
- affected Reference；
- future knowledge caution；
- local / broader scope。

提示不是：

> 历史修正力。

---

# 15. Information Boundary

普通汉末 Character：

> 不知道 Original History / Divergence。

Traveler：

> 只有其定义支持的 historical knowledge。

Character memory 与 Resolver Reference：

> 分开。

OOC / GM1：

> 可以查看更完整 Reference / causal explanation，但不进入 Character Knowledge。

---

# 16. G8 UI Contribution

本包：

> **不 owns 一级 Extension Surface。**

## Core `信息`

可以贡献：

- OOC historical reference；
- source / dispute；
- known divergence；
- explanation；
- reference validity。

普通沉浸模式可以完全隐藏这些。

## `系统` Surface

若：

- System ON；
- Historical Assistance enabled；

可贡献：

```text
系统
└─ 历史参照
   ├─ 原历史
   ├─ 已确认变化
   └─ 未来知识参考价值
```

## Global Notice

System 可根据 Significant Signal：

> 显示“历史已经改变！”。

History 本身不抢 Global Notice 文案 Owner。

---

# 17. Save / Restore

必须恢复：

- loaded Reference set；
- source / dispute；
- Reference Validity；
- Divergence links；
- Historical Knowledge Relevance；
- derived-context cache version if any；
- signal emission / consumption boundary。

Restore 后：

- 不重新联网研究旧世界；
- 不把后来新 Reference 结果反向污染旧 Save；
- Divergence links 必须重新指向恢复后的正式 Event history。

---

# 18. Standard Regression Scenarios｜20

1. 208 年到来但关键前提失效，不触发赤壁；
2. 孙策存活只重评估相关江东继承链；
3. key character 提前死亡不让全国历史全失效；
4. 原应死亡者被救下 → Reference invalidation + signal；
5. 类似历史结果由不同人物实现可标 differently/approximately realized；
6. 具体事件失效但 derived structural relevance 仍可存在；
7. History derived pressure 不创建新的 War Event；
8. Traveler 原历史记忆仍在但 relevance 下降；
9. 荆州改变不自动让河北 Reference 全失效；
10. T0 后联网查询只新增 Reference；
11. Resolver 与 Character memory 冲突时两层并存；
12. disputed sources 保留争议；
13. Reference 不创建 NPC Plan；
14. History 不暗调 War RNG；
15. 小事不触发全局重算；
16. 小事后续导致关键人物死亡时由正式死亡 Event 触发；
17. Significant Divergence 只发安全 signal；
18. System 未安装时不弹系统提示；
19. Save / Restore 恢复当时 Reference state；
20. 世界几十年后完全走新历史仍正常继续，不回正史。

---

# 19. Host / G9 Requirements

- Historical Reference store；
- Reference safe entity links；
- Preconditions predicate；
- source / dispute metadata；
- Game Event subscription；
- affected-neighborhood lookup；
- read-only cross-owner query；
- derived context / cache semantics；
- Historical Knowledge Relevance；
- Significant Divergence Signal；
- Traveler/System conditional dependency；
- `信息` / `系统` Surface contribution；
- Save / Restore；
- idempotent re-evaluation。

禁止任意 JS 因果图。

---

# 20. Migration From v0.1.1

## 保留

- Original History Reference；
- Preconditions；
- Reference Validity；
- Divergence；
- local causal re-evaluation；
- Historical Knowledge Relevance；
- T0 boundary；
- No Historical Correction；
- Traveler signal。

## 重构

- Structural Pressure State → Derived Historical Structural Pressure Reference；
- Divergence Event → Event-linked annotation；
- Politics / Economy / War refs → v0.2 read-only；
- Traveler old package → `穿越与系统` Historical Assistance Module；
- UI → Core `信息` + conditional `系统` contribution。

## 删除

- 任何可能把 Structural Pressure 当当前 World Trend 的语义；
- History 自己推动当前世界的路径；
- System-specific UI ownership；
- 旧三国人物能力包直接依赖。

---

# 21. Final Freeze

> **History 管参照，不管命运。**
>
> **Divergence 是对正式 Event 的历史参照解释，不是第二 Event History。**
>
> **Structural Pressure 是 read-only Derived Reference Context，不是第二 World Trend。**
>
> **T0 后 Game State 永远高于现实历史。**
>
> **Traveler/System Historical Assistance 条件依赖本包；本包不依赖 System。**
>
> **本包不 owns 一级 Surface，只贡献 Core“信息”和可选“系统 > 历史参照”。**
