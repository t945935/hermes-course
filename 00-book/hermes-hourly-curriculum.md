# Hermes Agent 逐小時課程表（87 小時：從入門到會開發）

> 將官方文件拆成 87 個「1 小時可完成」的單元。
> 每單元 = 讀一段官方文件 + 動手做 + 驗收。
> 節奏建議：每天 2h → 約 6-7 週；每天 8h → 約 2 週。

**圖例**：🖥️ 在終端操作 ｜ 📖 讀官方文件 ｜ 🧪 實驗比較 ｜ ✍️ 產出檔案

---

# 課程一：會用（H1-H10）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H1 | Hermes 是什麼 + 環境檢查 | 🖥️ `git --version`、`uname -r` 確認 WSL2；📖 讀 Installation 首頁段落 | 能說出 Hermes 與一般 chatbot 的 3 個差異 |
| H2 | 安裝 + 健康檢查 | 🖥️ `curl -fsSL https://hermes-agent.nousresearch.com/install.sh \| bash`；`source ~/.bashrc`；`hermes doctor` | doctor 無 ✗；能解釋 2 個 ⚠ |
| H3 | Provider 設定 + 第一次對話 | 🖥️ `hermes setup --portal`（OAuth）；`hermes` 問「你是誰」 | 完成一次真實對話 |
| H4 | 三種對話模式 | 🖥️ 互動模式 / `hermes -z "..."` / `hermes --resume` 續接；試 3 個斜線指令 | 隨機抽考能正確選用模式 |
| H5 | CLI 子指令巡禮 | 🖥️ 逐一跑 `hermes model/tools/config get/sessions/status`，記錄輸出 | 不看文件列得出 8 個子指令用途 |
| H6 | TUI 操作 | 🖥️ 練習切換輸入/歷史捲動/快捷鍵 | 能完成一次純 TUI 工作流 |
| H7 | config.yaml 解析 | 📖 Configuration；🖥️ 開 `~/.hermes/config.yaml` 標出 model/provider/tools 區塊 | 能指出任一選項在檔案哪一節 |
| H8 | 模型切換實驗 | 🖥️ `hermes model` 換第二個模型；🧪 比較同一問題的回答風格 | 能用一句話描述兩模型差異 |
| H9 | 工具與授權機制 | 📖 Tools & Toolsets；🖥️ `hermes tools` 巡邏 10 個工具 | 能預測指令執行前是否需授權 |
| H10 | 程式碼執行 | 🖥️ 給 Hermes 一份 CSV，叫它用 `execute_code` 分析 | 拿到正確的分析結果 |

**🏁 課程一 checkpoint**：能用 Hermes 完成一個日常任務並解釋過程。

---

# 課程二：會進階（H11-H43）

## 主題 A｜Sessions 與 Context（H11-H14）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H11 | Session 管理 | 🖥️ 建 3 個主題 session，練習列出/續接 | 能說出 session 生命週期 |
| H12 | Context Files | 🖥️ 在你的專案資料夾跑 `hermes`，把一份文件設為 context | 它能回答該文件內容問題 |
| H13 | 有無 context 對比 | 🧪 同一問題「有餵/沒餵」各答一次 | 記錄並說明品質差異 |
| H14 | Context 策略設計 | ✍️ 寫出你工作區的 context 策略清單（常駐/一次性） | 有明確策略文件 |

## 主題 B｜Memory（H15-H19）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H15 | 記憶原理 | 📖 Memory 系統；🖥️ 看記憶存放位置 | 能說明記憶 vs session 差別 |
| H16 | 寫入與驗證 | 🖥️ 告訴它 3 件事 → 開新 session 確認還記得 | 跨 session 記憶成功 |
| H17 | 記憶治理 | 🖥️ 練習查/增/刪一筆記憶（含故意造錯再刪） | 能獨立治理記憶 |
| H18 | 學習循環觀察 | 🧪 讓它完成任務並記錄它如何沉澱經驗 | 說得出「經驗→記憶/技能」流程 |
| H19 | 進階記憶 | 📖 Memory Providers；🖥️ 認識 Honcho | 能說明內建 vs 外部記憶差異 |

## 主題 C｜Skills（H20-H25）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H20 | Skills 目錄巡禮 | 🖥️ `hermes skills list` 逛 58 個內建技能分類 | 能說出 5 個分類各舉 1 例 |
| H21 | 啟用內建技能 | 🖥️ 啟用 systematic-debugging 並實際觸發一次 | 技能被正確載入與使用 |
| H22 | 安裝社群技能 | 🖥️ 從 agentskills.io 安裝 1 個 | 安裝後可觸發 |
| H23 | 有/無技能對比 | 🧪 同一任務「有技能 vs 無技能」 | 記錄品質差異並下結論 |
| H24 | 技能管理 | 🖥️ 停用/更新/刪除一個技能 | 全部操作無錯誤 |
| H25 | 概念總結 | ✍️ 寫一張「工具 vs 技能 vs 記憶」對照表 | 對照表完成 |

