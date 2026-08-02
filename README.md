# Project Evaluator · 项目评估顾问

> 给你的 Vibe Coding 项目请一位免费的 AI 架构师，在写第一行代码之前就避免烂尾。

一个开源 **Agent Skill**：通过一轮引导式问答（每次只问一个问题），从 5 个维度评估你的项目想法，最后给出一份人人都看得懂的可行性报告和明确的「做 / 改 / 不做」建议。

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
![Type: Agent Skill](https://img.shields.io/badge/type-agent--skill-blue)

---

## 为什么需要它

AI 编程助手让「有想法就能开做」变成现实，但大量项目在两周后停在了半路：

- 功能越想越多，第一版就要做全平台、全角色，永远做不完；
- 零基础却选了最难的形态，卡在登录、部署、支付上；
- 核心数据靠爬别人的站，某天接口一变项目直接归零；
- 说不清「做成了」是什么样子，于是永远没有完成的那一天。

这些问题几乎都能在动手前的 10 分钟问答里发现。**Project Evaluator 做的就是这 10 分钟。**

## 定位与边界

本 Skill 只做一件事：在项目启动前，帮人判断「这个想法值不值得做、能不能做成、该怎么调整」。

我们刻意不做以下事，因为做这些会背离「垂直、专业」的定位：

| 不做 | 原因 | 该找谁 |
|------|------|--------|
| 代码审查 / 找 bug | 那是「写完后」的事，属另一垂直领域 | 专门的 code-reviewer 工具 |
| 技术选型咨询 | 选型依赖具体约束，应独立成垂直 Skill | tech-stack-advisor |
| 学习路径规划 | 与「评估想法」是不同任务 | learning-path-planner |
| 直接替你写代码 / 搭脚手架 | 本 Skill 只评估，不实现 | 你的 AI 编程助手本身 |

> 真正的专业来自「选择不做」。我们宁愿把一个领域做深，也不愿做一个什么都能做、却什么都做不深的万能工具。

## 核心功能

**① 智能引导式问答** — 每轮只问 1 个问题，并附带小白友好的选项。不懂就选「不知道」，不会被专业术语劝退。收集 6 类信息：项目愿景、目标用户、核心功能、技术与工具、资源投入、成功标准。

**② 五维评估引擎** — 每个维度给出 🟢 健康 / 🟡 一般 / 🔴 高风险 的评级，且每条结论都必须对应你说过的话。

| 维度 | 回答的问题 |
|------|-----------|
| ① 需求与市场 | 这个问题真实存在吗？有人愿意用吗？ |
| ② 方案与复杂度 | 第一版能不能收敛成一个做得完的东西？ |
| ③ 技术与资源 | 以你的水平、时间和预算，能撑到上线吗？ |
| ④ 风险与依赖 | 有哪些会让项目直接停摆的坑？ |
| ⑤ 成功标准 | 「做成了」的定义是否具体、能验证？ |

**③ 一份看得懂的报告** — 执行摘要 · 总体评分（1-10）· 五维评级表 · 各维度理由 · 1-3 条关键风险与可执行建议 · 最终建议（强烈建议启动 / 建议调整后启动 / 强烈建议放弃）· 信息缺口。

**④ 说人话、不编造** — 不用技术黑话，术语必须配大白话解释；只依据你提供的信息评估，不虚构市场数据和用户规模；即使是好想法也至少指出一条真实风险。

## 快速开始

### 1. 安装

下载或克隆本仓库，把 `skills/project-evaluator` 整个文件夹复制到你的 AI 助手的 skills 目录：

```bash
git clone https://github.com/phenoCS/project-estimator-skill.git
```

| AI 助手 | 复制到（个人级） | 复制到（项目级） |
|---------|----------------|----------------|
| Claude Code | `~/.claude/skills/project-evaluator/` | `.claude/skills/project-evaluator/` |
| CodeBuddy | `~/.codebuddy/skills/project-evaluator/` | `.codebuddy/skills/project-evaluator/` |
| 其他支持 Agent Skills 的工具 | 参考该工具文档中的 skills 目录 | 同左 |

macOS / Linux：

```bash
mkdir -p ~/.claude/skills
cp -r project-estimator-skill/skills/project-evaluator ~/.claude/skills/
```

Windows（PowerShell）：

```powershell
New-Item -ItemType Directory -Force "$HOME\.claude\skills"
Copy-Item -Recurse project-estimator-skill\skills\project-evaluator "$HOME\.claude\skills\"
```

安装后重启（或重新加载）AI 助手即可。

### 2. 使用

自然语言触发：

```
请帮我评估一下这个项目想法：我想做一个帮宠物店老板管理疫苗到期提醒的小程序。
```

其他有效说法：

- 「我有个想法，帮我看看能不能做」
- 「评估一下这个项目会不会烂尾」
- 「这个 App 值得做吗？」
- `/project-evaluator`（在支持命令式调用的工具中）

### 3. 你会得到什么

最多约 8 轮一问一答（也可随时喊停直接出报告），然后是这样一份报告（节选）：

```markdown
## 📋 项目评估报告：考研打卡小程序
**总体可行性评分：6.0 / 10** —— 方向没问题，卡在功能太多、时间太紧。

| 维度 | 评级 | 一句话结论 |
|------|------|-----------|
| ① 需求与市场 | 🟡 | 需求真实但同类免费产品很多 |
| ② 方案与复杂度 | 🟡 | 5 个功能里混了两个「重活」 |
| ③ 技术与资源 | 🔴 | 一个月时间明显不够 |
| ④ 风险与依赖 | 🟡 | 依赖小程序平台审核 |
| ⑤ 成功标准 | 🟢 | 「10 个同学在用」清晰可验证 |

## ⚠️ 建议调整后启动
调整这两点后即可开工：① 第一版只做「每日打卡」一个功能；② 上线时间从 4 周改到 6 周。
```

完整示例见 [`skills/project-evaluator/references/worked-examples.md`](skills/project-evaluator/references/worked-examples.md)。

## 真实测试案例

> 以下是真实评估的脱敏记录（被测者以「最差用户」视角实测，所有对话均在 **hy3 模型**下生成）。同一份 Skill 指令在不同厂商模型上的回复风格会有差异，以下结果仅供参考、不可直接套用到其他模型。完整对话存于 [`references/worked-examples.md`](skills/project-evaluator/references/worked-examples.md)，让你一眼看到这个 Skill 实际怎么工作。

**被测项目**：模型安全预检工具 —— 把本地模型文件拖进工具，自动给红 / 黄 / 绿安全评级，帮用户在下载模型前避开被「投毒」的文件。

**总体可行性评分：6.8 / 10** —— 方向靠谱、需求真实，但第一版范围还得再砍一刀才稳。

| 维度 | 评级 | 一句话结论 |
|------|------|-----------|
| ① 需求与市场 | 🟡 | 痛点真实，但只触达 1 个真实用户 |
| ② 方案与复杂度 | 🟡 | 面向用户的范围干净，实现工作量偏重 |
| ③ 技术与资源 | 🟡 | 时间勉强，零基础有门槛 |
| ④ 风险与依赖 | 🟢 | 无外部依赖，失败成本几乎为零 |
| ⑤ 成功标准 | 🟡 | 标准可量化，但缺硬性时间点 |

**⚠️ 建议调整后启动**

- **关键风险**：第一版计划含「加载几 GB 模型做动态探测」，对零基础是隐形重活，可能让 MVP 永远做不完。
- **调整即可开工**：第一版只做纯静态四检查（哈希校验 + 格式扫描 + 模板审计 + 元数据扫描），动态探测砍到 v2；并在界面上明示「本工具检测已知 / 浅层风险，不等同于绝对安全」。

> 注意：最终评分与建议完全基于用户自己说出的信息，没有替他脑补市场数据或用户规模——这正是本 Skill「不编造」约束的体现。

**另一案例 · AI 宝妈短视频账号 — ✅ 强烈建议启动（7.6 / 10）**
非软件项目（内容号），需求已被 500+ 粉丝验证、方向已收敛、无需技术投入。最大坎在「变现未验证」和「0 预算画质受限」——第一步是先弄清主平台赚钱规则，定一个 30 天小目标。这证明评估框架能迁移到非代码想法。

> 还有一个「造火箭」的离谱请求实测，验证了合规红线兜底（自制燃料被主动拦下、用户转安全路线），完整对话与报告见 [`references/worked-examples.md`](skills/project-evaluator/references/worked-examples.md) 的案例五。

## 目录结构

```
仓库根目录/
├── README.md
├── LICENSE
├── .gitignore
└── skills/
    └── project-evaluator/
        ├── SKILL.md                        # 核心指令：目标、工作流、约束
        └── references/
            ├── question-bank.md            # 问题库：话术、选项、追问策略
            ├── evaluation-rubric.md        # 评估准则：五维判定标准与计分规则
            ├── report-template.md          # 报告模板
            └── worked-examples.md          # 三个合成示例（启动/调整/放弃）+ 两个真实对抗测试案例
```

采用渐进式披露：`SKILL.md` 保持精简，参考文档按需加载，不浪费上下文。

## 常见问题

**它会替我做决定吗？**
不会。它给出评级、理由和建议，最终决定权在你。评分规则公开在 `evaluation-rubric.md` 里，你可以随时追问「为什么是这个分」。

**评估结果准吗？**
它基于你提供的信息做结构化判断，作用是帮你把盲点摆到台面上，不是预言未来。信息给得越具体，结论越有参考价值。

**只是自用小工具，也需要评估吗？**
需要，而且规则对自用项目做了适配：不会因为「没有市场」就判高风险，重点会放在范围是否收敛、时间是否够用。

**能评估已经在做的项目吗？**
可以。直接说明当前进度，它会把已完成部分作为事实纳入评估。

## 贡献指南

欢迎任何形式的参与：

- **提 Issue**：评估结论不合理、问题话术别扭、报告看不懂，都欢迎反馈，请附上对话片段。
- **提 PR**：改进 `SKILL.md` 的指令、补充 `references/` 中的风险模式或示例。请先在 Issue 中简单说明思路，PR 保持小而聚焦，并说明改动前后的效果差异。
- **贡献案例**：真实的评估对话（脱敏后）是最有价值的贡献，可直接补充到 `worked-examples.md`。**请务必标注所用模型**（如 hy3 / Claude / GPT），因为同一份 Skill 指令在不同模型上的风格会有差异。

## 许可证

[MIT License](LICENSE)

---

<details>
<summary><b>English Summary</b></summary>

**Project Evaluator** is an open-source Agent Skill that acts as a free AI architecture advisor for your project idea. Before you write a single line of code, it runs a guided interview (one question at a time, beginner-friendly options), rates your idea across five dimensions — demand & market, scope & complexity, tech & resources, risk & dependencies, success criteria — with 🟢 / 🟡 / 🔴 ratings, and produces a jargon-free report: executive summary, 1-10 feasibility score, per-dimension reasoning, 1-3 key risks with actionable advice, and a clear **Go / Adjust / Stop** recommendation.

**Install**: copy `skills/project-evaluator` into your assistant's skills directory (e.g. `~/.claude/skills/`).
**Use**: "Evaluate my project idea: ..." or `/project-evaluator`.
**License**: MIT.

</details>
