# Hermes Agent 學習教材大綱（由淺至深）

> 教材來源：https://hermes-agent.nousresearch.com/docs（官方文件，含簡中版）
> 本大綱把官方文件重新編排成「課程」，每單元附閱讀資料 + 實作練習 + 驗收標準。
> 時數以「邊讀邊做」估算；純閱讀約除以 3。

---

## 學習總覽

| 課程 | 定位 | 單元 | 時數 | 產出能力 |
|---|---|---|---|---|
| 課程一 | 會用（初級） | 0-4 | ~10h | 獨立操作 Hermes 完成日常任務 |
| 課程二 | 會進階功能（中級） | 5-11 | ~33h | 部署 bot、自動化、擴充技能 |
| 課程三 | 會開發（進階） | 12-16 | ~44h | 開發 plugin / 技能、貢獻開源 |
| 期末專題 | 整合應用 | — | ~10h | 一個真實專案作品 |

**建議投入順序**：課程一全做 → 課程二挑 Memory / Skills / Cron → 課程三只學 Skill / Plugin 開發，約 60h 即達進階使用者水準。

---

# 課程一：會用（初級） ~10 小時

## 單元 0｜安裝與環境準備（1.5h）

**學習目標**
- 了解 Hermes Agent 是什麼、能裝在哪
- 完成 WSL2 安裝並通過健康檢查

**閱讀材料**
- Installation：`/docs/getting-started/installation`
- Platform Support：`/docs/getting-started/platform-support`
- WSL2 Guide：`/docs/user-guide/windows-wsl-quickstart`

**實作練習**
1. 確認環境：`git --version`、`curl --version`、`uname -r`（須為 WSL2）
2. 執行官方安裝：`curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash`
3. 重新載入 shell：`source ~/.bashrc`
4. 確認版本：`hermes --version`（應顯示 v0.21+）
5. 健康檢查：`hermes doctor`——試著解讀每一行 ✓/⚠ 的意思

**驗收**：`hermes doctor` 沒有 ✗ 級錯誤；能說出 3 個 ⚠ 的原因與修法。

---

## 單元 1｜第一次對話 Quickstart（2h）

**學習目標**
- 設定 LLM provider 並完成人生第一次對話
- 熟悉 Hermes 會話的基本型態

**閱讀材料**
- Quickstart：`/docs/getting-started/quickstart`
- Nous Portal 整合：`/docs/integrations/nous-portal`

**實作練習**
1. 執行 `hermes setup --portal`（一次 OAuth 搞定模型 + 搜尋/圖片/TTS/瀏覽器）
2. 啟動互動 CLI：`hermes`，問它「你是誰、你能做什麼」
3. 用單行指令模式：`hermes -z "用三句話介紹 Hermes"`
4. 問一個需要工具的問題（例如：「查一下現在台幣對日圓匯率」），觀察它如何呼叫 web search
5. 開新 session 繼續同一話題，練習 `/help` 與斜線指令

**驗收**：能完成一次「需要工具」的對話並描述過程；知道 `-z` / 互動模式 / session 的差異。

---

## 單元 2｜CLI 操作（2h）

**學習目標**
- 熟悉常用子指令與 TUI 操作

**閱讀材料**
- CLI Usage：`/docs/user-guide/cli`
- TUI 介面：`/docs/user-guide/tui`
- CLI Reference（當字典查）：`/docs/reference/cli-commands`

**實作練習**
1. 逐一執行並記錄輸出：`hermes model`、`hermes tools`、`hermes config get`、`hermes sessions`、`hermes status`
2. 練習 session 管理：開新 session → 對話 → 列出 → 續接（`hermes --resume <name>`）
3. 用 `hermes --help` 找出 3 個你沒用過的旗標，實測其中 1 個
4. 練習 TUI 快速鍵（切換輸入/輸出、捲動歷史）

**驗收**：不看文件能說出 8 個以上子指令各自用途；能續接昨天的工作。

---

## 單元 3｜設定與模型（2h）

**學習目標**
- 看懂 config.yaml 與 .env 的分工
- 能切換模型與 provider

**閱讀材料**
- Configuration：`/docs/user-guide/configuration`
- Configuring Models：`/docs/user-guide/configuring-models`
- Providers：`/docs/integrations/providers`

**實作練習**
1. 開啟 `~/.hermes/config.yaml`，找出並說明 model / provider / tools 區塊
2. 檢視 `~/.hermes/.env`，確認哪些 API key 已設定（**不要把 key 貼出來**）
3. `hermes model` 切換到第二個模型，觀察回答風格差異
4. `hermes config set` 改一個選項，用 `hermes config get` 確認生效
5. 手動編輯 config 加入一個新 provider 設定，壞掉時用 `hermes doctor --fix` 修復

