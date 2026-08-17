---
title: 汉末三国：军略与战争｜Expansion Pack
aliases:
  - 三国战争机制拓展包
  - 汉末三国军事拓展包
  - Han Late Three Kingdoms Warfare Expansion
created: 2026-08-16
updated: 2026-08-16
status: candidate
version: 0.2
workflow_mode: light-asset
operation_mode: major-rewrite
asset_type: expansion-pack
output_profile: obsidian-markdown
asset_family: 汉末三国：天下未定
world_pack: "[[汉末三国_天下未定_World_Pack_v0.2.2]]"
politics_expansion: "[[汉末三国_政争与势力_Expansion_Pack_v0.2.1]]"
economy_expansion: "[[汉末三国_财赋与治理_Expansion_Pack_v0.2]]"
combat_core: "[[战斗核心_Expansion_Pack_v0.1]]"
health_core: "[[身体状态核心_Expansion_Pack_v0.1]]"
survival_expansion: "[[生存需求与环境_Expansion_Pack_v0.2]]"
character_core: "[[人物能力与技艺_Expansion_Pack_v0.1.5]]"
history_expansion: "[[汉末三国_历史参照与分歧_Expansion_Pack_v0.2]]"
hard_dependencies:
  - "[[战斗核心_Expansion_Pack_v0.1]]"
  - "[[身体状态核心_Expansion_Pack_v0.1]]"
  - "[[汉末三国_政争与势力_Expansion_Pack_v0.2.1]]"
  - "[[汉末三国_财赋与治理_Expansion_Pack_v0.2]]"
creator_binding: pending
asset_spec_binding: pending
runtime_asset: true
language: zh-CN
tags:
  - 三国
  - ExpansionPack
  - 战争
  - 军略
  - Formation
  - Campaign
  - Command
  - WarFog
  - Siege
  - Naval
---

# 汉末三国：军略与战争｜Expansion Pack v0.2

> [!abstract] 一句话定位
> **本包拥有大于“直接个人战斗”的汉末三国战争层：Formation、指挥链、军令传播、战争迷雾、行军、战役、部队战斗、围城、水战、士气、组织、作战疲劳、补给状态、伤亡汇总与军事占领。**
>
> 当战争缩小到具体 Character / 小规模直接交手时：
>
> **交给 `EP-COMBAT-CORE`。**
>
> 当 Character 受到持续身体后果时：
>
> **交给 `EP-HEALTH-CORE`。**

> [!important] v0.2 是 Major Rewrite
> 旧 v0.1.1 的高层 War 结构继续保留，但以下 Ownership 正式剥离：
>
> - Character-scale Personal Combat → Combat Core；
> - Character Injury / Incapacitation / Physical Fatigue → Health Core；
> - Character Nutrition / Hydration / Sleep → Survival；
> - Character Skill mastery → EP-CHAR-CORE。
>
> 同时：
>
> - `Engagement` 改为 `Formation Battle`，避免与 Combat Engagement 冲突；
> - `Fatigue` 改为 `Formation Operational Fatigue`；
> - 命令 /军权与新版 Politics 对接；
> - Supply 与新版 Economy 对接；
> - 本包正式请求 `军略 / 战争` 一级 Extension Surface。

---

# 1. Scale Boundary｜战争层与战斗层

## 1.1 War owns

- War Theater / Conflict；
- Campaign；
- Military Formation；
- Command Chain；
- Military Order；
- Order Transmission；
- Military Intelligence Process；
- March；
- Formation Battle；
- Siege；
- Naval / Riverine Operation；
- Formation Strength / Composition；
- Training / Discipline；
- Cohesion；
- Morale；
- Formation Operational Fatigue；
- Readiness；
- Supply Condition；
- Formation casualties / captured / missing aggregate；
- Military Occupation；
- Local-to-Formation / Campaign propagation。

## 1.2 Combat Core owns