## 主題 D｜Cron 自動化（H26-H30）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H26 | Cron 原理 | 📖 Cron 文件；理解 expression 語法 | 能解釋 5 個 expression |
| H27 | 第一個 Cron | 🖥️ 定時輸出任務到 CLI | 任務準時執行 |
| H28 | 每日摘要專案 | 🖥️ 建「追蹤 2 個網站 → 摘要」任務 | 摘要如期產出 |
| H29 | 除錯演練 | 🖥️ 故意設錯 expression，用 doctor/logs 修復 | 能自己定位錯誤 |
| H30 | Script-only 模式 | 📖 cron-script-only；🖥️ 跑純腳本任務 | 純腳本 cron 成功 |

## 主題 E｜訊息平台 Bot（H31-H36）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H31 | Gateway 概念 + 建 bot | 📖 Messaging + Telegram；🖥️ BotFather 建立 bot | 拿到 token |
| H32 | 連線與手機測試 | 🖥️ 寫入 `~/.hermes/.env`，`hermes gateway start`，手機傳訊 | 手機→Hermes 通話成功 |
| H33 | 常駐服務 | 🖥️ `hermes gateway install`，重啟後驗證 | 重開機仍運作 |
| H34 | 遠端工具呼叫 | 🖥️ 在手機叫它查天氣/跑指令 | 工具經由手機觸發成功 |
| H35 | 權限控制 | 🖥️ 限制 bot 只回應你 | 他人訊息被拒絕 |
| H36 | 整合練習 | 🖥️ 把 H28 的摘要投遞到 Telegram | 手機收到自動摘要 |

## 主題 F｜安全性（H37-H39）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H37 | 風險模型 | 📖 Security；🖥️ 檢視授權模式設定 | 能寫出「信任/不信任清單」第一版 |
| H38 | 危險演練 | 🖥️ 模擬 `rm -rf` 場景，觀察確認流程；設黑名單 | 危險指令無法無聲通過 |
| H39 | Secrets 管理 | 🖥️ 檢查 `.env` 權限；📖 認識 1Password/Bitwarden 串接 | 確認 `.env` 僅本人可讀 |

## 主題 G｜MCP（H40-H43）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H40 | MCP 概念 + 設定 | 📖 MCP 文件；🖥️ 設定 1 個熱門 server | 工具出現在清單且可呼叫 |
| H41 | 工具過濾 | 🖥️ 只開放該 server 的部分工具 | 過濾生效 |
| H42 | 自寫 MCP server | 🖥️ 寫一個 hello-world MCP server 連進 Hermes | 自寫工具被呼叫 |
| H43 | MCP 安全檢視 | 🖥️ 檢視 server 信任設定；✍️ 安全筆記 | 能說明風險與防護 |

**🏁 課程二 checkpoint**：部署過 bot + cron + 至少 1 個技能，並能治理記憶。

---

# 課程三：會開發（H44-H87）

## 主題 H｜架構深入（H44-H51）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H44 | 原始碼導覽 | 📖 Architecture；🖥️ 逛 `~/.hermes/hermes-agent` 目錄 | 能說出核心模組位置 |
| H45 | Agent Loop 追蹤 | 🖥️ 找到主迴圈程式碼，畫出流程 | 能指出迴圈起點 |
| H46 | Prompt 組裝 | 🖥️ 追蹤 prompt assembly 流程 | 知道 system prompt 從哪拼接 |
| H47 | Provider Runtime | 🖥️ 追蹤一次 LLM 呼叫的程式路徑 | 能說出 provider 抽象 |
| H48 | 工具呼叫鏈 | 🖥️ 追蹤工具從定義→授權→執行的程式碼 | 能畫出呼叫鏈 |
| H49 | Session 儲存結構 | 🖥️ 解析 session 儲存格式 | 能讀懂一筆原始訊息 |
| H50 | 畫架構圖 | ✍️ 輸出你自己的架構圖（含 6 大元件） | 圖可向人講解 |
| H51 | 架構小考 | ✍️ 不開檔，寫出「一次對話的程式旅程」 | 200 字完整說明 |

## 主題 I｜Skill 開發（H52-H59）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H52 | 規格精讀 | 📖 Creating Skills + skill-authoring 範例 | 能說出 SKILL.md 必填欄位 |
| H53 | 主題設計 | ✍️ 選定你的 skill 主題與目標 | 1 頁設計稿 |
| H54 | 寫 SKILL.md | ✍️ 完成 SKILL.md + 流程步驟 | 檔案符合規格 |
| H55 | 安裝觸發 | 🖥️ `hermes skills` 安裝並觸發 | 技能成功運作 |
| H56 | 打磨 | 🧪 依官方檢查表逐項自評修正 | 檢查表全勾 |
| H57 | 自改進實驗 | 🧪 讓 Hermes 在使用中改進此 skill，觀察 diff | 能解釋它改什麼、為何 |
| H58 | 分享（選） | 🖥️ 上傳 Skills Hub / GitHub | 得到分享連結 |
| H59 | 技能開發複習 | ✍️ 寫一篇「如何寫好 skill」筆記 | 筆記含 5 條原則 |

