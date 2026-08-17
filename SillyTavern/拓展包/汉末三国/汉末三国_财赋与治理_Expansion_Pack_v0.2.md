---
title: 汉末三国：财赋与治理｜Expansion Pack
aliases:
  - 三国经济治理机制拓展包
  - Han Late Three Kingdoms Economy and Governance Expansion
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
character_core: "[[人物能力与技艺_Expansion_Pack_v0.1.5]]"
survival_expansion: "[[生存需求与环境_Expansion_Pack_v0.2]]"
health_core: "[[身体状态核心_Expansion_Pack_v0.1]]"
war_expansion: "[[汉末三国_军略与战争_Expansion_Pack_v0.2]]"
history_expansion: "[[汉末三国_历史参照与分歧_Expansion_Pack_v0.2]]"
creator_binding: pending
asset_spec_binding: pending
runtime_asset: true
language: zh-CN
tags:
  - 三国
  - ExpansionPack
  - 财政
  - 粮食
  - 人口
  - 劳力
  - 市场
  - 治理
  - 工程
  - 运输
---

# 汉末三国：财赋与治理｜Expansion Pack v0.2

> [!abstract] 一句话定位
> **本包拥有汉末三国社会与地方层的财赋、粮食与大宗物资、生产、人口与劳力、市场、行政执行、征发负担、公共工程、运输与民生压力。**
>
> 它回答：
>
> **“钱粮从哪里来、在哪里、怎样生产和移动；一个地方有权实施政策以后，行政网络实际做不做得到；战争、灾荒和过度征发怎样改变社会经济基础？”**
>
> 它不拥有 Character 的饥饿、口渴、睡眠、伤病和身体疲劳，也不拥有政治 Authority，不拥有 Character Skill State。

> [!important] v0.2 重构摘要
> 相对旧 v0.1.3：
>
> - 删除旧三国人物能力包依赖，改为贡献 Economy / Governance Skill Definitions 给 `EP-CHAR-CORE`；
> - 正式建立 `Economy → Survival → Health` 三层因果链；
> - `Administrative Reach` 重命名 / 收口为 `Local Governance Execution Capacity`；
> - 明确 Bulk Resource Stock 与 World OS Item / Placement 的桥接边界；
> - 不再把个人 Physical Fatigue / Injury / Disease 视为 Economy 状态；
> - 与新版 Politics v0.2 的 Authority / Jurisdiction 分权；
> - 与新版 War v0.2 建立正式 Supply / Damage / Demographic Handoff；
> - 不拥有一级“经济”Surface，改为贡献到 Politics 拥有的 `势力 / 政务`；
> - G9 之前只冻结语义，不冻结机器 Schema。

---

# 1. Scope Lock

## 1.1 本包必须负责

- Treasury / 可支配财力；
- Grain / Food Bulk Stock；
- Strategic Material Stock；
- Storage Context；
- Productive Capacity；
- Agriculture / production cycle；
- Demographic State；
- Labor Availability；
- Market Condition；
- Local Governance Execution Capacity；
- Public Burden；
- Livelihood Pressure；
- Infrastructure；
- Public Works；
- Tax / Extraction economic outcome；
- Relief economic outcome；
- Bulk Transport；
- Resettlement / displacement economic state；
- Economy Event；
- Economy Knowledge / safe projection；
- War / Politics / Survival 的受控 Handoff。

## 1.2 明确不负责

- Political Authority / Jurisdiction；
- Office / Political Control；
- Character Capability mastery；
- Nutrition / Hydration / Sleep Need；
- Physical Fatigue / Weakness；
- Injury / Disease / Poison；
- Treatment / Recovery；
- Formation / Campaign / Battle Outcome；
- Character Relationship；
- World OS Task / Commitment；
- Item Placement 的第二事实源；
- RNG / Dice / Formal Outcome / Atomic Commit。

---

# 2. Ownership Map

| 概念 | 唯一 Owner | Economy 如何使用 |
|---|---|---|
| Character Skill State | EP-CHAR-CORE | 读取相关 Skill |
| Political Authority / Control | 政争与势力 | 验证治理权限 |
| Character Survival Need | EP-SURVIVAL | 提供资源可用性 |
| Persistent Bodily State | EP-HEALTH-CORE | 不直接拥有 |
| Treasury | 本 Expansion | 正式职责 |
| Bulk Grain / Materials | 本 Expansion | 正式职责 |
| Productive Capacity | 本 Expansion | 正式职责 |
| Demographic / Labor | 本 Expansion | 正式职责 |
| Market | 本 Expansion | 正式职责 |
| Governance Execution Capacity | 本 Expansion | 正式职责 |
| Public Burden / Livelihood Pressure | 本 Expansion | 正式职责 |
| Infrastructure / Public Works | 本 Expansion | 正式职责 |
| Bulk Transport | 本 Expansion | 正式职责 |
| Discrete Item Instance / Placement | World OS Item owner | 通过桥接事务 |
| War Supply Consumption | War consumes Economy stock | 正式 Handoff |
| War damage / casualties | War Event → Economy | 接收后果 |
| Historical Reference | 历史参照与分歧 | 输出 Event |
| Program Outcome / Commit | Runtime | 执行 |

