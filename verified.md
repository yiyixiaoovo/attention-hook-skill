# 阶段 1.5b — 最终验证结论

- 候选集合：`candidates/framework.md`（21 条）
- 双验证者一致率：**0.762**，verified Jaccard：**0.875**
- 分歧条目：5 条 → 一律 `needs_review`
- 证伪 high 目标：['f20', 'p21', 'p34']

| id | 验证者一致结论 | 最终 | 依据 |
|---|---|---|---|
| f01 | verified | **verified** | 双验证者一致 |
| f02 | verified | **verified** | 双验证者一致 |
| f03 | verified | **verified** | 双验证者一致 |
| f04 | verified | **verified** | 双验证者一致 |
| f05 | reference | **reference** | 双验证者一致 |
| f06 | verified | **verified** | 双验证者一致 |
| f07 | verified | **verified** | 双验证者一致 |
| f08 | verified | **verified** | 双验证者一致 |
| f09 | verified | **verified** | 双验证者一致 |
| f10 | verified | **verified** | 双验证者一致 |
| f11 | needs_review | **needs_review** | 双验证者分歧（r1=reference / r2=needs_review） |
| f12 | needs_review | **needs_review** | 双验证者分歧（r1=reference / r2=verified） |
| f13 | needs_review | **needs_review** | 双验证者分歧（r1=reference / r2=needs_review） |
| f14 | needs_review | **needs_review** | 双验证者分歧（r1=reference / r2=needs_review） |
| f15 | verified | **verified** | 双验证者一致 |
| f16 | verified | **verified** | 双验证者一致 |
| f17 | verified | **verified** | 双验证者一致 |
| f18 | verified | **verified** | 双验证者一致 |
| f19 | verified | **verified** | 双验证者一致 |
| f20 | needs_review | **needs_review** | 双验证者分歧；证伪 high（r1=verified / r2=needs_review） |
| f21 | reference | **reference** | 双验证者一致 |

## 汇总

- verified: 14
- reference: 2
- needs_review: 5

> 说明：本表只覆盖 framework.md。principle.md 的 40 条作为能力卡的支撑规则使用，
> 不单独成为能力；counter-example.md 的 27 条作为 B 段边界素材。

---

## 第二批：视频留存（v01–v05，2026-11-23）

来源：两篇开放获取论文的片段（`source/short-video-engagement-2024.txt`、
`source/video-ad-hooking-period-2026.txt`），均为**单平台相关性研究**。

### 第一轮：写坏了，被验证者拦下

| 项 | 结果 |
|---|---|
| 候选数 | 6（v01–v06） |
| 一致率 | **0.167**（6 条里只 1 条一致） |
| verified Jaccard | **0.0** |
| 失败原因 | 把「论文测到什么」写成了「你该怎么做」：两篇都是相关性研究，候选却给出因果处方；v06 还凭空写了「平台按时长排序」 |

两位验证者独立指出同一问题，说明不是偶然。v06 已删除。

### 第二轮：改写为「度量与解读」导向后复验

| id | 结论 | 依据 |
|---|---|---|
| v01 | **verified** | ECR=P(watch>5s) 的定义 + 与 NAWP 相关 0.926，用于「开头效果」的早期读数 |
| v03 | **verified** | MOS 与互动弱相关的反例，削弱「画质是主因」的归因 |
| v05 | **verified** | hook 特征与 CPI 相关，但特征重要性按行业不同，无跨行业模板 |
| v04 | reference | 广告语境下的前 3 秒定义，只能界定问题，不能外推到自然内容 |
| v02 | needs_review → **弃用** | 源文明确说 AWP 同样受时长影响、应用 NAWP；候选却以 AWT÷时长当可比读数，被源文反证 |

复验：**一致率 1.0，verified Jaccard 1.0**（两位验证者逐条一致）。

