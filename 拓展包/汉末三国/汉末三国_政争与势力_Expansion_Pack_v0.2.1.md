---
title: 汉末三国：政争与势力｜Expansion Pack
aliases:
  - 三国政治机制拓展包
  - Han Late Three Kingdoms Politics Expansion
created: 2026-08-16
updated: 2026-08-16
status: candidate
version: 0.2.1
workflow_mode: light-asset
operation_mode: revise
asset_type: expansion-pack
output_profile: obsidian-markdown
asset_family: 汉末三国：天下未定
world_pack: "[[汉末三国_天下未定_World_Pack_v0.2.3]]"
character_core: "[[人物能力与技艺_Expansion_Pack_v0.1.5]]"
relationship_core: "[[关系与恋爱核心_Expansion_Pack_v0.2]]"
health_core: "[[身体状态核心_Expansion_Pack_v0.1]]"
economy_expansion: "[[汉末三国_财赋与治理_Expansion_Pack_v0.2]]"
war_expansion: "[[汉末三国_军略与战争_Expansion_Pack_v0.2]]"
history_expansion: "[[汉末三国_历史参照与分歧_Expansion_Pack_v0.2]]"
creator_binding: pending
asset_spec_binding: pending
runtime_asset: true
language: zh-CN
tags:
  - 三国
  - ExpansionPack
  - 政治
  - 势力
  - 官职
  - 外交
  - 继承
  - 政权
  - Authority
  - Jurisdiction
  - RuntimeExtensibleUI
---

# 汉末三国：政争与势力｜Expansion Pack v0.2.1

> [!abstract] 一句话定位
> **把汉末三国世界中的政治集团、政治归属、官职与职权、政治承认、政治控制、外交、继承、政治主张与政权转化，变成持续、可验证、由 Program 正式裁定和提交的政治机制。**
>
> 本包回答的是：
>
> **“谁在什么政治结构中拥有什么正式身份、权力、立场、主张和制度关系，这些政治事实怎样合法改变？”**
>
> 它不拥有私人感情、不拥有 Character Capability、不拥有 World OS Commitment，也不把政治身份变成玩家行为白名单。

> [!important] v0.2 重构依据
> 本版是对旧 `《汉末三国：政争与势力》v0.1.3` 的中度重构。
>
> 主要变化：
>
> - 删除对旧 `《汉末三国：人物能力与技艺》` 的依赖；
> - 改为消费通用 `EP-CHAR-CORE`，并贡献政治领域 Skill Definition；
> - 正式分离 Politics 与 Relationship Truth；
> - 正式分离 Political Agreement 与 World OS Commitment；
> - 政治婚姻不再由 Politics 拥有 Marriage Bond；
> - “政治支持”只表示正式政治立场 / 背书，不创建私人关系数值；
> - 接入 `EP-HEALTH-CORE` 的人物履职可用性读取边界；
> - 正式请求拥有 G8 一级 `势力 / 政务` Extension Surface；
> - 为后续 Economy 贡献到该 Surface 预留明确 Contributor 边界；
> - 不冻结 G9 asset-spec vNext 的机器字段。

---

# 0. Current Contract｜当前冻结方向

本版采用以下硬边界：

1. Politics 继续是汉末三国政治事实 Owner；
2. Character Capability 统一归 `EP-CHAR-CORE`；
3. Relationship / Romance 统一归 `EP-RELATIONSHIP-ROMANCE-CORE`；
4. World OS `Commitment` 继续拥有“谁明确答应了谁什么”；
5. Politics 可以拥有 Political Agreement / Institutional Relation，但不复制 Commitment；
6. Marriage Bond 属于 Relationship Core；婚姻政治后果属于 Politics；
7. Political Support / Endorsement 属于 Politics；私人 Trust / Respect / Attachment 属于 Relationship；
8. Authority / Jurisdiction 决定正式政治效果是否成立，不决定玩家能不能尝试；
9. Politics 不创建万能“忠诚度 / 合法性 / 政治点”；
10. Program 拥有 RNG / Formal Outcome / Atomic Commit；
11. 本包拥有一个一级 `势力 / 政务` Extension Surface；
12. Economy 可以向该 Surface contribute，但不能 owns 同一 Surface。

---

# 1. Scope Lock｜职责边界

## 1.1 本包唯一回答的问题

> **“一个人物或政治主体目前处在怎样的政治结构中；谁拥有什么正式政治身份、职权、承认、控制、外交关系、继承安排和政治主张；这些事实怎样通过合法政治行为发生改变？”**

