# 复盘知识库 — attention-hook

> 由 `scripts/kb_index.py` 从 `records/` 自动生成，**不要手工编辑**。

- 记录数：**1**
- 结论分布：支持 0、反驳 0、不充分 1、无效 0

## 记录

| 记录 | 日期 | 卡片 | 指标 | 状态 | 结论 | 证据 |
|---|---|---|---|---|---|---|
| [2026-11-hook-ab-types](records/2026-11-hook-ab-types.md) | 2026-11-23 | gap-design、concretize | preference_rating | 已完成 | 不充分 | own-experiment |

## 怎么用

1. 新验证先复制 `TEMPLATE.md` 到 `records/`，**跑之前**写死假设与判定阈值；
2. 跑完填结果，结论按四级判定，不充分就写 `inconclusive`；
3. 局限必须写；真实后台数据缺失时注明「非真实受众/非真实 CTR」；
4. 重新生成索引：`python3 scripts/kb_index.py books/attention-hook`。

