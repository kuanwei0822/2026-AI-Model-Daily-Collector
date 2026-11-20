# 每日模型情報 — 2026-11-20

> 涵蓋範圍：2026-11-19 \~ 2026-11-20

## TL;DR

- Google 發布 **Gemini 4 Neon**（2026-11-18 US / 11-19 台北）：1M context、$3 / $15 per 1M tokens，Artificial Analysis Intelligence Index 61（xhigh），定位中階但逼近前沿。
- Azure 於 11-19 退役 o3 / o3-mini / o4-mini，Vertex 退役 gemini-3.6-flash；仍在用的企業端點需立即遷移（退役後回 410 Gone）。
- 開源權重與主流推論引擎（vLLM / SGLang / llama.cpp / Ollama）在本期間皆無正式 release，僅 PR 層級的新模型支援。

## 閉源模型與 API

| 廠商 | 項目 | 重點 | 來源 |
| --- | --- | --- | --- |
| Google | Gemini 4 Neon 發布 | 1M context（1,048,576）；$3 input / $0.15 cached / $15 output per 1M；上架 Gemini API、AI Studio、Gemini app（Pro/Ultra）、Antigravity | [Google Blog](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-neon/)、[The Rundown](https://www.therundown.ai/news/google-gemini-4-neon-release) |

## 開源 / Open-weight

| 模型 | 參數 / 授權 / Context | 重點 | 來源 |
| --- | --- | --- | --- |
| — | — | 無重大更新 | — |

## 自架推論生態

- **vLLM / SGLang / llama.cpp / Ollama / TensorRT-LLM**：本期間無正式 release。PR 層級：vLLM [#68748](https://github.com/vllm-project/vllm/pull/68748) 新增 MiniCPM5-15B-A2.5B（BF16、INT4/W4A16），llama.cpp [#32588](https://github.com/ggml-org/llama.cpp/pull/32588) 新增 SenseNova Loop 支援（皆未確認合併）。
- **LiteLLM**（2026-11-20）：v1.112.0-dev.1、v1.111.0-rc.2、v1.108.12（LTS）；RPM/TPM 限流移至 Rust gateway，新增 Kimi K3.1 Pro、MiniMax M3.1 Flash 等價格條目。[GitHub Release](https://github.com/BerriAI/litellm/releases/tag/v1.112.0-dev.1)
- **Unsloth v0.1.920-beta**（2026-11-20）：AMD NPU Q4NX 載入、NVIDIA Cosmos3 FP8。[GitHub Release](https://github.com/unslothai/unsloth/releases/tag/v0.1.920-beta)
- 量化版本（AWQ / GPTQ / FP8）：無重大更新。

## Benchmark 與排行榜

- **Artificial Analysis**：Gemini 4 Neon Intelligence Index 61（xhigh）/ 60（high），11-19 測得，總榜第三。[Artificial Analysis](https://artificialanalysis.ai/models/gemini-4-neon)、[The Rundown](https://www.therundown.ai/news/google-gemini-4-neon-release)
- **Arena**：Google 自述 Gemini 4 Neon Agent Arena Index 1336（第二），尚待 Arena 官方榜單確認。LMArena 文字榜、SWE-bench 無明顯變動。

## 雲端平台上架

- **Google Vertex AI**：Gemini 4 Neon 列為 GA（2026-11-18）——僅見第三方自動化追蹤，未直接核對官方頁，標註「未證實」。[open-chat-studio PR #5046](https://github.com/dimagi/open-chat-studio/pull/5046)
- **Google Vertex AI**：gemini-3.6-flash 於 2026-11-19 退役，替代為 gemini-3.8-flash。[PR #5046](https://github.com/dimagi/open-chat-studio/pull/5046)
- **Azure AI Foundry**：o3（→ gpt-5.6-sol）、o3-mini / o4-mini（→ gpt-5.6-terra）於 2026-11-19 退役，退役後回 410 Gone。[PR #5046](https://github.com/dimagi/open-chat-studio/pull/5046)
- **AWS Bedrock**：無重大更新（官方 doc history 11-17 \~ 11-20 無新條目）。[Bedrock Doc History](https://docs.aws.amazon.com/bedrock/latest/userguide/doc-history.html)

## 對我的影響（自架 vLLM / 企業部署觀點）

- 若企業客戶仍在 Azure 呼叫 o3 / o3-mini / o4-mini 或 Vertex gemini-3.6-flash，請立即切換 deployment 名稱，否則請求會直接失敗。
- vLLM 無新 release、無新 open-weight 主力模型，自架環境本週不需升級；可追蹤 MiniCPM5 MoE（2.5B active）支援合併，適合低成本推論場景。
- Gemini 4 Neon 的 $3 / $15 定價成為新的閉源中階基準，做自架 vs API 成本比較時可更新參考值。

```json
{"date":"2026-11-20","range":{"from":"2026-11-19","to":"2026-11-20"},"items":[{"category":"closed","vendor":"Google","title":"Gemini 4 Neon released (1M context, $3/$15 per 1M)","url":"https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-neon/","importance":"high"},{"category":"benchmark","vendor":"Artificial Analysis","title":"Gemini 4 Neon Intelligence Index 61 (xhigh), #3 overall","url":"https://artificialanalysis.ai/models/gemini-4-neon","importance":"medium"},{"category":"cloud","vendor":"Google Vertex AI","title":"Gemini 4 Neon GA on Vertex AI (unverified)","url":"https://github.com/dimagi/open-chat-studio/pull/5046","importance":"medium"},{"category":"cloud","vendor":"Microsoft Azure","title":"Azure o3 / o3-mini / o4-mini retired","url":"https://github.com/dimagi/open-chat-studio/pull/5046","importance":"high"},{"category":"cloud","vendor":"Google Vertex AI","title":"gemini-3.6-flash retired, replaced by gemini-3.8-flash","url":"https://github.com/dimagi/open-chat-studio/pull/5046","importance":"medium"},{"category":"inference","vendor":"LiteLLM","title":"LiteLLM v1.112.0-dev.1 / v1.111.0-rc.2 / v1.108.12 LTS","url":"https://github.com/BerriAI/litellm/releases/tag/v1.112.0-dev.1","importance":"low"},{"category":"inference","vendor":"Unsloth","title":"Unsloth v0.1.920-beta (AMD NPU Q4NX, Cosmos3 FP8)","url":"https://github.com/unslothai/unsloth/releases/tag/v0.1.920-beta","importance":"low"}]}
```