## 1.2 本包必须负责

- Political Faction / Regime；
- Political Affiliation；
- Office Definition 的题材语义；
- Office Holding；
- Political Authority / Jurisdiction；
- Political Recognition；
- Political Control；
- Organization-to-Organization Diplomatic Relation；
- Political Agreement / Institutional Relation；
- Recruitment / Recommendation / Appointment；
- Political Endorsement / Opposition；
- Succession；
- Political Claim；
- Regime Formation / Transition；
- Political Event；
- Politics Knowledge / player-safe projection；
- Politics → War / Economy / History Handoff；
- Politics UI Surface Ownership。

## 1.3 本包明确不负责

- Character Personality；
- Character 六层 Capability State；
- Sentiment；
- Trust；
- Respect；
- Attachment；
- Relationship Commitment；
- Romantic Attraction；
- Relationship Memory；
- Marriage Bond；
- World OS Commitment；
- 私人财产与嫁资；
- Treasury / Grain / Tax Outcome；
- Formation / Campaign / Battle Outcome；
- HP / Injury / Disease / Treatment / Recovery；
- Historical Reference Validity；
- RNG / Dice；
- Formal Outcome；
- Atomic Commit；
- Creator / asset-spec 最终机器 Schema。

---

# 2. Ownership Map｜唯一事实源

| 概念 | 唯一 Owner | Politics 如何使用 |
|---|---|---|
| 人格 / 价值观 /长期目标 | Character Definition | NPC 政治选择输入 |
| Character Capability | EP-CHAR-CORE | Optional Capability Integration |
| 私人 Relationship Truth | EP-RELATIONSHIP-ROMANCE-CORE | Context / Event Handoff |
| Marriage Bond | EP-RELATIONSHIP-ROMANCE-CORE | 读取成立事实 |
| 明确 Promise / Commitment | World OS Commitment | 引用 / 创建 Handoff |
| 政治集团 | 本 Expansion | 正式职责 |
| 政治归属 | 本 Expansion | 正式职责 |
| 官职 / Office Holding | 本 Expansion | 正式职责 |
| Authority / Jurisdiction | 本 Expansion + World / Office structure | 正式政治效果验证 |
| Political Recognition | 本 Expansion | 正式职责 |
| Political Control | 本 Expansion | 正式职责 |
| 外交政治关系 | 本 Expansion | 正式职责 |
| 继承 | 本 Expansion | 正式职责 |
| Political Claim | 本 Expansion | 正式职责 |
| 财政 / 粮食 /人口 /治理执行 | 财赋与治理 | Safe Read / Handoff |
| Formation / Campaign / Military Occupation | 军略与战争 | Safe Read / Handoff |
| Persistent Health | EP-HEALTH-CORE | 履职可用性输入 |
| Historical Reference / Divergence | 历史参照与分歧 | Event Consumer |
| World Time / Event / Knowledge | World OS / Runtime | 复用 |
| Formal Outcome / Atomic Commit | Runtime | 执行 |

---

# 3. Politics != Relationship｜政治事实与私人关系分离

这是本版最重要的收口之一。

## 3.1 私人关系归 Relationship Core

例如：

```text
A → B
Trust = 高
Respect = 高
Attachment = 高
```

属于：

> Relationship Core。

Politics 不保存第二套：

- 私人忠诚值；
- 好感；
- 友情；
- 爱情；
- 私人信赖。

## 3.2 Political Support｜政治支持

Politics 可以保存：

> **一个人物或政治主体在某个明确政治议题上的正式支持 / 反对 / 背书。**

例如：

- 公开支持曹丕继承；
- 拒绝承认某帝号；
- 支持某项联盟；
- 站在某派系一方；
- 表态拥护某一政治主张。

它回答：

> **“在这个政治议题上，他正式站在哪边？”**

不回答：

> “他私人有多喜欢这个人？”

## 3.3 同一人物可以关系亲近但政治反对

合法状态：

```text
Relationship:
A 很信任 B

Politics:
A 公开反对 B 的称帝主张
```

同样：

```text
Relationship:
A 与 B 私人关系很差

Politics:
A 因共同利益正式支持 B 的继承资格
```

两套事实不能互相覆盖。

## 3.4 不建立 Universal Loyalty Score

“忠诚”在汉末语境中可能同时涉及：

- 私人情感；
- 价值观；
- 政治归属；
- 公开政治立场；
- 对 Office / Regime 的责任；
- 明确 Commitment。

因此本包不建立：

> `loyalty = 82`