- Character-scale direct combat；
- Combat Engagement；
- Threat；
- Range；
- Reaction Window；
- Martial Action；
- Martial Outcome；
- Combat Consequence；
- direct Physical Impact Event。

## 1.3 Health owns

对已实例化 Character：

- Injury；
- Blood Loss；
- Pain；
- Physical Fatigue / Weakness；
- Consciousness；
- HP；
- Treatment / Recovery；
- bodily death state。

## 1.4 Survival owns

对已实例化 Character：

- Nutrition；
- Hydration；
- Sleep Need；
- Survival Load / Exposure。

---

# 2. Ownership Map

| 概念 | Owner |
|---|---|
| Character Capability | EP-CHAR-CORE |
| Direct Combat | EP-COMBAT-CORE |
| Character Health | EP-HEALTH-CORE |
| Character Survival Need | EP-SURVIVAL |
| Political Authority / Affiliation / Control | 政争与势力 |
| Grain / Treasury / transport / population source | 财赋与治理 |
| Formation / Campaign / Command / War Fog | 本 Expansion |
| Military Occupation | 本 Expansion |
| Political Control after occupation | Politics |
| Historical Reference | 历史参照与分歧 |
| Formal Outcome / Atomic Commit | Runtime |

---

# 3. War Skill Contribution

本包向 EP-CHAR-CORE 贡献六项 Skill Definition：

- **骑术**
- **统兵**
- **军阵**
- **军略**
- **侦察与军情**
- **军需组织**

不再定义：

- 长兵；
- 短兵；
- 射术；
- 徒手；
- 战术。

这些直接复用 Combat Core：

- 近战兵器；
- 远程兵器；
- 徒手格斗；
- 战术判断。

## 军略 vs 战术判断

`战术判断`：

> 当前直接 Combat / 局部战斗中的战术判断。

`军略`：

> Campaign / War Theater 层的长期军事目标、力量配置与战役规划。

---

# 4. Three War Layers

## 4.1 War Theater / Conflict

长期、大范围军事冲突。

记录：

- 参与政治主体；
- 主要军事目标；
- 战线；
- 活跃 Campaign。

政治敌对关系本身仍来自 Politics。

## 4.2 Campaign

围绕明确军事目标持续数日到数月：

- 攻取区域；
- 解围；
- 保护运输线；
- 夺取渡口；
- 围城；
- 防御；
- 撤退。

## 4.3 Formation Battle

Formation 之间已经形成实际军事接触的持续战斗状态。

它可以包含：

- 多个局部 Combat Context；
- 阵位变化；
- 士气 / Cohesion 更新；
- 撤退 /增援；
- Character direct combat。

`Formation Battle` 不等于 Combat Core 的 `Combat Engagement`。

---

# 5. Formation State

## 5.1 Strength

区分：

- present；
- combat-capable；
- wounded / unavailable aggregate；
- missing；
- captured；
- dead；
- deserted / detached。

匿名兵员可以 aggregate。

已实例化 Character：

> 身体事实归 Health。

## 5.2 Composition

高层兵种 / 功能组成：

- infantry；
- cavalry；
- ranged；
- naval；
- engineer / logistics；
- world-defined categories。

## 5.3 Training / Discipline

Formation 整体组织训练。

不是 Character Skill 平均值。

## 5.4 Cohesion

部队还能否：

- 保持编成；
- 接收命令；
- 协同行动。

与 Morale 分离。

## 5.5 Morale

部队集体继续承担军事风险的心理状态。

不等于：

-私人忠诚；
- Political Affiliation。

## 5.6 Formation Operational Fatigue

表示：

> **部队整体在行军、连续作战、缺乏轮换和供应压力下的作战疲劳。**

它是 Formation-level operational state。

不等于：

> Character Physical Fatigue。

Named Character 的疲劳由 Survival / Health 正式处理。

## 5.7 Readiness

