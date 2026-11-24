# 每日模型情報 — 2026-11-25
> 涵蓋範圍：2026-11-24 ~ 2026-11-25

## TL;DR
- 本時段整體平靜：OpenAI、Gemini、xAI、Mistral 官方 changelog 均無新模型、價格或 context 變更；自架推論框架與雲端平台也沒有新 release
- 邊界項目：Claude Platform release notes 標示 11-23（美西時間，與本時段前緣重疊）宣布 **Claude Opus 4.5 deprecated**，Claude API 將於 2027-01-22 退役，建議遷移至 Claude Opus 5.5；同一則公告推出 Enterprise Frontier Safeguards beta
- LMArena 11-24 上線 **Arena 3D leaderboard**（以 Code Arena 中要求 3D 結果的對戰排名）

## 閉源模型與 API
| 廠商 | 項目 | 重點 | 來源 |
| --- | --- | --- | --- |
| Anthropic | Claude Opus 4.5 deprecation（11-23 美西時間，範圍邊界） | `claude-opus-4-5-20251101` / `claude-opus-4-5` 進入 deprecated，Claude API 退役日 2027-01-22，官方建議改用 Claude Opus 5.5；同則公告另有 Enterprise Frontier Safeguards beta 與兩個新的 organization webhook event types | [Claude release notes](https://platform.claude.com/docs/en/release-notes/overview.md) |
| 其他廠商 | 無重大更新 | 官方 changelog 最新條目：OpenAI 11-19（gpt-live-1.1）、xAI 11-19（grok-build-0.1 EOL）、Mistral 11-17（Vibe Desktop GA）、Gemini API 10-30（Computer Use GA），皆不在範圍內；OpenAI deprecations 頁最新通知為 11-18 | [OpenAI changelog](https://developers.openai.com/api/docs/changelog)、[OpenAI deprecations](https://developers.openai.com/api/docs/deprecations.md)、[xAI release notes](https://docs.x.ai/developers/release-notes)、[Mistral release notes](https://docs.mistral.ai/resources/release-notes)、[Gemini API changelog](https://ai.google.dev/gemini-api/docs/changelog) |

## 開源 / Open-weight
| 模型 | 參數 / 授權 / Context | 重點 | 來源 |
| --- | --- | --- | --- |
| — | — | 無重大更新 | — |

註：以下為 11-23 的項目，早於本時段且官方頁面本次未能讀取，未收錄，僅供參考：inclusionAI Ling-3.2-air（媒體稱 124B MoE / 5.5B active、MIT、1M context，HF 頁面未能驗證）、AWS Strands Decider v2（媒體稱 Gemma 4 基底 2B–31B、Apache 2.0）。

## 自架推論生態
- vLLM、SGLang、llama.cpp、Ollama、TensorRT-LLM 無重大更新（最新 release：vLLM v0.33.0 11-02、SGLang v0.5.21 10-02、llama.cpp b12380 11-14、Ollama v0.40.17、TensorRT-LLM v1.3.0rc29 09-29）— [vLLM releases](https://github.com/vllm-project/vllm/releases)、[SGLang releases](https://github.com/sgl-project/sglang/releases)、[llama.cpp releases](https://github.com/ggml-org/llama.cpp/releases)、[Ollama releases](https://github.com/ollama/ollama/releases)、[TensorRT-LLM releases](https://github.com/NVIDIA/TensorRT-LLM/releases)

## Benchmark 與排行榜
- LMArena（11-24）：Arena 3D leaderboard 上線，以 Code Arena 中使用者明確要求 3D 結果的對戰進行排名；changelog 未列名次或分數 — [Arena leaderboard changelog](https://arena.ai/company/leaderboard-changelog)
- OpenClaw ShellBench（11-24，媒體報導，未見官方頁面）：新的 agent shell 任務 benchmark，受測模型含 GPT-6 Astra、GPT-6.1 Sol、Claude Fable 5.2、Gemini 4 Carbon、DeepSeek v4.1 Flash 等 — [The Deep View](https://www.thedeepview.com/articles/exclusive-openclaw-offers-an-agent-reality-check)
- Artificial Analysis：本次無法讀取頁面，未確認

## 雲端平台上架
- 無重大更新（AWS Bedrock 最新上架公告為 11-17 GPT-6.2 Astra / Sol；Microsoft Foundry Blog 最新為 11-21，非模型上架；Vertex AI 未找到本時段公告）

## 對我的影響（自架 vLLM / 企業部署觀點）
- 若有服務仍呼叫 `claude-opus-4-5` 系列，需在 2027-01-22 前完成遷移與回歸測試（Bedrock / Vertex 上的退役時程請另行確認）
- 自架框架本時段無新版本，維持 vLLM v0.33.0 即可，無需因本日消息調整部署

```json
{"date":"2026-11-25","range":{"from":"2026-11-24","to":"2026-11-25"},"items":[{"category":"closed","vendor":"Anthropic","title":"Claude Opus 4.5 deprecated; Claude API retirement 2027-01-22 (dated 11-23 US time, range boundary)","url":"https://platform.claude.com/docs/en/release-notes/overview.md","importance":"medium"},{"category":"benchmark","vendor":"LMArena","title":"Arena 3D leaderboard launched (Code Arena 3D battles)","url":"https://arena.ai/company/leaderboard-changelog","importance":"low"},{"category":"benchmark","vendor":"OpenClaw","title":"ShellBench agent benchmark launched (media report)","url":"https://www.thedeepview.com/articles/exclusive-openclaw-offers-an-agent-reality-check","importance":"low"}]}
```
