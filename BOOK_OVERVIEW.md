# attention-hook 语料整体理解（阶段 0 · Adler 分析阅读）

> 本文档是 cangjie-skill 流水线的阶段 0 产出，后续所有 extractor、能力卡与覆盖率审计以此为全局上下文。
>
> **引用约定**：正文 `"..."` 内的英文均为对应 `source/*.txt` 的逐字子串（仅对 OCR 换行处的空白做归一化）；每处注明文件，关键处注明所在小节或表。不写页码，不补语料没有的数字，不写"研究表明"式归因。
> **核验方式**：可用任意文本检索（如 PowerShell `Select-String -SimpleMatch`）在对应 `.txt` 中直接搜到；§0.3 给出本次核查用的检索词与结果。

## 基本信息

- **语料集**：attention-hook（5 份公开材料）
- **任务目标**：把"什么让人点开、看下去、转发"蒸馏成能给**文章与视频**用的 skill
- **实际覆盖**："转发/分享"有较强证据；"好奇心/信息缺口"有综述级机制证据、内容应用未验证；"点开/看完"无一手证据
- **证据构成**：2 份同行评议（1 份原论文 + 1 份综述）、2 份同一本畅销书的二手摘要、1 份作者访谈
- **时间跨度**：材料 2007–2024；一手传播数据采集于 2008 年（美国《纽约时报》）；好奇心综述发表于 2015 年
- **处理时间**：2026-11-22
- **阶段**：0 / 6（`PIPELINE_STATE.md` 中未勾选）

---

## 0. 语料修订与核验（本版已按修正后语料更新）

### 0.1 修订记录

**A. 好奇心文件已替换为正确的论文（上一版曾错页）**

- 现行文件：`kidd-hayden-2015-curiosity.txt`（82,853 字符，659 行）
- 标题：`"The psychology and neuroscience of curiosity"`；作者 Celeste Kidd、Benjamin Y Hayden
- 出处：`"Neuron. 2015 Nov 4;88(3):449–460"`；`"PMCID: PMC4635443"`、`"PMID: 26539887"`
- 自检：全文 `curiosit` **164 处**（`.txt` 全文、大小写不敏感）、`pancreatitis` **0 处**（本次逐字检索）
- 性质：**Perspective/综述**（原文自称 `"In this Perspective"`，并说 `"provide a selective overview of its current state"`），不是原始实验论文
- 影响：上一版"信息缺口零证据"的判断随之作废；§1、§2、§3、§4、§5、§6 的相关小节已按新文件重建，其余部分保留原结论。

**B. JMR 期刊标注更正**

- 文件刊头：`"Journal of Marketing Research , April 2012, Vol. 49, No. 2 (April 2012), pp. 192-"`；版权页：`"JOURNAL OF MARKETING RESEARCH, APRIL 2012"`
- 正确标注：**Journal of Marketing Research (JMR) 2012;49(2):192–205**。任务说明曾写 *Psychological Science*，已更正；后者是 Berger 2011 年的另一篇（本语料未收），不混用。
- **保留原观察**：JMR 自己承认负面情绪会伤品牌态度——`"while negative emotions may hurt brand and product attitudes"`；这条张力仍是 §3.2 C1 的核心。

### 0.2 其他读取与核查问题

- `berger-milkman-viral.txt` 含 **390 个 NUL 字节**，全在 JSTOR 水印行（`"This content downloaded from"` 前后）；直接按文本读会被判为二进制文件，抽取前必须清洗。
- 该文件是 JSTOR 扫描 OCR：有断词（`characteris tics`、`transmis sion`）、错字（`desian`）、公式丢失。**引文必须按空白归一化检索**，不要引用被 OCR 损坏的词。
- `kidd-hayden-2015-curiosity.txt` 是 PMC 的**作者稿**（`"Author manuscript"`），含网站导航与排版噪声；正文有少量错字（如 `"motivate new interested in the problem"`、把 Loewenstein 拼成 Lowenstein），引用按原样照录，不改字。
- `made-to-stick-summary.txt` 正文在文件里**重复出现两遍**（L141–155 与 L157–171 是同一段书评），统计"CHOP 说了几次"时不要重复计数。
- 目录里另有 `captivology-metadata.json`、`loewenstein-1994-alt.html` 等不在本次 5 份清单内的文件。仅做标题级核查：`loewenstein-1994-alt.html` 是 CMU 的 George Loewenstein 教师主页，**不是** 1994 论文正文。`_meta/` 按要求未读。

### 0.3 核查方法（可复现）

- 检索词：`curiosit` / `information gap` / `pancreatitis` / `Goldilocks` / `attention` / `8 second` / `eight second` / `attention span` / `short attention` / `秒`
- 好奇心文件：`curiosit` 164 处、`information gap` 2 处、`Goldilocks` 3 处（1 处在 Keywords，2 处在参考文献）、`pancreatitis` 0 处。
- `attention` 合计 31 处：Kidd & Hayden 20 处（含参考文献标题，正文是注意分配/婴儿注视研究）、JMR 9 处（7 处曝光/编辑注意力、2 处研究关注度）、CHOP 2 处（同一句重复）。**无一处谈注意力时长。**
- Kidd 文中 `seconds`/`minute` 各命中处均为实验计时（`"2.25 seconds"` 奖赏延迟、`"60 seconds"` 自由玩耍、`"about 15 minutes"` 探索），不是注意力时长。
- 注意力时长类检索（`8 second`/`eight second`/`attention span`/`short attention`/`秒`）在 5 份 `.txt` 中**全部 0 命中**（详见 §4.7）。

### 0.4 对阶段 0 的四条硬结论

1. **信息缺口/好奇心：现有综述级证据**（机制层强、内容应用层弱），可进入能力卡，但必须标"综述转述的实验 + 需内容场景自测"（§2.5）。
2. **一手传播数据仍只有一篇论文（JMR）**，其因变量是"是否进入 2008 年《纽约时报》最常被邮件列表"，不是点击、观看、完播或转化。
3. 其余 3 份有效材料（CHOP、HBS、访谈）是二手摘要与作者自述，只能提供"作者主张"，不能提供机制证据。
4. **新的最大缺口**：中文平台数据、视频场景验证，以及"缺口如何兑现而不滑向标题党"的现场证据（§4.8、§5.4）。

---

## 1. 材料定位（Adler 步骤 1：结构）

### 1.1 这批材料是什么类型

不是一本书，而是**一个混合证据包**：两篇同行评议（一篇传播学原论文、一篇神经科学综述）+ 两本畅销书的二手转述与作者访谈。没有统一作者、统一方法或统一结果变量。把它当"一本书"读会犯三个错：把二手摘要与原论文等权；把两套营销框架（SUCCESs、STEPPS）当成互相印证的发现；把实验室的"信息寻求"直接当成信息流里的"点开/看完"。

### 1.2 一句话主旨

> 这五份材料能支持的只有一句：内容是否被转发，与它是否唤起高唤醒情绪、是否被认为有用/有趣/意外相关，并受曝光位置与渠道约束（情绪一项有实验支持，其余为田野相关）；好奇心/信息寻求由可感知且适中的知识缺口驱动（综述级证据）；而"让人点开"与"让人看完"，语料没有一手证据。

### 1.3 骨架：7 个一级论点及其关系

| 编号 | 一级论点 | 来源 | 证据类型 | 与其他论点的关系 |
|---|---|---|---|---|
| A1 | 传播的近因是**唤醒度**，不是效价：高唤醒情绪（敬畏/愤怒/焦虑/愉悦）提升分享，低唤醒（悲伤）抑制分享 | JMR | 田野相关 + 3 个实验（因果，但 DV 为自评意愿） | 核心论点（传播链） |
| A2 | **实用、有趣、意外**是独立于情绪的正相关特征 | JMR | 田野控制变量 | 与 A1 并列（同一回归模型） |
| A3 | **曝光位置**与内容特征同量级；**渠道会翻转结论**（实用价值邮件↑、博客↓） | JMR | 田野 | A1–A2 的边界条件 |
| A4 | 可记忆性 = **SUCCESs 六原则**（简单/意外/具体/可信/情感/故事） | CHOP、HBS（同一本书） | 二手摘要 + 作者访谈 | 与 A1–A3 **结果变量不同**（记忆 ≠ 传播），不可互证 |
| A5 | 口碑 = **STEPPS 六驱动**（社交货币/触发器/情绪/公开性/实用价值/故事） | 作者访谈 | 作者自述，无定义无数据 | 与 A4 并行命名体系，与 A1 部分重叠但未互证 |
| A6 | **注意力的"获取"与"保持"是独立环节** | CHOP | 二手一句话 | 漏斗上游，却是证据最薄处 |
| A7 | **信息寻求由知识缺口驱动**：缺口适中时好奇最强（Goldilocks），好奇促进学习 | Kidd & Hayden 2015 | 同行评议综述（汇总多组实验；非内容场景） | 独立第二链（信息寻求链）；与 A1–A5 的"传播"链无交叉证据 |