---

# 3. Economy → Survival → Health

这是本版最重要的新链。

## 3.1 社会资源可用性属于 Economy

例如：

- 城中粮价高涨；
- 官仓只剩少量粮；
- 市场没有可饮水源；
- 旅店和住所有无；
- 药材短缺。

属于：

> 社会 / 地方 Resource Availability。

## 3.2 Character Need 属于 Survival

当一个 Character 实际无法获得食物：

```text
Economy:
food unavailable / inaccessible
↓
Survival:
Nutrition Need unmet
```

Economy 不保存：

> 角色当前 Hunger。

## 3.3 Bodily Consequence 属于 Health

如果缺粮长期持续：

```text
Survival:
Nutrition Deficit
↓
Health Handoff
↓
Health:
Weakness / physiological disturbance / hidden HP effect
```

因此：

```text
地区饥荒
!= Character Hunger
!= Character Bodily Condition
```

三层必须分开。

---

# 4. Character Skill Contribution

本包向 `EP-CHAR-CORE` 统一 Skill Registry 贡献六项 Skill Definition。

## 行政

- 公文与事务组织；
- 多事项协调；
- 地方政务执行；
- 官僚流程。

## 财计

- 账目；
- 收支；
- 财力配置；
- 资源规划。

## 商业

- 买卖；
- 渠道；
- 市场判断；
- 交易组织。

## 农政

- 农业生产；
- 土地；
- 农时；
- 农业治理。

## 工程与水利

- 公共工程；
- 灌溉；
- 河渠；
- 建设与维护组织。

## 运输组织

- 大宗运输；
- 中转；
- 仓储协调；
- 民用物流组织。

Character 当前 mastery：

> 只存在 EP-CHAR-CORE。

---

# 5. Politics vs Governance Execution

本包不回答：

> “谁有权征税 / 开官仓 / 征发劳役？”

这是 Politics。

正确三层：

```text
Politics:
有没有 Authority / Jurisdiction

Character Core:
执行者本人有多擅长

Economy:
地方组织网络实际能执行到什么程度
```

## 5.1 Local Governance Execution Capacity

旧 `Administrative Reach` 正式收口为：

> **Local Governance Execution Capacity｜地方治理执行能力**

它由：

- 官僚网络；
- 信息传递；
- 地方配合；
- 控制范围；
- 基础设施；
- 人员；
- 当前秩序；

共同形成。

它不是：

- Character 行政 Skill；
- Office 权限；
- Political Control；
- “治理度 0–100”。

---

# 6. Bulk Resource vs Item / Placement

这是 G9 必须保护的关键边界。

## 6.1 Bulk Resource Stock

Economy 可以拥有：

> **大宗、可替代、按数量或语义规模管理的 Resource Stock。**

例如：

- 官仓粮食；
- 地方粮秣；
- 财货；
- 木材；
- 金属；
- 布帛。

每个 Stock 至少语义上绑定：

- Owner；
- Storage / Place；
- Availability；
- Reserved purpose；
- Quantity / semantic amount。

## 6.2 Discrete Item Instance

当资源被实例化为：

- 某袋粮；
- 某箱铜钱；
- 某件具体工具；
- 某个可携带物品；

其当前 Placement：

> 归 World OS Item / Placement。

## 6.3 Materialization / Aggregation Bridge

禁止同一批资源同时存在：

```text
Economy grain +100
+
Inventory rice bags +100
```

却没有扣减关系。

正确链：

```text
Bulk Stock
↓ atomic withdraw/materialize
Discrete Item Instance
```

反向：

```text
Discrete fungible items
↓ atomic deposit/aggregate
Bulk Stock
```

G9 需要正式桥接 Contract。

---

# 7. Core States

## 7.1 Treasury

可用于：

- 采购；
- 支付；
- 雇佣；
- 投资；
-公共支出。

有钱：

> 不等于当前地点有粮。

## 7.2 Grain / Food Bulk Stock

回答：

- 有多少；
- 在哪里；
- 谁拥有 / 控制；
- 是否可调拨；
- 是否锁定用途；
- 是否有损耗风险。

## 7.3 Strategic Material Stock

只把持续影响玩法的重要实物升级为 Resource。

不建立无限商品百科。

## 7.4 Productive Capacity

表示某地区 / Production Site 持续产出能力。

受：