这种万能状态。

必须根据具体语义落到对应 Owner。

---

# 4. Marriage Boundary｜政治婚姻分权

## Relationship Core owns

- Marriage Bond；
- 双方 Directed Relationship；
- Relationship Agreement；
- Boundary；
- Relationship Memory。

## Politics owns

- 联姻提案的政治条件；
- 家族 / 势力是否支持；
- 联姻产生的 Political Agreement；
- Alliance / Recognition / Succession consequence；
- 对政治主张的影响。

## Economy owns

- 嫁资；
- 财产；
- 土地；
- Resource transfer。

因此：

```text
Marriage
!=
Political Alliance
!=
Economic Transfer
!=
Love
```

一场婚姻可以成立，而政治联盟失败。

也可以形成政治合作，而双方没有 Romantic Attraction。

---

# 5. Political Agreement vs World OS Commitment

## 5.1 Political Agreement｜政治制度关系

Politics 可以拥有持续的政治协议状态，例如：

- Alliance；
- Non-aggression；
- Submission / Suzerainty；
- Mutual Recognition；
- Joint Political Objective；
- Cease-hostility political agreement。

它保存：

> 参与政治主体之间已经成立的制度性 / 政治关系。

## 5.2 Commitment｜明确承诺对象

如果协议中出现：

> “我方承诺在三个月内提供五千石粮。”

或：

> “我答应在遭到进攻时出兵相救。”

则具体 Promise：

> **必须进入 World OS Commitment。**

正确链：

```text
Political Negotiation
↓
Political Agreement established
+
explicit promises extracted
↓
World OS Commitment
```

之后：

- Agreement 是否仍成立 → Politics；
- Promise 是否履行 / 违背 → Commitment；
- 财政能否支付 → Economy；
- 出兵是否发生 → War。

## 5.3 Politics 不复制 Commitment lifecycle

Politics 不建立：

- pending political promise；
- fulfilled political promise；
- broken political promise；

第二套状态。

它只引用正式 Commitment，并消费履行 / 违背 Event 的政治后果。

---

# 6. Character Capability Integration｜人物能力接口

旧三国人物能力包已经退役。

本包现在统一消费：

> `EP-CHAR-CORE｜人物能力与技艺`

## 6.1 Politics contributes Skill Definitions

本包向统一 Skill Registry 贡献：

### 法政

- 法令；
- 官制；
- 制度；
- 程序；
- 政治规范。

### 人事与识才

- 判断人才；
- 职责匹配；
- 组织用人。

不等于：

> 读心 / 看穿人格。

### 外交

- 政治主体之间的正式沟通；
- 条件交换；
- 长期政治关系设计。

### 辩说

- 论证；
- 说服；
- 反驳；
- 正式 / 非正式政治表达。

### 政局判断

- 权力结构；
- 派系；
- 时机；
- 名义与实际力量；
- 政治风险。

## 6.2 Politics 不拥有 Skill mastery

正确：

```text
Politics
→ contributes Skill Definition

EP-CHAR-CORE
→ owns Character Skill State
```

禁止：

```text
Politics.characterPolitics = 90
```

## 6.3 Capability 不能强制政治结果

即使：

- 辩说顶尖；
- 外交顶尖；
- 政局判断顶尖；

也不能：

- 强迫 NPC 背叛；
- 强迫势力投降；
- 强迫 Marriage；
- 越过 Authority；
- 创造不存在的资源；
- 抹掉政治核心利益。

Capability 只影响：

> 真实可改变空间中的执行质量。

---

# 7. Political State Model｜政治状态模型

## 7.1 Political Faction / Regime

表示一个持续政治主体：

- 当前是否存在；
- 公开身份；
- 领导结构；
- 政治中心；
- 成员 / 附属结构；
- 被哪些主体承认。

它不拥有：

- 全部军队；
- 全部财政；
- 人物全部关系。

---

## 7.2 Political Affiliation

表示 Character / Organization 与政治主体之间的正式政治关系。

例如：

- formal service；
- retainer / staff；
- subject；
- vassal-like relation；
- temporary political cooperation；
- independent；
- withdrawn。

一个 Character 可以同时拥有多个不同层次身份。

不能压成：

> 一个 `factionId`。

---

## 7.3 Office Holding

记录 Character 当前正式持有的官职 / 政治职位。

至少语义上回答：

- Office 是什么；
- 谁授予；
- 何时生效；
- jurisdiction；
-职责；
- 是否有争议；
- 当前哪些主体承认；
- 当前是否仍有效。