**关系**：A1–A5 属"传播链"（A1–A3 同一论文内部递进：机制 → 并列预测项 → 边界；A4/A5 是两套营销框架的并行命名，重复计数风险见 §3.3）；A6–A7 属"信息寻求/注意链"，其中 A7 是综述级机制，A6 只有二手一句话；**两条链在本语料里没有一篇研究把它们连起来**——没有"信息缺口→转发"或"好奇→完播"的证据。这是本语料最大的结构性空白。

### 1.4 核心问题：语料的问题 ≠ 用户的问题

- **语料回答的问题**：为什么某些内容被大量**转发**（JMR，且只在美国 2008 年邮件语境）？信息寻求如何被**知识缺口**驱动（Kidd & Hayden，实验室任务）？
- **用户要解决的问题**：怎样修饰文章和视频，让人**点开、看下去、转发**？

语料覆盖了"转发"与"信息寻求"两条链，却缺"点开"和"看完"；两者相差两个环节。本阶段最重要的边界就是：**不要把"转发研究"或"实验室信息寻求"当成"注意力研究"用。**

### 1.5 材料定位表

| 文件 | 实际讲了什么机制 | 证据类型 | 可信度（层级/权重） | 能支撑什么 | 不能支撑什么 |
|---|---|---|---|---|---|
| `kidd-hayden-2015-curiosity.txt` | 信息缺口/好奇心、Goldilocks、好奇心促进学习、神经奖励机制 | 同行评议综述（Neuron 2015, Perspective；汇总多组实验） | 高（综述级，权重约 0.8；非一手数据） | 机制方向与实验例证（信息寻求/注意/学习） | 内容/视频/平台/点击/完播；不能当"标题党操作手册" |
| `berger-milkman-viral.txt` | 情绪唤醒、实用、意外、兴趣、曝光位置、渠道反转 | 同行评议 JMR 2012：6956 篇田野 + 3 实验 | 高（唯一一级证据，权重 1.0） | "分享/上榜"的条件相关与实验因果 | 点击、观看、完播、转化；2008 NYT 邮件之外的场景 |
| `made-to-stick-summary.txt` | SUCCESs 六原则（CHOP 通讯书评） | 二手摘要（2024-11-25） | 中低（二手，权重约 0.2） | 该书观点的转述、可作案例库 | 原书原文、任何测量、"六原则有效" |
| `hbs-ideas-that-stick.txt` | 同一本书 + 知识诅咒（HBS Alumni 访谈） | 二手摘要/作者访谈（2007-03-01） | 中低（二手，且直接访作者，权重约 0.2） | 作者自述、术语、类比 | 任何证据、预测能力 |
| `berger-contagious-interview.txt` | STEPPS 六驱动（营销博客访谈） | 作者访谈（2015-04-18） | 低（作者自述 + 不可核验案例，权重约 0.2） | 作者主张与术语名 | 任何机制证据；客户案例不可核验 |

**可信度差异在哪**：

1. **测量 vs 断言**：只有 JMR 有原始数据与统计；Kidd & Hayden 是同行评议**综述**（汇总他人实验，不产生新数据）；CHOP/HBS/访谈没有任何测量。综述 ≠ 二手摘要：前者经同行评议并交代文献，后者只是书评/访谈。
2. **独立 vs 同源**：CHOP 与 HBS 讲的是同一本书（*Made to Stick*），HBS 还直接采访作者；访谈讲的是 *Contagious*，而 *Contagious* 作者就是 JMR 论文作者。**这三份材料不构成相互独立的验证**，"两处都这么说"不等于两个证据。Kidd & Hayden 是独立来源，但研究的是另一条问题链（信息寻求，不是传播）。
3. **结果变量不同**：CHOP/HBS 说"记住（memorable）"，JMR 测"被分享（most e-mailed）"，Kidd & Hayden 测"信息寻求/注意/学习"，访谈说"catch on"。这四个不是同一个变量。
4. **时代与渠道不同**：2008 邮件数据、2007 书、2015 神经科学综述、2015 营销访谈、2024 疫苗通讯书评。

### 1.6 下游引用标注规则（写进每个能力卡）

- JMR：可写"证据支持（**仅限分享/上榜这一结果变量**）"；不得写成"提高点击/完播"。
- Kidd & Hayden：写"（综述：Kidd & Hayden 2015）"，只能写"综述汇总显示"，不得写"本语料实验证明"——原始实验由综述转述，不在语料里。
- 二手摘要：必须写"（二手摘要：CHOP）"或"（二手摘要：HBS Alumni）"，只能写"该书主张"。
- 访谈：写"（作者访谈）"，只能写"作者主张"。
- "注意力只有 8 秒"：**禁用**（§4.7）。

---

## 2. 解释（Adler 步骤 2）：机制清单

### 2.0 证据强度定义

- **强**：同行评议 + 有数据（田野和/或实验），结果在多个模型、子样本中稳健；**或**同行评议综述系统汇总多组实验（标"综述级"）。**必须同时标结果变量**（分享/信息寻求/学习/观看），否则"强"没有意义。
- **中**：同行评议的田野相关证据，未做因果实验；或构念定义/操作化含糊。
- **弱**：只有二手摘要或作者访谈里的断言、清单、案例；无测量、无对照。
- **无**：语料没有可用文本。

> 综述级说明：Kidd & Hayden 是同行评议 Perspective/综述，引文是**综述原文**，它转述的原始实验不在语料里——可作"机制共识"，不可作"本语料实验证明"。

### 2.1 关键术语（作者本人的用法，不是字典用法）

| 术语 | 作者在语料中的用法 | 与常识用法的差异 |
|---|---|---|
| viral（JMR） | 操作化为"是否进入《纽约时报》most e-mailed 榜"（二元变量）：`"an article a released online on day t earns a position on the most e-mailed list and 0 otherwise"` | 常识=播放量/转发量；论文里是"被邮件"这一行为 |
| most e-mailed list | `"The New York Times continually reports which articles from its website have been the most e-mailed in the past 24 hours"`，公开榜单、每 15 分钟更新 | 不是阅读量，不是推荐量 |
| arousal / activation | `"Arousal is a state of mobilization."`；高唤醒促发行动，`"Given that sharing information requires action"` | 常识=情绪强弱；作者=生理动员状态 |
| emotionality | 用 LIWC 统计正/负词占比（7630 词表） | 常识=煽情；作者=词频指标 |
| positivity | 正面词比例减负面词比例 | 常识=正能量；作者=文本情感差 |
| practical utility | 提供可操作、能省钱/改善生活的信息（示例：Voter Resources） | 常识=有用；作者=可执行信息 |
| interest | 编码者 1–5 分量表，语料**没有给独立定义** | 常识=兴趣；作者=主观评分 |
| surprise | 编码者 1–5 分量表 | 同上 |
| get and hold attention（CHOP 二手） | `"Unexpected refers to using relevant but unanticipated ways to both get and hold attention."` | 常识=抓眼球；原文只有这一句，**没有时长、没有测量** |
| Simple（二手） | `"Simple refers to determining the core idea of the message and how to share it."` | ≠"短"；是"找到核心" |
| Unexpected（二手） | `"Unexpected refers to using relevant but unanticipated ways to both get and hold attention."` | 关键在 relevant（相关但未预料），不是猎奇 |
| Concrete（二手） | `"Concrete refers to presenting ideas in ways that are relatable and easy to understand."` | 可感知、可想象，不是"细节多" |
| Credible（二手） | `"Credible refers to giving information in a way that is convincing or easily tested."` | 关键在 "easily tested"（可检验） |
| Emotional（二手） | `"Emotional refers to making people care about your message."` | **≠ JMR 的高唤醒**；是"让人在意" |
| Stories（二手） | `"Stories not only offer a way to accomplish some of the aforementioned characteristics, but they are also memorable and can inspire people to act."` | 结果变量是"记住+行动"，不是"分享" |
| curse of knowledge（二手） | `"We are all the IT guy in our fields of expertise."`；`"The smarter we get, the more problematic it is to communicate that knowledge to other people."` | 专家越懂越难讲明白；类比，无测量 |
| STEPPS 六项（访谈） | 只有名称：`"There are 6 key drivers of word of mouth. I’ve put them in an acronym called STEPPS"`（列表含 Social Currency、Triggers、Emotion、Public、Practical Value、Stories，见访谈 L41–51） | **语料没有给其中任何一项下定义**，不得代拟 |
| information gap（信息缺口，综述） | 引 Loewenstein 定义：`"a cognitive induced deprivation that arises from the perception of a gap in knowledge and understanding."`；综述最终取 `"a drive state for information"` 这一宽定义 | 常识=好奇心；作者=知识缺口造成的"渴" |
| priming dose（引子剂量） | `"a small amount of information serves as a priming dose, which greatly increases curiosity."` | 常识=先给结论；作者=先给一点信息会放大好奇 |
| Goldilocks effect / 适度差异 | Keywords 含 `"Goldilocks effect, uncertainty"`；中等不确定性/信息量时注意与好奇最强（婴儿 `"moderately discrepant"` 时注视最多；trivia 在中等信心时最好奇） | 常识=越意外越好；作者=太可预测或太意外都会让人走开 |
| curiosity vs information-seeking（综述） | 综述不严格区分二者：`"it is a special form of information-seeking distinguished by the fact that it is internally motivated"`；但承认内/外动机难分，最后取宽定义 | 常识=好奇心是性格；作者=可操作的信息寻求驱动 |

