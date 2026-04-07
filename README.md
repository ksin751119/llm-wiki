# LLM Wiki

A pattern for building personal knowledge bases using LLMs. See [LLM_WIKI.md](LLM_WIKI.md) for the full idea.

本專案的 skill 參考了 Andrej Karpathy 的 [llm-wiki.md](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 這篇文章，將其中的抽象理念具體實作為可操作的 Claude Code skill。

## 完整使用教學（繁體中文）

**第一次使用？** 請看 [使用教學.md](使用教學.md) — 從安裝 Obsidian 到日常操作，一步一步帶你走完。

---

## llm-wiki-guide Skill

本專案包含一個 Claude Code skill（`llm-wiki-guide.skill`），引導你一步步建立與維護自己的 LLM Wiki。

### 安裝方式

```bash
# 將 skill 壓縮包解壓到 Claude Code 的 skills 目錄
unzip llm-wiki-guide.skill -d ~/.claude/skills/
```

安裝後重啟 Claude Code，skill 將自動被偵測。

### 指令一覽

| 指令 | 說明 |
|------|------|
| `/llm-wiki-guide` | 顯示選單，引導你到正確的步驟 |
| `/llm-wiki-guide:setup` | 初始化新的 wiki（建立目錄、Schema、git init） |
| `/llm-wiki-guide:ingest` | 將新的來源資料吸收到 wiki 中 |
| `/llm-wiki-guide:query` | 對 wiki 提問，可選擇將答案存回 wiki |
| `/llm-wiki-guide:lint` | 對 wiki 進行健康檢查（矛盾、孤立頁面、缺口） |
| `/llm-wiki-guide:status` | 檢查 wiki 狀態並獲得下一步建議 |

### 典型工作流程

```
1. /llm-wiki-guide:setup       ← 執行一次來初始化
2. /llm-wiki-guide:ingest      ← 每新增一個來源就執行
3. /llm-wiki-guide:query       ← 隨時探索你的 wiki
4. /llm-wiki-guide:lint        ← 每約 5 次 ingest 執行一次（skill 會自動提醒）
5. /llm-wiki-guide:status      ← 隨時查看進度
```

---

## Skill 架構說明

### 核心理念（來自 LLM_WIKI.md）

LLM Wiki 的核心概念是：LLM **持續建構並維護一個持久的 wiki**，而非每次查詢都從零開始檢索。知識被編譯一次，然後持續更新，交叉引用已經建好，矛盾已經被標記，綜合分析反映了所有已讀過的資料。

### 三層架構

```
Schema (CLAUDE.md)  ← LLM 行為規則，與使用者共同演化
Wiki   (wiki/)      ← LLM 擁有的 markdown 頁面 + 索引 + 日誌
Raw    (raw/)       ← 不可變的原始文件，由人工策展
```

- **Raw 層**：你策展的原始資料集合（文章、論文、圖片、資料檔）。LLM 只讀不寫，這是你的事實來源。
- **Wiki 層**：LLM 生成的 markdown 檔案目錄。包含摘要、實體頁面、概念頁面、比較、綜覽、綜合分析。LLM 完全擁有這一層。
- **Schema 層**：`CLAUDE.md` 告訴 LLM 這個 wiki 的結構、慣例與工作流程。這是關鍵的設定檔，讓 LLM 成為有紀律的 wiki 維護者。

### 檔案結構

`.skill` 是一個 zip 壓縮包，內含 7 個檔案：

```
llm-wiki-guide/
├── SKILL.md                          # 主入口：子命令路由 + 快速選單
└── references/
    ├── setup-guide.md                # 初始化流程（5 個步驟）
    ├── ingest-guide.md               # 來源吸收流程（6 個步驟 + 檢查點機制）
    ├── query-guide.md                # 查詢流程（7 個步驟，含深度探索模式）
    ├── lint-guide.md                 # 健康檢查流程（8 項檢查）
    ├── writing-standards.md          # 寫作規範（語氣、長度、品質控管）
    └── page-templates.md             # 頁面模板（Summary、Concept、Entity）
```

**各元件職責：**

| 檔案 | 職責 |
|------|------|
| `SKILL.md` | Skill 主入口。定義子命令路由、快速選單、各操作的摘要說明，以及 status 的內聯執行邏輯 |
| `setup-guide.md` | 引導使用者選擇領域與語言，建立目錄結構（`raw/`、`wiki/`），生成量身定做的 Schema（`CLAUDE.md`），初始化 git |
| `ingest-guide.md` | 讀取來源 → 與使用者討論重點 → 建立摘要頁面 → 串聯更新所有相關頁面 → 更新索引、日誌與反向連結。每 15 次吸收觸發品質檢查點 |
| `query-guide.md` | 讀取索引找相關頁面 → 綜合回答（附引用）→ 提供深度探索模式（多輪對話）→ 沉澱洞見 → 可選擇存回 wiki |
| `lint-guide.md` | 執行 8 項健康檢查，生成結構化的健康報告，自動修復可修復的問題，建議後續行動 |
| `writing-standards.md` | 定義百科全書式寫作語氣、頁面長度目標、反塞爆/反薄弱規則、Tensions 格式 |
| `page-templates.md` | 提供 Summary、Concept、Entity 三種頁面的骨架模板 |

---

## 各子命令詳細說明

### setup — 初始化

5 個步驟的引導流程：

1. **詢問領域與語言** — 你的 wiki 主題是什麼？用什麼語言？
2. **選擇 wiki 路徑** — 建議 `~/wiki-{domain}` 或自訂
3. **建立目錄結構** — 建立 `raw/`、`raw/assets/`、`wiki/`，初始化空白的 `index.md`、`log.md`、`_backlinks.json`
4. **生成 Schema** — 根據你的領域量身產生 `CLAUDE.md`，包含目錄結構、頁面命名規則、Ingest/Query/Lint 工作流程、寫作標準、三大維護原則
5. **確認就緒** — 告知下一步是放入來源檔案並執行 ingest

**Schema 三大維護原則：**
- 矛盾出現時必須詢問，不可靜默覆寫
- 僅有單一來源支持的主張使用歸因語氣（「根據 {來源}⋯」）
- 討論時不確定就問，不要假設使用者立場

### ingest — 來源吸收

6 個步驟 + 檢查點機制：

1. **辨識來源** — 列出 `raw/` 中的檔案，或接受使用者貼上的文字/URL
2. **閱讀與擷取** — 讀取完整來源，擷取關鍵主張、實體、概念、與現有 wiki 的矛盾/支持
3. **與使用者討論** — 呈現 5-8 個重點，詢問要強調或跳過的部分
4. **建立摘要頁面** — 依寫作標準寫出 `wiki/summary-{name}.md`（目標 20-40 行）
5. **串聯更新** — 掃描索引找所有相關頁面，逐一更新實體/概念/綜合頁面，標記矛盾並收集到 Tensions 區段
6. **更新索引、日誌與反向連結** — 更新 `index.md`、`_backlinks.json`、`log.md`

**品質關卡（每次更新頁面後檢查）：**
- Anti-Cramming：同一子主題的第 3 段 → 拆分為獨立頁面
- Anti-Thinning：多個來源提及但頁面不到 15 行 → 充實內容
- 長度檢查：超過類型目標範圍 → 考慮拆分

**每 15 次 Ingest 檢查點：** 暫停進行品質審計（新頁面數量、品質檢查、反塞爆審核、重建反向連結）。

### query — 查詢

7 個步驟，含深度探索模式：

1. **理解問題** — 判斷類型：事實查詢、比較、綜合分析、缺口分析
2. **找相關頁面** — 讀取 `index.md` + `_backlinks.json`，高反向連結頁面優先
3. **閱讀與綜合** — 讀取相關頁面，綜合回答並附上引用、信心等級、矛盾、缺口
4. **選擇輸出格式** — 事實 → 簡潔文字、比較 → 表格、綜合 → 結構化分析、缺口 → 清單
5. **深度探索（可選）** — 多輪對話，引用 wiki 頁面為討論素材，主動追問與挑戰
6. **沉澱洞見** — 探索結束後總結 3-5 個關鍵洞見
7. **存回 wiki** — 可選擇將答案或洞見儲存為永久 wiki 頁面

### lint — 健康檢查

執行 8 項檢查：

| # | 檢查項目 | 說明 |
|---|---------|------|
| 1 | 矛盾掃描 | 找出同一事實在不同頁面的不同陳述 |
| 2 | 孤立頁面偵測 | 透過 `_backlinks.json` 找出無入站連結的頁面 |
| 3 | 缺失頁面偵測 | 找出頻繁被提及但沒有獨立頁面的概念/實體 |
| 4 | 過時主張檢查 | 找出只引用舊來源的頁面 |
| 5 | 交叉引用審計 | 確保相關頁面互相連結 |
| 6 | Anti-Cramming/Thinning 審計 | 檢查頁面是否超過或低於長度目標 |
| 7 | 資料缺口分析 | 辨識覆蓋不足的主題，建議尋找新來源 |
| 8 | Tensions 審計 | 驗證矛盾標記是否正確收集到概念頁面的 Tensions 區段 |

檢查完成後生成結構化的健康報告，自動修復可修復的問題（如補充交叉引用），並建議後續行動。

### status — 狀態檢查

無需參考檔案，直接內聯執行：統計頁面與日誌數量、讀取最近 5 筆日誌、讀取索引概覽、報告統計數據、根據狀態建議下一步行動。

---

## 相較 LLM_WIKI.md 原始概念新增的功能

`llm-wiki-guide.skill` 將 [LLM_WIKI.md](LLM_WIKI.md) 的抽象理念具體實作為可操作的流程，並新增了以下功能：

| 新增功能 | 說明 |
|---------|------|
| **Backlinks 系統** | `_backlinks.json` 反向連結索引，用於查詢時優先讀取高連結頁面，也用於孤立頁面偵測 |
| **Tensions & Open Questions** | 概念頁面新增專門區段，集中追蹤跨來源的矛盾與未解問題 |
| **寫作品質控管** | Anti-Cramming（同一子主題第 3 段即拆分）和 Anti-Thinning（多來源提及的主題不可只留空殼）規則 |
| **頁面長度目標** | 每種頁面類型有明確行數範圍（如 Summary 20-40 行、Concept 40-100 行） |
| **15 次吸收檢查點** | 每 15 次 ingest 自動暫停，審計新頁面數量、品質、長度，重建反向連結 |
| **深度探索模式** | Query 的多輪對話探索（Step 5-6），引用 wiki 頁面討論，沉澱洞見後可存回 wiki |
| **8 項 Lint 檢查** | 原版概述 6 項，新增 Anti-Cramming/Thinning 審計和 Tensions 審計 |
| **百科全書式寫作標準** | 明確禁止 AI 腔調、孔雀詞、社論語氣，要求事實陳述、短句、歸因語氣 |
| **頁面模板系統** | Summary、Concept、Entity 三種標準骨架模板 |
| **智慧提醒系統** | 根據 `log.md` 中的操作次數自動建議下一步（第 1 次 ingest 後建議 query、每 5 次建議 lint 等） |
| **Wiki 維護三原則** | Schema 內建三條原則：矛盾必問、標記不確定性、討論時先釐清再假設 |

---

## 智慧提醒

Skill 透過 `log.md` 自動追蹤 wiki 狀態，適時提供建議：

- 第 1 次 ingest 之後 → 建議嘗試 query
- 每 5 次 ingest → 提醒執行 lint
- 每 15 次 ingest → 強制觸發品質檢查點
- 查詢產生有價值的答案 → 詢問是否存為 wiki 頁面
- 吸收時發現矛盾 → 標記並建議 lint
- 探索時發現矛盾 → 無論是否存頁面，都收集到 Tensions 區段