Office 是正式 State。

Event 只记录：

> 曾经任命过。

---

## 7.4 Authority / Jurisdiction

Authority 回答：

> **当前角色 / 政治主体是否具有让某种政治效果正式成立的制度性权力来源。**

Jurisdiction 回答：

> **这种权力在哪些对象 / 地域 / 组织范围内有效。**

它们不是：

> 玩家输入许可。

无权者仍可尝试：

- 宣称任命；
- 伪造诏令；
- 冒名代表；
- 私下命令；
- 威胁；
- 收买；
- 政治表演。

只是：

> 对应“合法正式效果”不自动成立。

---

## 7.5 Political Recognition

方向性表达某政治主体是否承认：

- Office；
- Regime；
- Ruler；
- Successor；
- Territory Claim；
- Political Status。

Recognition 可以：

- 单向；
- 条件性；
- 局部；
- 暂时；
- 公开 / 私下不同。

不建立全球唯一：

> Legitimacy Score。

---

## 7.6 Political Control

表示某政治主体对 Region / Place 的：

- 实际行政控制；
- 名义主张；
- 外部承认关系。

必须区分：

```text
Claim
!=
Office jurisdiction
!=
Military Occupation
!=
Actual Political Control
!=
Recognition
```

War 可以产生：

> Military Occupation。

Politics 再决定：

> 是否形成行政接管 / Political Control。

---

## 7.7 Diplomatic Political Relation

用于 Organization / Faction 之间持续关系：

- alliance；
- hostility；
- neutral；
- submission；
- suzerainty；
- mutual recognition；
- non-recognition。

不要求对称。

---

## 7.8 Succession

用于表达：

- 当前领导；
- 已指定候选；
- 公开候选；
- Political Endorsement；
- Regency；
- Succession dispute；
- Succession resolution。

指定继承人：

> 不等于自动继承成功。

---

## 7.9 Political Claim

保存公开 / 正式提出的：

- Office Claim；
- Succession Claim；
- Territorial Claim；
- Regime Name；
- Imperial / Royal Claim；
- Orthodoxy Claim。

Claim 是真实政治行为。

但：

> Claim != Recognition != Control。

---

# 8. Core Gameplay Loops｜主要玩法闭环

## 8.1 仕进 / 政治归属

```text
接触政治主体
↓
投奔 / 征辟 / 推荐 /招揽
↓
Character-specific political choice
↓
接受 / 拒绝 / 试用 / 附条件
↓
Political Affiliation
↓
职责与后续政治 Event
```

## 8.2 Office

```text
出现职务需求
↓
推荐 / 任命
↓
Authority / jurisdiction validation
↓
目标自主接受 / 拒绝
↓
Office Holding
↓
职责 / Authority change
```

## 8.3 Diplomacy

```text
利益 / 威胁 / 争议
↓
Proposal
↓
authorized representation
↓
negotiation
↓
Political Agreement
+
World OS Commitment if explicit promise
↓
future fulfillment / violation
```

## 8.4 Succession

```text
领导权真空 / 退位 /死亡 /失能
↓
读取既有 succession state
↓
政治支持 /反对 /候选
↓
control + recognition + office + war context
↓
Succession Resolution
↓
领导变化 / 摄政 / 分裂 / 未决
```

## 8.5 Regime Transition

```text
政治条件变化
↓
Claim / declaration
↓
internal establishment
↓
Recognition
↓
Political Control
↓
Regime State change
```

---

# 9. Open Attempt｜开放尝试与政治效果

本包继续冻结：

> **身份和 Authority 约束正式政治效果，不删除玩家尝试。**

例如普通县吏说：

> “我任命你为荆州牧。”

正确结果是：

```text
Attempt happened
↓
Authority insufficient
↓
Legal Office Holding NOT created
↓
Possible Event:
false order / political performance / fraud / provocation
↓
NPC / Politics / Relationship consequence
```

而不是：

> 输入按钮灰掉。

---

# 10. Political Actions｜高频结构化政治行为

这些是机制化路径，不是玩家行为全集。

- 求见 / 建立政治接触；
- 投奔 / 请求加入；
- 招揽；
- 举荐；
- 正式任命；
- 撤职；
- 辞官；
- 改变 Political Affiliation；
- 提出联盟；
- 提出臣属 / 接受册封；
- 宣布独立；
- 承认 / 撤回承认；
- 公开支持 / 反对政治候选；
- 指定继承候选；
- 建立新政治集团；
- 宣布政权 / 变更名号；
- 提出政治婚姻条件；
- 签订 / 终止 Political Agreement；
- 提出新的 Political Claim。

