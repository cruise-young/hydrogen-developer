# Hydrogen Developer

Hydrogen Developer 是一套面向 AI 编程助手的开发技能. 你描述期望的业务行为, 助手先检查代码并判断改动类型. 遇到需要设计的需求, 你可以在写代码前核对输入输出和改造位置, 交付时用同一个例子验收.

当前套件版本为 v2.8. 日常使用统一入口 `hydrogen-developer`, 各模块按阶段加载.

## 快速开始

使用 `skills` CLI 需要 Node.js 22.20 或更高版本和 `npx`. 从 GitHub 安装时运行下面的命令. `-g` 表示安装到当前用户, 可跨项目使用. [CLI 安装说明](https://github.com/vercel-labs/skills#install-a-skill)

```sh
npx skills add cruise-young/hydrogen-developer --skill hydrogen-developer -g
```

要试用当前工作区中的改动, 可以直接从本地目录安装. [本地安装与更新](#本地安装与更新)

安装后在 Codex 中打开要修改的项目, 可以从一条具体需求开始.

> `$hydrogen-developer` 订单列表筛选为待发货后, 我希望导出所有符合条件的订单, 包括下一页的订单.

## Bug / Task / Story 怎么选

助手会先说明分类和理由, 你也可以调整分类. 只要方案和验收已经明确, 跨多个文件的局部改动也可以按 Task 处理.

| 类型 | 适用场景 | 处理方式 |
| --- | --- | --- |
| Bug | 已有约定的行为失效, 例如原本能导出全部匹配订单, 现在只导出当前页. | 定位原因, 修复并回归验证. |
| Task | 目标, 方案和影响范围已明确, 例如按已有接口约定增加一个筛选字段. | 直接实施局部改动, 验证受影响的行为. |
| Story | 新增或实质改变端到端业务能力, 需要系统设计, 或跨服务契约仍待确定. | 先确认书面设计和实施计划, 再逐任务开发和验收. |

## 怎么评审一个 Story

1. **先看书面设计 (spec).** 正文依次写需求背景与目标, 输入与预期输出, 设计规格, 验收标准. 先读前两节就应能判断结果. 以上面的导出为例, 假设每页一条, A 和 B 待发货, C 已发货. 筛选后导出的文件应只有 A 和 B, 各出现一次. 界面或状态变化可配截图或流程图, 通过条件仍写在正文.
2. **再看实施计划.** 你确认 spec 后, 助手按可独立验收的结果拆任务. 每个改造点占一行, 写清文件和方法, 当前行为, 具体改法与复用点, 怎么验及实际结果. 已有代码附文件链接和方法名, 新位置标为拟新增. 比如导出入口可以复用列表的筛选条件, 取数范围要覆盖全部匹配订单.
3. **按原计划验收.** 你确认计划后, 助手在每个任务开工前引用对应的行, 经你确认后实施. 完成后把正向和相关边界用例的实测结果回填原行, 验证受限的部分注明原因. 最终由你审阅代码差异和回归结果并提交.

spec 和计划默认放在工作区根目录的 `设计文档/<需求名称>/`. 同一需求延续时更新原文档. 系统总览, 服务边界等架构资料放在 `架构文档/`.

## 编码时怎样取舍

Ponytail 的最小完整改动原则已内置在 `hydrogen-coding` 中, 编码和审查时都会用到.

- **先看改动落在哪一层.** 比如网关收到一次任务上报, 其中既有结果也有状态. 先查两项写入有没有先后依赖, 再看已有 Kafka 链路能否分别承接. 当两项处理可以独立完成且已有投递机制满足可靠性要求时, 可以在网关分发, 让 task 服务复用已有处理方法.
- **先找合适的现成工具.** JSON, 字符串, ID, 时间等操作先查当前模块的用法和依赖. Java 项目优先沿用适用的 Hutool, Guava 或 Spring 工具. 工具有影响当前用例的缺陷, 依赖成本过高或不符合业务契约时, 可改用其他现有实现或自行封装小方法.
- **让主方法保留业务主干.** 在入口能读出步骤, 关键分支和写入顺序. 有独立职责的细节可以放进只调用一次的子方法. 新增兜底或重试要有真实的失败场景. Java 变量使用显式类型声明, 包括测试和示例, 禁用 `var` 和 `final var`.

## 本地安装与更新

要使用当前工作区的内容, 在本仓库根目录执行以下命令.

```sh
npx skills add . --skill hydrogen-developer -g
```

手动安装时, 将仓库放进编程助手支持的技能目录, 目录名使用 `hydrogen-developer`, 保留根目录 `SKILL.md` 与 `references/` 的相对位置.

从 GitHub 全局安装后, 可用 `npx skills list -g` 查看已安装的技能. 更新这个套件时运行 `npx skills update hydrogen-developer -g`. [CLI 命令参考](https://github.com/vercel-labs/skills/blob/main/docs/commands.md)

## 规则入口

根目录定义了按需加载的顺序. [套件入口](SKILL.md)

| 要查的内容 | 模块 |
| --- | --- |
| 需求澄清, 方案比较和 spec 的四节模板 | [hydrogen-brainstorming](references/hydrogen-brainstorming/SKILL.md#story-spec-正文) |
| 按任务组织的改造点表和验收方式 | [hydrogen-task-plans](references/hydrogen-task-plans/SKILL.md#默认文档结构) |
| 任务分流, 代码复用, Java 约定与交付检查 | [hydrogen-coding](references/hydrogen-coding/SKILL.md) |
| 中文文档, 日常沟通, 进度和交付说明 | [hydrogen-output](references/hydrogen-output/SKILL.md) |

套件的小版本使用一位数字, 例如 v2.9 之后是 v3.0. 各模块的变更记录见对应规则文件. [MIT 许可证](LICENSE)