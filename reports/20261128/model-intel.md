# 每日模型情報 — 2026-11-28
> 涵蓋範圍：2026-11-27 ~ 2026-11-28

## TL;DR
- OpenAI 修正 GPT-6.2 Astra / Sol 的計價錯誤：先前部分用戶誤享折扣，修正後 Astra 用量上限約快 40% 觸頂、Sol 約快 25%；合資格訂閱者獲額外一次用量重置，Business 用戶至 2026 年底免費使用 Fast Mode（官方公告未查到，以媒體報導為準）
- Tencent 開源 DFly2（0.85B speculative decoder，放在 `tencent/Hy4-flash` repo），報導稱可與 vLLM / SGLang 整合；官方宣稱 DeepSeek-V4.1-Flash 在 64K context 下 throughput 最多提升 81%（廠商自報，未獨立驗證）
- 美國感恩節週，其餘區塊（開源權重、vLLM release、排行榜、雲端上架）在時間範圍內皆無重大更新

## 閉源模型與 API
| 廠商 | 項目 | 重點 | 來源 |
|---|---|---|---|
| OpenAI | GPT-6.2 Astra / Sol 計價錯誤修正 | 修正誤給部分用戶的折扣；用量上限觸頂速度 Astra 約快 40%、Sol 約快 25%（與前一週相比）；合資格訂閱者獲額外用量重置，Business 用戶至 2026 年底免費 Fast Mode。依 The Neuron 11/27 摘要，未找到 OpenAI 官方公告 | [The Neuron 2026-11-27](https://www.theneuron.ai/digest/everything-that-happened-in-ai-today-november-27-2026/) |

## 開源 / Open-weight
| 模型 | 參數 / 授權 / Context | 重點 | 來源 |
|---|---|---|---|
| — | — | 無重大更新 | — |

## 自架推論生態
- **Tencent DFly2（開源 speculative decoding drafter）**：0.85B 參數，透過 `tencent/Hy4-flash` repo 釋出，報導稱可與 vLLM / SGLang 整合。廠商宣稱 DeepSeek-V4.1-Flash 在 64K context 下 throughput 最多提升 81%、Hy4 Flash agent 任務最多快 4.2 倍（廠商自報；授權條款未查證）。來源：[The Neuron 2026-11-27](https://www.theneuron.ai/digest/everything-that-happened-in-ai-today-november-27-2026/)、[AI Daily Post](https://aidailypost.com/news/tencents-dfly2-reuses-kv-cache-faster)
- vLLM：時間範圍內無新 release；最新 blog 文章為 11/24（ERNIE 5.5 Flash Preview day-0 支援），不在範圍內。來源：[vLLM blog RSS](https://vllm.ai/blog/rss.xml)
- SGLang、llama.cpp、Ollama、TensorRT-LLM：無重大更新

## Benchmark 與排行榜
- 無重大更新（LMArena changelog 最新一筆為 11/24 的 Arena 3D 排行榜，不在範圍內）。來源：[Arena Leaderboard Changelog](https://arena.ai/blog/leaderboard-changelog/)

## 雲端平台上架
- 無重大更新

## 對我的影響（自架 vLLM / 企業部署觀點）
- DFly2 若授權允許商用，可作為 DeepSeek-V4.1-Flash 長 context 推論的 speculative decoding drafter 候選；建議先確認授權與實際整合的 vLLM 版本，再以自家流量重新量測，不要直接採信廠商的 81% 數字
- 若團隊有使用 GPT-6.2 Astra / Sol 作為對照或 fallback，用量上限觸頂會變快，需重新估算配額與成本

```json
{"date":"2026-11-28","range":{"from":"2026-11-27","to":"2026-11-28"},"items":[{"category":"closed","vendor":"OpenAI","title":"GPT-6.2 Astra / Sol 計價錯誤修正，用量上限觸頂加快","url":"https://www.theneuron.ai/digest/everything-that-happened-in-ai-today-november-27-2026/","importance":"medium"},{"category":"inference","vendor":"Tencent","title":"DFly2 開源 speculative decoding drafter（0.85B，支援 vLLM / SGLang）","url":"https://aidailypost.com/news/tencents-dfly2-reuses-kv-cache-faster","importance":"medium"}]}
```