**驗收**：能獨立新增一個 provider；知道改設定後要驗證的流程。

---

## 單元 4｜基礎工具實作（3h）

**學習目標**
- 認識 60+ 內建工具的分類與授權機制

**閱讀材料**
- Tools & Toolsets：`/docs/user-guide/features/tools`
- Toolsets Reference：`/docs/reference/toolsets-reference`
- Code Execution：`/docs/user-guide/features/code-execution`

**實作練習**
1. `hermes tools` 列出工具，挑 10 個常用的分類記下來
2. 對話中實測：檔案讀寫、終端指令執行、程式碼執行（python）
3. 練習 `execute_code`：叫 Hermes 寫一段 Python 處理你給的 CSV
4. 測試工具的「需授權」行為：指令執行前是否詢問你？練習同意/拒絕
5. 關閉一個你不用的工具，確認對話中不再出現

**驗收**：能預期哪些工具會被呼叫、哪些需要授權；能自己開關工具集。

---

# 課程二：會進階功能（中級） ~33 小時

## 單元 5｜Sessions 與 Context Files（4h）

**學習目標**
- 理解 session 生命週期與續接機制
- 用 context files 餵專案內容給 Hermes

**閱讀材料**
- Sessions：`/docs/user-guide/sessions`
- Context Files：`/docs/user-guide/features/context-files`
- Context References：`/docs/user-guide/features/context-references`

**實作練習**
1. 建立 3 個不同主題的 session，練習跨 session 與續接
2. 在同一個資料夾跑 `hermes`，確認它自動帶入該專案的 context
3. 手動把一份文件設為 context file，問 Hermes 關於該文件的問題
4. 比較「有餵 context」與「沒餵 context」的回答品質差異
5. 練習刪除/封存舊 session

**驗收**：能設計自己的工作區 context 策略（哪些檔該常駐、哪些該一次帶入）。

---

## 單元 6｜Memory 系統（5h）

**學習目標**
- 理解 Hermes 的跨 session 記憶機制與限制

**閱讀材料**
- Memory：`/docs/user-guide/features/memory`
- Memory Providers：`/docs/user-guide/features/memory-providers`
- Honcho：`/docs/user-guide/features/honcho`

**實作練習**
1. 告訴 Hermes 3 件你的事（語言偏好、工作、常用工具）
2. 開新 session 確認它還記得（驗證記憶生效）
3. 用 `hermes memory`（或對應指令）手動檢視/新增一筆記憶
4. 故意餵一筆錯誤記憶，練習刪除
5. 觀察「學習循環」：讓它執行一個任務並記錄它如何把經驗寫成技能或記憶

**驗收**：能解釋記憶儲存在哪、如何手動治理（查/增/刪）。

---

## 單元 7｜Skills 系統（6h）

**學習目標**
- 理解 skills = agent 的程序性記憶
- 會安裝、啟用、編寫基礎 skill

**閱讀材料**
- Skills：`/docs/user-guide/features/skills`
- Work with Skills：`/docs/guides/work-with-skills`
- Creating Skills：`/docs/developer-guide/creating-skills`（閱讀即可，實作在課程三）
- Skills Catalog：`/docs/reference/skills-catalog`

**實作練習**
1. `hermes skills list` 列出已安裝的 58 個內建技能，逛一圈分類
2. 啟用 1 個技能，實際觸發它（例如 systematic-debugging 或 test-driven-development）
3. 到 Skills Hub（agentskills.io）安裝 1 個社群技能
4. 對同一個任務「有技能 vs 無技能」各做一次，記錄品質差異
5. 用 `hermes skills` 管理：停用、更新、刪除

**驗收**：能說出技能與一般工具/記憶的差別；能自行安裝並驗證一個技能。

---

## 單元 8｜Cron 自動化（5h）

**學習目標**
- 學會排程任務並投遞到指定頻道

**閱讀材料**
- Cron：`/docs/user-guide/features/cron`
- Automate with Cron：`/docs/guides/automate-with-cron`
- Cron Troubleshooting：`/docs/guides/cron-troubleshooting`

**實作練習**
1. 建立第一個 cron 任務：每天定時輸出一句話到 CLI
2. 建立「每日摘要」cron：蒐集你關注的 2 個 RSS/rss 或網站，整理成摘要
3. 練習暫停（pause / resume）與刪除 cron
4. 故意設定錯誤的 cron expression，練習用 `hermes doctor` / logs 除錯
5. （加分）用 cron-script-only 模式跑純腳本任務：`/docs/guides/cron-script-only`

**驗收**：能設計一套自己的自動化流程（例如每日早晨簡報）。

---

## 單元 9｜訊息平台 bot（6h）

