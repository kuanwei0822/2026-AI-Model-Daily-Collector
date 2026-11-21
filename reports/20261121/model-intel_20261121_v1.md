# 每日模型情報 — 2026-11-21

> 涵蓋範圍：2026-11-20 \~ 2026-11-21

## TL;DR

- 過去 24 小時是平靜的一天：唯一有明確日期的模型 / API 更新是 OpenAI 在 API 推出 `gpt-live-1.1`（語音模型），並新增 Standby 計費模式。
- 開源權重、自架推論框架（vLLM / SGLang / llama.cpp / Ollama）、Benchmark 與雲端平台在範圍內皆無重大更新；近期項目（Gemini 4 Neon、Hy4 Flash 權重、GPT-6.2 上 Arena）都落在 11-18 / 11-19，不予收錄。

## 閉源模型與 API

| 廠商 | 項目 | 重點 | 來源 |
| --- | --- | --- | --- |
| OpenAI | GPT-Live-1.1 上架 API（`gpt-live-1.1`）+ Standby 模式（2026-11-20） | 即時語音模型；口音一致性與任務完成率提升；Standby 在靜默 5–60 秒後暫停模型、WebRTC 連線保持，計費 $0.02/min（active 為 $0.05/min） | [OpenAI Developer Community](https://community.openai.com/t/gpt-live-1-1-has-arrived-in-the-api/1418537) |

## 開源 / Open-weight

| 模型 | 參數 / 授權 / Context | 重點 | 來源 |
| --- | --- | --- | --- |
| 無重大更新 | — | — | — |

## 自架推論生態

- 無重大更新（範圍內無新 release；目前最新：vLLM v0.33.0 於 11-02、llama.cpp v1.0.0 於 11-13、Ollama v0.40.16 於 11-09、SGLang v0.5.21 於 10-02）。

## Benchmark 與排行榜

- 無重大更新（LMArena changelog 最新一筆為 11-19）。

## 雲端平台上架

- 無重大更新。

## 對我的影響（自架 vLLM / 企業部署觀點）

- 無新的直接影響。提醒（既有公告、非本期新項目）：Anthropic `claude-sonnet-4-5-20250929` 將於 2026-11-30 退役，若企業部署仍有呼叫需於月底前切換（[Model deprecations](https://platform.claude.com/docs/en/about-claude/model-deprecations)）。

```json
{"date":"2026-11-21","range":{"from":"2026-11-20","to":"2026-11-21"},"items":[{"category":"closed","vendor":"OpenAI","title":"GPT-Live-1.1 available in API with Standby mode","url":"https://community.openai.com/t/gpt-live-1-1-has-arrived-in-the-api/1418537","importance":"medium"}]}
```
