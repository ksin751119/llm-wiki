# LLM Wiki Guide Skill v2 — Design Spec

> Date: 2026-04-07
> Status: Draft
> Scope: llm-wiki-guide.skill 三項優化

## Background

對比參考系統 `reference/llm-knowledge-base`（7 個 slash commands、4 層架構、origin-aware compilation）與現有 `llm-wiki-guide.skill`（5 個子命令、3 層架構、_backlinks.json），識別出可借鏡的優勢功能。

經討論後確定 3 項變更，排除了 origin 二分（不必要的摩擦）、format conversion（投入產出比低）、獨立 explore 子命令（與 query 合併更自然）。

## Change 1: Query 升級為三階段流程

### 問題

現有 query 是一問一答。對話中的有價值討論結束後消失，無法沉澱回 wiki。使用者需要的不只是答案，而是深化理解的過程。

### 設計

將 query-guide.md 的 5 步改為 7 步。原 Step 1-4 保留不動，原 Step 5 拆成 3 個新步驟：

**Step 5: 追問深入（新增）**

回答完後追加：「想繼續深入這個方向嗎？我可以幫你進一步探索。」

- 使用者說「不用」→ 跳到 Step 7
- 使用者繼續 → 進入對話探索模式：
  - 引用 wiki 頁面作為討論素材
  - 發現矛盾時明確指出
  - 主動追問，不只被動回答
  - 持續直到使用者滿意或自然結束

**Step 6: 洞見整理（新增）**

對話探索結束後：

1. 總結對話中的 3-5 個關鍵洞見（一句話一個）
2. 標記哪些跟既有 wiki 有矛盾
3. 呈現給使用者確認

只在 Step 5 進入探索模式時觸發。使用者在 Step 5 說「不用」則跳過。

**Step 7: 存回 wiki（擴充原 Step 5）**

- 只有答案（沒探索）→ 問要不要存答案為頁面（原行為）
- 有洞見整理 → 問：「要把這些洞見存為 wiki 頁面嗎？」
  - 是 → 寫頁面（通常 `synthesis-*`）、更新 index/log/backlinks。如果洞見包含矛盾，歸集到相關 concept 頁面的 `## Tensions & Open Questions` 區段（見 Change 2）
  - 否 → 結束。但如果對話中發現了矛盾，仍然歸集到相關 concept 頁面的 Tensions 區段（矛盾記錄不依賴使用者是否選擇存頁面）

**log.md 格式：**
- 純問答：`## [{date}] query | {question summary}`（不變）
- 有探索：`## [{date}] query+explore | {topic summary}`（新標記）

**Smart Reminders 新增：**

| 條件 | 提示 |
|------|------|
| 對話探索產生了矛盾 | 「發現 {N} 個矛盾，建議跑 `/llm-wiki-guide:lint`」 |
| 對話探索但選擇不存 | 「沒關係。如果之後想回顧，下次可以再問類似的問題。」 |

### 向下相容

不想探索的使用者在 Step 5 說「不用」，體驗與 v1 完全一致。

### 受影響檔案

- `references/query-guide.md` — 重寫（加 Step 5-7、更新 Post-Query Reminders）
- `SKILL.md` — query 描述更新、Smart Reminders 表格新增 2 行

---

## Change 2: Concept 頁面加入 Tensions & Open Questions

### 問題

矛盾散落在各 summary 頁面的 `> **Contradiction:**` 標記中，讀者需要逐頁翻找才能看到全貌。缺乏一個集中的地方呈現同一概念下的所有矛盾和未解問題。

### 設計

**Concept 頁面新增固定區段：**

```markdown
concept-xxx.md
├── 一句話摘要（首行）
├── ## Overview
├── ## Key Points（按主題分段）
├── ## Tensions & Open Questions    ← 新增
└── ## Cross-References
```

**每條 tension 的格式：**

```markdown
## Tensions & Open Questions

- **{簡述矛盾}** — {來源A} 認為 X，但 {來源B} 認為 Y。
  （見 [summary-a](summary-a.md)、[summary-b](summary-b.md)）

- **{未解問題}** — 目前 wiki 缺乏足夠資料判斷 Z，需要更多來源。
```

**規則：**
- 每條一個矛盾或一個未解問題，不混在一起
- 必須附來源連結
- 已解決的 tension 移除（解決過程記在 log.md）
- 沒有 tension 時寫 `*目前無已知矛盾。*`，不刪除區段

**觸發來源（3 種）：**
1. Ingest 時發現新來源與既有內容衝突
2. Query 探索時對話中發現的矛盾
3. Lint 時掃描出的不一致

### Ingest 流程變更

