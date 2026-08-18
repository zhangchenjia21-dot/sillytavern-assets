# sillytavern-assets

个人使用的 SillyTavern 资产创作与维护仓库。

## AI 入口

任何 GPT、Codex、Grok 或其它 Agent 开始资产任务前，先读 [`AGENTS.md`](./AGENTS.md)，再读目标工作区最近的局部 `AGENTS.md`。

正式资产正文只保留一份；完整正文留在仓库中，不重复复制进长 Agent Prompt。

## 仓库结构

本仓库同时提供三种互补视图，但正式资产正文只保留一份。

```text
世界包/        # Canonical World Pack Store
人物卡/        # Canonical Character Card Store
拓展包/        # Canonical Expansion Pack Store
资产族/        # Asset Family Workspace：按完整作品聚合创作、审核与版本管理
通用资产库/    # Generic Asset Library Workspace：跨世界通用机制的治理与维护
```

### 1. 按资产类型

`世界包 / 人物卡 / 拓展包` 是正式资产正文的唯一事实源，适合未来 Creator 的单资产浏览、编辑和验证。

### 2. 按资产族

`资产族/` 按完整作品聚合 World Pack、Character Cards、专用 Expansion、所消费的通用 Expansion，以及蓝图、版本矩阵、创作规范和审核资料。

资产族目录只保存索引和管理资料，**不得复制第二份正式资产正文**。

### 3. 通用资产库

`通用资产库/` 管理跨多个 World Pack 复用的 Expansion，包括总蓝图、版本矩阵、Owner / Dependency 关系、维护规范和后续路线。

真正的通用 Expansion 正文仍位于：

`拓展包/通用拓展包/`

## 四个概念

```text
世界包 / 人物卡 / 拓展包
= 资产是什么

资产族
= 哪些资产共同组成一部作品

通用资产库
= 哪些机制可以被多个作品复用

Bundle
= 某个资产族在某一版本锁下的交付物
```

当前仍处于 Semantic Asset 阶段。正式机器 Manifest、Bundle Schema、Validator 与 Creator Binding 等待项目 current source 对 G9 `tavern-asset-spec vNext` 正式授权后再建立。
