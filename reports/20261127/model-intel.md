# 每日模型情報 — 2026-11-27
> 涵蓋範圍：2026-11-26 ~ 2026-11-27

## TL;DR
- 過去 24 小時（適逢美國感恩節）沒有確認落在範圍內的新模型、新權重或 API 價格變更；主要廠商官方頻道安靜。
- Google Vertex AI Extensions 依先前公告於 2026-11-26 之後關閉，仍在使用 Extensions 的整合需改用 Gemini Enterprise Agent Platform 的替代方案。
- 自架推論生態（vLLM、Arena 排行榜等）在範圍內沒有新 release 或排名變動；vLLM 最新 v0.34.x 為較早釋出。

## 閉源模型與 API
| 廠商 | 項目 | 重點 | 來源 |
|---|---|---|---|
| — | 無重大更新 | 範圍內未找到有明確日期的新模型、價格、context window / rate limit 或 deprecation 公告 | — |

## 開源 / Open-weight
| 模型 | 參數 / 授權 / Context | 重點 | 來源 |
|---|---|---|---|
| — | — | 無重大更新（最新可見釋出為 11/23 的 Ling-3.2-air，已超出範圍） | — |

## 自架推論生態
- 無重大更新。vLLM、SGLang、Ollama、llama.cpp、TensorRT-LLM 在範圍內未查到新 release（SGLang / Ollama / llama.cpp / TensorRT-LLM 的 GitHub releases 頁本次無法讀取，僅以搜尋結果確認未見新版）。

## Benchmark 與排行榜
- 無重大更新。LMArena 官方 changelog 最新一筆為 2026-11-24（Arena 3D leaderboard 上線），範圍內無新條目。

## 雲端平台上架
- **Google Vertex AI**：Vertex AI Extensions 依 2026-05-26 的 deprecation 公告，於 2026-11-26 之後關閉服務；Vertex AI 文件已停止更新，服務移至 Gemini Enterprise Agent Platform。來源：https://docs.cloud.google.com/vertex-ai/generative-ai/docs/release-notes
- AWS Bedrock、Azure AI Foundry：範圍內無新增或下架模型。

## 對我的影響（自架 vLLM / 企業部署觀點）
- 若企業內部有串接 Vertex AI Extensions 的工具呼叫流程，應確認已遷移，否則 11/26 之後呼叫會失敗。

```json
{"date":"2026-11-27","range":{"from":"2026-11-26","to":"2026-11-27"},"items":[{"category":"cloud","vendor":"Google","title":"Vertex AI Extensions 於 2026-11-26 之後關閉","url":"https://docs.cloud.google.com/vertex-ai/generative-ai/docs/release-notes","importance":"low"}]}
```