装备、集结、警戒、部署和当前可作战准备状态的军事摘要。

## 5.8 Supply Condition

由 Economy 的：

- Grain；
- transport；
- material；
- finance；

派生为战争层：

- sufficient；
- strained；
- critical；
- cut off。

它不是第二粮食库存。

---

# 6. Command / Order

## 6.1 Command Chain

Politics 提供：

> 正式军权 / Affiliation / Authority。

War 保存：

> 当前实际军事指挥链、代理和失联状态。

## 6.2 Military Order

至少语义上保存：

- sender；
- recipient；
- issued time / place；
- intent；
- objective；
- validity condition；
- transmission state；
- execution state。

## 6.3 Order lifecycle

```text
issued
→ in transit
→ delivered
→ interpreted
→ executing / adjusted / refused / impossible
→ completed / failed / superseded
```

命令发出：

> 不等于部队已经移动。

## 6.4 NPC autonomy

下属不是 RTS 单位。

在：

- 命令过时；
- 信息改变；
-目标已不可能；
- 通信中断；
- 新生死风险；

等情况下，可基于 Character Definition + Duty + current knowledge 合理调整。

---

# 7. War Fog / Military Knowledge

Military truth 与 Player Knowledge 分开。

玩家只能通过：

- direct observation；
- scout；
- messenger；
- report；
- prisoner；
- ally；
- local source；

获得军情。

军情需要：

- source；
- observed time；
- received time；
- confidence；
- staleness；
- contradiction。

UI 不默认显示：

> 后台精确敌军、士气、伏兵、粮食。

---

# 8. March / Operational Movement

Formation 移动考虑：

- Region / Place / route；
- distance；
- terrain；
- weather；
- Formation size；
- baggage；
- Supply；
- Operational Fatigue；
- Cohesion；
- scouting；
- enemy pressure。

大军：

> 不瞬移、不瞬间转向、不瞬间渡河。

强行军：

> 用更高 Operational Fatigue / Cohesion / straggler risk 换速度。

对于 Player / named Character 的生存负荷：

> 可额外 Handoff Survival。

---

# 9. Direct Combat Invocation

当 Formation Battle 中出现：

- 武将冲阵；
- 城门争夺；
- 单挑；
- 小队突击；
- 护卫；
- Character 被近身攻击；

正确链：

```text
War:
Battlefield / Formation Context
↓
Combat Core:
direct combat
↓
Combat Consequence
↓
Health:
bodily consequence if any
↓
War:
propagate only military-relevant consequence
```

例如：

```text
敌军主将被 Combat Core 判定俘获
↓
War:
Command State disrupted
↓
Cohesion / Morale may change
```

War 不重做：

> Personal Combat Resolution。

---

# 10. Casualty / Health Boundary

## 10.1 Anonymous aggregate personnel

War 可以保存：

- killed aggregate；
- wounded / unavailable aggregate；
- captured；
- missing；
- deserted。

不要求十万士卒拥有 Health Profile。

## 10.2 Named Character

如果一个正式 Character 受伤：

```text
Combat / War Physical Impact
↓
EP-HEALTH-CORE
```

War 读取：

- can fight；
- can command；
- unconscious；
- dead；

等合法身体结果。

War 不保存第二 Injury。

---

# 11. Economy Integration

Economy 是 War 持续运行的正式 Supply Provider。

## Economy → War

- Grain；
- Treasury；
- material；
- transport；
- recruitment population / labor context；
- infrastructure。

## War → Economy

- resource consumption；
- requisition；
- storage loss；
- infrastructure damage；
- population casualties / displacement；
- route interruption。

War 不允许：

> `armyFood` 独立于 Economy 真值。

---

# 12. Politics Integration

Politics 提供：

- Military Authority；
- Affiliation；
- Alliance / Hostility；
- political war objective；
- surrender / armistice terms。

War 提供：