**學習目標**
- 把 Hermes 部署成 Telegram / Discord bot，隨時用手機呼叫

**閱讀材料**
- Messaging Overview：`/docs/user-guide/messaging/`
- Telegram Setup：`/docs/user-guide/messaging/telegram`
- Discord Setup：`/docs/user-guide/messaging/discord`
- Gateway：`/docs/user-guide/features/tool-gateway`（若用 gateway 服務）

**實作練習**
1. 用 BotFather 建立 Telegram bot 取得 token，寫入 `~/.hermes/.env`
2. 啟用 gateway：`hermes gateway start`，用手機傳訊息測試
3. 設定 gateway 為常駐服務（`hermes gateway install`），重開機後驗證仍運作
4. 在 Telegram 裡叫它執行一個工具任務（例如查天氣）
5. 練習權限控制：限制 bot 只能回應你
6. （加分）把單元 8 的 cron 摘要投遞到 Telegram

**驗收**：Hermes 能在你不在電腦前時透過手機正常運作。

---

## 單元 10｜安全性（3h）

**學習目標**
- 理解 agent 的風險模型，學會保護自己

**閱讀材料**
- Security：`/docs/user-guide/security`
- Secure on a Work Machine：`/docs/guides/secure-hermes-on-a-work-machine`
- Secrets（Bitwarden/1Password）：`/docs/user-guide/secrets/index`

**實作練習**
1. 檢視你目前的授權模式（command approval 設定）並說明風險
2. 演練：叫 Hermes 執行 `rm -rf` 等級的危險指令，觀察它如何要求授權
3. 設定一組危險指令黑名單或確認規則
4. 檢視 `~/.hermes/.env` 權限（`ls -l`，應只有你能讀）
5. （加分）串接 1Password / Bitwarden secrets

**驗收**：能寫出「你信任 Hermes 做什麼、不信任做什麼」的清單並落實到設定。

---

## 單元 11｜MCP 整合（4h）

**學習目標**
- 學會用標準 MCP 協定擴充 Hermes 工具

**閱讀材料**
- MCP：`/docs/user-guide/features/mcp`
- Use MCP with Hermes：`/docs/guides/use-mcp-with-hermes`
- MCP Config Reference：`/docs/reference/mcp-config-reference`

**實作練習**
1. 找一個熱門 MCP server（例如 filesystem 或 GitHub），設定進 Hermes
2. 驗證工具出現在工具清單，實際對話呼叫一次
3. 練習 MCP 工具過濾（只開放部分工具）
4. 自己寫一個「hello world」MCP server（用任何語言），連進 Hermes
5. 檢視 MCP 安全設定（哪些 server 可信任）

**驗收**：能獨立設定、過濾、驗證一個 MCP server。

---

# 課程三：會開發（進階） ~44 小時

## 單元 12｜架構深入（8h）

**學習目標**
- 理解 agent loop、prompt 組裝、provider runtime

**閱讀材料**
- Architecture：`/docs/developer-guide/architecture`
- Agent Loop：`/docs/developer-guide/agent-loop`
- Prompt Assembly：`/docs/developer-guide/prompt-assembly`
- Provider Runtime：`/docs/developer-guide/provider-runtime`

**實作練習**
1. 閱讀 `~/.hermes/hermes-agent` 原始碼，找到 agent loop 的主迴圈
2. 用 debug 工具追蹤一次對話的完整流程（prompt 組裝 → LLM → 工具 → 回傳）
3. 檢視中間產物：session 儲存的原始訊息結構
4. 畫出你自己版本的架構圖（可用 `hermes` 或手繪）

**驗收**：能向別人解釋「一次對話背後程式做了哪些事」。

---

## 單元 13｜Skill 開發（8h）

**學習目標**
- 寫出可分享、可被 agent 自主改進的 skill

**閱讀材料**
- Creating Skills（精讀）：`/docs/developer-guide/creating-skills`
- Work with Skills（複習）：`/docs/guides/work-with-skills`
- Skill Authoring（內建技能，可當範例）：`hermes skills` 裡的 hermes-agent-skill-authoring

**實作練習**
1. 寫 1 個你自己的 skill（例如「整理會議記錄」），含 SKILL.md + 流程
2. 用 `hermes skills` 安裝自己的 skill 並觸發驗證
3. 依 hermes-agent-skill-authoring 的規格重新打磨你的 skill（命名、frontmatter、檢查表）
4. 讓 Hermes 在「使用中」改進你的 skill，觀察它改動了什麼
5. 上傳到 Skills Hub 或 GitHub 分享（可選）

**驗收**：產出一個符合官方規格、agent 能自行調用的 skill。

---

## 單元 14｜Plugin 開發（10h）

**學習目標**
- 學會 Hermes 擴充的第一公民：plugins

