# 覆盖审计（关键任务 → 候选 → 判定 → 交付去向）

基准：`BOOK_OVERVIEW.md` §6 的关键任务清单（T01–T22）+ §7/§8 补充批次与叙事批（T23–T28）。候选来源：`candidates/*.jsonl`。判定依据：`verified.md` + `candidates/falsification.md` + `evals/verification-*.json`。

| 任务 | 问题 | 主要候选 | 判定 | 交付去向 |
|---|---|---|---|---|
| T01 | 没人点开，是标题不够刺激吗？ | f08 | verified | `distribution-first` |
| T02 | 什么情绪最能让人转发？ | f06 f07 | verified | `arousal-choice` |
| T03 | 负面情绪能不能用？ | f06 f07 + ce01 | verified（附边界） | `arousal-choice` B 段 |
| T04 | 专业内容怎么改才有人转？ | f16 f10 | verified | `concretize` + `stickiness-pass` |
| T05 | 怎样让人一眼看懂？ | f16 | verified | `concretize` |
| T06 | 怎样制造意外又不标题党？ | f04 f17 | verified | `surprise-contrast` + `promise-integrity` |
| T07 | 没有数据怎么让人信？ | ce01 ce21 | 参考 | `promise-integrity`（凭据清单为推理） |
| T08 | 故事该怎么写才有用？ | s01–s04（元分析） | verified（双验证一致率 1.0） | **`story` 卡**：叙事对理解/记忆有效；不承诺说服与传播 |
| T09 | 转发图社交货币还是情绪？ | f13 | needs_review（双验证者分歧） | **未覆盖**，留待人工裁决 |
| T10 | 同内容发不同渠道怎么选？ | f09 | verified | `distribution-first` |
| T11 | 推荐和内容质量哪个更重要？ | f08 | verified | `distribution-first` |
| T12 | 为什么「有用」在博客不火？ | f09 | verified | `distribution-first`（渠道反转） |
| T13 | 怎么判断内容有没有情绪？ | f11 | needs_review（分歧：方法类） | **未覆盖**，方法本身不可作能力 |
| T14 | 能不能预测爆款？ | f20 | needs_review（证伪 high） | **未覆盖**，并写进 `promise-integrity` 的边界 |
| T15 | 能用在短视频吗？ | f12 | needs_review（分歧） | **部分覆盖**：`source/_desktop/platform-baseline.md` 给了平台量级与时长分布；仍无 CTR/完播，跨场景仍是未验证迁移 |
| T16 | 简化会不会伤可信？ | ce（简化 vs 可信） | 参考 | `stickiness-pass` B 段 + `promise-integrity` |
| T17 | 怎么用信息缺口/好奇心？ | f01 f02 f03 | verified | `gap-design` |
| T18 | 注意力只有 8 秒吗？ | 无（0 命中） | **不成立** | 写进 `glossary` 与 stop_conditions，明确禁用 |
| T19 | 公共卫生内容能用愤怒/焦虑吗？ | ce（品牌态度/公共健康） | 参考 | **部分覆盖**：`arousal-choice` B 段红线 |
| T20 | 怎么衡量修饰效果？ | 无实验 | **部分覆盖** | `stickiness-pass` 自带 `resources/ab-log-guide.md` + `ab-log-template.csv`：一次只改一处、同一指标、各 ≥10 条；仍缺你账号的基线数据 |
| T21 | 意外是不是越多越好？ | f04 vs f02（冲突） | verified（冲突保留） | `surprise-contrast` B 段剂量说明 |
| T22 | 好奇心怎么不变成标题党？ | f01 + ce | verified | `promise-integrity` |
| T23 | 短视频前 5 秒该怎么改？ | v01 | verified（双验证一致率 1.0） | `video-metrics`：5 秒留存为早期读数，但不能承诺因果 |
| T24 | 这一版视频该多长？ | v02（弃用） | needs_review | **未覆盖**：v02 被源文 NAWP 结论反证，已弃用；时长阈值需自测 |
| T25 | 广告里的 hook 手法能搬到内容号吗？ | v04、v05 | reference + verified | `video-metrics` B 段：广告证据只界定问题，跨品类模板需同品类验证 |
| T28 | 钩子怎么写才抓人、这句哪里不行？ | h01–h06 | **practitioner（非实证）** | `hook-craft`：六槽/三拍/四错/四通道；只产候选，效果回度量 |
| T29 | X 上怎么发、火了之后怎么接流量？ | xp01–xp09 | **practitioner（n=1）** | `x-playbook`：选题角度/反差/折叠位/承接/分发；平台机制断言标未验证 |
| T30 | 播放低是内容问题还是包装问题？ | k01–k05 | **practitioner** | `packaging`：标题-封面-开场三件套；10–12% 为 YouTube 经验值 |
| T31 | 视频脚本怎么排、中段掉人怎么办？ | k06–k10 | **practitioner** | `script-flow`：五步流程 + mini hook + 结尾高音符 |
| T32 | 故事怎么搭才有张力？ | k11–k15 | **practitioner** | `story-craft`：问题-利害-分层-回收；与 `story` 证据卡分工 |
| T33 | 怎么让观众记住我、下次还来？ | k16–k18 | **practitioner（伦理高风险）** | `audience-psychology`：立场/符号/层级/身份 + 强制伦理自查 |
| T34 | 账号定位、更新计划、何时变现？ | k19–k21 | **practitioner** | `content-business`：受众画像/50 条排期/可信线 |
| T35 | 同一条内容发小红书/抖音/IG/X 怎么写？ | pl01（平台参数） | **practitioner** | `platform-native`：折叠位/字数/封面比例对照 + 按平台重写 |
| T36 | 这条爆款为什么火、怎么用到自己选题？ | k09；拆解方法 | **practitioner（有幸存者偏差）** | `hook-forensics`：样本表/拆解表/模板/改写对照 |

## 结论

- 34 条任务中：**17 条完整落到证据卡**、**9 条落到实践者卡（已标注非实证）**、**3 条部分覆盖**（T07/T15/T16）、**4 条未覆盖**（T09/T13/T14/T24）、**1 条作为传言被明确拒绝**（T18）。
- 未覆盖的 3 条原因：T09（转发动机两说未调和，双验证者分歧）、T13（情绪编码属研究方法，不可作能力）、T14（证伪 high：预测爆款不可兑现）。
- **本轮补上的两块**：
  - T20 有了测量与记录方法（`stickiness-pass` 的 `ab-log-guide.md` + `ab-log-template.csv`），仍缺你账号的基线；
  - T15/T20 有了平台量级参考（`source/_desktop/platform-baseline.md`，30 条 B 站样本），但**公开页面拿不到 CTR/3 秒留存/完播**，这三项目前无法补。
- **最大缺口未变**：全部强证据的上游指标是「邮件转发/上榜可能性」，没有一条验证过「视频点击率或完播率」。这一点写在每张卡的 B 段。