> **注意**：标"（二手）"的行，引文来自二手摘要对原书内容的**转述**，不是原书原文（本语料没有 *Made to Stick* 原书）；标"（访谈）"的行只来自 Heidi Cohen 访谈；标"（综述）"的行引文来自 Kidd & Hayden 2015 综述**原文**（不是其转述的原始实验论文）。引用时须写「（二手摘要：CHOP）」或「（作者访谈）」或「（综述：Kidd & Hayden 2015）」，不得写成"作者原话"。

### 2.2 机制清单（15 条；M13 已按修正后语料重建）

> 出处栏写法：`JMR` = 同行评议论文；`kidd-hayden-2015-curiosity.txt` = 同行评议综述（Neuron 2015，引文为综述原文）；`（二手摘要：CHOP）` = CHOP 通讯书评；`（二手摘要：HBS Alumni）` = HBS 校友文章（含作者访谈）；`（作者访谈）` = Heidi Cohen 访谈。强度定义见 §2.0；"结果变量"一栏必须与强度一起读。

| ID | 机制（可迁移表述） | 出处 | 关键逐字证据 | 强度 | 证据类型 / 结果变量 |
|---|---|---|---|---|---|
| M01 | 高唤醒情绪（敬畏、愤怒、焦虑、愉悦/幽默）提升转发 | JMR | `"Virality is partially driven by physiological arousal."`；`"Content that evokes high-arousal positive (awe) or negative (anger or anxiety) emotions is more viral."` | **强** | 田野相关 + 实验因果（amusement N=49、anger N=45；唤醒自评中介）；DV=分享意愿/上榜 |
| M02 | 低唤醒情绪（悲伤）抑制转发 | JMR | `"Content that evokes low-arousal, or deactivating, emotions (e.g., sadness) is less viral."` | **强** | 田野 + 实验（sadness N=47）；DV 同上 |
| M03 | 效价：正面内容更易传播；负面内容只在"高唤醒"时可能有利 | JMR | `"The results indicate that positive content is more viral than negative content, but the relationship between emotion and social transmission is more complex than valence alone"`；`"the coefficient on positive words is considerably larger than that on negative words"` | **强** | 田野相关（效价未做因果实验）；DV=上榜 |
| M04 | 实用价值/信息性提升分享 | JMR | `"informative (practically useful), interesting, and surprising articles are more likely to make the New York Times' most e-mailed list"` | **强（但渠道依赖）** | 田野控制变量；博客方向反转（§2.3 M04、C3）；DV=上榜 |
| M05 | 意外性提升上榜 | JMR | 同上 `"interesting, and surprising articles are more likely"` | **中** | 田野控制变量；无独立实验；与 CHOP 的「Unexpected」同名不同测 |
| M06 | 兴趣提升上榜 | JMR | `"more practically useful, interesting, and surprising content is more viral"` | **中** | 田野控制变量；构念定义模糊 |
| M07 | 简单/核心信息 | （二手摘要：CHOP）（二手摘要：HBS Alumni） | `"Simple refers to determining the core idea of the message and how to share it."` | **弱** | 二手摘要；作者归纳；无测量 |
| M08 | 具体性（抽象 → 具体） | （二手摘要：CHOP）（二手摘要：HBS Alumni） | `"Concrete refers to presenting ideas in ways that are relatable and easy to understand."`；`"But we demonstrate a greater understanding of the underlying situation if we talk about concrete details and specific actions and stories."` | **弱** | 二手摘要/作者访谈；无测量 |
| M09 | 可信/可检验 | （二手摘要：CHOP） | `"Credible refers to giving information in a way that is convincing or easily tested."` | **弱** | 二手摘要；无测量 |
| M10 | 故事 | （二手摘要：CHOP）（二手摘要：HBS Alumni） | `"Stories not only offer a way to accomplish some of the aforementioned characteristics, but they are also memorable and can inspire people to act."`；`"We respond instinctively to this aspirational story of a guy who overcame big odds."` | **弱** | 二手 + 作者访谈；JMR 完全没测故事 |
| M11 | 社交货币/自我呈现 | （作者访谈，仅名称）+ JMR（解释性假说） | `"Social Currency"`（仅名词，无定义）；JMR：`"people may share content to help others, generate reciprocity, or boost their reputation"` | **弱** | 访谈只列名；JMR 是解释性推测，且被其结论弱化（见 C4） |
| M12 | 触发器/公开性 | （作者访谈，仅名称） | STEPPS 列表中的 `Triggers`、`Public`（访谈 L41–51，无任何展开） | **弱** | 仅名称；JMR 只把环境线索列为未来方向：`"making certain topics more accessible"` |
| M13 | 信息缺口/好奇心：可感知的知识缺口驱动信息寻求；缺口适中时最强；先给一点信息会放大好奇 | kidd-hayden-2015-curiosity.txt | `"a cognitive induced deprivation that arises from the perception of a gap in knowledge and understanding."`；`"a small amount of information serves as a priming dose, which greatly increases curiosity."` | **强（综述级）／应用层弱** | 同行评议综述汇总实验；DV=信息寻求/注意/学习，非点击/转发 |
| M14 | 注意力的"获取与保持"（钩子/开场） | （二手摘要：CHOP） | `"Unexpected refers to using relevant but unanticipated ways to both get and hold attention."` | **弱** | 二手一句话；无时长、无测量 |
| M15 | 曝光位置/分发与内容特征同量级 | JMR | `"While being featured prominently, for example, increases the likelihood that content will be highly shared"`；`"content characteristics are of similar importance (see Figure 2)"` | **强** | 田野（同论文）；说明分发可"机械地"提升传播：`"which could mechanically increase their virality"` |

**重要边界（M01/M03）**：不是"所有负面情绪都促进"——JMR 的厌恶（disgust）**不显著**：`"we do not find any significant relationship between disgust and virality"`。起作用的不是"负面"这个标签，而是情绪类别及其唤醒水平。

**M13 补充**：Goldilocks（缺口太大或太小都不最优）在综述里有明确依据（Keywords、婴儿 U 型、trivia 中等信心峰值），但全部是**实验室/婴儿研究**，不是内容场景；细节与引用见 §2.5。注意形状措辞：原文正文写 `"U-shaped function of confidence"`，但描述与图注呈现的是"中等信心时最好奇"——引用时用描述句，别把形状标签当公式。

### 2.3 每个机制的可迁移动作与边界

| ID | 可迁移到文章/视频的动作 | 边界 / 反例 / 注意 |
|---|---|---|
| M01 | 用敬畏（震撼数据/大图景）、幽默、愤慨、紧迫感写标题与开场；给读者一个"高唤醒"的入口 | 仅"转发"有据，点开/留存无据；伦理红线：不制造恐慌、不煽动仇恨；公共健康慎用（见 C1） |
| M02 | 不以悲伤/无力感作为主情绪与收尾；共情可以，但不要让它成为分享的唯一驱动力 | 悲伤叙事对"陪伴型深度观看"可能有用——语料无数据，不能反推 |
| M03 | 正面框架优先；负面情绪只在"高唤醒 + 品牌可承受"时使用 | 负面情绪可能伤品牌态度（C1）；不要为了传播牺牲长期信任 |
| M04 | 把信息做成可执行清单/步骤/资源；明确"读者能立刻用什么" | 博客方向上实用价值反转（C3）；公开信息流的效果需自测 |
| M05 | 反常识数据、意外对比、预期违背放标题/封面/开场 | 必须与正文一致（外部伦理约束）；JMR 只测上榜，未测点击 |
| M06 | 设计"值得看下去"的兴趣点（悬念、冲突、具体人物） | 构念模糊，无法直接操作化；需 A/B |
| M07 | 一句话说清核心信息，删枝蔓 | 过度简化会伤可信与准确（C2） |
| M08 | 抽象名词换成具体的人/动作/数字/场景；用可感知的细节 | 细节必须真实，不能编造——这与 M09 绑定 |
| M09 | 给数字、来源、可复现演示、可自行检验的凭据 | 这是防"虚假承诺"的主要机制；也是 C1 的约束面 |
| M10 | 人物—冲突—转折—结果；让故事承载核心信息而非装饰 | 弱证据；故事不能替代事实核查 |
| M11 | 设计"转发后显得聪明/有用/有品味"的理由；分享文案点明价值 | JMR 结论更偏"内部唤醒"（C4）；只能当诊断假设，不能当主策略 |
| M12 | 触发情境线索（"下次遇到 X 时想到这个"）；提高公开可见性/可模仿性 | 语料只有名称，纯假设，不能写进 skill 的"方法" |
| M13 | 在标题/开场提出"可感知、可兑现"的缺口：先给一点信息，留一个明确问题；按 Goldilocks 校准不确定性（别什么都不给，也别一次给完/太抽象） | 仅实验室证据（trivia/图片/玩具/婴儿/动物）；"缺口"必须真实可兑现，否则滑向标题党（外部伦理约束）；视频与中文平台需自测 |
| M14 | 把"获取注意"与"保持注意"分开设计、分开测 | 无任何时长数据；"8 秒"禁用（§4.7）。Kidd & Hayden 的注意测量是婴儿"看/移开"（look-away），不是内容观看时长 |
| M15 | 发布前先检查曝光位置/渠道/首轮流量池，再决定改不改文案 | JMR 的"位置"是 NYT 首页，不等于算法推荐；迁移需平台数据 |

