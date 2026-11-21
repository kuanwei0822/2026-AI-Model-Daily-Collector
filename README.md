# AI 模型資訊每日蒐集器 (AI-Model-Daily-Collector)

每天自動蒐集最新 LLM / AI 模型情報的個人 Agent。

版本：V1.0

> **注意：** 本 repo 中的每日報告由 AI Agent 自動產生，內容可能有誤或遺漏，請以報告中附上的原始來源為準。

## 簡介

模型更新的速度太快，AI 模型相關資訊每天都在變，手動追蹤既耗時又容易漏。

這個專案的目標：

1. 每天自動產出一份整理好的最新模型情報。
2. 設計重點放在**資安要求**、**技術選型（低系統複雜度）**與**方案取捨（低成本、高 CP 值）**，以達成高資安、低維運。
3. 專案會持續演進，逐步加入更多自動化功能，並改進架構與運作模式。

## 功能

- 每天固定時間，透過 Web Search 蒐集過去 24 小時（週一涵蓋 72 小時）的模型情報
- 依固定格式產出繁體中文報告（技術名詞保留英文），每一項都附來源連結
- 報告結尾附上機器可讀的 JSON 區塊，供後續程式處理
- 自動維護一份索引，記錄每日報告的連結、涵蓋範圍與項目數
- 同步到本地 repo 時保留版本紀錄，報告內容更新時遞增版本號，不覆蓋舊檔

## 架構總覽

<圖片另外產生>

兩個任務完全分開：

- **蒐集任務**（排程、雲端）：只負責蒐集資料，並存放於 Claude Docs。
- **同步任務**（手動、本地）：只負責把報告匯出到本地 repo 的 `reports/`。
- **上 GitHub**：一律由人手動 commit 與 push。

## 資安設計

刻意將 Agent 與 GitHub Repo 分開，不讓 Agent 直接存取 GitHub，避免遭到利用。

### 威脅與對策

| 威脅 | 對策 |
| --- | --- |
| GitHub Token、Repo、Commit 等敏感資訊外洩 | Agent 完全不接觸 GitHub，也不持有任何 GitHub 憑證 |
| Agent 被惡意利用，對 Repo 做破壞性操作 | 不讓 Agent 執行 git 指令；commit / push 一律由人手動進行 |
| 網頁內容夾帶 Prompt Injection（例如惡意指令、可疑連結被寫進報告） | 報告公開前一律人工檢查 diff；蒐集任務只能使用 WebSearch / WebFetch |
| 蒐集任務 Agent 無法接觸到本機檔案 | 蒐集任務跑在雲端，無法存取本機 |
| 同步任務 Agent 誤改或刪除本地檔案 | 同步任務只能寫入固定路徑，不修改、改名或刪除既有檔案 |

**Hard Action**：

1. 蒐集任務跑在雲端，物理上碰不到本機與 Git 憑證。
2. Push 到 GitHub 必須由人手動完成，Agent 無法自行公開任何內容，「Push 前人工檢查 diff」是整個流程中最重要的一道防線。

## 解決方案 Solution

### 1. 定時觸發：使用 Anthropic Claude Scheduler

每天都要自動蒐集，所以需要一個定時觸發機制。

不使用自己的筆電跑排程，因為電腦可能關機、睡眠、斷線，或被手動關閉。

評估過的選項：

- 使用 Anthropic Claude Scheduler 內建的定時任務。
- 在自己的主機上跑定時任務，這個主機需要 24 小時開著並連網，自建排程（systemd）。
- 雲端方案（AWS），在雲端跑定時任務。

目前選擇 Anthropic Claude Scheduler。未來需求變大時，再評估自建主機或雲端方案。

### 2. 資料儲存：Claude Docs

蒐集任務產出的報告直接存放在 Claude Docs，不需要額外的雲端儲存空間。

缺點是資料運用彈性不高，無法直接轉移到地端，因此另外設計了同步任務來補足這一段。

### 3. 同步到本地端：手動觸發的同步任務

使用者打開電腦時，手動觸發同步任務：

1. 讀取「每日模型情報 — 索引」Doc，取得所有報告清單。
2. 逐日比對 Doc 的 rev 與本地 `manifest.json`：
    - 本地沒有這份報告 → 新增 v1
    - rev 相同 → 跳過
    - rev 不同 → 新增下一個版本，舊版本保留
