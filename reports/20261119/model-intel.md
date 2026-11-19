# 每日模型情報 — 2026-11-19
> 涵蓋範圍：2026-11-18 ~ 2026-11-19
> 註：本次為首份報告（無先前報告），蒐集過去 24 小時。部分項目美國時間為 11-17（台北時間已是 11-18），一併收錄並標註。

## TL;DR
- OpenAI 發布 GPT-6.2 Astra / Sol（API 同步上線，Astra $8/$40、比 GPT-6 Astra 降價 20%；Sol 維持 $2/$10），Artificial Analysis Intelligence Index 排第 2，僅次 Claude Fable 5.2；AWS Bedrock 同步 GA。
- Google 發布 Gemini 4 Neon（介於 Carbon 與 Hydrogen 之間，1M context，$3/$15），透過 Gemini API、AI Studio 與企業產品推出，AA Index 61。
- Microsoft 於 Ignite 發布 MAI Code 2 / MAI Code 2 Flash 編碼模型（GitHub Copilot 可用，Flash 於 Microsoft Foundry limited preview）；開源權重本期無重大新釋出。

## 閉源模型與 API
| 廠商 | 項目 | 重點 | 來源 |
|---|---|---|---|
| OpenAI | GPT-6.2 Astra / GPT-6.2 Sol（11-17 美國時間 / 11-18 台北） | API model id `gpt-6.2-astra`、`gpt-6.2-sol`，上線即支援 Ultrafast。Astra：$8 input / $0.40 cached / $40 output（每 1M tokens），比 GPT-6 Astra 便宜 20%；Sol：$2 / $0.10 / $10（與 GPT-6.1 Sol 相同）。第三方追蹤顯示 context 約 1.1M（官方頁未載明）。官方未提 deprecation。 | [OpenAI](https://openai.com/index/introducing-gpt-6-2-astra-sol/)、[System card](https://deploymentsafety.openai.com/gpt-6-2-astra-sol)、[Opper tracker](https://opper.ai/model-releases) |
| OpenAI | Astra for Law 6.2 | 法律研究評測全項通過率 53.8%（9 月約 46%），ChatGPT Enterprise 客戶可申請 | [OpenAI](https://openai.com/index/astra-law-6-2/) |
| Google | Gemini 4 Neon（11-18） | 定位介於 Carbon 與 Hydrogen，宣稱 Carbon 等級品質、Flash 等級速度；1M context；$3 / $15（Hydrogen 的 2 倍）。Argon / Carbon 促銷價 $2/$10 至 11-30，之後回到 $4/$20。經 Gemini API、AI Studio、企業產品推出，Gemini app（AI Pro/Ultra）與 Antigravity 可用。 | [Google Blog](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-neon/)、[9to5Google](https://9to5google.com/2026/11/18/gemini-4-neon-announcement/)、[The Rundown](https://www.therundown.ai/news/google-gemini-4-neon-release) |
| Google | Gemini 資料保留政策 | 暫時對話 / 關閉歷史的對話改為保留約 2 個月（原 72 小時），可單獨 opt-out 訓練而保留歷史（消費端，非 API） | [Ars Technica](https://arstechnica.com/ai/2026/11/google-will-let-you-opt-out-of-ai-training-in-gemini-without-losing-your-history/) |
| Microsoft | MAI Code 2 / MAI Code 2 Flash（11-17 Ignite 美國時間） | 編碼模型；GitHub Copilot 可用，Code 2 Flash 於 Microsoft Foundry limited-access preview；宣稱企業編碼綜合分達 GPT-6.1 Sol 98%、Opus 5.5 96%，成本約 Sol 40%。未公布 list price 與 context。將「很快」上 OpenRouter 等。 | [Microsoft AI](https://microsoft.ai/news/introducing-mai-code-2-and-mai-code-2-flash/) |

## 開源 / Open-weight
| 模型 | 參數 / 授權 / Context | 重點 | 來源 |
|---|---|---|---|
| — | — | 無重大更新（範圍內未找到有明確日期的新權重釋出；Tencent Hy4 flash 於 11-17 03:44 UTC 釋出，早於本期範圍，未列入） | — |

## 自架推論生態
- vLLM：範圍內無新 release（最新 v0.34.0 為 11-16 發布，不在範圍內；該版有 `--block-size` 預設改 64、`gpu_memory_utilization` 預設 1.0、移除 Model Runner V1 等 breaking changes，升級前請留意）。[ai-tldr](https://ai-tldr.dev/releases/vllm-v0-34-0/)
- SGLang：v0.5.23 被回報從 v0.5.22 起在 H20-3e（SM90）concurrency 12 下 per-step decode latency 上升 33–45%（regression，issue #49336）。[Digest 2026-11-18](https://github.com/duanyytop/agents-radar/issues/4363)、[sglang#49336](https://github.com/sgl-project/sglang/issues/49336)
- llama.cpp：無正式 release；b12488–b12496 commits 新增 Qwen3-TTS ICL/reference mode、Kokoro TTS、OpenCL A7 DP4A kernels（Q4_0/Q4_K/Q5_K/Q6_K/Q8_0）、AMD GCN 啟用 stream_k。[b12496](https://github.com/ggml-org/llama.cpp/commit/b12496)
- Ollama / TensorRT-LLM：無重大更新。

## Benchmark 與排行榜
- Artificial Analysis Intelligence Index（11-17）：GPT-6.2 Astra 升至第 2（比 GPT-6 Astra +5，超越 Gemini 4 Carbon 60、Claude Opus 5.5 59），第 1 仍為 Claude Fable 5.2；GPT-6.2 Sol 57（+2）。Astra 在 Coding Agent Index 持平，Sol 下滑 3 分（SWE-Atlas-QnA-AA -14）；AA-Omniscience 幻覺率 Astra 59% / Sol 55%。[Artificial Analysis](https://artificialanalysis.ai/articles/openai-has-the-2-model-in-the-intelligence-index-with-the-release-of-gpt-6-2-astra-and-gpt-6-2-sol)
- Gemini 4 Neon：AA Index 61（xhigh）/ 60（high）；GraphWalks 95.2（Opus 5.5 66.8、GPT-6.2 Sol 80.1）；Terminal-Bench 4.1 與 FrontierCode 2.0 仍由 Opus 5.5 領先。[The Rundown](https://www.therundown.ai/news/google-gemini-4-neon-release)

## 雲端平台上架
- AWS Bedrock：GPT-6.2 Astra 與 GPT-6.2 Sol GA（含 Astra Ultrafast mode）（11-17 美國時間）。[AWS What's New](https://aws.amazon.com/about-aws/whats-new/2026/11/openai-gpt-6-2-astra-sol-amazon-bedrock)
- Microsoft Foundry：MAI Code 2 Flash limited-access preview；Baseten 推論平台進入 Foundry public preview，供 Azure 客戶執行 open models。[Microsoft AI](https://microsoft.ai/news/introducing-mai-code-2-and-mai-code-2-flash/)、[Seeking Alpha](https://seekingalpha.com/news/4673999-microsoft-foundry-adds-baseten-deepseek-ai-inference)
- Google Vertex AI：Gemini 4 Neon 經「企業產品」推出，Vertex AI 具體上架狀態未見明確公告。

## 對我的影響（自架 vLLM / 企業部署觀點）
- 若正評估升級 vLLM 0.34.0：注意 block-size 與 gpu_memory_utilization 預設值變更，現有部署參數需重新校驗，避免 OOM 或 decode latency 上升。
- SGLang 0.5.23 在 Hopper 系（H20）有 decode latency regression，生產環境建議暫留 0.5.22。
- 閉源價格持續下修（GPT-6.2 Sol $2/$10、Gemini 4 Neon $3/$15），自架 TCO 比較基準需更新；Bedrock 已同步提供 GPT-6.2，企業可走既有 AWS 合約導入。

```json
{"date":"2026-11-19","range":{"from":"2026-11-18","to":"2026-11-19"},"items":[{"category":"closed","vendor":"OpenAI","title":"GPT-6.2 Astra / GPT-6.2 Sol released (API, Astra $8/$40, Sol $2/$10)","url":"https://openai.com/index/introducing-gpt-6-2-astra-sol/","importance":"high"},{"category":"closed","vendor":"OpenAI","title":"Astra for Law 6.2","url":"https://openai.com/index/astra-law-6-2/","importance":"low"},{"category":"closed","vendor":"Google","title":"Gemini 4 Neon released (1M context, $3/$15)","url":"https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-4-neon/","importance":"high"},{"category":"closed","vendor":"Google","title":"Gemini consumer data retention extended to ~2 months","url":"https://arstechnica.com/ai/2026/11/google-will-let-you-opt-out-of-ai-training-in-gemini-without-losing-your-history/","importance":"low"},{"category":"closed","vendor":"Microsoft","title":"MAI Code 2 and MAI Code 2 Flash","url":"https://microsoft.ai/news/introducing-mai-code-2-and-mai-code-2-flash/","importance":"medium"},{"category":"inference","vendor":"SGLang","title":"v0.5.23 decode latency regression on H20 (SM90)","url":"https://github.com/sgl-project/sglang/issues/49336","importance":"medium"},{"category":"inference","vendor":"llama.cpp","title":"b12488-b12496: Qwen3-TTS ICL, Kokoro TTS, OpenCL DP4A kernels","url":"https://github.com/ggml-org/llama.cpp/commit/b12496","importance":"low"},{"category":"benchmark","vendor":"Artificial Analysis","title":"GPT-6.2 Astra #2 on Intelligence Index behind Claude Fable 5.2","url":"https://artificialanalysis.ai/articles/openai-has-the-2-model-in-the-intelligence-index-with-the-release-of-gpt-6-2-astra-and-gpt-6-2-sol","importance":"medium"},{"category":"benchmark","vendor":"Google","title":"Gemini 4 Neon AA Index 61, GraphWalks 95.2","url":"https://www.therundown.ai/news/google-gemini-4-neon-release","importance":"low"},{"category":"cloud","vendor":"AWS","title":"GPT-6.2 Astra and Sol GA on Amazon Bedrock","url":"https://aws.amazon.com/about-aws/whats-new/2026/11/openai-gpt-6-2-astra-sol-amazon-bedrock","importance":"high"},{"category":"cloud","vendor":"Microsoft","title":"Baseten inference platform public preview on Microsoft Foundry","url":"https://seekingalpha.com/news/4673999-microsoft-foundry-adds-baseten-deepseek-ai-inference","importance":"low"}]}
```