### 2.4 论证链拆解

**JMR 田野链**：6956 篇 NYT 首页文章（2008-08-30 至 11-30，`"6956 articles"`）→ 其中 `"20% earned a position on the most e-mailed list"` → 2566 篇随机子样本由 3 名编码者人工编码（`"They received the title and summary of each article, a web link to the article's full text, and detailed coding instructions"`）→ logistic 回归 + 日固定效应 + 曝光位置/印刷版面/作者名气/长度/复杂度/主题等控制 → 情绪系数（原文：`"a one-standard deviation increase in the amount of anger an article evokes increases the odds that it will make the most e-mailed list by 34%"`；`"a one-standard-deviation increase in awe increases the odds of making the most e-mailed list by 30%"`）→ 与曝光时长比较（`"equivalent to spending an additional 2.9 hours as the lead story on the New York Times website"`）。**注意**：情绪编码依据是标题+摘要（JMR 原文如此），"唤醒"是按情绪类别先验假设，不是测量。

**JMR 实验链**：2a 广告故事（amusement，`"Participants (N = 49) were randomly assigned to read"`）；2b 客服故事（anger，N=45）；3 新闻故事（sadness，N=47）→ 自评分享可能性（`"they would be to share it with others"`，原文 OCR 断行所致）→ 自评唤醒 → 中介检验 → 结论"唤醒驱动传播"。

**Kidd & Hayden 综述链**：以 Loewenstein 信息缺口理论为纲（信息缺口定义 + "引子剂量"）→ 引 Kang et al. 2009 的 trivia + fMRI 研究（中等信心时最好奇、好奇者愿为答案付费）→ 引 Jepma et al. 2012 的模糊图片研究（好奇是厌恶状态）→ 引 Kidd, Piantadosi & Aslin 2012/2014 的婴儿视觉/听觉序列研究（注意在中等信息量处最稳）→ 引动物 bandit 与不确定性任务（信息本身可当奖赏）→ 用 Tinbergen 四问组织 → 结论是研究议程。**注意**：这是 Perspective 的"选择性综述"（`"provide a selective overview of its current state"`），不是系统综述/meta 分析；原始实验不在语料内，数字只有它转述的（如信息价值约为奖赏的 25%）。

**二手材料的论证链**：案例归纳 → 命名 → 清单化（CHOP：`"Using the acronym SUCCESs, the authors described why some ideas are more memorable than others"`；HBS：`"six principles of stickiness"`）。访谈链：断言 → 列表（`"Word of mouth isn’t random or luck, there’s a science behind why things go viral."`）→ 客户自报案例。全程无对照、无测量、无结果变量。

→ **三条论证链的证据等级完全不同（JMR 田野+实验／Kidd & Hayden 综述汇总／CHOP、HBS、访谈的作者断言），不能并置为"研究 + 书互相印证"。**

### 2.5 信息缺口/好奇心：补源后它支持什么、不支持什么

**支持的（机制层）**

1. **好奇心 = 信息缺口驱动**。综述引 Loewenstein 理论：`"a cognitive induced deprivation that arises from the perception of a gap in knowledge and understanding."`；并给"引子剂量"：`"a small amount of information serves as a priming dose, which greatly increases curiosity."`
2. **Goldilocks 效应在综述里**。关键词含 `"Goldilocks effect, uncertainty"`；两条实验线索：(a) 婴儿对信息量极低或极高的序列最易移开注意：`"infants’ probability of looking away was greatest to events of either very low information content"`，而在中等信息量处最少移开（`"least likely to look away at events with intermediate information content"`）；(b) 人对 trivia 的好奇在"有一点概念但没把握"时最高：`"they were most curious when they had some idea about the answer, but lacked confidence."`
3. **好奇促进学习**：`"curiosity enhances learning"`；且高好奇状态下连无关材料也记得更好：`"the curiosity state led to better learning, even for the things people weren’t curious about."`
4. **神经机制：好奇招募奖赏/学习系统**：`"Brain activity in the caudate nucleus and inferior frontal gyrus (IFG) was associated with self-reported curiosity."`；信息本身有价值：`"the value of information about a reward is about 25% of the value of the reward itself—surprisingly high."`
5. **可引用的实验细节**（均由综述转述，不是本语料一手数据）：
   - **Kang et al. 2009**：trivia + fMRI；好奇者 `"willing to pay for the information"`；中等信心时最好奇；`"the learning effect was particularly strong on trials on which subjects’ guesses were incorrect"`。
   - **Jepma et al. 2012**：模糊图片；好奇伴随厌恶相关脑区激活——`"curiosity is a fundamentally aversive state"`（这是 Jepma 研究的结论）。
   - **Gruber et al. 2014**：trivia + 无关面孔；高好奇状态下对无关面孔的记忆更好。
   - **Kidd, Piantadosi & Aslin 2012/2014**：`"7- and 8-month-old infants"` 的视觉/听觉序列，look-away 呈 U 型。
   - **Blanchard, Hayden & Bromberg-Martin 2015**：猴子的 curiosity tradeoff 任务，信息价值≈奖赏的 25%。
   - **Bromberg-Martin & Hikosaka 2009**：猴子偏好"无战略收益"的即时信息。
   - **Schulz & Bonawitz 2007**：`"children prefer to play with toys that violate their expectations"`，并愿探索"因果被混淆"的玩具。
6. **代价与双面性**：`"its overexpression contributes to distractibility"`；`"Curiosity is thought of as the noblest of human drives, and is just as often as it is denigrated as dangerous"`。

**不支持的（应用层）**

- **没有内容/视频/平台场景**：全文 `viral` 0、`social media` 0、`headline` 0、`click` 0、`advertising` 0、`marketing` 0、`sharing` 0；`internet` 仅 1 次（`"browsing the internet"`）。没有点击率、完播率、转发量。
- **没有"钩子/标题"操作建议**：原文是研究议程，且明确 `"we are reluctant to commit to a strict definition now."`
- **没有注意力时长主张**：`seconds`/`minute` 都是实验计时（`"2.25 seconds"`、`"60 seconds"`、`"about 15 minutes"`）。
- **不讨论"缺口如何兑现、能不能骗、标题党代价"**——这是应用方必须自己补的伦理与验证。
- **不能把 Goldilocks 当参数配方**：它说的是"最优信息量/不确定性"这一方向，不是"悬念留几秒/给几个信息点"的配方。原文对形状的措辞还与图注不完全一致（正文 `"U-shaped function of confidence"`，图注是"中等信心时最"），引用时用描述句。

**引用规则**：写"（综述：Kidd & Hayden 2015）""综述汇总显示"；不写"实验证明"（原始实验不在语料内）。

---

## 3. 机制之间的关系（前置、冲突、合成）

### 3.1 前置条件

- **P1 被看到优先于文案**：JMR 证明曝光位置与内容特征"同量级"（M15），6956 篇里只有 20% 上榜。修饰文案之前，先确认有没有曝光。
- **P2 结果变量要分层**：记住（*Made to Stick* 语境）≠ 转发（JMR 语境）≠ 信息寻求/学习（Kidd & Hayden 语境）≠ 观看（无证据）。四个目标必须分开设计、分开测量。
- **P3 高唤醒是"放大器"，具体/故事是"载体"**：没有载体，情绪没有可转述的内容；没有情绪，载体不被行动。**这是推断**——语料没有检验交互（JMR 没测 concrete/story，二手材料没测传播）。
- **P4 可信是实用与故事的守门条件**：CHOP 把 Credible 定为 `"convincing or easily tested"`；若实用信息不可检验，就滑向虚假承诺。语料没有讨论欺骗，这是**外部伦理约束**，不是语料结论。
- **P5 两条链分开用**：传播链（A1–A5、M01–M12/M14/M15）与信息寻求链（A7、M13）在本语料内**没有交叉证据**；用"好奇心"论证"转发"、或用"高唤醒"论证"看完"，都是越界推理。缺口只能从"信息寻求/继续看"这一侧讲，不能从"分享"这一侧讲。