3. 將報告匯出為 Markdown，寫入 `reports/YYYYMMDD/`。

### 4. 上 GitHub：人工 commit / push

不讓 Agent 直接 push。在本地檢查 diff 後，手動執行：

```bash
git add reports/
git commit -m "reports: YYYY-MM-DD"
git push
```

## 蒐集範圍

| 類別 | 內容 |
| --- | --- |
| 閉源模型與 API | 新模型、版本更新、價格、context window、rate limit、deprecation |
| Open-weight 模型 | 新權重釋出（參數量、授權、context 長度） |
| 自架推論生態 | vLLM、SGLang、llama.cpp、Ollama、TensorRT-LLM、量化版本（AWQ / GPTQ / FP8） |
| Benchmark | LMArena、SWE-bench、Artificial Analysis 等排行榜變動 |
| 雲端平台 | AWS Bedrock、Azure AI Foundry、Vertex AI 上架 / 下架 |

收錄規則：

- 只收錄有明確日期、且在時間範圍內的項目
- 優先採用官方來源（官方 blog、release notes、GitHub releases、Hugging Face model card）
- 忽略傳聞；重大傳聞會標註「未證實」
- 某區塊沒有新消息就寫「無重大更新」，不硬湊

## 報告格式

每份報告為固定結構的 Markdown：

```markdown
# 每日模型情報 — YYYY-MM-DD
> 涵蓋範圍：YYYY-MM-DD ~ YYYY-MM-DD

## TL;DR
## 閉源模型與 API
## 開源 / Open-weight
## 自架推論生態
## Benchmark 與排行榜
## 雲端平台上架
## 對我的影響（自架 vLLM / 企業部署觀點）
```

結尾附機器可讀的 JSON：

```json
{
  "date": "YYYY-MM-DD",
  "range": { "from": "YYYY-MM-DD", "to": "YYYY-MM-DD" },
  "items": [
    {
      "category": "closed | open | inference | benchmark | cloud",
      "vendor": "",
      "title": "",
      "url": "",
      "importance": "high | medium | low"
    }
  ]
}
```

每日資料夾內的 `manifest.json` 記錄版本歷史：

```json
{
  "date": "YYYY-MM-DD",
  "doc_url": "",
  "versions": [
    { "version": 1, "file": "model-intel_YYYYMMDD_v1.md", "rev": 1, "pulled_at": "YYYY-MM-DDTHH:MM:SS+08:00" }
  ]
}
```

## Repo 結構

```
2026-AI-Model-Daily-Collector/
├── README.md
├── docs/                             # （規劃中）
│   ├── architecture.md               # 方案比較與架構細節
│   ├── security.md                   # 威脅模型與防護清單
│   └── decisions/                    # ADR（架構決策紀錄）
├── deploy/                           # （規劃中）
│   ├── systemd/                      # 自建主機排程
│   ├── k8s/                          # Kubernetes 部署
│   └── aws/                          # AWS 雲端方案（Terraform）
└── reports/
    ├── 20261119/                     # 第一天手動建立，尚未套用版本規則
    │   └── model-intel.md
    └── 20261120/                     # 之後開始套用版本規則
        ├── model-intel_20261120_v1.md
        └── manifest.json
```

## 前置需求

- 可使用 Anthropic Claude Scheduler 與 Claude Docs 的 Claude 付費方案
- 本地端：Git，以及可連線本地資料夾的 Claude 桌面版（執行同步任務用）

## License

本專案採用 CC BY 4.0（姓名標示 4.0 國際）授權。

你可以自由分享、修改，也可以商業使用本專案內容，但須標註出處（作者與本 repo 連結），並說明是否有修改。

- 授權範圍僅限本專案自行撰寫的內容（prompt、文件、報告文字）。
- 報告中引用或摘要的第三方內容，著作權仍屬原作者，請依原始來源的條款使用。

## 免責聲明

- 本專案的每日報告由 AI Agent 自動產生，可能含有錯誤、遺漏或過時資訊，僅供參考，請以原始來源為準。
- 本專案內容按「現狀」提供，不提供任何明示或默示的保證。因使用本專案內容而產生的任何損失或後果，作者不負任何責任。
- 報告內容不構成技術選型、採購或投資建議。