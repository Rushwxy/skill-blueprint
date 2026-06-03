# Skill Blueprint — 自然语言 → 工程 Skill 的自动翻译器

> **先搜再建，不重复造轮子。工具学人，而非人学工具。**

一个元 Skill：你只需要用大白话说"我想做一个什么样的 Skill"，它自动帮你搜索是否已有现成方案、推导执行骨架、生成标准格式的 SKILL.md。零门槛，工程结构全由 AI 翻译。

---

## 设计哲学

### 核心原则：先搜再建（Search-Before-Build）

Agent Skill 生态正在爆发，但大部分 Skill 都是"重复造轮子"。我们的答案是：

```
用户需求 → 典型度判断 → 搜索匹配 → 复用/改编/新建
                ↑                        ↑
          常见需求才搜             能改就不重新造
```

这不是多一步，是把"新建"从默认选项降格成了备选。

### 三层决策模型

| 层 | 名称 | 做的事 | 耗时 |
|:--:|------|------|:--:|
| 0 | **典型度判断** | 这个需求常见吗？值得搜吗？ | 1秒 |
| 1 | **级联搜索** | 本地 Skill → GitHub 开源 → Web | 1轮 |
| 2 | **骨架生成** | 自然语言 → 标准化 SKILL.md | 1轮+1确认 |

### 顺人性设计（AI Naive 底层原则）

- **零门槛**：用户用自然语言描述需求，AI 自动翻译为工程结构
- **一次确认**：不做马拉松式交互，推一次骨架 + 一次确认
- **反例约束**：每个 step 都有"⚠️ 别犯"标注，防止 agent 自嗨

---

## 快速开始

### 安装

将 `skill-blueprint/SKILL.md` 放入你的 WorkBuddy skills 目录：

```bash
# WorkBuddy 用户级 skills 目录
~/.workbuddy/skills/skill-blueprint/SKILL.md
```

### 使用

直接用大白话说你的需求：

> "创建一个 skill，每天监控 GitHub 热榜上跟 AI agent 相关的新项目，筛出最值得关注的 TOP 10"

skill-blueprint 会自动：
1. 判断这是常见需求 → 触发搜索
2. 搜索本地/社区/开源 → 确认无现成方案
3. 推导执行骨架（step 0→1→2→...→final）
4. 展示骨架让你确认
5. 生成标准格式的 SKILL.md

---

## 成果示范：github-trend-monitor

[examples/github-trend-monitor/](examples/github-trend-monitor/) 是用 skill-blueprint 从"我想监控 GitHub 热榜"这句话生成的真实成品。

**工作流全程**：
1. 用户一句话描述 → skill-blueprint 推导 4 步骨架
2. 用户要求加"全局热榜"（打破信息茧房）→ 3 轨扩为 4 轨
3. 确认 → 写入 SKILL.md → 立即加载执行
4. 首次运行产出：6 个 agent/self-evolution 相关 TOP 项目 + 6 条全局趋势信号

---

## SKILL.md 标准骨架

skill-blueprint 产出的每个 Skill 遵循统一格式：

```markdown
---
name: skill-name
description: 一句话描述 + 触发条件
agent_created: true
---

# Skill Name — 一句话概述

## 触发条件
- 触发词
- 触发场景

## 执行流程
### Step 1: 步骤名
- 目标 / 输入 / 执行 / 输出 / 验收 / ⚠️ 别犯

### Step 2: ...
...

### Step final: 收尾

## 全局约束
## 局限说明
```

---

## 为什么做这个

Agent Skill 生态有三个痛点：

1. **创建门槛高**：不是所有人都会写规范化的 Skill 文件
2. **重复造轮子**：没有人/agent 在创建前先搜索是否已有方案
3. **格式不统一**：不同人/agent 产出的 Skill 结构各异，互不可读

skill-blueprint 解决这三件事：
- 零门槛输入（自然语言）
- 先搜再建（预检层）
- 统一骨架（标准化输出）

它是 Skill 生态的基础设施——不替代任何 Skill，而是帮所有 Skill 更快、更规范地出生。

---

## 兼容性

当前为 WorkBuddy 平台原生 Skill。将核心思想移植到其他 agent 平台（Claude Code / Cursor / Copilot）的思路请见下文「移植指南」。

### 移植到其他平台

skill-blueprint 的核心价值在**设计思想**而非具体实现。移植时保留：

1. **预检层**（典型度判断 + 级联搜索）——平台无关
2. **骨架规范**（step 的目标/输入/执行/输出/验收/反例）——平台无关
3. **一次确认**的交互模式——平台无关

需要替换的只是具体工具调用（如 WorkBuddy 的 Skill 工具 → Claude Code 的 skills 机制）。

---

## 许可

MIT

---

## 作者

由 Rush 与 WorkBuddy 协作设计和迭代。
