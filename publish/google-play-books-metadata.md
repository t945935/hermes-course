# Google Play Books · 後設資料表

> 上架入口：https://play.google.com/books/publish/ （Partner Center）
> 檔案需求（官方 2026 現行）：EPUB 3.3 首選（EPUB 3 / EPUB 2 亦可）· **必須通過 EpubCheck 驗證** · 或 PDF
> 建議同時提供 EPUB + PDF 兩種格式（Google 提供兩種閱讀模式）

## 交付檔案清單

| 檔案 | 規格 | 狀態 |
|---|---|---|
| `HermesAgent100Hours.epub` | EPUB 3，已內嵌封面，通過結構驗證 | ✅ 已備妥 |
| `cover.jpg`（另傳用） | JPEG 1600×2400，最小 640px、最大 7200px | ✅ 已備妥 |
| PDF 版（選用，建議補） | 供「原版面」閱讀模式 | ⬜ 未做（需要時可再產） |

- Google 建議上傳命名：`<ISBN>.epub`、`<ISBN>_frontcover.jpg`（無 ISBN 亦可，系統會自動指派）

## 後設欄位建議值

| 欄位 | 建議值 | 說明 |
|---|---|---|
| **Title** | `Hermes Agent 100 小時` | 必填 |
| **Subtitle** | `會用・會聰明用・會開發・做出專案成果` | 與封面文字一致 |
| **Description** | 見下方「書籍簡介（可複製）」 | 商店頁顯示用 |
| **Language** | `繁體中文 (zh-TW)` | 必填 |
| **ISBN / other identifier** | 留空亦可 | 無 ISBN 由系統自動指派；有自有 ISBN 才填 |
| **Format** | `Ebook` | 預設 |
| **Genre / Subject** | BISAC 標準（推薦），最多 **3 個**：<br>1. `COM004000` Computers / Artificial Intelligence / General<br>2. `COM051230` Computers / Programming / Software Development<br>3. `COM060040` Computers / Internet / General | 第一項最重要；Play Store 分類來自 BISAC |
| **Contributors** | Author: `Happy eBook Authors` | 必填 |
| **Age group** | 留空 | 一般技術書不需限制 |
| **Release date** | 留空 = 立即上架 | 或填 `YYYY-MM-DD` 預定日 |
| **Publication date** | `2026-09-14` 或實際出版日 | 書目資訊，不影響上架 |
| **Page count** | 留空 | Google 自動偵測 |
| **Rights** | 版權已確認，非公版 | Partner Center 內勾選 |

## 上架步驟（摘要）
1. Partner Center → **Add New Book**
2. 填後設欄位（對照上表）
3. Content 頁上傳 `HermesAgent100Hours.epub`（＋ `cover.jpg`，名稱建議 `ISBN_frontcover.jpg`）
4. 設定價格與銷售區域（依你的意願）
5. Submit → 等 Google 審查（EpubCheck + 內容審核）

## 書籍簡介（可複製）

> Hermes Agent 不是聊天機器人，而是一個會自我改進的 AI agent——它能讀檔案、跑指令、上網、記住你、自動化任務。本書把 Hermes 官方文件重新編排成一套「由淺入深、每小時一個單元、邊讀邊做」的課程：18 章、100 小時，從安裝、對話、工具、記憶、技能、自動化排程，一路做到外掛開發與開源貢獻。每節遵循「閱讀 → 動手做 → 驗收」三步驟，最後以一個完整期末專題驗收所學。附錄收錄作者實際走完 100 小時課程的 24 份實作筆記——中文世界第一本 Hermes Agent 完整學習實錄。