未预定义的：

- 伪造诏书；
- 冒名代表；
- 私下策反；
- 假传任命；
- 政治勒索；

仍由 Runtime 忠实理解并映射到正式状态 / Event。

---

# 11. Resolution Contract｜政治裁定链

```text
Political Attempt
↓
Player / NPC Agency Authorization
↓
Current Political State
↓
Authority / Jurisdiction
↓
Character Definition
↓
Relationship Context if relevant
↓
World OS Commitments if relevant
↓
EP-CHAR-CORE Capability if relevant
↓
Economy / War / Health context if relevant
↓
确定性条件
↓
必要时 Program Resolution / RNG
↓
Political Outcome Candidate
↓
Validation
↓
Atomic Commit
↓
Political State / Event / Commitment Handoff
↓
Player-safe Feedback
```

## 11.1 不滥用 Dice

以下通常无需 Dice：

- 有权任命 + 对方明确接受；
- 无权者要求合法任命生效；
- NPC 核心立场明确不可改变；
- 已成立 Political Agreement 的确定性状态更新。

只有真正：

- 不确定；
- Capability 有意义；
- 多种 Outcome 都合理；
- 风险事前成立；

才请求 Program Resolution。

---

# 12. Recruitment / Appointment / Diplomacy / Succession

## 12.1 Recruitment

必须读取：

- Character Definition；
- 当前 Political Affiliation；
- Relationship；
- Commitment；
- 安全；
- 家庭 / 社会条件；
- 提供职位；
- 当前政治风险。

高 Skill：

> 不等于自动加入。

## 12.2 Appointment

先做确定性检查：

1. Office 是否存在；
2. 任命者有无 Authority；
3. jurisdiction 是否匹配；
4. 目标是否愿意接受；
5. 当前是否有冲突 Holding。

条件明确时：

> 不需要 Dice。

## 12.3 Diplomacy

Outcome 必须读取：

- 当前利益；
-共同威胁；
- Political Relation；
- Recognition；
- 可兑现 Commitment；
- Economy；
- War；
- Character leader decision。

不能通过高骰：

> 让根本不可能的无条件臣服成立。

## 12.4 Succession

继承不是把旧领导的：

- Office；
- Control；
- Relationship；
- Army；
- Recognition；

全部复制给继承人。

它必须独立结算。

---

# 13. Health Integration｜身体状态与履职

Politics 不拥有：

- 伤势；
- 疾病；
- 疲劳；
- 意识；
- HP。

但可以读取 Health Core 的正式结果，例如：

```text
Character:
严重昏迷 / 无法履职
↓
Politics:
Office duties require regency / temporary delegation / succession review
```

注意：

> Health 只提供身体事实。

是否：

- 摄政；
- 罢免；
- 继承；
- 权力真空；

仍由 Politics + World rules 决定。

---

# 14. Cross-domain Handoffs

## 14.1 Politics ↔ Relationship

Politics → Relationship：

- public support；
- betrayal；
- marriage political pressure；
- appointment；
- dismissal；
- protection；
- political conflict；

可以形成 Source Event。

Relationship 决定：

> Character 如何解释这些 Event。

Relationship → Politics：

- Marriage Bond；
- known interpersonal context；

可成为政治输入。

不允许 Relationship 数值直接写：

> Political Affiliation。

---

## 14.2 Politics ↔ Economy

Politics 提供：

- Authority；
- Political Control；
- public policy；
- tax / requisition decision；
- Office / jurisdiction。

Economy 负责：

- 能不能执行；
- 收到多少；
- 地区受到什么长期经济影响。

例如：

```text
Politics:
免税命令合法成立

↓
Economy:
行政网络是否执行
↓
实际收入 / 民生后果
```

---

## 14.3 Politics ↔ War

Politics → War：

- command authority；
- affiliation；
- alliance / hostility；
- political war objective；
- surrender political terms。

War → Politics：

- Military Occupation；
- commander captured / killed；
- Formation collapse；
- campaign result；
- military surrender。

War 不自动写：

> Political Control。

---

## 14.4 Politics → History

Politics 输出：

- Succession Change；
- Regime Formation；
- Recognition Change；
- Political Control Change；
- Major Alliance Change；
- other high-impact Political Event。

History：

> 只重评估 Reference。

不能要求 Politics：

> 贴回现实历史。

---

# 15. Information Boundary｜政治信息边界

## 15.1 通常玩家可知