### 3.2 冲突与张力（C1–C8；C1 最大）

**C1 ★最大张力：高唤醒（尤其愤怒/焦虑）提升传播 vs 品牌/信任受损与"不得虚假承诺"。**

- 一边：JMR 证明愤怒/焦虑/敬畏提升上榜几率（M01），甚至建议 `"public health information should be more likely to be passed on if it is framed to evoke anger or anxiety rather than sadness"`。
- 另一边：JMR 自己承认 `"while negative emotions may hurt brand and product attitudes"`；CHOP 的疫苗沟通语境要求可信、不伤害（`"convincing or easily tested"`、`"Emotional refers to making people care about your message."`）。
- 这是**传播目标与信任/伦理目标的取舍**，不是可以两全的技术问题。
- 用户举例的"制造缺口 vs 不得虚假承诺"：见 C8——现在语料有"缺口"文本，但只有机制证据，没有伦理/兑现证据，张力仍需外部约束补足。

**C2 SUCCESs 内部张力：Simple（简化）vs Credible（易检验）+ 准确性。** 过度简化会削掉限定条件、损害可核验性（`"Simple refers to determining the core idea"` vs `"convincing or easily tested"`）。二手摘要没有讨论这一冲突。

**C3 实用价值的渠道反转**：`"Notably, the effect of practical utility reverses"`——同样"有用"的内容，邮件分享↑、博客分享（边际）↓。"有用就火"没有普适结论。

**C4 动机论 vs 内部状态论**：访谈把 Social Currency 列为六大驱动之一，JMR 也把自我呈现当解释（`"boost their reputation"`），但 JMR 最终结论是 `"social transmission may be less about motivation and more about the transmitter's internal states"`。两说未调和。

**C5 负面情绪的"可用"与"有害"并存**：JMR 一边建议用愤怒/焦虑（M01、C1），一边承认负面情绪伤品牌态度——同一篇论文内部的目标冲突。

**C6 记忆框架 vs 传播框架**：A4/A5 的书讲"让人记住/流传"，JMR 测"让人转发"。把"记得住"当"传得开"是下游最常见的误用（§4.3）。

**C7 "意外越多越好" vs Goldilocks**：JMR 田野里"越意外越易上榜"（线性正相关，M05）；Kidd & Hayden 的实验室证据是"信息量/不确定性适中最好"——婴儿对极高信息量的事件也会移开注意，人对太陌生与太熟悉的问题都不最好奇（M13）。两者结果变量不同（上榜 vs 注意/好奇），但都指向"剂量"：一个是单调相关，一个是中间最优。**语料无法调和**；实操只能按目标分别自测，不能把"越意外越好"当定律。

**C8 制造缺口 vs 不得虚假承诺**：Kidd & Hayden 支持"缺口→信息寻求"，但没有研究"人为制造的缺口是否被兑现、欺骗的代价"；Jepma 研究还说好奇本身可能是厌恶状态（`"curiosity is a fundamentally aversive state"`）。应用上只能写成：缺口必须真实、内容必须兑现，否则是短期点击换长期信任——**这是外部伦理约束 + 推断，不是语料实证**。"标题党"在本语料中没有被研究。

### 3.3 重复计数警告

- **SUCCESs 六项与 STEPPS 六项不可相加**：Emotional/Emotion、Stories/Stories、Practical Value 有对应；其余（Simple/Concrete/Credible vs Social Currency/Triggers/Public）**不是同一概念**。
- **JMR 只覆盖其中三项左右**（emotion≈Emotional/Emotion、surprise≈Unexpected、practical utility≈Practical Value）。故事、具体、简单、可信、社交货币、触发器、公开性**都不在 JMR 的检验里**。
- **好奇心（M13）与"意外/注意"（M05、M14）也不能相加**：前者是知识缺口驱动的信息寻求，后者是预期违背/注意捕获；Kidd & Hayden 没有测"意外标题"，JMR 没有测"知识缺口"。
- 因此"6+6+论文机制=18 条"是虚假完备。本阶段只归并出 15 条，其中机制层强证据 6 条（M01–M04、M13、M15；M13 为综述级）。

### 3.4 合成顺序（推断，不是语料结论）

分发/曝光检查 → 目标与结果变量选择（记住/转发/看完/继续看）→ 情绪选型（高唤醒）→ 信息缺口设计（先给一点、留一个明确问题；按受众先验知识校准）→ 载体（具体、故事、一句话核心）→ 可信兜底（可检验、缺口可兑现）→ 渠道适配（订阅/邮件 vs 公开信息流）→ 自测（A/B 与平台数据）。

**标注**：除"分发""情绪""实用""信息缺口方向"外，其余排序无直接证据，属本阶段的工程推断，下游不得写成作者方法。

---

## 4. 批判（Adler 步骤 3）

### 4.1 哪些是实验室结论：没有在真实信息流里验证

- 3 个实验 N=49/45/47，因变量是"你有多大可能分享"的自评（`"they would be to share it with others"`），**不是真实分享行为**；刺激是单篇故事；没有信息流、算法排序、秒级划走场景。
- "唤醒"是自评量表，不是生理测量；中介检验靠自评。
- 田野的"情绪"是文本编码推断，"唤醒"从未被测量——是按情绪类别先验假设（awe/anger/anxiety=高唤醒，sadness=低唤醒）。
- 因此："高唤醒→分享"在本语料里是**田野相关 + 实验室自评意愿因果**，不是"真实信息流中的行为因果"。
- Kidd & Hayden 的实验更靠前：trivia、模糊图片、婴儿看序列、猴子赌博任务——测的是信息寻求/学习，不是内容消费；连"看一段内容"都不是，遑论点开/完播。
- 更关键：**"让人点开"和"让人看完"从未被测量**。语料里 `attention` 合计 **31 处**，无一处谈时长：JMR 9 处（7 处曝光/编辑注意力、2 处研究关注度）；Kidd & Hayden 20 处（注意分配/婴儿注视，含参考文献标题）；CHOP 2 处是同一句 `"get and hold attention"` 的重复。没有任何留存量或注意力时长。

### 4.2 田野结论的边界

- 数据：2008 年 NYT，6956 篇，DV=进入 most e-mailed 榜（公开榜单、每 15 分钟更新），美国、英语、精英媒体、邮件文化。
- 20% 的基准率；榜单本身是公开的"社会证明"，论文没有讨论上榜对后续分享的反向影响（**批判者视角，非论文自述**）。
- 邮件多为 1 对 1/小范围；论文自己说 broadcasting 的问题数据回答不了：`"Although our data do not allow us to speak to this issue"`，并指出 `"broadcasting is self focused"`、`"audience size moderates"` 可能调节。把邮件结论迁到公开短视频是跨量级跳跃。
- 论文自己发现博客渠道上实用价值反转，却没给出机制解释（只推测"博客是评论"）。
- 无法外推到 2020s 的算法推荐、首轮流量池、完播率优化生态；语料里没有"平台/算法"概念。

### 4.3 哪些是作者的经验归纳，却常被当成定律

- **SUCCESs 六原则**：来自案例归纳（`"Using the acronym SUCCESs, the authors described why some ideas are more memorable than others"`），无对照、无测量；CHOP 是书评、HBS 是访谈。而且 CHOP 评述者自己用的是 `"I suspect the people in the audience that day remember Dr. Offit’s point"` 和 `"Dr. Offit’s demonstration was likely memorable because it met several of the criteria outlined by the authors."`——**未测记忆，是猜测**。
- **专家直觉当规律**：HBS 访谈里 Dan Heath 说 `"The instant I read that story, I knew her idea was going to stick."`——以直觉替代验证。
- **STEPPS 六驱动**：访谈只给名称（`"There are 6 key drivers of word of mouth. I’ve put them in an acronym called STEPPS"`），`"Word of mouth isn’t random or luck, there’s a science behind why things go viral."` 是承诺而非证据。
- **客户案例不可核验**：`"One person used the ideas to increase their Facebook traffic by 400%."`、`"A music artist used the ideas to make $100,000 in a day selling their mixtape"`——自报、无基线、无对照。
- **curse of knowledge**：只有类比（`"We are all the IT guy in our fields of expertise."`），无测量，却常被当成解释一切的机制。
- **Kidd & Hayden 的综述容易被当"好奇心定律"**：它自己定位为 Perspective/选择性综述，明确 `"we lack even the most basic integrative theory"`、`"we are reluctant to commit to a strict definition now."`；引用它是引用"机制共识 + 研究议程"，不是引用操作配方。
- **结论**：CHOP/HBS/访谈的所有清单只能写成"作者主张"，不能写"研究发现"；Kidd & Hayden 可以写"综述汇总显示"，但不能写"实验证明"。

### 4.4 互相矛盾之处（9 处）