- Military Occupation；
- Campaign result；
- commander captured / killed；
- formation collapse；
- military surrender。

Military Occupation：

> 不自动成为 Political Control。

---

# 13. Formation Battle Resolution

大型部队战斗：

> 不是一次 d20。

至少经历：

```text
contact
↓
deployment / initial situation
↓
key formation actions
↓
local Combat consequences
↓
loss / Cohesion / Morale update
↓
reinforcement / retreat / pursuit choices
↓
battle conclusion
```

Dice 只解决：

> 状态和规则处理后仍真正不确定的局部节点。

---

# 14. Local-to-Higher Propagation

局部成功只有存在实际传播链才影响 Formation / Campaign。

例如：

## Commander captured

```text
Combat Outcome
→ commander captured
→ Command State disruption
→ Cohesion risk
→ possible Formation Battle effect
```

## Gate opened

```text
Combat Outcome
→ gate access changes
→ friendly movement becomes possible
→ Formation position changes
→ Siege / Battle situation changes
```

## Morale event

必须考虑：

- 谁看见；
- 消息是否传播；
- leader reputation；
- current Morale / Cohesion。

不允许：

> “名将杀一人 → 全军 -30 士气”。

---

# 15. Siege / Naval

## Siege

是长期 Campaign / Process，持续读取：

- defender；
- fortification；
- Supply；
- Economy；
- Morale；
- disease / Health context；
- relief army；
- engineering；
- time。

攻城强攻：

> 是 Formation Battle + multiple local Combat Context，不是一骰破城。

## Naval / Riverine

继续复用 Formation / Command / Morale / Cohesion。

额外读取：

- ship / transport resource；
- waterway；
- current；
- wind；
- boarding；
- naval training；
- fire conditions。

---

# 16. Retreat / Pursuit

撤退区分：

- orderly；
- fighting withdrawal；
- disorder；
- rout。

追击需要：

- Cohesion；
- Fatigue；
- information；
- route；
- command。

不是：

> 免费追加伤害。

---

# 17. Open Attempt

普通士卒可以喊：

> “全军撤退！”

Attempt 成立。

但：

- 无正式 Authority；
- 是否有人听从；
- 是否引发局部后果；

由世界裁定。

同样：

- 假传军令；
- 砸锅；
- 破坏桥梁；
- 私自袭营；
- 强行冲阵；

都不因为 Action Registry 缺项被禁止。

---

# 18. G8 UI Surface

本包正式请求一级：

> **`军略 / 战争` Extension Surface**

推荐：

```text
军略 / 战争
├─ 战争态势
├─ 战役
├─ 军队
├─ 军令
├─ 军情
├─ 围城
└─ 水战（按需）
```

## Direct Combat UI

Character 当前直接作战：

> 使用 Combat Core 的 Narrative Contextual Surface。

不要把“我正在被长矛刺向胸口”放进战略管理页面。

## Map Overlay

可以贡献：

- known friendly formation；
- last-known enemy；
- occupation；
- campaign route；
- uncertainty。

不得泄露后台 War Truth。

---

# 19. Save / Restore

必须恢复：

- Formation；
- Strength / Composition；
- Cohesion / Morale / Operational Fatigue；
- Readiness / Supply Condition；
- Command Chain；
- Orders；
- military intel knowledge；
- March / Campaign / Formation Battle；
- Siege / Naval process；
- Occupation；
- casualties aggregate；
- linked named Character health outcome refs；
- Event boundary。

Restore：

- 不重掷；
- 不重复传令；
- 不重复伤亡；
- 不重复资源消耗。

---

# 20. Standard Regression Scenarios｜26

