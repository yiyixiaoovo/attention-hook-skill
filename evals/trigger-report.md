# 触发评测判分 — attention-hook

- runs: 41（TP 14 / FP 7 / FN 0 / TN 20）
- precision 0.667 / recall 1.000 / **F1 0.800**
- 兄弟混淆率: 0.000（0/6）

| case | expected | selected | 判定 |
|---|---|---|---|
| arousal-choice-e-01#r1 | edge_case | attention-hook | FP |
| arousal-choice-n-01#r1 | should_not_trigger | none | TN |
| arousal-choice-n-02#r1 | should_not_trigger | none | TN |
| arousal-choice-t-01#r1 | should_trigger | attention-hook | TP |
| arousal-choice-t-02#r1 | should_trigger | attention-hook | TP |
| concretize-e-01#r1 | edge_case | attention-hook | FP |
| concretize-n-01#r1 | should_not_trigger | none | TN |
| concretize-n-02#r1 | should_not_trigger | none | TN |
| concretize-t-01#r1 | should_trigger | attention-hook | TP |
| concretize-t-02#r1 | should_trigger | attention-hook | TP |
| distribution-first-e-01#r1 | edge_case | attention-hook | FP |
| distribution-first-n-01#r1 | should_not_trigger | none | TN |
| distribution-first-n-02#r1 | should_not_trigger | none | TN |
| distribution-first-t-01#r1 | should_trigger | attention-hook | TP |
| distribution-first-t-02#r1 | should_trigger | attention-hook | TP |
| gap-design-e-01#r1 | edge_case | attention-hook | FP |
| gap-design-n-01#r1 | should_not_trigger | none | TN |
| gap-design-n-02#r1 | should_not_trigger | none | TN |
| gap-design-t-01#r1 | should_trigger | attention-hook | TP |
| gap-design-t-02#r1 | should_trigger | attention-hook | TP |
| promise-integrity-e-01#r1 | edge_case | attention-hook | FP |
| promise-integrity-n-01#r1 | should_not_trigger | none | TN |
| promise-integrity-n-02#r1 | should_not_trigger | none | TN |
| promise-integrity-t-01#r1 | should_trigger | attention-hook | TP |
| promise-integrity-t-02#r1 | should_trigger | attention-hook | TP |
| sibling-01#r1 | sibling | humanize-cn | OK |
| sibling-02#r1 | sibling | humanize-cn | OK |
| sibling-03#r1 | sibling | ppt-master | OK |
| sibling-04#r1 | sibling | unslop | OK |
| sibling-05#r1 | sibling | reverse-any-video | 未中兄弟(reverse-any-video) |
| sibling-06#r1 | sibling | office-docx | OK |
| stickiness-pass-e-01#r1 | edge_case | attention-hook | FP |
| stickiness-pass-n-01#r1 | should_not_trigger | none | TN |
| stickiness-pass-n-02#r1 | should_not_trigger | none | TN |
| stickiness-pass-t-01#r1 | should_trigger | attention-hook | TP |
| stickiness-pass-t-02#r1 | should_trigger | attention-hook | TP |
| surprise-contrast-e-01#r1 | edge_case | attention-hook | FP |
| surprise-contrast-n-01#r1 | should_not_trigger | none | TN |
| surprise-contrast-n-02#r1 | should_not_trigger | none | TN |
| surprise-contrast-t-01#r1 | should_trigger | attention-hook | TP |
| surprise-contrast-t-02#r1 | should_trigger | attention-hook | TP |

> 本报告只给原始配对计数与比率；统计非劣需预注册界值 + McNemar/配对 Bootstrap（§10.3），不在此自动宣布。