1. **JMR 内部**：实用价值邮件↑ vs 博客↓（`"Notably, the effect of practical utility reverses"`）。
2. **流行说法 vs JMR**：负面新闻传得快 vs 正面内容更易传播（`"positive content is more viral than negative content"`）；同时"负面=不传"也不对（愤怒/焦虑可传）。两种简化都错。
3. **动机论 vs 内部状态论**：社交货币（访谈）vs `"social transmission may be less about motivation and more about the transmitter's internal states"`（JMR）。
4. **传播 vs 品牌**：JMR 证明愤怒/焦虑促进上榜，又承认负面情绪伤品牌态度。
5. **公共健康语境**：JMR 建议用愤怒/焦虑框架 vs CHOP 的疫苗沟通强调可信、不伤害——两套材料的价值取向冲突。
6. **记忆 vs 传播**：A4/A5 的结果变量是"记住/流传"，JMR 是"分享"。两份材料并列时最容易被误当互证，实际不可比。
7. **好奇是奖赏还是厌恶**：Kang 研究里好奇伴随奖赏/愉悦，Jepma 研究里 `"curiosity is a fundamentally aversive state"`；综述自己说两研究的"差异大于相似"（`"the differences between the two studies were larger than the similarities"`）。
8. **形状措辞不一致**：正文写 `"U-shaped function of confidence"`，但同段描述与图注是"中等信心时最好奇"（中间峰值）；照录原文，不替作者改，也不把形状标签当公式。
9. **惊喜的单调 vs Goldilocks 的中间最优**：JMR 的 surprise 与上榜是线性正相关，Kidd & Hayden 的婴儿注意在信息量适中时最稳（§3.2 C7）。两条证据方向不同、结果变量不同，不能合并成一句"越意外越好"。

### 4.5 未被证明的假设

- 情绪类别固定对应唤醒水平（田野未测唤醒）。
- 标题+摘要能代表全文情绪（JMR 编码输入即如此）。
- 自评分享意愿能预测真实分享行为。
- 2008 年 NYT 邮件行为能外推到 2020s 算法信息流与短视频。
- 综述转述的实验室实验能代表"好奇心在内容场景成立"（没有内容刺激、没有平台）。
- "知识缺口"可以被内容制作者稳定制造并兑现（语料没有这类研究）。
- 好奇心机制与转发机制可以叠加使用（语料没有交叉证据）。
- 婴儿/猴子的注意与信息寻求能外推到成人刷信息流（实验室任务是 trivia、图片、玩具、赌博，不是信息流）。
- "记住"→"传播"（*Made to Stick* 的隐含链条；JMR 未测记忆）。
- 六原则可叠加、无冲突、无交互（二手摘要隐含）。
- 传播量是内容质量/价值的代理（JMR 只测上榜，不测理解、信任、后续行为）。
- 二手摘要忠实于原书（语料没有原书，无法核对）。
- 受众同质（JMR 的 NYT 读者 ≠ 你的受众）。

### 4.6 时代局限与立场盲点

- **时代**：2008 数据 / 2012 论文 / 2007 书 / 2015 神经科学综述 / 2015 访谈 / 2024 书评；前算法推荐、前短视频、前 AI 生成内容。语料没有"完播率""流量池""推荐权重"这类概念与指标，"page views" 只在营销建议里一笔带过（`"thus increasing page views"`），且未被测量。
- **立场**：营销学教授 + 畅销书作者 + 咨询公司（访谈自述 `"I’m a Professor at the Wharton School and bestselling author of Contagious"`）；二手材料来自疫苗教育通讯与校友杂志，带推荐意图；Kidd & Hayden 是认知科学/神经科学实验室视角。研究视角都是"刺激侧如何引发反应"，不讨论接收方、平台、伦理与信息质量。
- **样本**：JMR 是美国精英媒体、英文、邮件；Kidd & Hayden 是婴儿、猴子、大学生做 trivia/图片/玩具任务；两者对中文平台与内容消费者都零证据。
- **盲点**：把"传播"默认当好事（不管传播什么）；忽略负面情绪的外部性（JMR 只提品牌态度，未提公共伤害）；忽略好奇心的代价（分心、被操纵）。

### 4.7 特别核查：「注意力只有 8 秒」

- **检索**：5 份 `.txt` 全文，`8 second` / `eight second` / `attention span` / `short attention` / `秒` **全部 0 命中**。
- **语料里 `attention` 合计 31 处**：JMR 9 处（7 处曝光/编辑注意力，如 `"external drivers of attention (e.g., how prominently content was featured)"`；2 处研究关注度）；Kidd & Hayden 20 处（注意分配/婴儿注视，含参考文献标题）；CHOP 2 处是同一句 `"get and hold attention"` 的重复。**没有任何一处谈注意力时长或留存量。**
- Kidd & Hayden 文中 `seconds`/`minute` 的全部命中都是实验计时（`"2.25 seconds"` 奖赏延迟、`"60 seconds"` 自由玩耍、`"about 15 minutes"` 探索），不是注意力时长。
- **结论**：**「注意力只有 8 秒」在本语料中没有出处、没有证据，属未经证实的流行传言，不得作为任何 skill 的前提，也不得写进给用户的文案建议。**
- 同时不要把"证伪"当结论：语料也没有说"注意力不是 8 秒"；正确表述是"**本语料对注意力时长没有任何主张**"。
- 与 `PIPELINE_STATE.md` 的硬约束一致（"不写「注意力只有 8 秒」这类已被证伪的流行说法"）。

### 4.8 最强反对意见

> 这五份材料里只有一篇有原始传播数据（JMR，因变量是"是否进入 2008 年《纽约时报》最常被邮件列表"）；三个实验测的是约 50 人读完一个故事后自评的转发意愿；好奇心那份是同行评议**综述**，汇总的是 trivia、模糊图片、婴儿看序列、猴子赌博等实验室任务，没有一条内容/视频/平台数据；其余是书评、校友访谈与作者访谈，没有测量。用它蒸馏"注意力钩子方法论"，等于**用转发研究冒充注意力研究、用实验室信息寻求冒充信息流好奇、用作者经验冒充机制证据、用美国 2008 年邮件行为冒充中文算法信息流**。任何承诺提高点开率/完播率的 skill，都超出这批材料能支持的范围；好奇心机制最多支持"缺口设计的方向性假设 + 必须自测"，不能直接写成"钩子公式"。

### 4.9 批判如何进入下游 Boundary

每条能力卡必须带：证据等级与结果变量（分享/信息寻求/记忆/观看）；适用来源（JMR 原论文 / Kidd & Hayden 综述 / CHOP-HBS 二手 / 访谈）；不适用场景（非邮件渠道、短视频、中文平台、高风险话题）；伦理红线（不虚假承诺、不制造恐慌、公共健康慎用愤怒/焦虑、缺口必须兑现）；必须补的数据（§5.4）；"8 秒"禁用声明。

---

## 5. 应用边界（Adler 步骤 4）

### 5.1 总原则

1. **先分清结果**：点开 / 看完 / 转发 / 记住 / 继续看（信息寻求）。本语料对"转发"有原论文级证据、对"信息寻求/继续学"有综述级机制证据，对"记住"只有二手主张，对"点开/看完/转化"没有一手证据。
2. **把每条机制写成"候选改动 + 自测指标"**，而不是"定律"。
3. **分发优先**：改文案之前先确认曝光与渠道（M15）。
4. **伦理约束优先于传播效率**（C1）。
5. **缺口必须兑现**：信息缺口只能用"真实内容"兑现；这是 C8 的硬约束，不是文案技巧。
6. **两条链分开用**：好奇心只用于"继续看/信息寻求"侧的目标，不拿它论证转发；高唤醒只用于"分享"侧（P5）。

### 5.2 可直接落地（不依赖平台数据；但明确结果变量）

| 动作 | 依据机制 | 强度 | 结果变量 | 注意 |
|---|---|---|---|---|
| 情绪选型：用敬畏/幽默/愤慨/紧迫等高唤醒写法；不用悲伤作主调 | M01、M02 | 强 | 分享 | 伦理红线；公共健康慎用 |
| 正面框架优先 | M03 | 强 | 分享 | 非绝对；负面高唤醒可破例 |
| 实用信息可执行化（清单/步骤/资源） | M04 | 强（渠道敏感） | 邮件/订阅分享 | 公开信息流需自测 |
| 发布前检查曝光/位置/渠道 | M15 | 强 | 分享 | 不等于算法推荐 |
| 把"记住"/"转发"/"继续看"分目标、分指标 | A4/A5 vs JMR vs Kidd & Hayden | 强（元规则） | 全部 | 防概念混用 |

### 5.3 可直接落地但必须自测（弱/中证据）

具体化改写（M08，弱）、一句话核心信息（M07，弱）、意外钩子（M05，中）、**信息缺口钩子（M13，综述级机制/应用需自测；含 Goldilocks 校准）**、故事骨架（M10，弱）、可检验凭据（M09，弱但伦理必需）、兴趣点设计（M06，中但定义模糊）、社交货币角度（M11，弱）。