> 这一轮的价值不在「最后过了」，而在**第一轮被拦住了**：如果没有双验证，
> 那 6 条会被写进能力卡，把相关性包装成因果。

## 汇总（含第二批）

- verified: 17（framework 14 + 视频 3）
- reference: 3（f05、f21、v04）
- needs_review: 5（f11 f12 f13 f14 f20）
- 弃用: 1（v02）；删除: 1（v06）

---

## 第三批：叙事/故事（s01–s04，2026-11-23）

来源：Mar et al. 2021 元分析（*Psychonomic Bulletin & Review*，CC BY，PMC8219577）——
75+ 独立样本、33,000+ 被试、150 个效应量。片段见 `source/narrative-memory-meta-2021.txt`。

| id | 结论 | 依据 |
|---|---|---|
| s01 | **verified** | 故事比说明文更好懂、更好记（理解与回忆） |
| s02 | **verified** | 平均效应 >0.5 SD，且对单一研究不敏感（留一法稳健） |
| s03 | **verified** | 元分析自报发表偏倚：低精度研究效应更大 → 0.5 SD 应视为上限 |
| s04 | **verified** | 作者明确反对「把所有信息强行写成故事」 |

双验证：**一致率 1.0，verified Jaccard 1.0**（两位验证者逐条一致）。两人都指出 s02 最弱——
它只是引用口径，须与 s03 成对使用；这一点已写进 `story` 卡 E 段第 5 步。

另：Rahmani et al. 2025 的 77 项 RCT 元分析（叙事 vs 无信息有效；叙事 vs 非叙事仅略强且不显著）
是更好的边界证据，但 Cambridge 页面反爬导致无法取得可核对全文，**未入库**，只记录在
`experiments/research/narrative-shortlist.md`。宁可不引，也不引没核对过的原文。

## 汇总（全部三批）

- verified: 21（framework 14 + 视频 3 + 叙事 4）
- reference: 3（f05、f21、v04）
- needs_review: 5（f11 f12 f13 f14 f20）
- 弃用: 1（v02）；删除: 1（v06）

能力卡：9 张（新增 `video-metrics`、`story`）。

---

## 实践者附录（h01–h06，2026-11-25）——**不进入双重验证**

来源：Kallaway 钩子体系，经 BuildOS 三篇二手分析与频道快照转述（`source/kallaway-secondary-2026.txt`）。

- `evidence: practitioner`，**0 控制实验、0 样本量、0 提升数据**，示例为幸存者样本。
- 因此**不跑三重验证**：这套材料不是"主张是否成立"的问题，而是"是否忠实转述"。
  入库只做了引用回源（6 条逐字命中）。
- 用途限定在流程与诊断；任何效果问题回到 `video-metrics` 的度量。
- 对应能力卡：`hook-craft`（B 段第一条即声明证据等级最低）。

> 这是本套技能里唯一明确标为「非证据」的一批候选。保留它是因为：
> 六槽体检、四错诊断、四通道对齐是可以直接执行的结构工具，而"因为来源不是论文就一律不用"会让技能少掉一半可用性。
> 原则是：**流程可以借，效果不能借。**

## 实践者附录二（xp01–xp09，2026-11-25）——同样不进入双重验证

来源：作者本人（@bpflmzj）提供的爆款方法论长帖原文（`source/x-playbook-author-2026.txt`）。

- 性质：单一作者、n=1 案例（作者称约 150 万曝光、90k 转化、当时约 2000 粉，**本仓库未独立核实**；「90k」口径原文未定义）。
- 这是**第一手经验**，比二手转述的 Kallaway 体系更直接，但同样**不是实证主张**：不跑三重验证，只核引用回源。
- 三条平台机制断言（「显示更多增加权重」「算法精准推荐」「转帖权重高于评论」）**无公开依据**，卡片里已逐条标为未验证，并给出"当假设自测"的处理方式。
- 对应能力卡：`x-playbook`（B 段第 2 条列明三条未验证断言）。

