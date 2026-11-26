# 复盘知识库

记录「这张卡在实际使用中到底有没有用」。**只记真实发生过的实验**，不记感觉。

## 为什么需要它

技能卡给的是方法与边界；它们**不能证明**在某个人、某个账号、某个平台上有效。
知识库把每次验证沉淀成可追溯的记录，让「下次该怎么做」有依据，而不是每轮从头猜。

对应 `x-playbook` 与 `video-metrics` 的要求：效果判定回到指标与 A/B 记录。

## 一条记录长什么样

见 `TEMPLATE.md`。每条记录是一个 markdown 文件，放在 `records/`，文件名即 id：

```
records/2026-11-hook-ab-types.md
```

frontmatter 必填：`id`、`date`、`cards`（必须是在册能力 slug）、`metric`、`status`、`evidence`、`verdict`。

## 记录规则

1. **先写假设再跑**：假设、指标、判定阈值写在跑之前（预注册）；跑完只填结果。
2. **卡与指标都要指得回**：`cards` 用能力 slug（校验器会核对），`metric` 用 `video-metrics` 的口径或明确的评分量表。
3. **结论分四级**：`supports` 支持 / `contradicts` 反驳 / `inconclusive` 不充分 / `invalid` 实验无效。
4. **不美化**：不充分的结论就写 `inconclusive`；样本小、评者不是真人等局限必须写。
5. **真实数据才入库**：没有真实后台数据时，用可控小实验并注明「非真实受众/非真实 CTR」。
6. **敏感数据不入库**：不放平台后台截图、个人隐私、未脱敏的用户信息。

## 索引

`INDEX.md` 由 `scripts/kb_index.py` 生成，不要手改；CI 会检查「重新生成后 git diff 为空」。

```bash
python3 scripts/kb_index.py books/attention-hook          # 生成 INDEX.md
python3 scripts/kb_index.py books/attention-hook --check  # CI：校验记录 + 索引是否为最新
```

## 与卡的关系

- 记录 `cards` 指向能力卡；一张卡可以有多条记录。
- 记录结论**不修改卡**：卡是方法，记录是证据。只有多条同向记录 + 足够证据等级，才考虑改卡。
- 记录中的指标口径以 `video-metrics` 卡为准；没有指标口径的「有效」不算记录。
