# 每日模型情報 — 2026-11-23
> 涵蓋範圍：2026-11-20 ~ 2026-11-23

## TL;DR
- Thinking Machines 於 11-20 釋出 open-weight **Inkling 2 Mini**（26.4B MoE / 3.4B active、looped layers、Apache 2.0、最長 1M context），提供 NVFP4 / MXFP8 單一約 20GB 檢查點
- 閉源 API 本時段無新模型、價格或 deprecation 公告：OpenAI、Anthropic、Google Gemini、xAI、Mistral 官方 changelog 最新條目皆早於 11-20
- 自架推論框架（vLLM / SGLang / llama.cpp / TensorRT-LLM）與雲端平台本時段皆無新 release；Hugging Face transformers v5.24.0（11-21）新增 Inkling 2 Mini 等模型支援

## 閉源模型與 API
| 廠商 | 項目 | 重點 | 來源 |
| --- | --- | --- | --- |
| 全部 | 無重大更新 | 官方 changelog 最新條目：OpenAI 11-19（gpt-live-1.1）、Claude API 11-17（Linked billing beta）、xAI 11-19（grok-build-0.1 EOL）、Gemini API 10-30、Mistral 10-29，皆不在範圍內 | [OpenAI changelog](https://developers.openai.com/api/docs/changelog)、[Claude release notes](https://platform.claude.com/docs/en/release-notes/overview)、[xAI release notes](https://docs.x.ai/developers/release-notes) |

## 開源 / Open-weight
| 模型 | 參數 / 授權 / Context | 重點 | 來源 |
| --- | --- | --- | --- |
| Thinking Machines Inkling 2 Mini | 26.4B MoE / 3.4B active（looped layers 跑 3 次，等效約 5.4B active）· Apache 2.0 · 最長 1M | 11-20 釋出；text + image 輸入、text 輸出；單一約 20GB 檢查點（NVFP4 / MXFP8），官方標示可在 DGX Spark 或 32GB+ Apple silicon 執行；Ollama release notes 列 SWE-Bench Verified 79.2%（自評） | [Hugging Face model card](https://huggingface.co/thinkingmachines/Inkling-2-Mini)、[Artificial Analysis](https://artificialanalysis.ai/) |

註：Sarvam-105B-1711（105B MoE / 10.3B active，Apache 2.0）依 llmreference 為 11-17 發布、HF 頁面未標日期，不在本時段，未收錄。

## 自架推論生態
- Hugging Face transformers v5.24.0（11-21）：新增 Inkling 2 Mini、Apertus 1.5、Omnilingual ASR、Lara Mini、SarvamMoE / SarvamMLA、HY4-VL、EXAONE 等架構支援；breaking change：`past_key_values` / `cache_params` 改名為 `cache`，需 peft ≥ 0.22.0（來源為 Releasebot 彙整，GitHub releases 頁面快取尚未顯示）— [Releasebot](https://releasebot.io/updates/huggingface)
- vLLM、SGLang、llama.cpp、TensorRT-LLM 無重大更新（最新 release：vLLM v0.33.0 11-02、SGLang v0.5.21 10-02、llama.cpp b12380 11-14、TensorRT-LLM v1.3.0rc29 09-29）
- Ollama：v0.40.17 已支援 Inkling 2 Mini（僅 Apple silicon），但 release 標示日期為 11-10，不計入本時段 — [Ollama releases](https://github.com/ollama/ollama/releases)

## Benchmark 與排行榜
- Artificial Analysis 11-20 發布 Inkling 2 Mini 評測文章與語言模型評測；11-22 新增 InclusionAI LingSante-3.1-flash 評測（首頁 changelog，未列分數）— [Artificial Analysis](https://artificialanalysis.ai/)
- LMArena：11-20 Recraft V4.1 Flash 加入 Text-to-Image Arena；11-21 ~ 11-23 無新增 — [Arena leaderboard changelog](https://arena.ai/blog/leaderboard-changelog/)

## 雲端平台上架
- 無重大更新（AWS Bedrock 文件最新為 11-19；Vertex AI release notes 本時段無條目，頁面標示已停止更新並轉向 Gemini Enterprise Agent Platform 文件；Azure AI Foundry 未找到本時段公告）

## 對我的影響（自架 vLLM / 企業部署觀點）
- Inkling 2 Mini 為 Apache 2.0、active 僅 3.4B 且支援 1M context，是低成本長上下文 agent 的候選；但 looped transformer 為新架構，vLLM v0.33.0 是否已支援需自行確認（目前只確認 transformers v5.24.0 與 Ollama 支援）
- 官方檢查點僅 NVFP4 / MXFP8，NVFP4 需 Blackwell 世代才有效能優勢；Hopper / Ampere 環境需等社群 FP8 / BF16 版本或自行驗證
- 若內部服務依賴 transformers 的 `past_key_values` 參數，升級到 v5.24.0 前需先改寫

```json
{"date":"2026-11-23","range":{"from":"2026-11-20","to":"2026-11-23"},"items":[{"category":"open","vendor":"Thinking Machines","title":"Inkling 2 Mini open-weight release (26.4B MoE / 3.4B active, looped layers, Apache 2.0, 1M context, NVFP4/MXFP8)","url":"https://huggingface.co/thinkingmachines/Inkling-2-Mini","importance":"high"},{"category":"inference","vendor":"Hugging Face","title":"transformers v5.24.0 adds Inkling 2 Mini, Apertus 1.5, SarvamMoE and more; cache argument rename (breaking)","url":"https://releasebot.io/updates/huggingface","importance":"medium"},{"category":"benchmark","vendor":"Artificial Analysis","title":"Inkling 2 Mini (11-20) and LingSante-3.1-flash (11-22) evaluations added","url":"https://artificialanalysis.ai/","importance":"low"},{"category":"benchmark","vendor":"LMArena","title":"Recraft V4.1 Flash added to Text-to-Image Arena","url":"https://arena.ai/blog/leaderboard-changelog/","importance":"low"}]}
```
