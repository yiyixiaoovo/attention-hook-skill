# attention-hook-skill

给文章与短视频的**开头、标题、封面**做诊断与改写的技能包。给 AI Agent 用：装进 Claude Code / Codex / DeepSeek Harness 等支持 `SKILL.md` 的环境，用户问「开头怎么改」「钩子为什么平」「这条标题算不算标题党」时自动路由到对应能力卡。

**18 张能力卡**：9 张证据卡（论文/元分析）+ 9 张实践者卡。每张卡都带证据边界段，实践者卡明确写「0 控制实验、不承诺效果」。

## 安装

**方式一：复制 skill（最简单）**

```bash
git clone https://github.com/yiyixiaoovo/attention-hook-skill.git
cp -r attention-hook-skill/skills/attention-hook ~/.claude/skills/attention-hook
# DeepSeek Harness: 复制到 ~/.dsh/skills/attention-hook
```

**方式二：Claude Code 插件**

```
/plugin marketplace add yiyixiaoovo/attention-hook-skill
/plugin install attention-hook@attention-hook
```

**方式三：只拿单卡**——`skills/attention-hook/references/capabilities/<slug>.md` 每个文件都是一张独立可读的卡，直接读也可以。

## 里面有什么

```
skills/attention-hook/
├── SKILL.md              # 入口：路由表 + 核心原则 + 边界
└── references/
    ├── capabilities/     # 18 张卡（R/I/A1/A2/E/B 六段）
    ├── capability-graph.md   # 能力关系图（可叠加/要点相反/依赖）
    ├── capability-index.md   # 意图与关键词索引
    ├── cheatsheet.md     # 一句话规则速查
    ├── overview.md       # 整书概览
    └── glossary.md       # 术语
evals/
├── test-prompts/         # 18 个路由评测文件（162 条用例，minimum_pass_rate 0.8）
└── behaviors/            # 8 个行为评测（24 用例 / 72 个必须出现的判断项）
knowledge-base/           # 复盘记录：预注册假设 + 四级结论 + 局限
source/                   # 可公开的摘录与来源说明（PROVENANCE.md）
INDEX.md                  # 能力总表
verified.md               # 证据结论与差分记录
coverage-audit.md         # 关键任务覆盖审计（证据/实践者/未覆盖）
```

## 18 张卡

| 卡 | 一句话 |
|---|---|
| `gap-design` | 先给一点信息，再留一个能兑现的问题 |
| `arousal-choice` | 看唤醒度，不看正负情绪 |
| `concretize` | 抽象名词换成能看见、能数、能想象的细节 |
| `surprise-contrast` | 找相关但没预料到的角度，不是猎奇 |
| `distribution-first` | 先确认在哪曝光，再决定优化打开还是转发 |
| `stickiness-pass` | 发布前用六项清单过一遍 |
| `promise-integrity` | 钩子必须能指回正文兑现它的那段 |
| `video-metrics` | 先量 5 秒留存，再谈改法 |
| `story` | 故事更好懂好记，不等于更会说服 |
| `hook-craft` | 三拍/六槽/四错/四通道（实践者） |
| `x-playbook` | X 上怎么发、火了怎么接流量（实践者） |
| `packaging` | 标题-封面-开场三件套（实践者） |
| `script-flow` | 五步脚本 + mini hook + 结尾高音符（实践者） |
| `story-craft` | 问题-张力-分层释放（实践者） |
| `audience-psychology` | 立场/符号/痴迷层级 + 强制伦理自查（实践者） |
| `content-business` | 受众画像/50 条排期/可信线（实践者） |
| `platform-native` | 小红书 3:4、IG 125 字符折叠、抖音 3 秒、X 280（参数会漂移） |
| `hook-forensics` | 样本表→拆解表→提炼槽位→改写对照 |

## 证据政策

- 每张卡的 **B 段**写明它**不能**支持什么；强证据（元分析/同行评审）与实践者经验**不混写**。
- 实践者卡（`hook-craft`、`x-playbook`、`packaging`、`script-flow`、`story-craft`、`audience-psychology`、`content-business`、`platform-native`、`hook-forensics`）**没有控制实验**，只提供操作流程，不承诺提升。
- 效果必须自己测：见 `knowledge-base/`（结论与局限）与 `stickiness-pass` 的 A/B 表。

## 来源与许可

- 代码与卡片文本：MIT（见 `LICENSE`）。
- 来源清单与许可见 `source/PROVENANCE.md`；只收录短摘录，不收录受版权保护的全文。
- 实践者材料来自公开视频字幕与开源技能仓库的整理：Kallaway 频道字幕（短摘录）、Instagram 技能包（MIT，逐字引用一处）、小红书图文参数（AGPL 仓库仅提取数字事实，未复制表达）。

## 关于

本仓库是 [cangjie-skill](https://github.com/kangarooking/cangjie-skill) 能力 Bundle 的编译产物之一；同一 Bundle 可编译为 single（本仓库）或 pack（路由 + 独立技能）。