依身份与来源：

- 公开 Office；
- 公开 Regime；
- 公开 Alliance；
- 公开 Claim；
- 已公布继承人；
- 已知 Political Control；
- 玩家自己的政治身份。

## 15.2 默认隐藏

- secret political endorsement；
- secret diplomacy；
- private succession plot；
- concealed defection intent；
- hidden faction plan；
- private recognition bargain。

## 15.3 Political State != Player Knowledge

Runtime 可以知道：

> 某派系正在秘密支持某继承人。

玩家若没有合法来源：

> UI 不显示。

---

# 16. Runtime-extensible UI｜G8 Surface Contract

本包正式请求：

> **拥有一个一级 Extension Surface：`势力 / 政务`**

当前只是产品语义，不冻结 G9 Surface ID。

## 16.1 推荐二级 View

```text
势力 / 政务
├─ 概览
├─ 势力
├─ 官职
├─ 人才
├─ 外交
├─ 继承
└─ 政治主张
```

后续 `财赋与治理` 可向该 Surface contribute：

```text
财赋
民生
工程
```

Economy：

> 不能重复 owns 同一一级 Surface。

## 16.2 Core Surface Contributions

同时可以向：

### 人物

贡献：

- Office Badge；
- Political Affiliation；
- public Political Endorsement；
- known Office history。

### 地图

贡献：

- Political Control Overlay；
- Claim Overlay；
- disputed region。

必须区分：

> Control / Claim / Military Occupation。

### 信息

贡献：

- public political event；
- known diplomacy；
- known succession information；
- political rumor / knowledge。

### 目标

引用：

- 玩家正式接受的政治 Task / Objective。

Politics 不自己建立第二 Task Owner。

## 16.3 Action Intent

UI 中：

- 任命；
- 招揽；
- 外交；
- 支持候选；
- 政权宣言；

按钮只能生成：

> Action Intent。

UI 不直接修改 Political State。

## 16.4 Host Authority

资产描述：

- View；
- Section；
- Card；
- Map Overlay；
- Action Intent。

Host 决定：

- Layout；
- Responsive；
- Accessibility；
- Safe Component；
- Player ordering。

---

# 17. Initialization｜初始化

T0 Bootstrap 可以从：

- World Pack；
- Historical Baseline；
- Character Definition；
- current time anchor；

建立：

- Political Faction；
- Affiliation；
- Office Holding；
- Recognition；
- Political Control；
- Diplomatic Relation；
- Succession；
- Claim。

这些进入：

> Game Instance。

不回写 Expansion Definition。

---

# 18. Save / Restore

必须恢复：

- Faction State；
- Affiliation；
- Office Holding；
- Recognition；
- Political Control；
- Diplomatic Relation；
- Political Agreement；
- Succession；
- Claim；
- Political Event boundary；
- Player Knowledge；
- linked World OS Commitments；
- UI-independent authoritative state。

Restore：

- 不重新调用模型决定谁是皇帝；
- 不因为现实历史更新覆盖旧 Save；
- 不回滚玩家 Surface ordering preference。

---

# 19. Standard Regression Scenarios｜20 个

## T-POL-01｜合法任命

有 Authority，Office 存在，对方明确接受。

期望：

- 无意义 Dice 不发生；
- Office Holding 正式成立。

## T-POL-02｜越权任命

县吏宣布任命州牧。

期望：

- Attempt 成立；
- 合法 Office 不成立；
- 可产生政治 / 欺诈 Event。

## T-POL-03｜玩家未接受任官

NPC 要玩家当军师。

期望：

- Invitation 可以发生；
- 玩家不自动接受；
- Office / Affiliation 不变。

## T-POL-04｜高辩说不能强制背叛

目标核心利益明确冲突。

期望：

- Capability 不覆盖 Character autonomy。

## T-POL-05｜政治支持与私人关系分离

A 与 B 私人关系很好，但 A 公开反对 B 称帝。

期望：

- Relationship 不被 Politics 自动改成敌对；
- Political Opposition 成立。

## T-POL-06｜政治婚姻

双方 Marriage 成立。

期望：

- Relationship Core owns Marriage；
- Politics 可以建立 Alliance candidate；
- Alliance 不自动成立。

## T-POL-07｜联盟含明确承诺

联盟协议约定三月内运粮。

期望：

- Alliance → Politics；
- 运粮 Promise → World OS Commitment；
- 财力 / 粮食 Outcome → Economy。

## T-POL-08｜Commitment 违背

盟友未按期出兵。

