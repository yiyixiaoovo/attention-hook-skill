# 语料溯源（source/）

本目录只保存**可公开再分发的文本**（`.txt`，由抓取/OCR 得到的纯文本）与抓取快照。
**不保存受版权保护的原始 PDF**——它们留在仓库外，只在此登记哈希，便于核对"这份 txt 到底来自哪一份 PDF"。

## 已移出仓库的原始文件

| 文件 | 说明 | SHA-256 | 状态 |
|---|---|---|---|
| berger-milkman-viral.pdf | Berger & Milkman, "What Makes Online Content Viral?", *Journal of Marketing Research* 49(2), 2012, 192–205（JSTOR 版本，OCR） | `7d3da7990e466caa83a22c452071c5968755bbbc5c8fb7b76dcaebe9543e4066` | **未入库**（2.5 MB，受版权保护，不随公开仓库再分发） |
| short-video-engagement.pdf | Li et al., "Delving Deep into Engagement Prediction of Short Videos", ECCV 2024（arXiv:2410.00289） | `a510860b09c655f7030f1b03df3e327beb59a07d211bb18799a2017648af6459` | **未入库**（13.8 MB）；入库的是按锚点提取的片段文本 |
| video-ad-hooking-period.pdf | Zhang et al., "Decoding the Hook: A Multimodal LLM Framework for Analyzing the Hooking Period of Video Ads"（arXiv:2602.22299） | `e937b9e425c88ffb675e488905aeb5988e619c4e4523d4ddb61c177c62d54787` | **未入库**（4.8 MB）；入库的是按锚点提取的片段文本 |

对应的可分发文本：

- `berger-milkman-viral.txt`（由上述 PDF 提取，仅用于逐字引用核验）
- `short-video-engagement-2024.txt`、`video-ad-hooking-period-2026.txt`：**只保留引用所需段落**（约 5 KB / 4 KB），不是全文

引用核对只依赖 `.txt`；如需复核原始版式，请自行从 arXiv / JSTOR 获取原文，用上面的哈希确认是同一份。

### 抽取时的唯一文本修复

arXiv PDF 经 PyMuPDF 抽取后，行尾断词会留下 `engage- ment` 这类碎片。入库片段做了两步处理，**不改动任何字词**：

1. 空白归一化（硬换行压成单空格）
2. 跨行断词还原：`(\w)-\s+(\w)` → `\1\2`（只还原被换行断开的单词；原文中本来就存在的连字符会被一并合并，这是已知的极小误差）

这两步由 `tools/build_video_excerpts.py` 完成，可重跑。

## 其余语料

| 文件 | 类型 | 备注 |
|---|---|---|
| kidd-hayden-2015-curiosity.txt | 同行评议综述（PMC 开放获取） | Neuron 2015，可分发 |
| made-to-stick-summary.txt | 二手摘要 | 非原书，引用时须标注 |
| hbs-ideas-that-stick.txt | 二手摘要 | 同上 |
| berger-contagious-interview.txt | 作者访谈 | 同上 |
| `_meta/` | 未采用的弱资料 | 不进入证据链 |
| `_desktop/` | 桌面抓取的平台快照 | 只作能力证据与量级参考，不作方法论证据 |

## 规则

1. 任何 `.pdf`/`.epub` 等原始出版物一律不入库（`.gitignore` 已排除 `books/*/source/*.pdf`）。
2. 新增语料必须在本书 `PIPELINE_STATE.md` 的语料表登记来源与证据等级。
3. 二手摘要不得被当作原书原文引用；`.txt` 里逐字可检索到的才算引用。
