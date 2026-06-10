# mregg-skill

一个可移植的 AI 协作可靠性协议。

它不是人格皮肤、提示词技巧，也不是针对某个模型的包装器。它是一个可复用的操作协议，用于真正重要的工作：先澄清再行动、从证据出发推理、暴露问题、比较选项、披露降级方案，最终交付可被检验的产出。

项目的公开名称仍可称为 **MrEgg.skill**。机器可读的文件夹名和 skill id 为 **`mregg-skill`**，以兼容要求小写字母、数字和连字符的 skill 系统。

## 它解决什么问题

当 AI 给出错误、模糊、过度自信或隐藏失败的回复，其代价高于一个稍显结构化的流程时，就该用 `mregg-skill`。

它让 AI 助手做到：

- 当模糊性影响结果时先提问；模糊性无害时标注假设并继续推进；
- 当长任务偏离原始目标时重新校准方向；
- 根据反馈修订时不丢弃仍然有效的部分；
- 区分证据、推理、假设和不确定性；
- 给出客观批评，而非讨好用户；
- 比较多个选项并结合权衡给出推荐；
- 重试之前先披露失败；使用降级方案时披露并标注可靠性等级；
- 在宣称完成之前对交付物进行审计。

目标不是让每个回答都变长，而是让重要回答值得信赖。

## 何时触发

**中触发策略** —— skill 只在三种情况下激活：

1. **显式调用** —— `mregg-skill`、`MrEgg.skill`、"use the MrEgg method"、"use the reliability protocol"、按旦旦的方法。
2. **可靠性行为请求** —— "别脑补"、"不要讨好我"、"区分证据和假设"、"比较选项并推荐一个"、"披露降级方案"、"审计后再说完成"等。
3. **高风险工作** —— 发布、上线、提交、交接、批量或不可逆的修改。

它刻意**不**在以下场景触发：打招呼、快速事实问答、常规编码或编辑、普通的多步骤执行。可靠性不是仪式感，常规工作应该保持高效。

弱别名（`MrEgg`、`Dandan`、`旦旦`、`蛋蛋`、`是旦不是蛋`）单独出现永远不触发 —— 只有同时伴随可靠性请求才触发。

## 强度级别

skill 始终使用够用的最低级别：

| 级别 | 名称 | 输出 |
|---:|---|---|
| 0 | 关闭 | 正常回复，无标记 |
| 1 | 轻量 | 结论 → 假设 → 输出 → 快速检查 |
| 2 | 结构化 | 只用有实际内容的章节 |
| 3 | 审计 | 完整结构，含风险、降级披露和最终审计 |

激活时，可见痕迹默认只有一行标记 —— `Reliability mode: light` / `structured` / `audit` —— 而不是沉重的模板。

实用提示词：

```text
Use mregg-skill in light mode. 保持简洁。
Use mregg-skill in structured mode for the analysis, then light mode for execution.
Use full audit mode. 包括假设、证据、风险、不确定性、降级方案和最终审计。
```

更多调用模式（每条都附预期行为）：[references/prompt-patterns.md](references/prompt-patterns.md)。

## 项目结构

```text
mregg-skill/
├── SKILL.md                          # 规范入口 —— 自足，单独可用
├── README.md
├── README_CN.md
├── CHANGELOG.md
├── LICENSE
├── agents/
│   └── openai.yaml                   # OpenAI 系工具的可选元数据
├── evals/
│   └── evals.json                    # 机器可读测试用例
├── protocols/                        # 深度内容，按需加载
│   ├── clarify-before-acting.md      # 问 vs 假设：决策表
│   ├── stay-on-goal.md               # 目标校准 + 基于反馈修订
│   ├── evidence-and-options.md       # 证据纪律、选项比较、概念解释、边界注释
│   ├── failure-and-fallback.md       # 问题透明 + 降级披露
│   └── deliver-and-audit.md          # 完成前检查清单
├── references/
│   ├── compatibility.md              # 各工具安装与使用说明
│   ├── output-checklist.md           # 复杂输出的检查清单
│   ├── privacy-boundaries.md         # 公开/隐私边界
│   └── prompt-patterns.md            # 调用提示词 + 预期行为
└── tests/
    └── pressure-scenarios.md         # 人类可读回归场景
```

## 设计原则

- **SKILL.md 自足。** 只读 SKILL.md 的工具（或较弱的模型）就能获得正确的基本行为：触发表、强度级别、核心规则和全部响应模板。协议文件提供深度，而非必需上下文。
- **决策表优于散文。** 触发判定和澄清判定都是"命中第一行即生效"的表格，能力较弱的模型也能确定性地执行。
- **可靠的过程，轻量的输出。** 触发不等于沉重模板，级别与风险匹配。
- **元技能，不是替代品。** 领域 skill（编码、写作、专利、文档解析）做实际工作，`mregg-skill` 提供可靠性层：

```text
先用 PDF 提取 skill 读取文件，再用 mregg-skill 审计提取结果和不确定性。
```

## 安装

整个包是纯 Markdown/JSON —— 无脚本、无网络访问、无依赖。

- **Claude Code**：把文件夹复制到 `~/.claude/skills/mregg-skill/`。每次更新后需重新复制；已安装的副本不会自动同步。
- **Claude.ai / 桌面版**：把文件夹本身打成 zip（解压后必须是 `mregg-skill/` 目录），通过 Skills 上传。
- **OpenAI 系工具**：理解 `agents/openai.yaml` 的工具读取该元数据；其余工具直接使用 SKILL.md。
- **其他任意工具**：支持 Agent Skills 就指向该文件夹；不支持就把 SKILL.md 粘贴为系统指令/自定义指令 —— 它可以独立工作。

各工具详情：[references/compatibility.md](references/compatibility.md)。

## 测试与维护

- [tests/pressure-scenarios.md](tests/pressure-scenarios.md) —— 23 个人类可读回归场景，含反例（常规工作不得触发；显式要求简洁时简洁永远优先）。
- [evals/evals.json](evals/evals.json) —— 13 个机器可读用例。

当 skill 表现异常时，先添加测试用例，再修改协议。两个失效方向都要盯：在常规工作上过度触发，以及在高风险或显式请求的可靠性工作上触发不足。

## 重要边界

- 它不会让 AI 自动变正确；它让假设、证据、失败和建议足够可见，以便人类判断。
- 它不能替代领域专业知识、来源验证、测试或代码执行。
- 在低风险任务上，它永远不得覆盖用户对简洁的明确要求。
- 它永远不得暴露隐私身份、账户数据、密钥、本地路径或机密项目事实。

## 许可证

Apache License 2.0 —— 见 [LICENSE](LICENSE)。

## 核心理念

> 过程的可靠性成就结果的可靠性。

`mregg-skill` 不承诺 AI 永远正确。它迫使协作过程变得足够可见，以便人类能够做出判断。