期望：

- Commitment 标记正式违背；
- Politics 消费 Event 决定 Alliance 后果；
- 不维护第二 Promise state。

## T-POL-09｜秘密继承支持

NPC 私下支持候选人。

期望：

- 世界状态可存在；
- 玩家无合法来源时 UI 不显示。

## T-POL-10｜Health 导致无法履职

君主重伤昏迷。

期望：

- Health owns bodily truth；
- Politics 可以处理摄政 / succession pressure；
- 不复制昏迷状态。

## T-POL-11｜军事占领 != 政治控制

War 占领县城。

期望：

- Politics 读取 Military Occupation；
- Political Control 需单独成立。

## T-POL-12｜称帝但无人承认

地方首领称帝。

期望：

- Claim 成立；
- Regime / Recognition 分开；
- 不自动控制更多地区。

## T-POL-13｜Recognition 不对称

A 承认 B 为合法君主；C 不承认。

期望：

- 两条方向性 Recognition 并存。

## T-POL-14｜Character Skill contribution

Politics 定义辩说 Skill。

期望：

- Character mastery 保存于 EP-CHAR-CORE；
- Politics 不存第二份 skill level。

## T-POL-15｜Economy contributor surface

Economy 安装。

期望：

- 财赋 / 民生进入 `势力 / 政务`；
- 不出现第二个同名一级 Surface Owner。

## T-POL-16｜Map Overlay

某地区 Claim 与 Control 不一致。

期望：

- UI 视觉区分；
- 不把 Claim 画成实际控制。

## T-POL-17｜T0 后历史污染

当前世界政治格局已改变。

期望：

- 不按现实历史强制未来 Political Event。

## T-POL-18｜Save / Restore

联盟破裂后读回旧 Save。

期望：

- Alliance、Office、Recognition、Knowledge 全部回到旧状态。

## T-POL-19｜重复任命请求

客户端重试。

期望：

- 一个 Office change；
- 一个 Event；
- no duplicate commit。

## T-POL-20｜未预定义政治尝试

玩家伪造诏书。

期望：

- 不因 Action Registry 缺项拒绝；
- 处理伪造 / 欺骗 /政治后果；
- Authority 不被自动授予。

---

# 20. Host Requirements

| ID | Host 能力 | 必需性 | 缺失行为 |
|---|---|---|---|
| HR-POL-01 | Organization / Faction runtime | 必需 | 无法完整运行 |
| HR-POL-02 | Multi-layer Political Affiliation | 必需 | 政治身份过度简化 |
| HR-POL-03 | Office Definition / Holding | 必需 | 任官无法正式化 |
| HR-POL-04 | Authority / Jurisdiction validation | 必需 | 正式政治效果失控 |
| HR-POL-05 | Directional Recognition / Diplomacy | 必需 | 政治关系降级 |
| HR-POL-06 | Political Control / Claim | 必需 | 地区政治无法表达 |
| HR-POL-07 | NPC autonomous political choice | 必需 | NPC 退化为玩家工具 |
| HR-POL-08 | EP-CHAR-CORE Capability Query | 推荐 | 专业政治能力降级 |
| HR-POL-09 | Relationship safe read / event handoff | 推荐 | 人际政治上下文降级 |
| HR-POL-10 | World OS Commitment integration | 必需 | Agreement 会复制 Promise |
| HR-POL-11 | Health availability read | 推荐 | 履职状态粗粒度 |
| HR-POL-12 | Economy / War safe integration | 推荐 | 跨域政治后果降级 |
| HR-POL-13 | Event / Knowledge | 必需 | 历史与信息不可追踪 |
| HR-POL-14 | Save / Restore | 必需 | 长期政治不可用 |
| HR-POL-15 | Atomic Commit / idempotency | 必需 | 重复任命 / 半提交 |
| HR-POL-16 | Extension Surface Ownership | 推荐 | 文本降级 |
| HR-POL-17 | Map Overlay | 推荐 | 地缘政治只能文本 |

---

# 21. Dependency / Integration Position

## Required Semantic Provider

- `汉末三国：天下未定 World Pack`；
- World OS / Runtime。

## Optional / Strong Integrations

- `EP-CHAR-CORE`；
- `EP-RELATIONSHIP-ROMANCE-CORE`；
- `EP-HEALTH-CORE`；
- `财赋与治理`；
- `军略与战争`；
- `历史参照与分歧`。

本包不因为某一 Optional Integration 缺失就：

> 建立第二套对应状态。

例如没有 Relationship Core：

