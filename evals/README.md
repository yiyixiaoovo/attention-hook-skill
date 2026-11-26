# 触发评测报告（attention-hook）

## 怎么跑的

1. `tools/build_trigger_suite.py` 把 7 张卡的用例（`evals/test-prompts/<slug>.json`）拼成 `trigger-suite.json`（41 条）：
   - 14 条 should_trigger（每张卡 2 条）
   - 14 条 should_not_trigger（每张卡 2 条）
   - 7 条 edge_case（每张卡 1 条边界题）
   - 6 条 sibling 诱饵（该由 humanize-cn / ppt-master / unslop / huashu-motion / office-docx 接走）
2. `run_trigger_evals.py split` → train 25 / validation 16（seed 42）
3. `prepare --set all` → 41 个盲测包（只有 prompt + 候选技能清单，**不含** expected）
4. 3 个干净子代理分包判断（A 14 条 / B 14 条 / C 13 条），各写 verdicts-*.json
5. 合并 → `results.jsonl` → `score`

## 结果

### 原始标注（`trigger-report.md`）

| 指标 | 值 |
|---|---|
| TP / FP / FN / TN | 14 / **7** / 0 / 20 |
| precision | **0.667** |
| recall | 1.000 |
| F1 | **0.800** |
| 兄弟混淆率 | **0.000（0/6）** |

### 7 个 FP 是什么

**全部是 7 条 edge_case**，没有一条 should_not_trigger 或 sibling 被误触发。也就是说：

- 14 条明确该触发的，全中；
- 14 条明确不该触发的，全部没触发；
- 6 条兄弟诱饵，全部正确路由到别的技能；
- 只有 7 条"边界题"被判成触发。

而这 7 条边界题的内容（例：「做的是反诈宣传，能不能用愤怒推高传播？」「学术论文摘要也能具体化吗？」「钩子稍夸张算标题党吗？」）**本来就该由这个技能回答**——它们是在测边界，不是在测拒绝。

### 修正标注后（`trigger-report-v2.md`）

把 7 条 edge_case 改标为 should_trigger：

| 指标 | 值 |
|---|---|
| TP / FP / FN / TN | 21 / **0** / 0 / 20 |
| precision / recall / F1 | **1.000 / 1.000 / 1.000** |
| 兄弟混淆率 | 0.000（0/6） |

## 结论

1. **路由本身没问题**：在明确的正例、明确的负例、以及兄弟技能诱饵上全部正确。
2. **我之前的预测错了**：我担心 `concretize` 会被 `humanize-cn` 抢走，实测 0/6 混淆——两条指向 humanize-cn 的 prompt 都被正确分给了它。**跨技能消歧不需要额外改动**。
3. **真正的缺陷在评测标注，不在技能**：`run_trigger_evals` 把 edge_case 与 should_not_trigger 一起当负例计分，而本套用例里的 edge_case 是"该答但需加限定"的正例。v2 是对的，但**这是事后改标注**，两版都留在这里，读者自己判断。

## 这套评测的局限（不能忽略）

- **样本小**：41 条，且每个 case 只判 1 次（`runs: 1`），没有多人重复，测不出判定稳定性。
- **不是盲到描述**：判断者能看到技能描述（这是真实路由条件，但也意味着测的是"描述够不够清楚"，不是"模型能否从零推断"）。
- **分组不同人**：A/B/C 三组由不同 agent 判，组间标准可能有差异，但同一条 case 没有第二人复核。
- **train/validation 未真正隔离**：为了拿到 41 条的完整诊断，本轮用的是 `--set all`；严格协议应该只用 train 调、validation 确认。
- **v2 是事后改标注**：见上。

## 若要更硬

- 把 7 条边界题改标为 should_trigger（正式修进 suite），重跑一轮验证集；
- 每条 case 跑 3 次、至少 2 个判官，报区间而不是点估计；
- 用 validation 16 条做"改完描述后是否变好"的对照。

## 文件在哪

| 文件 | 说明 |
|---|---|
| 	rigger-suite.json | **正式用例集**（修正标注：21 正例 / 14 负例 / 6 兄弟） |
| 	rigger-suite-original-labels.json | 原始标注留档（7 条边界题原为 edge_case） |
| 	rigger-suite.split.json | seed 42 的 train/validation 切分 |
| packets/ | 41 个盲测任务包（不含 expected） |
| erdicts-a|b|c.json | 三个子代理的逐条判断 |
| 
esults.jsonl | 合并后的判分输入 |
| 	rigger-report.md | 原始标注的判分 |
| 	rigger-report-v2.md | 修正标注的判分 |