**閱讀材料**
- Plugins（功能總覽）：`/docs/user-guide/features/plugins`
- Build a Hermes Plugin：`/docs/developer-guide/plugins/index`
- Adding Tools：`/docs/developer-guide/adding-tools`
- Plugin LLM Access：`/docs/developer-guide/plugin-llm-access`

**實作練習**
1. 照官方範例建立一個最小 plugin（hello world tool）
2. 新增第二個工具：一個有參數、有錯誤處理的真實功能
3. plugin 串接外部 API（自選一個公開 API）
4. 製作 plugin 的 config schema，讓使用者可設定
5. 撰寫 plugin 的說明文件並打包分發（本地安裝驗證）

**驗收**：產出一個功能完整、有文件、可安裝的 plugin。

---

## 單元 15｜Provider 與終端後端（8h）

**學習目標**
- 能接自訂模型、部署到遠端/容器

**閱讀材料**
- Local Models：`/docs/user-guide/local-models`
- Local Ollama：`/docs/guides/local-ollama-setup`
- Docker：`/docs/user-guide/docker`
- Adding Providers（開發向）：`/docs/developer-guide/adding-providers`

**實作練習**
1. 在本機跑 Ollama，把 Hermes 指向本地模型，比較與雲端模型差異
2. 用 Docker 跑一個 Hermes 容器實例
3. 練習 SSH 後端：把 agent 跑在另一台機器
4. （加分）嘗試 serverless 後端（Daytona / Modal），比較成本

**驗收**：能獨立決定「這個任務該用哪個模型、跑在哪裡」。

---

## 單元 16｜貢獻開源（10h）

**學習目標**
- 進入 Hermes 開發者社群，貢獻第一個 PR

**閱讀材料**
- Contributing：`/docs/developer-guide/contributing`
- Codebase Ownership：`/docs/developer-guide/codebase-ownership`
- Tests 與 QA：repo 內 `scripts/run_tests.sh`（安裝時已有）

**實作練習**
1. 在你本機 `~/.hermes/hermes-agent` 建立 branch，跑通測試
2. 從 GitHub Issues 挑一個 good-first-issue
3. 修 bug 或加測試，寫清楚 commit message
4. 建立符合規範的 PR（含測試、文件）
5. 參與一次社群討論（Discord / GitHub Discussion）

**驗收**：成功發送一個被 review 的 PR（包含或不包含合併都算完成）。

---

# 習題本（選做，配合課程進度）

官方 Guides 就是現成習題，學完對應單元就做：

| 學完單元 | 建議習題 |
|---|---|
| 1-4 | Tips & Best Practices：`/docs/guides/tips` |
| 5 | Delegation Patterns：`/docs/guides/delegation-patterns` |
| 6-7 | Use SOUL with Hermes：`/docs/guides/use-soul-with-hermes` |
| 8 | Daily Briefing Bot、Automation Blueprints：`/docs/guides/daily-briefing-bot` |
| 9 | Team Telegram Assistant：`/docs/guides/team-telegram-assistant` |
| 11 | Use MCP with Hermes：`/docs/guides/use-mcp-with-hermes` |
| 全課程 | GitHub PR Review Agent：`/docs/guides/github-pr-review-agent` |

---

# 期末專題（Capstone） ~10h

**題目（擇一）**：
1. **個人自動化助理**：Telegram bot + 每日簡報 cron + 至少 1 個自寫 skill，連續跑 7 天
2. **團隊協作助理**：GitHub PR review agent + 週報 + 專案 context 策略
3. **產品化外掛**：把單元 14 的 plugin 打磨成可發佈狀態並寫完整文件

**評分標準**（自己檢核）：
- [ ] 使用 3 個以上不同功能（工具 / 記憶 / 技能 / cron / MCP…）
- [ ] 具備基本安全性設定
- [ ] 有設計說明（架構圖或流程說明）
- [ ] 出錯時知道用 `hermes doctor` / logs 除錯

---

# 學習環境小抄

```bash
hermes                 # 互動對話
hermes -z "..."        # 單行指令
hermes setup           # 設定精靈（--portal 最快）
hermes doctor          # 健康檢查（--fix 自動修）
hermes model           # 選模型/provider
hermes tools           # 管理工具集
hermes skills          # 管理技能
hermes sessions        # 管理 session
hermes config get/set  # 讀寫設定
hermes gateway         # 訊息平台 gateway
hermes cron            # 排程任務
hermes update          # 更新
```

**官方網路資源**：文件站 `/docs` ｜ GitHub `NousResearch/hermes-agent` ｜ Discord `discord.gg/NousResearch` ｜ Skills Hub `agentskills.io` ｜ LLM 可讀版 `/docs/llms.txt`