1. 普通士卒喊全军撤退不会直接改全军状态；
2. 伪造军令可能被信但不获得合法 Authority；
3. 正式军令未送达则下属不执行；
4. 命令到达时过时可自主调整；
5. 军情只显示玩家已知；
6. 冲突侦察报告不静默覆盖；
7. 强行军增加 Formation Operational Fatigue；
8. named Character 连续熬夜由 Survival/Health 处理；
9. 钱多但前线断粮仍 Supply critical；
10. 武将冲阵调用 Combat Core；
11. Combat 伤势由 Health Core；
12. 武将局部成功不自动让万人溃败；
13. 大战不能单骰；
14. 确定性包围不强制五五开骰；
15. 下属合理改变过时命令；
16. 违令产生 War/Politics/Relationship Event；
17. 有序撤退可成功；
18. 追击不是免费伤害；
19. 围城持续一月推进正式 Process；
20. 水战读取水域 /船只 /训练；
21. Military Occupation 不自动 Political Control；
22. 主将被俘不必然全军投降；
23. Player Character 可真实死亡，但 Health/World OS 决定身体死亡链；
24. 重复军令提交幂等；
25. Save / Restore 恢复围城与军令；
26. T0 后不因现实历史强制赤壁 /官渡 Outcome。

---

# 21. Host Requirements

| 能力 | 必需性 |
|---|---|
| Persistent Formation | 必需 |
| Command Chain / Order | 必需 |
| Timed message transmission | 必需 |
| NPC autonomous order execution | 必需 |
| War Fog / Knowledge | 必需 |
| Combat Core invocation | 必需 |
| Health Core named-character handoff | 必需 |
| Politics Authority / Occupation handoff | 必需 |
| Economy supply / damage handoff | 必需 |
| Timed March / Campaign | 必需 |
| Multi-stage Formation Battle | 必需 |
| Casualty aggregation | 必需 |
| Atomic Commit / idempotency | 必需 |
| Save / Restore | 必需 |
| Extension Surface | 推荐 |
| Map Overlay | 推荐 |
| Survival named-character integration | Optional |

---

# 22. Creator / G9 Requirements

需要声明式支持：

- Formation；
- command hierarchy；
- Order / message；
- timed movement；
- Campaign；
- Formation Battle；
- Siege；
- Naval；
- Morale / Cohesion / Operational Fatigue；
- Supply Condition；
- Combat invocation；
- casualty aggregate；
- Economy consume / damage；
- Politics authority / occupation；
- History Event；
- War Skill contribution；
- `军略 / 战争` Surface。

不能允许 War 自建 Combat Engine / Health Engine / Economy ledger。

---

# 23. Migration From v0.1.1

## 保留

- 三层战争结构；
- Formation；
- Command / Order；
- Fog of War；
- March；
- Campaign；
- Morale / Cohesion；
- Siege；
- Naval；
- Retreat / Pursuit；
- Military Occupation；
- aggregate casualties；
- Open Attempt。

## 移交

- Personal Combat → Combat Core；
- Character injury / physical fatigue / incapacitation → Health Core；
- Character sleep / hunger / hydration → Survival；
- Character skill state → EP-CHAR-CORE。

## 重命名 / 重构

- Engagement → Formation Battle；
- Fatigue → Formation Operational Fatigue；
- 战术 / 长兵 /短兵 /射术不再由 War 定义；
- War contributes 6 military skills；
- Supply 绑定 Economy；
- Command Authority 绑定 Politics；
- UI owns `军略 / 战争`。

---

# 24. Final Freeze

> **War 管军队和战役，Combat 管直接打斗，Health 管身体。**
>
> **Formation Operational Fatigue 不等于 Character Physical Fatigue。**
>
> **Formation Battle 不等于 Combat Engagement。**
>
> **War 只消费 Economy 的真实 Supply，不建第二军粮。**
>
> **Military Occupation 不等于 Political Control。**
>
> **个人武勇先经 Combat 形成局部 Consequence，再由 War 判断是否传播到 Formation / Campaign。**
>
> **本包拥有“军略 / 战争”一级 Extension Surface；直接战斗继续留在中央 Contextual UI。**