- 政治仍可运行；
- 但私人关系上下文降级；
- Politics 不能自己创建 Trust / Love。

---

# 22. Creator / asset-spec vNext Requirements

未来协议需要能够表达：

- Faction / Organization；
- Political Affiliation；
- Office Definition / Holding；
- Authority / Jurisdiction；
- Recognition；
- Political Control；
- Claim；
- Diplomatic Relation；
- Political Agreement；
- Succession；
- Political Skill Contribution；
- World OS Commitment Handoff；
- Relationship / Economy / War safe link；
- Extension Surface Ownership；
- Contributor View / Section；
- Map Overlay；
- Conflict detection。

不能要求：

- 任意 JS；
- Politics 自建 NPC AI；
- Politics 自建 Relationship Engine；
- Politics 自建 Commitment Engine；
- Creator 自己 Commit Game State。

---

# 23. Migration From v0.1.3

## Removed

- 旧 `汉末三国：人物能力与技艺` dependency；
- Politics 自己解释人物“政治 / 魅力”能力的降级路线；
- 模糊的“政治支持 = 私人关系”空间；
- Political Agreement 与 Commitment 混用风险；
- Politics 对 Marriage Bond 的潜在 Ownership；
- 旧 Survival Health Owner 引用。

## Added / Rebound

- EP-CHAR-CORE；
- Politics Skill Contribution；
- EP-RELATIONSHIP-ROMANCE-CORE；
- World OS Commitment；
- EP-HEALTH-CORE availability read；
- G8 `势力 / 政务` Surface Ownership；
- Economy Surface Contribution boundary。

## Preserved

- Faction；
- Affiliation；
- Office；
- Authority；
- Recognition；
- Control；
- Diplomacy；
- Succession；
- Claim；
- Regime Transition；
- Open Attempt；
- NPC autonomy；
- Knowledge boundary。

---

# 24. Quality Gate

| Gate | Result |
|---|---|
| Scope / Ownership | PASS |
| Character Core Rebind | PASS |
| Political Skill Contribution | PASS |
| Relationship Boundary | PASS |
| Marriage Boundary | PASS |
| World OS Commitment Boundary | PASS |
| Political Support Boundary | PASS |
| Open Attempt | PASS |
| NPC Autonomy | PASS |
| Authority / Jurisdiction | PASS |
| Recognition / Control separation | PASS |
| Health read boundary | PASS |
| Economy / War handoff | PASS |
| Information boundary | PASS |
| Program Authority | PASS |
| Save / Restore | PASS |
| G8 Surface Ownership | PASS |
| Definition / Instance | PASS |
| Creator Authorability | PASS / G9 pending |

---

# 25. Current State

```text
汉末三国：政争与势力 v0.2.1

Legacy v0.1.3 review            COMPLETE
Character Capability migration  COMPLETE
Relationship boundary           COMPLETE
Commitment boundary             COMPLETE
Political Skill contribution    COMPLETE
G8 Surface ownership            COMPLETE
Semantic Candidate              CURRENT
G9 machine binding              PENDING
Cross-asset final audit         PASS / PATCHED
```

---

# 26. Final Freeze

> **Politics 拥有正式政治结构，不拥有人物私人感情。**
>
> **Political Support 是正式政治立场，不是 Relationship Trust / Attachment。**
>
> **Political Agreement 是制度关系；明确 Promise 进入 World OS Commitment。**
>
> **Marriage Bond 归 Relationship Core；Politics 只处理婚姻的政治条件与后果。**
>
> **人物政治能力全部进入 EP-CHAR-CORE；本包只贡献政治领域 Skill Definition。**
>
> **Authority / Jurisdiction 约束正式效果，不删除玩家尝试。**
>
> **本包拥有“势力 / 政务”一级 Extension Surface；后续财赋与治理向其贡献，不重复 owns。**
>
> **Program 最终拥有政治 Outcome 与 Atomic Commit。**


---

# v0.2.1 修订说明｜资产族版本引用闭环

本次不修改 Politics 机制正文，只做跨资产引用收敛：

1. World Pack 改绑 `汉末三国：天下未定 v0.2.3`；
2. Economy 改绑 `财赋与治理 v0.2`；
3. War 改绑 `军略与战争 v0.2`；
4. History 改绑 `历史参照与分歧 v0.2`；
5. Frontmatter 补登记 `身体状态核心 v0.1`，与正文 Health Integration 保持一致；
6. 由此闭合 Economy / War / History 已预指向 `Politics v0.2.1` 的版本关系。