- 劳力；
- 季节；
- 水利；
- 战争破坏；
- 安全；
- 技术与政策；

影响。

## 7.5 Demographic State

保存合理粒度：

- 人口；
- 流入 / 流出；
- displaced / refugee pressure；
- 家庭稳定；
- 长期死亡 / 迁徙后果。

人口不是：

> 一次性 Resource 点。

## 7.6 Labor Availability

与人口相关但不同。

征兵、农忙、疾病、徭役都会改变：

> 当前可投入生产 /运输 /工程的劳力。

## 7.7 Public Burden

综合表达：

- 税；
- 征粮；
- 徭役；
- 运输；
- 重复摊派；

对居民的现实负担。

## 7.8 Livelihood Pressure

表示地方居民面对：

- 粮食；
- 收入；
- 灾害；
- 战争；
- 市场；
- 债务 /失业；

的综合生活压力。

它不等于：

> 对统治者的 Sentiment。

## 7.9 Market Condition

高层表示：

- 供给充足；
- 正常；
- 紧缺；
- 严重短缺；
- 交易受阻；
- 价格压力。

不默认做全国实时价格模拟。

## 7.10 Infrastructure

道路、水利、桥梁、仓储等长期设施的：

- 可用性；
- 维护；
- 作用范围；
- 破坏。

---

# 8. Core Rules

1. 资源必须有来源；
2. Bulk Resource 必须有位置 / Storage Context；
3. 有钱不等于有粮；
4. 生产需要权威时间；
5. 运输不是瞬移；
6. Market 不是无限商店；
7. 极端征收可以尝试，但后果真实；
8. 人口不是普通可消费货币；
9. 征兵 / 徭役 /迁徙 /死亡必须分开；
10. 公共工程需要建设与维护；
11. 战争破坏必须进入正式经济 State；
12. 灾后 /战后恢复需要时间与投入；
13. 政策必须经过 Governance Execution；
14. 身份不构成经济行为输入禁令；
15. Economy 不创建 Character Hunger / Injury；
16. UI 不直接修改 Resource。

---

# 9. High-frequency Actions

- Purchase / Sell；
- Establish Business；
- Agricultural Production；
- Store / Withdraw；
- Bulk Transfer；
- Tax / Extraction；
- Corvee / Public Labor；
- Relief；
- Tax Reduction / Deferral；
- Public Works；
- Repair Infrastructure；
- Tuntian；
- Resettle Refugees；
- Bulk Transport；
- Private low-level economic activity by high-status character。

Action Definition：

> 不是自由输入白名单。

---

# 10. Resolution Contract

```text
Economic / Governance Attempt
↓
Player / NPC Authorization
↓
Politics Authority if required
↓
Character Capability
↓
Resource / Place / Time
↓
Local Governance Execution Capacity
↓
Market / Population / Labor / Infrastructure
↓
确定性条件
↓
必要时 Program RNG
↓
Economic Outcome Candidate
↓
Validation
↓
Atomic Commit
↓
Resource / State / Event
↓
Survival / War / Politics / History Handoff
↓
Player-safe Feedback
```

---

# 11. War Integration

## Economy → War

提供：

- Grain；
- Treasury；
- strategic materials；
- bulk transport；
- labor / recruitment source；
- infrastructure；
- supply availability。

War 不能自己创建：

> 第二份军粮库存。

## War → Economy

提交：

- resource consumption；
- warehouse loss；
- road / bridge / irrigation damage；
- population death / capture / displacement；
- labor loss；
- route disruption；
- military requisition Event。

Economy 根据正式 War Outcome：

> 更新社会经济 State。

---

# 12. Politics Integration

Politics 提供：

- Authority；
- Political Control；
- Office / jurisdiction；
- tax / requisition decision；
- public policy。

Economy 决定：

- 是否执行到位；
- 收入多少；
- 实际资源移动；
- 地方长期后果。

政治命令成立：

> 不等于经济结果自动成立。

---

# 13. History Integration

Economy 输出高影响 Event：

- Tuntian established；
- Famine / shortage；
- Major displacement；
- Economic collapse；
- Major recovery；
- Large public works；
- Tax / extraction crisis。

History：

> 只做 Original History Reference 重评估。

---

# 14. Information Boundary

玩家可见精度必须服从 Knowledge。

世界真实：

> 某仓有 82,413 斛。

玩家只掌握粗账：

> UI 可以显示“约八万斛 / 储备充足”。

隐藏私人仓库、远方真实库存、秘密截留：

> 不发送浏览器。

---

# 15. G8 UI Contribution

本包：

> **不拥有新的一级 Extension Surface。**

它向 Politics 拥有的：

> `势力 / 政务`

贡献二级 View / Section：

```text
势力 / 政务
├─ 财赋
├─ 民生
└─ 工程
```

