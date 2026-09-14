# H7 實作紀錄：config.yaml 解析

> 完成日期：2026-09-14 ｜ 檔案：`~/.hermes/config.yaml`（177 行，_config_version: 44）

## 區塊總覽（重點）
| 區塊 | 關鍵設定 | 我的理解 |
|---|---|---|
| **model** | default: upstage/solar-pro4:free, provider: nous, base_url…/v1 | 模型+API 位址，H3 設定的 |
| **database** | journal_mode: wal | SQLite WAL 模式（並行安全） |
| **runtime** | nofile_soft_limit: 4096 | 檔案描述符上限 |
| **agent** | max_turns: 500, reasoning_effort: medium | 單 session 最大回合數、推理力度 |
| **terminal** | backend: local, timeout: 180, cwd: . | 終端執行環境（超時 180 秒） |
| **browser** | inactivity_timeout: 120 | 瀏覽器閒置逾時 |
| **tool_loop_guardrails** | warnings_enabled: true, hard_stop(非互動): true | ⚠️ 工具迴圈防護：非互動模式硬停 |
| **compression** | enabled: true, threshold: 0.5 | context 壓縮（50% 門檻觸發） |
| **prompt_caching** | cache_ttl: 5m | prompt 快取 5 分鐘 |
| **display** | streaming: true, skin: default | 顯示行為 |
| **stt** | enabled: true, language: en | 語音輸入 |
| **memory** | enabled: true, char_limit: 2200 | 記憶系統（第 6 章主角） |
| **delegation** | max_iterations: 250 | 子任務委派上限 |
| **skills** / **plugins** | enabled: [] | 技能/外掛（第 7、14 章主角） |
| **cron** | catch_up_missed: true | 排程錯過補跑 |
| **code_execution** | timeout: 300, max_tool_calls: 50 | 程式碼執行上限 |
| **updates** | check: true, backup_keep: 5 | 更新檢查+保留 5 份備份 |
| **platform_toolsets** | cli/telegram/discord/whatsapp/slack… | 各平台工具集開關（第 9 章） |

## 相關指令（實測）
- `hermes config get <key>` → 讀單一鍵（如 `hermes config get model`）
- `hermes config get <key> --json` → JSON 格式
- `_config_version: 44` → H2 時 `doctor --fix` 從 v0 遷移到 v44

## 驗收自評
✅ 能指出 config 5 大區塊（model/agent/terminal/memory/platform）
✅ 知道壓縮、快取、防護等進階開關在哪
✅ 會用 `hermes config get` 查設定
✅ 知道「模型設定放 config.yaml 第一段」