# 每日模型情報 — 2026-11-23

> 涵蓋範圍：2026-11-20 \~ 2026-11-23

## TL;DR

- Sarvam AI 於 11-22 釋出 open-weight 檢查點 Sarvam-105B-1711（105B MoE / 10.3B active，Apache 2.0），官方主打 NVFP4 版本（約 65GB），並標示以 vLLM 0.33.0 測試可服務
- 閉源 API 本時段無新模型或價格公告：OpenAI、Anthropic、Google、Mistral、xAI 官方 changelog 最新條目皆早於 11-20
- 自架推論框架（vLLM / SGLang / llama.cpp / Ollama / TensorRT-LLM）與雲端平台本時段皆無新 release

## 閉源模型與 API

| 廠商 | 項目 | 重點 | 來源 |
| --- | --- | --- | --- |
| OpenAI | GPT-5.6 Sol 促銷價結束（未證實） | 第三方部落格稱促銷價於 11-21 結束、恢復標準價；OpenAI 官方 changelog 未見對應公告，未列費率 | [local-ai-zone](https://local-ai-zone.github.io/blog/November_2026_AI_Model_Updates.html) |
| 其他廠商 | 無重大更新 | 官方 changelog 最新條目：OpenAI 11-19（GPT-Live-1.1）、Claude API 11-17、xAI 11-19、Gemini API 10-30、Mistral 10-29，皆不在範圍內 | [OpenAI changelog](https://developers.openai.com/api/docs/changelog)、[Claude release notes](https://platform.claude.com/docs/en/release-notes/overview) |

## 開源 / Open-weight

| 模型 | 參數 / 授權 / Context | 重點 | 來源 |
| --- | --- | --- | --- |
| Sarvam AI Sarvam-105B-1711 | 105B MoE / 10.3B active · Apache 2.0 · vLLM 範例 max-model-len 131072（媒體稱延伸至 160K，未一致） | 以 sarvam-105b 為底的後訓練版本，主打企業 agent、客服、語音 agent；官方 repo 為 NVFP4（約 65GB，可單張工作站 GPU），另有 BF16 版（sarvamai/sarvam-105b-1711-bf16）。自評 IFBench 82.5、tau2-Bench 85.5；標示以 vLLM 0.33.0 測試 | [Hugging Face model card](https://huggingface.co/sarvamai/sarvam-105b-1711)、[Unite.AI](https://www.unite.ai/sarvam-ai-releases-open-weight-105b-checkpoint-for-enterprise-agents/) |

註：Thinking Machines Inkling 2 Mini（11-20）已收錄於 11-22 報告，此處不重複。

## 自架推論生態

- 無重大更新（各專案最新 release 皆早於本時段：vLLM v0.33.0 為 11-02、SGLang v0.5.21 為 10-02、Ollama v0.40.16 為 11-09、llama.cpp b12380 為 11-14、TensorRT-LLM v1.3.0rc29 為 09-29）

## Benchmark 與排行榜

- [Artificial Analysis](https://artificialanalysis.ai/) 11-22 新增 InclusionAI LingSante-3.1-flash 的語言模型評測（首頁 changelog，未列分數）
- [Arena leaderboard changelog](https://arena.ai/blog/leaderboard-changelog/) 最新一筆為 11-20（Recraft V4.1 Flash 加入 Text-to-Image Arena），11-21 \~ 11-23 無新增

## 雲端平台上架

- 無重大更新（AWS Bedrock 文件最新為 11-19；Vertex AI release notes 本時段無條目；Azure AI Foundry what's new 頁面無法讀取）

## 對我的影響（自架 vLLM / 企業部署觀點）

- Sarvam-105B-1711 為 Apache 2.0、active 僅 10.3B，且官方已標示 vLLM 0.33.0 可服務，是本週少數可直接在現有 vLLM 版本上試的新 MoE 候選
- 官方主推 NVFP4 權重需 Blackwell 世代 GPU 才有效能優勢；Hopper / Ampere 環境建議改用 BF16 版或社群 FP8 量化，並自行驗證 context 長度（131K vs 160K）

```json
{"date":"2026-11-23","range":{"from":"2026-11-20","to":"2026-11-23"},"items":[{"category":"open","vendor":"Sarvam AI","title":"Sarvam-105B-1711 open-weight release (105B MoE / 10.3B active, Apache 2.0, NVFP4 + BF16)","url":"https://huggingface.co/sarvamai/sarvam-105b-1711","importance":"high"},{"category":"closed","vendor":"OpenAI","title":"GPT-5.6 Sol promotional pricing ends (unverified, third-party report)","url":"https://local-ai-zone.github.io/blog/November_2026_AI_Model_Updates.html","importance":"low"},{"category":"benchmark","vendor":"Artificial Analysis","title":"LingSante-3.1-flash evaluation added","url":"https://artificialanalysis.ai/","importance":"low"}]}
```