### 顺便修正原文的三处问题（入库引用保留原样，说明放这里）

1. 原文说「一共五个板块」，实际列了 6 节（选题/钩子/AI/承接/梗/排版时间）。
2. 「90k 转化」缺口径——如果是新增关注（2000 → ~9.2 万），那是比"150 万曝光"更强的卖点，不该含糊。
3. 「显示更多增加权重」与「读者不用解释背景就能看懂」存在张力：把关键信息后置会降低第一屏信息密度。卡片 B 段按"先可理解、再谈折叠"处理。

## 实践者附录三（k01–k23，2026-11-25）——同样不进入双重验证

来源：Kallaway 频道**前 19 条高播放视频的自动英文字幕**（约 9.7 万词），按锚点逐条摘录入库
（`source/kallaway-transcripts-2026.txt`）；完整转录稿不入库。

- `evidence: practitioner`；自动字幕可能有识别错误；无控制实验、无样本量。
- 只核引用回源（134 条片段 0 缺失），不跑三重验证。
- 本轮新增 5 张卡：`packaging`、`script-flow`、`story-craft`、`audience-psychology`、`content-business`；
  并扩写 `hook-craft`（表情对齐、AI 固定 prompt）。

### 差分结论（他讲了而我们没收）

按 19 条字幕的概念覆盖统计 + 语境判读：

| 他覆盖、我们原来没有 | 落点 |
|---|---|
| 包装优先（标题/封面/开场确认；CTR 10–12%） | `packaging` |
| 整篇脚本五步 + mini hook + 结尾高音符 | `script-flow` |
| 故事技法（张力/分层/多巴胺阶梯） | `story-craft` |
| 受众心理（立场/符号/痴迷层级） | `audience-psychology` |
| 账号层（画像/50 条计划/可信线） | `content-business` |
| 画面表情与标题情绪对齐、AI 固定 prompt | 扩写 `hook-craft` |

### 我们的独有部分（他 0 命中）

唤醒度/效价（arousal/valence）、元分析、发表偏倚、相关≠因果、知识诅咒、NAWP/观看比例口径——
这些在 19 条字幕里全部为 0。**他的空白就是证据卡的护城河**：他教"怎么做"，我们教"怎么判断有没有用、什么时候不能做"。

## 实践者附录四（平台原生化 + 爆款拆解，2026-11-26）

来源与许可边界：

- **Instagram 125 字符折叠**：逐字引自 `sergebulaev/instagram-skills`（**MIT**）的 caption checklist。
- **小红书封面/正文页参数**：来自 `op7418/guizang-social-card-skill`（**AGPL-3.0**）的 `platform-specs.md`，
  只提取**数字与结构**作为事实，**未复制表达**；AGPL 内容不进入本项目。
- **爆款拆解四步**：方法为通用流程（选样本→拆解→提炼模板→改写对照），参考
  `Xiangyu-CAS/xiaohongshu-ops-skill` 的爆款复刻链路思路（该仓库**无许可证**，不引用其文字）；
  R 段引用改用我们已有的 Kallaway 字幕（k09）。
- 新增 2 张卡：`platform-native`、`hook-forensics`；均 `evidence: practitioner`，无实验、无效果承诺。
- 平台参数会随版本漂移：本卡是 2026-11 口径，发布前核对官方文档。

### 行为评测（不是证据，是质量检查）

新增 `evals/behaviors/`：核心 8 张卡各 3 条 `input/context/expect`，共 24 条用例、72 个必须出现的判断项。
它们不用于自动判分，供人工/评审 Agent 对照；路由评测（`evals/test-prompts/`）仍保持 162 条。

### 校验器新增强制项

`description` 超过 1024 字符（Agent Skills 规范）、反引号能力名解析失败、承诺式表述（未在否定语境）、
行为评测格式错误——四类均告警，`--strict` 下为错误。