**用法**：只作为"候选改写"，必须做小规模 A/B 或前后对比；不能写进"保证有效"的 skill。

### 5.4 必须先补平台数据（否则不可用）

| 数据 | 为什么必须 | 语料现状 |
|---|---|---|
| 曝光量 / 推荐来源占比 | 区分"没曝光"与"没点开" | 无 |
| CTR / 封面点击率（按位置、人群） | JMR 的 DV 不含点击 | 无 |
| 前 3 秒/5 秒留存、划走率 | 视频独有；语料无时长数据 | 无 |
| 平均观看时长、完播率、复看率 | 同上 | 无 |
| 转发率，并区分私聊/公开/截图 | JMR 只有邮件 vs 博客两种 | 无 |
| 收藏/点赞/评论（与转发分开） | 行为异质、动机不同 | 无 |
| 受众构成与基线 | NYT 读者 ≠ 你的受众 | 无 |
| 品类/主题基线 | JMR 控制 20 个主题但未给系数 | 无 |
| 品牌/信任/负面反馈指标 | JMR 承认负面情绪伤品牌态度，但自己没测 | 无 |
| 长期疲劳/重复暴露 | 无 | 无 |
| 算法规则/流量池 | 语料完全没有平台/算法概念 | 无 |
| narrowcasting vs broadcasting 的实际比例 | JMR 自己说数据回答不了 | 无 |
| 受众先验知识水平 | Goldilocks 校准必需：缺口"适中"相对受众已有知识定义 | 无；Kidd & Hayden 只有实验室任务 |
| 缺口钩子的打开/继续观看效果 | 好奇机制没有内容场景数据，必须 A/B | 无 |
| "缺口是否兑现"的完成/复访指标 | C8 需要证明兑现没有伤害信任 | 无 |

### 5.5 不能落地 / 不要用

- "注意力只有 8 秒"（§4.7）
- 把 JMR 的 +34%/+30% 当 CTR/播放量预期（那是 2008 年上榜几率的变化）
- 把"上榜率"当"爆款率/推荐率"
- 把 Goldilocks 当参数公式（悬念几秒、给几个信息点——语料没有这种配方）
- 在标题里制造无法兑现的缺口（标题党——语料未研究，按 C8 禁用）
- 把 CHOP/HBS 的案例（Subway、cantaloupe、Halloween candy）当模板
- 在公共健康/高风险话题上优先用愤怒/焦虑（C1、C5）
- 把"故事/具体/简单/可信"当已验证的六原则一次性套用（弱证据 + 重复计数）

### 5.6 文章 vs 视频的映射

| 部位 | 可用机制 | 证据等级 | 必须先有的数据 |
|---|---|---|---|
| 文章标题 / 封面 | M05、M01、M03 | 中/强（结果=分享） | CTR、曝光 |
| 视频封面 / 标题 | M05、M01 | 中/强 | CTR、首帧点击 |
| 文章开头 / 视频前 3 秒 | M01、M06、M14、M13 | 强/中/弱/强（综述级） | 3 秒留存、受众先验知识 |
| 正文 / 视频中段 | M04、M08、M10、M09、M13 | 强/弱/弱/弱/强（综述级，应用于"继续看"） | 平均观看、完播、缺口兑现度 |
| 结尾 / CTA | M04、M11 | 强/弱 | 转发率、转化 |
| 分享卡 / 转发文案 | M11、M01 | 弱/强 | 私聊/公开转发比 |
| 发布策略 | M15 | 强 | 推荐占比、流量池 |

### 5.7 可 skill 化 / 不适合 / 预估数量 / 优先级

**可 skill 化（9 个候选）**：

1. 情绪唤醒改写（M01–M03）
2. 实用价值包装（M04）
3. 分发位置与渠道检查（M15）
4. **信息缺口/好奇心钩子（M13，含 Goldilocks 校准与"兑现"检查）**
5. 具体化改写（M08）
6. 一句话核心信息（M07）
7. 可信凭据与防虚假承诺（M09）
8. 故事骨架（M10）
9. 意外钩子（M05）

（M06 兴趣并入 1/9；M11 社交货币作诊断子项；M12 暂缓；M14 并入 9 且需平台数据。）

**预估 skill 数量：7–10 个能力单元**（阶段 1.5 定去留，不硬凑）。

**不适合 skill 化**：具体案例（Subway、cantaloupe、United Airlines）、实验刺激材料（trivia 题、模糊图片、婴儿序列、猴子赌博任务）、作者个人经历、书评推荐语、客户自报案例、访谈寒暄——只作 example 引用。

**优先级（从"最能赋能普通人"角度）**：

1. 情绪唤醒选型（强证据、立刻可用）
2. 信息缺口/好奇心钩子（综述级机制、方向明确但需自测）
3. 具体化改写（弱证据但低风险、最贴近"修饰"）
4. 实用价值包装（强证据、渠道敏感）
5. 分发/渠道检查（强证据、成本最低、最常被忽略）
6. 可信凭据（伦理底线；也是缺口兑现的守门）
7. 故事骨架（用户要求覆盖，但弱证据）
8. 意外钩子（需 A/B；注意 C7 剂量冲突）
9. 社交货币诊断（弱）

---

## 6. 关键任务清单（覆盖率审计基准）

> 每题颗粒度到"能对应某个机制"；"尚缺条件"一栏是阶段 1.5 独立核查时必须承认的缺口，不用常识补成作者的方法。

| task_id | 读者会带着来问的问题 | 对应机制 | 语料位置 | 预期交付物 | 重要性依据 | 尚缺条件 |
|---|---|---|---|---|---|---|
| T01 | 我的内容没人点开，是标题不够刺激吗？ | M14、M15 | JMR §Discussion（曝光与内容同量级） | 把问题拆成曝光/点开/看完/转发四层，给出检查顺序 | 不分层会把分发问题误当文案问题 | 平台曝光量与 CTR |
| T02 | 什么情绪最能让人转发？ | M01–M03 | JMR Abs.、§Study 1、Table 4 | 情绪选型表 + 低唤醒排除清单 | 强证据，直接影响文案 | 无（仅转发） |
| T03 | 负面情绪到底能不能用？ | M01、M03 + C1 | JMR §Study 1、§Discussion（品牌态度 / 公共健康两处） | 可用条件、剂量与红线清单 | 传播 vs 品牌/伦理冲突 | 品牌信任数据 |
| T04 | 专业内容怎么改才有人转？ | M04、M07、M08 | JMR Table 4（practical utility）；CHOP 术语表 Simple/Concrete | 抽象内容 → 可执行清单的改写样例 | 强证据（实用）+ 弱（具体） | 读者基线 |
| T05 | 怎样让人一眼看懂？ | M07、M08 | CHOP 术语表 Simple/Concrete；HBS 访谈（具体性） | 核心句 + 具体化改写对照 | 弱证据但低风险 | 需自测 |
| T06 | 怎样制造意外又不标题党？ | M05 | JMR §Study 1；CHOP 术语表 Unexpected | 意外点与正文一致性检查表 | 中证据，最易滥用 | CTR 数据 |
| T07 | 没有数据怎么让人信？ | M09 | CHOP 术语表 Credible | 可检验凭据清单（数字/来源/演示/反例） | 伦理底线，防虚假承诺 | 无 |
| T08 | 故事该怎么写才有用？ | M10 | CHOP 术语表 Stories；HBS 访谈（Jared 一例） | 人物—冲突—结果骨架 + 反例 | 用户明确要求覆盖 | 故事效果的平台数据 |
| T09 | 人转发到底图什么：社交货币还是情绪？ | M11 vs M01、C4 | JMR §Discussion（自我呈现 → 内部状态）；访谈 STEPPS 列表 | 双假设诊断（社交货币/内部唤醒），不二选一 | 两说未调和 | 转发动机调研 |
| T10 | 同样内容发邮件/朋友圈/视频号，该选哪个渠道？ | M04、M15 | JMR §Discussion（实用价值反转） | 渠道匹配表 | 同一论文发现的方向反转 | 各渠道基线 |
| T11 | 平台推荐和内容质量哪个更重要？ | M15 | JMR §Discussion（曝光位置与内容特征同量级） | "先查分发、再改文案"决策单 | 同量级，强证据 | 推荐占比 |
| T12 | 为什么"有用"的内容在博客不火？ | M04 | JMR §Discussion（实用价值反转） | 渠道假设检验清单 | 论文自己发现的反转 | 博客/信息流数据 |
| T13 | 怎么判断我的内容有没有情绪？ | M01、M02 | JMR §Study 1 编码方法（LIWC/人工编码） | 人工编码流程 + 平台行为代理 | 语料有可借鉴的编码方法（仅方法） | 生理/行为测量 |
| T14 | 能不能预测爆款？ | A1–A3 + §4.8 | JMR §Study 1 | 用概率语言说明，给损失函数 | 语料只支持"上榜可能性" | 大规模样本 |
| T15 | 这套方法能用在短视频吗？ | M14 + §4.2 | JMR §Discussion（narrowcasting/broadcasting、受众规模） | 迁移清单：哪些必须重测 | 邮件→算法短视频跨量级 | 完播/留存/推荐数据 |
| T16 | 简化会不会伤可信？ | C2 | CHOP C2 vs C5 | 简化—准确权衡清单 | SUCCESs 内部张力 | 受众理解测试 |
| T17 | 怎么用"信息缺口/好奇心"？ | M13 | Kidd & Hayden（信息缺口理论、Goldilocks、Kang 等实验） | "先给一点、留一个明确问题"的缺口设计 + 按受众先验知识校准 + 兑现清单 | 综述级机制；最易滑向标题党 | 受众先验知识、打开/继续观看数据 |
| T18 | 注意力是不是只有 8 秒？ | §4.7 | 无（全文 0 命中） | 禁用声明 + 替代表述 | 流行传言，无证据 | 无 |
| T19 | 疫苗/公共健康内容能用愤怒、焦虑吗？ | C1、C5 | JMR §Discussion（品牌态度 / 公共健康）；CHOP 术语表 | 高风险场景红线清单 | 伦理冲突 | 公共健康传播证据 |
| T20 | 怎么衡量修饰后的效果？ | §5.4 | JMR §Study 1（榜单定义）；Kidd & Hayden（信息寻求指标） | 指标层级（曝光→CTR→留存→完播→转发→信任）+ 基线 | 语料只测分享与信息寻求 | 全套平台数据 |
| T21 | 意外/惊喜是不是越多越好？ | M05 vs M13（C7） | JMR §Study 1（surprise 正相关）；Kidd & Hayden（婴儿注意 U 型） | 剂量校准表（按目标/受众分开定） | 两条证据方向冲突 | 平台 A/B、受众基线 |
| T22 | 好奇心内容怎么防止变成标题党？ | M13、C8 | Kidd & Hayden（缺口→信息寻求）；CHOP 术语表 Credible | 缺口—兑现检查表（缺口是否真实、是否在内容内回答） | 伦理/信任底线；语料无兑现研究 | 兑现度与复访数据 |