## 主題 J｜Plugin 開發（H60-H69）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H60 | Plugin 概念 | 📖 Plugins 總覽 + 官方最小範例 | 能說出 plugin 與 skill 差別 |
| H61 | Hello-world Plugin | 🖥️ 照範例建立並安裝你的第一個 plugin | `hermes` 能呼叫它的工具 |
| H62 | 參數與錯誤處理 | 🖥️ 加第二個工具：含參數、try/except | 錯誤輸入有友善訊息 |
| H63 | 串接外部 API | 🖥️ 選一個公開 API 做成工具 | API 資料正確回傳 |
| H64 | Config Schema | 🖥️ 讓工具參數可被使用者設定 | 設定後行為改變 |
| H65 | 邊界案例 | 🧪 測空值/超時/斷線等 5 個邊界 | 全部有處理 |
| H66 | 寫測試 | 🖥️ 為 plugin 寫 3 個單元測試並跑綠 | 測試全過 |
| H67 | 寫文件 | ✍️ README：安裝/設定/範例 | 陌生人照文件能用 |
| H68 | 打包分發 | 🖥️ 打包並在本機「乾淨環境」安裝驗證 | 安裝流程無痛 |
| H69 | Plugin 總結 | ✍️ 把 H59 筆記延伸成「plugin vs skill 選擇指南」 | 指南完成 |

## 主題 K｜Provider 與部署（H70-H77）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H70 | 本地模型概念 | 📖 Local Models + Ollama 指南 | 知道接本地模型的理由 |
| H71 | Ollama 接線 | 🖥️ 安裝 Ollama，把 Hermes 指向本地模型 | 本地模型對話成功 |
| H72 | 模型比較實驗 | 🧪 同一任務雲端 vs 本地各做一次 | 記錄品質/速度/成本三維比較 |
| H73 | Docker 部署 | 🖥️ 用 Docker 跑一個 Hermes 實例 | container 內 agent 可對話 |
| H74 | SSH 後端 | 🖥️ 練習把 agent 跑在另一台機器 | 遠端後端成功 |
| H75 | Serverless（選） | 🖥️ 認識 Daytona/Modal | 說得出使用場景 |
| H76 | 成本分析 | ✍️ 算一份「雲端 vs 本地 vs serverless」成本對照 | 有明確結論 |
| H77 | 部署決策總結 | 🧪 給 3 個情境各自選方案並說明理由 | 決策合理可辯護 |

## 主題 L｜貢獻開源（H78-H87）

| 時 | 單元 | 動手做 | 驗收 |
|---|---|---|---|
| H78 | 貢獻規範 | 📖 Contributing 文件 | 能說出 PR 要求清單 |
| H79 | 本機測試 | 🖥️ 在 `~/.hermes/hermes-agent` 跑 `scripts/run_tests.sh` | 測試可執行且看懂結果 |
| H80 | 挑 Issues | 🖥️ 從 GitHub Issues 選 1 個 good-first-issue | 確定題目與範圍 |
| H81 | 動手修 bug | 🖥️ 修復並本機驗證 | bug 被實際修掉 |
| H82 | 補測試 | 🖥️ 為修正寫測試防回歸 | 測試覆蓋該案例 |
| H83 | Commit 規範 | 🖥️ 寫出符合 repo 風格的 commit message | message 通過自我 review |
| H84 | 開 PR | 🖥️ 建立含描述與測試的 PR | 拿到 PR 網址 |
| H85 | Review 修正 | 🖥️ 針對意見修改並回應 | 對話串完整收斂 |
| H86 | 社群參與 | 📖 逛 Discord / GitHub Discussion 回 1 則問題 | 完成第一次互動 |
| H87 | 結業總複習 | ✍️ 自評能力矩陣（✅/🟡/❌）+ 90 天路線圖 | 矩陣 + 路線圖完成 |

**🏁 課程三 checkpoint**：發出過 1 個被 review 的 PR（合併與否皆可）。

---

# 期末專題（選做，H88-H97，共 10h）

| 時 | 內容 |
|---|---|
| H88-89 | 選題 + 設計（個人自動化助理 / 團隊協作助理 / 產品化外掛） |
| H90-93 | 核心功能建置（bot + cron + skill/plugin + 記憶） |
| H94-95 | 安全性 + 文件 + 架構圖 |
| H96 | 除錯與打磨（用 doctor/logs） |
| H97 | 結案簡報（對自己或朋友 demo） |

**自評清單**：使用 ≥3 種功能｜有安全設定｜有設計文件｜能自行除錯。

---

# 一站速查

| 課程 | 時數 | 單元涵蓋 |
|---|---|---|
| 課程一 會用 | H1-H10（10h） | 安裝→對話→CLI→設定→工具 |
| 課程二 會進階 | H11-H43（33h） | Sessions/Memory/Skills/Cron/Bot/安全/MCP |
| 課程三 會開發 | H44-H87（44h） | 架構/Skill/Plugin/部署/貢獻 |
| 期末專題 | H88-H97（10h） | 整合專案 |

**最低可行路徑（60h）**：H1-H10 全做 → 主題 B/C/D（H15-H30）→ 主題 I/J（H52-H69）→ 結業自評。跳過 bot、MCP、部署、貢獻，之後需要再回頭補。