还可以贡献：

### 地图

- production overlay；
- shortage；
- transport；
- infrastructure。

### Place / Region Detail

- local economy；
- market；
- livelihood；
- infrastructure。

### 物品

- bulk storage / item bridge 的玩家安全引用。

### Player Character Detail

- personal economy summary。

Host 仍拥有：

- layout；
- responsive；
- safety；
- accessibility。

---

# 16. Save / Restore

必须恢复：

- Treasury；
- Bulk Stocks；
- Production；
- Demographic；
- Labor；
- Governance Execution；
- Public Burden；
- Livelihood；
- Market；
- Infrastructure；
- Public Works；
- Bulk Transport；
- related Event / Knowledge；
- Resource↔Item bridge committed boundary。

读档后不得：

- 重复收税；
- 重复发放赈粮；
- 重复物化库存；
- 用新历史资料覆盖旧经济状态。

---

# 17. Standard Regression Scenarios｜20

1. 正常小额买粮无需 Dice；
2. 有钱但本地无粮不能瞬间买到；
3. 皇帝亲自卖粮允许但产生时间 /职责 /社会上下文；
4. 无 Authority 不能合法调官仓，但可尝试偷 /骗 /强取；
5. 开仓赈济真实减少库存；
6. 极端征税可执行但提高负担与长期风险；
7. 屯田不是即时产粮；
8. 过重徭役降低 Labor Availability；
9. War 破坏水利后 Productive Capacity 下降；
10. 战争结束不自动恢复；
11. 角色买不到食物 → Survival Need，不直接 Health；
12. Survival 缺食长期化 → Health Condition；
13. Economy 不保存 Character Hunger；
14. Bulk Stock 物化为 Item 必须原子扣减；
15. Item 存回仓库不能双算库存；
16. Politics 免税命令合法，但地方执行可能不完全；
17. Economy Skill mastery 只在 EP-CHAR-CORE；
18. 隐藏粮仓不泄露；
19. Save / Restore 不重复资源事务；
20. Economy 内容只 contribute `势力 / 政务`，不重复 owns 一级 Surface。

---

# 18. Host Requirements

| 能力 | 级别 |
|---|---|
| Located Bulk Resource | 必需 |
| Resource ↔ Item bridge | 必需于高精度库存 |
| World Time / Timed Process | 必需 |
| Region / Place binding | 必需 |
| Production / Infrastructure persistence | 必需 |
| Demographic / Labor | 必需 |
| Politics Authority read | Governance 路径必需 |
| EP-CHAR-CORE Skill query | 推荐 |
| Survival Resource availability handoff | 推荐 |
| War resource consume / damage handoff | 完整战争必需 |
| Knowledge-safe projection | 必需 |
| Atomic Commit / idempotency | 必需 |
| Save / Restore | 必需 |
| Surface Contribution | 推荐 |

---

# 19. Creator / G9 Requirements

未来需要声明式支持：

- Bulk Resource；
- Storage Context；
- Timed Production；
- Population / Labor；
- Governance Execution；
- Market Condition；
- Public Burden / Livelihood；
- Infrastructure；
- Resource ↔ Item bridge；
- Politics Authority dependency；
- War consume / damage interface；
- Survival availability handoff；
- Economy Skill contribution；
- `势力 / 政务` Surface contribution。

禁止任意 JS 经济公式。

---

# 20. Migration From v0.1.3

## 保留

- Treasury / Grain；
- Productive Capacity；
- Demographic / Labor；
- Market；
- Public Burden / Livelihood；
- Infrastructure；
- Tuntian；
- Relief；
- Tax / Corvee；
- Bulk Transport；
- Open Attempt。

## 重构

- Administrative Reach → Local Governance Execution Capacity；
- Character Skill → EP-CHAR-CORE；
- Survival old interface → Economy → Survival → Health；
- War supply interface → new War v0.2；
- UI → contribute Politics Surface；
- Resource / Item 双轨 → bridge contract。

## 删除

- 任何个人 Physical Fatigue / Injury / Disease / Recovery Ownership；
- 旧三国人物能力包 dependency；
- Economy 自己维护 Character “治理能力”的可能性。

---

# 21. Final Freeze

> **Economy 拥有社会和地方层钱粮、生产、人口、劳力、市场、行政执行、工程与民生。**
>
> **Survival 拥有 Character 生存需求；Health 拥有身体结果。**
>
> **Politics 决定有没有权；Character Core 决定人物会不会做；Economy 决定组织和资源实际能不能做到。**
>
> **War 消费 Economy 的真实资源，不复制军粮。**
>
> **Bulk Resource 与 Item / Placement 必须通过原子桥接，不允许双库存。**
>
> **本包只 contribute `势力 / 政务`，不拥有第二个一级 Economy Surface。**