---

## ✅ 阶段 0 质量门检查

- [x] 主旨能用一句话说清（§1.2）
- [x] 骨架列出 3–7 个一级论点（7 个：A1–A7）
- [x] 关键术语按原文实际含义列出，不凑数（§2.1，21 条）
- [x] 已检查局限、前提与未证明假设；无证据处标"无/待补"，未编造三条批判
- [x] 已列出关键任务清单（22 条），含来源、交付物、重要性依据、尚缺条件
- [x] 已做「注意力只有 8 秒」专项核查（§4.7）
- [x] 已区分综述/原论文/二手摘要/访谈，未把二手摘要写成原书原文
- [ ] 已向用户展示并得到确认（**待 lead 转交用户确认**）

### 待用户确认的 3 个决策

1. **Kidd & Hayden 的强度记法**：接受"强（综述级，机制层）／弱（应用层）"这种双层标注吗？还是统一降为"中"？
2. **好奇心 skill 的定位**：作为独立候选（本版已列入 §5.7 第 4 位），还是并入"意外钩子"（M05）？两条证据链其实不同（信息寻求 vs 转发/意外）。
3. **结果变量范围**：是否接受"转发链与信息寻求链分开蒸馏；点开率/完播类能力卡等平台数据后再做"这一边界？

**用户确认时间**：待确认

---

## §7 补充批次（第二批素材，2026-11-23）

第一批语料的上游指标是「邮件转发 / 榜单」，没有一条验证过「视频看多少」。为补这个洞，新增两篇开放获取论文（片段文本见 `source/`，PDF 未入库，见 `source/PROVENANCE.md`）：

| 来源 | 类型 | 结果变量 | 强度 |
|---|---|---|---|
| Li et al., ECCV 2024（arXiv:2410.00289） | 9 万条 Snapchat 短视频的预测建模 | NAWP（归一化平均观看比例）、ECR（观看 >5s 的概率） | **中**（单平台、相关性、非因果） |
| Zhang et al., arXiv:2602.22299 | 广告投放数据 + 多模态 LLM 特征分析 | 每次转化成本（CPI） | **中**（广告语境、特征重要性、非因果） |

### 新增机制

- **M16 前 5 秒留存与整体观看比例同向。** ECR 定义为 P(watch >5s)，实测与 NAWP 相关系数 0.926（单平台）。含义：开头几秒不是「氛围」，是可以单独度量的杠杆。
- **M17 留存必须按时长归一化，时长本身是变量。** 长视频天然更难看完全，用绝对观看时长或点赞数比较不同时长的视频会得出错误结论；时长由创作者决定、又被平台排序，应先定型。
- **M18 前 3 秒是广告语境下的独立窗口。** hook 期的主题与声学特征与 CPI 相关；但同一套 hook 手法在电商/医疗/快消的效果排序不同——**没有跨行业通吃的模板**。

### 反例（值得单列）

- **制作质量不等于互动。** 视频质量评估的 MOS 分数与互动量相关性很弱（同一论文的对照发现）。把预算全压在画质上，可能是在解一个不存在的问题。

### 与第一批的关系

- 第一批的「信息缺口 / 唤醒度」回答**要点什么**；第二批回答**前几秒的留存怎么度量**。两条链在「开头」汇合，但证据来源不同，不可互相引用。
- 原决策 3 曾把「点开率/完播类能力卡」推迟到有平台数据之后。本批解除了其中**可做的一半**（留存度量口径、前 5 秒结构）；另一半（本账号 CTR、完播基线）仍需自有后台数据。

### 新增关键任务

| ID | 用户任务 | 机制 | 来源 | 交付物 | 尚缺 |
|---|---|---|---|---|---|
| T23 | 短视频前 5 秒该怎么改？ | M16 | 2410.00289 | 前 5 秒检查表 + 两指标判定 | 本账号 5 秒留存基线 |
| T24 | 这一版视频该多长？ | M17 | 2410.00289 | 时长决策清单（品类对标） | 各品类最优时长阈值 |
| T25 | 广告里的 hook 手法能搬到内容号吗？ | M18 | 2602.22299 | 迁移检查表（先同品类小样本验证） | 内容号 A/B 数据 |

### 证据边界（必须写进卡片）

1. 两篇的结果变量都不是「内容账号的完播率」：一篇是观看比例，一篇是广告转化成本。
2. 都是单一平台的观察/建模研究，**不能推出「改了就会涨」**。
3. ECR 的「5 秒」是平台指标定义，不是创作规律；换平台要重测。

---

## §8 第三批素材（叙事/故事，2026-11-23）

第一批里故事（f18「人物+劣势+克服」）只有二手转述，被判为单案例最小归纳。本批用一篇开放获取元分析替换它：

| 来源 | 类型 | 样本 | 结果变量 | 强度 |
|---|---|---|---|---|
| Mar et al., 2021, *Psychonomic Bulletin & Review*（CC BY, PMC8219577） | 元分析 | 75+ 独立样本、33,000+ 被试、150 个效应量 | 理解与回忆 | **中**（元分析，但作者自报发表偏倚） |

### 新增/替换的机制

- **M19 故事提升「接得住」，不提升「被说服」。** 故事比说明文更好懂、更好记，平均效应 >0.5 SD 且对单一研究不敏感；但结果变量是理解与回忆，不是态度改变、转发或完播。
- **M20 效应量应视为上限。** 该元分析自己检出发表偏倚：低精度研究报告的效应更大。引用 0.5 SD 时必须同时说明这一点。
- **M21 反对全盘故事化。** 作者明确说该结果不应被理解为「把所有信息强行写成故事」，尤其当信息本来不以叙事呈现时。

### 与第一批的关系

- 替换 f18 的证据基础：从二手转述升级为元分析，同时**收窄**它的适用范围（原 f18 隐含「故事有用于传播」，本批明确无此证据）。
- 与「具身细节/具体化」（f16）分工：具体化是句子层，叙事是体裁层。

### 新增关键任务

| ID | 用户任务 | 机制 | 来源 | 交付物 | 尚缺 |
|---|---|---|---|---|---|
| T26 | 这段内容该不该写成故事？ | M19、M21 | Mar 2021 | `story` 卡的体裁决策流程 | 中文内容/短视频语境的叙事研究 |
| T27 | 故事能提升转发吗？ | 无证据 | — | 明确回答「无依据」 | 叙事 vs 非叙事的传播实验 |

### 证据边界

1. 结果变量是理解与回忆，多为即时纸面测试；**无转发、完播、说服的证据**。
2. 发表偏倚已被检出，效应量应按上限理解。
3. 未纳入「叙事 vs 非叙事」正面对比的开放获取元分析（Rahmani 2025 页面反爬，无法核对全文）；因此**不得**宣称「故事更有说服力」。
4. 纳入研究多来自教育/健康传播，不能直接外推到 AI 工具类内容。
