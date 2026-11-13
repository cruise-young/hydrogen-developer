# Hydrogen Developer

面向 AI 编程助手的开发工作流技能, 覆盖需求澄清, 实施计划, 代码开发和文档表达.

当前套件版本: v2.3. 以一个技能入口分发, 按阶段读取内置模块.

## 包含什么

| 模块 | 用途 |
| --- | --- |
| hydrogen-brainstorming | Story 需求澄清, 方案比较和设计规格 |
| hydrogen-task-plans | 将已确认设计转为可审核的实施计划 |
| hydrogen-coding | Bug / Task / Story 分流, 开发规范与验证 |
| hydrogen-output | 文档, 日常回复, 进度汇报和交付说明 |

Bug 和边界明确的 Task 使用轻量流程. Story 按设计确认, 计划确认和逐任务实施推进. 写作模块随包提供, 无需单独安装.

## 安装

运行以下命令安装:

```sh
npx skills add cruise-young/hydrogen-developer --skill hydrogen-developer -g
```

按提示选择使用的 AI 编程工具. 此命令使用 skills CLI, 需要本机具备其要求的 Node.js 环境.

也可以将本仓库下载并解压到目标工具支持的技能目录, 文件夹命名为 hydrogen-developer, 保留 SKILL.md 与 references 的相对位置.

## 使用示例

- 使用 hydrogen-developer 分析这个需求, 先判断属于 Bug, Task 还是 Story.
- 按 hydrogen-developer 为已确认的设计编写实施计划.
- 按 hydrogen-developer 修复这个缺陷, 并验证受影响的行为.

具体加载方式以目标工具为准. 技能提供工作流程和规范, 不提供项目依赖或外部服务.

## 更新

```sh
npx skills check
npx skills update
```

## 目录

```text
SKILL.md
README.md
references/
  hydrogen-brainstorming/
  hydrogen-task-plans/
  hydrogen-coding/
  hydrogen-output/
```

根目录 SKILL.md 是统一入口. references 中的规则及附属文件按需读取. Java 命名, 分层, 注释和工具库等具体约定见开发模块, 使用时结合项目现状与用户明确要求.

## 版本约定

小版本使用一位数字: v2.3, v2.4, ..., v2.9, v3.0. 各模块的历史变更见对应 SKILL.md 的版本记录.