# 每日模型情報 — 2026-11-26
> 涵蓋範圍：2026-11-25 ~ 2026-11-26

## TL;DR
- 本時段主要廠商無新基礎模型或價格變動；唯一 API 異動是 OpenAI changelog 11-24（美西時間，範圍邊界）的兩則：**Healthcare model configurations**（`gpt-6.2-astra-healthcare` 等 4 款，Responses API）與 `chat-latest` snapshot 更新
- 開源邊界項目：PrismML 11-24 釋出 **Ternary Bonsai 2.5 27B**（基於 Qwen3.8 27B、Apache 2.0、模型檔約 5.9 GB），主打 agentic coding
- 自架推論框架（vLLM / SGLang / llama.cpp / Ollama / TensorRT-LLM）與雲端平台本時段皆無新 release / 上架公告

## 閉源模型與 API
| 廠商 | 項目 | 重點 | 來源 |
| --- | --- | --- | --- |
| OpenAI | Healthcare model configurations（11-24 美西時間，範圍邊界） | Responses API 推出醫療用模型設定：`gpt-6.2-astra-healthcare`、`gpt-6.2-sol-healthcare`、`gpt-6-astra-healthcare`、`gpt-6.1-sol-healthcare`，搭配臨床問答 harness，web search 使用專屬醫療來源索引；頁面未列價格數字。註：條目內容取自頁面摘要，未逐字核對 | [OpenAI changelog](https://developers.openai.com/api/docs/changelog) |
| OpenAI | `chat-latest` 更新（11-24 美西時間，範圍邊界） | `chat-latest` snapshot 改指向 ChatGPT（Plus / Pro / Business / Enterprise）目前最新模型；官方仍建議 production 使用 GPT-6.2 系列。註：同上，未逐字核對 | [OpenAI changelog](https://developers.openai.com/api/docs/changelog) |
| 其他廠商 | 無重大更新 | 官方頁面最新條目：Claude Platform 11-23、Gemini API 11-19（Genie 4 GA、Tool retrieval Preview）、xAI 11-19、Mistral 10-30，皆不在範圍內；OpenAI deprecations 最新通知仍為 11-18 | [Claude release notes](https://platform.claude.com/docs/en/release-notes/overview.md)、[Gemini API changelog](https://aistudio.google.com/docs/changelog)、[xAI release notes](https://docs.x.ai/developers/release-notes)、[Mistral release notes](https://docs.mistral.ai/resources/release-notes)、[OpenAI deprecations](https://developers.openai.com/api/docs/deprecations.md) |

## 開源 / Open-weight
| 模型 | 參數 / 授權 / Context | 重點 | 來源 |
| --- | --- | --- | --- |
| PrismML Ternary Bonsai 2.5 27B（11-24，範圍邊界） | 27B（ternary，約 5.9 GB）/ Apache 2.0 / Context 未標示 | 基於 Qwen3.8 27B，官方稱在 coding、重複 tool use 與多步驟任務有提升；權重已上 Hugging Face collection | [PrismML 公告](https://prismml.com/news/bonsai-2-5-27b)、[Hugging Face collection](https://huggingface.co/collections/prism-ml/bonsai-25-27b) |

## 自架推論生態
- vLLM、SGLang、llama.cpp、Ollama、TensorRT-LLM 無重大更新（最新 release：vLLM v0.33.0 11-02、SGLang v0.5.21 10-02、llama.cpp b12380 11-14、Ollama v0.40.17、TensorRT-LLM v1.3.0rc29 09-29）— [vLLM releases](https://github.com/vllm-project/vllm/releases)、[SGLang releases](https://github.com/sgl-project/sglang/releases)、[llama.cpp releases](https://github.com/ggml-org/llama.cpp/releases)、[Ollama releases](https://github.com/ollama/ollama/releases)、[TensorRT-LLM releases](https://github.com/NVIDIA/TensorRT-LLM/releases)

## Benchmark 與排行榜
- 無重大更新（LMArena changelog 最新為 11-24 Arena 3D leaderboard，已於前日報告收錄；Artificial Analysis 本次未讀取）— [Arena leaderboard changelog](https://arena.ai/company/leaderboard-changelog)

## 雲端平台上架
- 無重大更新（未找到 AWS Bedrock、Microsoft Foundry、Vertex AI 本時段的模型上架或下架公告）

## 對我的影響（自架 vLLM / 企業部署觀點）
- Bonsai 2.5 27B 以 ternary 量化把 27B 壓到約 5.9 GB，若有邊緣或單卡部署需求可評估；但需先確認 vLLM 是否支援其 ternary 格式（官方公告未提及 vLLM 支援）
- OpenAI healthcare 模型設定僅限 Responses API，若企業內有醫療場景且已用 OpenAI，可留意；自架 vLLM 部署無需調整

```json
{"date":"2026-11-26","range":{"from":"2026-11-25","to":"2026-11-26"},"items":[{"category":"closed","vendor":"OpenAI","title":"Healthcare model configurations for Responses API (gpt-6.2-astra-healthcare etc.; dated 11-24 US time, range boundary)","url":"https://developers.openai.com/api/docs/changelog","importance":"medium"},{"category":"closed","vendor":"OpenAI","title":"chat-latest snapshot updated (dated 11-24 US time, range boundary)","url":"https://developers.openai.com/api/docs/changelog","importance":"low"},{"category":"open","vendor":"PrismML","title":"Ternary Bonsai 2.5 27B open weights, Apache 2.0 (dated 11-24, range boundary)","url":"https://prismml.com/news/bonsai-2-5-27b","importance":"medium"}]}
```
