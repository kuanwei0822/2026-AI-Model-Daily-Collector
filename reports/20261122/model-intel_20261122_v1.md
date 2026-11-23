# 每日模型情報 — 2026-11-22

> 涵蓋範圍：2026-11-21 \~ 2026-11-22

## TL;DR

- Thinking Machines 釋出 open-weight 模型 Inkling 2 Mini（26.4B 總參數 / 3.4B active 的 looped MoE，Apache 2.0，context 最長 1M），官方權重即為 NVFP4 + MXFP8 混合精度
- 閉源 API、自架推論框架（vLLM / SGLang / llama.cpp / Ollama）、雲端平台在本時段皆無新的官方發布
- LMArena changelog 最新一筆為 11-20（圖像模型），本時段無新增項目

## 閉源模型與 API

| 廠商 | 項目 | 重點 | 來源 |
| --- | --- | --- | --- |
| — | 無重大更新 | 本時段無有明確日期的官方發布；Genie 4 上 Gemini API、Gemini API Tool Retrieval 皆為 11-19 發布，不在範圍內 | — |

## 開源 / Open-weight

| 模型 | 參數 / 授權 / Context | 重點 | 來源 |
| --- | --- | --- | --- |
| Thinking Machines Inkling 2 Mini | 26.4B 總參數 / 3.4B active（loop 後每 token 約 5.4B effective）· Apache 2.0 · 最長 1M tokens | Looped MoE（24 層，中間 12 層跑 3 次；128 experts、每 token 路由 8 個）；text + image 輸入、text 輸出；checkpoint 約 20GB，原生 NVFP4 + MXFP8 混合精度。Model card 標示釋出日 2026-11-20（美國時間），落在本次 24 小時窗口起點附近 | [Hugging Face model card](https://huggingface.co/thinkingmachines/Inkling-2-Mini) |

## 自架推論生態

- 無重大更新（各專案最新 release 皆早於本時段：vLLM v0.33.0 為 11-02、SGLang v0.5.21 為 10-02、Ollama v0.40.16 為 11-09、llama.cpp b12380 為 11-14）

## Benchmark 與排行榜

- 無重大更新（[Arena leaderboard changelog](https://arena.ai/blog/leaderboard-changelog/) 最新一筆為 11-20 Recraft V4.1 Flash 加入 Text-to-Image Arena，11-21、11-22 無新增）

## 雲端平台上架

- 無重大更新

## 對我的影響（自架 vLLM / 企業部署觀點）

- Inkling 2 Mini 為 Apache 2.0、active 參數僅 3.4B，約 20GB 權重可放進單張 32GB 以上 GPU，適合作為企業內部低成本自架候選；但 looped MoE 架構與 NVFP4/MXFP8 混合精度需確認 vLLM 是否已支援，目前 vLLM 最新 release（v0.33.0，11-02）早於模型發布，導入前應先查 vLLM main branch 或等下一版
- NVFP4 原生權重需 Blackwell 世代 GPU 才能發揮效能，Hopper / Ampere 環境可能需改用社群量化版本

```json
{"date":"2026-11-22","range":{"from":"2026-11-21","to":"2026-11-22"},"items":[{"category":"open","vendor":"Thinking Machines","title":"Inkling 2 Mini open-weight release (26.4B/3.4B active MoE, Apache 2.0, 1M context)","url":"https://huggingface.co/thinkingmachines/Inkling-2-Mini","importance":"high"}]}
```
