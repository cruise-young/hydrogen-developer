---
name: hydrogen-developer
description: 按 Hydrogen 规范处理代码变更，区分 Bug、Task、Story；Story 依次完成需求设计、实施计划和逐任务开发。用于用户要求采用 Hydrogen 流程或规范进行开发时。
---

# Hydrogen Developer

> 版本: v2.2 (2026-11-13).

本套件将 hydrogen-brainstorming、hydrogen-writing-plans、hydrogen-coding 合并分发，保留各模块原始规则和附属文件。所有相对路径均相对于本文件所在目录。

## 入口与按需加载

1. 先读取 [开发规范与分类规则](references/hydrogen-coding/SKILL.md)，按其中定义区分 Bug、Task、Story；用户已确认的分类、阶段和授权继续有效。
2. Bug、Task 按开发规范中对应的轻量流程执行，不套用 Story 流程。
3. Story 需求设计阶段读取 [需求设计](references/hydrogen-brainstorming/SKILL.md)。
4. Story 书面设计确认后读取 [实施计划](references/hydrogen-writing-plans/SKILL.md)。
5. Story 书面计划确认后回到开发规范，按其逐任务执行规则开发。

文档写作按需读取 [清晰写作规则](references/hydrogen-writing/SKILL.md), 日常协作采用模块内的四条规则.

## 套件内部名称解析

模块中要求加载或调用以下技能时，直接读取对应的本地文件并遵循其规则；无需另外安装同名技能，也不要因系统技能列表中没有这些独立名称而中断：

| 模块名称 | 本地规则文件 |
| --- | --- |
| hydrogen-brainstorming | [references/hydrogen-brainstorming/SKILL.md](references/hydrogen-brainstorming/SKILL.md) |
| hydrogen-writing-plans | [references/hydrogen-writing-plans/SKILL.md](references/hydrogen-writing-plans/SKILL.md) |
| hydrogen-coding | [references/hydrogen-coding/SKILL.md](references/hydrogen-coding/SKILL.md) |
| hydrogen-writing | [references/hydrogen-writing/SKILL.md](references/hydrogen-writing/SKILL.md) |

附属资源路径以引用它的模块文件所在目录为基准解析。其他未随包提供的工具或技能按实际环境可用性处理，不虚构可用能力。保留模块中的阶段确认、范围控制和用户优先规则；本入口不授予提交、发布、部署或额外修改权限。