`references/ingest-guide.md` Step 5 Cascade Update，在「Flag contradictions」之後加一步：

> **歸集 Tensions：** 標記了 `> **Contradiction:**` 時，同時將矛盾摘要寫入相關 concept 頁面的 `## Tensions & Open Questions`。一個矛盾可能影響多個 concept 頁面。

原有的行內 `> **Contradiction:**` 標記保留——它在 summary 頁面標記衝突點。Tensions 區段是歸集，把散落的矛盾集中到 concept 頁面。

### Lint 流程變更

`references/lint-guide.md` 新增第 8 項檢查：

> **8. Tensions Audit**
> - 掃描所有 `> **Contradiction:**` 標記，確認每條都已歸集到對應 concept 頁面 Tensions 區段
> - 檢查 Tensions 條目是否仍有效（來源頁面還在、矛盾未被後續來源解決）
> - Action: 補漏歸集、移除已解決的 tension

Lint Report Format 新增一節：

```
## Tensions ({N})
1. {concept-page} — {N} unresolved tensions
2. {N} contradictions not yet collected into Tensions sections
```

### Writing Standards 變更

`references/writing-standards.md` Structure Rules 新增：

> - Concept 頁面必須包含 `## Tensions & Open Questions` 區段，位於 Cross-References 之前
> - 即使無矛盾也保留此區段（寫 `*目前無已知矛盾。*`）

Length targets 不變（concept 40-100 lines），Tensions 計入總行數。

### 受影響檔案

- `references/writing-standards.md` — Structure Rules 新增 2 條
- `references/ingest-guide.md` — Step 5 加一步
- `references/lint-guide.md` — 加第 8 項檢查 + report format
- `references/setup-guide.md` — Schema 模板 concept 頁面說明更新

---

## Change 3: Schema 模板加入 Wiki Maintenance Principles

### 問題

現有 Schema 模板（setup-guide.md 的 Step 4）定義了結構和流程，但沒有定義 LLM 維護 wiki 時的行為規範。導致 LLM 可能靜默覆蓋舊資訊、把單一來源寫成定論、或在不確定使用者意圖時自行假設。

### 設計

在 Schema 模板的 `## Conventions` 之後新增：

```markdown
## Wiki Maintenance Principles

1. **發現矛盾時問，不靜默覆蓋**
   新來源與既有 wiki 內容衝突時，標記 `> **Contradiction:**` 並歸集到
   相關 concept 頁面的 Tensions 區段。不要靜默用新資訊覆蓋舊資訊。
   如果無法判斷哪邊正確，問使用者。

2. **標記不確定性**
   只有單一來源支持的主張，用歸因句式：「According to {source}, ...」
   不寫成定論。多來源交叉驗證的主張才用斷言句式。

3. **Ingest 討論時追問到清楚**
   討論來源的關鍵要點時，如果不確定使用者想強調什麼、
   或對某個觀點的態度，追問。不自行假設使用者的立場。
```

**只有 3 條，理由：**
- 都直接影響 wiki 內容品質
- 通用互動原則使用者可自行加在 CLAUDE.md 別處
- 少即是多，LLM 更容易遵守

**Setup 流程調整：**

Step 4 生成 Schema 後確認時，額外說明：

> 「Schema 包含 3 條 wiki 維護原則。如果你有自己偏好的互動方式，可以在 CLAUDE.md 中自由新增。」

### 受影響檔案

- `references/setup-guide.md` — Schema 模板新增區段 + Step 4 確認話術

---

## File Impact Summary

| 檔案 | 動作 | 變更摘要 |
|------|------|---------|
| `SKILL.md` | 修改 | query 描述更新 + Smart Reminders 新增 2 行 |
| `references/query-guide.md` | 修改 | 5 步 → 7 步（加 Phase 2 追問 + Phase 3 沉澱） |
| `references/ingest-guide.md` | 修改 | Step 5 加 Tensions 歸集步驟 |
| `references/writing-standards.md` | 修改 | Structure Rules 加 Tensions 區段規範 |
| `references/setup-guide.md` | 修改 | Schema 模板加互動原則 + concept 說明 |
| `references/lint-guide.md` | 修改 | 加第 8 項 Tensions Audit |

不新增任何檔案。不刪除任何檔案。

## Risk Assessment

| 變更 | 改動量 | 風險 |
|------|--------|------|
| Query 升級 | 中 | 低 — 向下相容，不想探索的使用者體驗不變 |
| Tensions & Gaps | 中 | 低 — 新增區段，不改既有結構 |
| 互動原則 | 小 | 極低 — 只影響新建 wiki 的 Schema 模板 |
