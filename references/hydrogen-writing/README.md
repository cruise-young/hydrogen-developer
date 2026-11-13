# Hydrogen Writing｜清晰文档写作

一个面向 Codex 的中文写作 Skill：**结构优化、重点前置、表达清晰、通俗化解释、去 AI 味**。

## 设计来源

综合下列 Skill 的方法，而不是直接打包它们的代码；使用本 Skill 不需要预先安装四个原版 Skill。

| 方法来源 | 融合能力 |
| --- | --- |
| [doc-coauthoring](https://github.com/anthropics/skills/tree/main/skills/doc-coauthoring) | 读者目标、结构迭代、读者测试 |
| [general-writing](https://github.com/msimchowitz/writing-skills/tree/main/for-agents/general-writing) | 精简、清晰、保持作者语气 |
| [humanizer](https://github.com/blader/humanizer) | 去除机械化 AI 写法 |
| [anti-defensive-writing](https://github.com/Kiterlin/anti-defensive-writing) | 观点前置、必要而克制的限定 |

本 Skill 的 `SKILL.md` 是独立编写的工作流，未复制原项目的完整说明文件。原项目版权与许可证以各自仓库为准。

## 安装到 Codex（Windows）

1. 解压 ZIP，得到 `hydrogen-writing` 文件夹。
2. 在 PowerShell 执行：

```powershell
$dest = Join-Path $HOME '.agents\skills'
New-Item -ItemType Directory -Force -Path $dest | Out-Null
Copy-Item -Path '.\hydrogen-writing' -Destination $dest -Recurse -Force
```

以上命令需要在解压后、能看到 `hydrogen-writing` 文件夹的目录中执行。如果文件夹已经存在，`-Force` 不一定能清除旧文件，更新时建议先备份旧版。

最终路径应为：

```text
C:\Users\你的用户名\.agents\skills\hydrogen-writing\SKILL.md
```

也可以只对某一个项目启用：把文件夹放在项目根目录的 `.agents/skills/hydrogen-writing/` 下。

> 来源：[Codex Skills 官方说明](https://learn.chatgpt.com/docs/build-skills?translationFallback=zh-Hans)。若新 Skill 未显示，重新开启 Codex 会话或重启 App。

## 使用示例

在 Codex 会话中输入：

```text
使用 $hydrogen-writing 优化 docs/方案.md。
目标读者是不了解技术的业务同事。
要求：先给结论、优化章节、把术语解释清楚、删除空话和 AI 味；
保留所有事实、参数、风险与技术限制。
请直接修改文件，并说明主要变化。
```

```text
使用 $hydrogen-writing 检查 docs/README.md，
先只诊断问题，不直接修改。重点关注结构、表达和读者理解障碍。
```

```text
使用 $hydrogen-writing，根据以下材料起草一份项目建议书，
读者是管理层，先给推荐方案、理由、成本与风险。
没有数据支持的内容标为待确认，不要编造。
```

## 设计边界

- 自动润色不等于事实核验，仍需要人为确认数字、风险及关键决定。
- 不应该为了口语化而删除技术准确性、法律必要限定或来源引用。
- 本 Skill 没有自动调用外部独立读者测试，默认使用内部静态读者视角检查。
