# 注意力与钩子：跨来源方法论汇编（Kidd & Hayden 2015；Berger & Milkman 2012；Made to Stick / Contagious 二手摘要） — Skill Index

> 本文件由 `scripts/build_index.py` 从 `verified.yaml` 自动生成，**不要手工编辑**。

## 关于这套技能

- **入口**：`attention-hook`（18 个能力，其中高重要度 11 个）
- **能力图**：编译产物内的 `capability-graph.md`（单技能形态在 references 目录下）
- **来源与边界**：`verified.md`、`BOOK_OVERVIEW.md`、`coverage-audit.md`
- **评测**：`evals/test-prompts/<slug>.json`（每技能 9 条用例）

## 能力列表

| 能力 | 标题 | 重要度 | 一句话 | 相邻能力 |
|---|---|---|---|---|
| `gap-design` | 信息缺口设计：先给一点，再留一个能兑现的问题 | high | 开头给足背景的一小段，然后留一个具体、可兑现、答案不在下一句的问题。 | hook-craft（可叠加）；surprise-contrast（可叠加）；promise-integrity（依赖） |
| `arousal-choice` | 情绪选型：看唤醒度，不看正负 | high | 先问这条内容要激起哪种高唤醒情绪，再检查它与内容是否匹配。 | story（可叠加）；audience-psychology（要点相反） |
| `concretize` | 具体化改写：抽象名词换成可感知的细节 | high | 逐句找出抽象名词，换成能看见、能数、能想象的具体细节。 | story-craft（可叠加）；script-flow（可叠加） |
| `surprise-contrast` | 预期违背：相关但没预料到 | medium | 找一个与主题相关、但读者没预料到的角度，而不是单纯的惊吓或猎奇。 | hook-craft（可叠加）；story-craft（要点相反） |
| `distribution-first` | 先看曝光位置，再改文案 | high | 先确认这条内容会在哪曝光、由谁看到，再决定优化打开率还是优化转发。 | packaging（可叠加）；video-metrics（可叠加）；platform-native（可叠加） |
| `stickiness-pass` | 黏性终检：六项一次过 | medium | 发布前用一张清单过一遍：简单、意外、具体、可信、情绪、故事。 | video-metrics（可叠加）；script-flow（可叠加） |
| `promise-integrity` | 承诺与兑现：别把钩子做成标题党 | high | 每个钩子都要能指回正文里兑现它的那一段；兑现不了就删钩子，不要删承诺。 | packaging（要点相反）；x-playbook（要点相反）；gap-design（可叠加） |
| `video-metrics` | 视频留存度量：先量前 5 秒，再谈改法 | high | 先用 5 秒留存与归一化观看比例量出问题在开头还是中段，再决定改哪里。 | content-business（可叠加）；stickiness-pass（可叠加） |
| `story` | 故事的作用与滥用：更好懂好记，不等于更会说服 | high | 先用故事让人记住，别用它承诺说服；引用效应量时说明它是上限。 | story-craft（可叠加）；concretize（可叠加） |
| `hook-craft` | 钩子打磨：六槽、三拍、四错、四通道（实践者体系） | medium | 用三拍搭骨架、六槽做体检、四错做诊断、四通道做对齐；只产候选，效果回到度量。 | gap-design（可叠加）；script-flow（可叠加）；packaging（可叠加）；hook-forensics（可叠加） |
| `x-playbook` | X 平台发布与承接：选题、反差、折叠位、承接、分发 | medium | 发布前过选题/角度/第一句/反差/排版，发布后 10 分钟做评论区/简介/置顶三件承接。 | packaging（可叠加）；audience-psychology（可叠加）；content-business（依赖） |
| `packaging` | 包装：标题、封面、开场三件套 | high | 先定标题与封面，再写内容；开场必须确认点击。 | distribution-first（依赖）；promise-integrity（要点相反）；hook-craft（可叠加）；platform-native（可叠加） |
| `script-flow` | 脚本流程：包装 → 大纲 → 开场 → 正文 → 结尾 | high | 五步固定顺序，正文每点之间埋 mini hook，结尾留高音符。 | packaging（依赖）；hook-craft（可叠加）；stickiness-pass（可叠加） |
| `story-craft` | 故事技法：用问题、张力与分层释放把人留住 | medium | 把答案切成层，每层只给一点，再抛一个新问题。 | story（可叠加）；surprise-contrast（要点相反）；script-flow（可叠加） |
| `audience-psychology` | 受众心理：从一条内容到一群会回来的人 | medium | 明确立场、绑定已有讨论的符号、分层加深、给身份感。 | promise-integrity（依赖）；content-business（可叠加） |
| `content-business` | 内容生意：选对人、做够量、等到可信线 | medium | 先选一个能连做 50 条的受众，再按周排 50 条，前 10 条只看数据不下结论。 | packaging（可叠加）；video-metrics（可叠加） |
| `platform-native` | 平台原生：先按平台的硬参数改，再谈创意 | high | 先查折叠位与字数预算，再按平台重写第一句，不要缩放同一句。 | packaging（可叠加）；distribution-first（依赖）；hook-craft（可叠加） |
| `hook-forensics` | 爆款拆解：从已爆的内容里提取可复用的结构 | high | 选 5–10 条样本，逐条拆标题/封面/三拍/结构，只提炼槽位与顺序，不抄句子。 | hook-craft（可叠加）；video-metrics（依赖）；platform-native（可叠加） |

## 怎么用

1. 先读编译产物的入口（`SKILL.md`），按路由表只加载 1 张能力卡；
2. 能力之间怎么组合、谁先谁后，看编译产物内的 `capability-graph.md`；
3. 证据等级以每张卡 B 段为准；标 `practitioner` 的卡不提供效果承诺。

