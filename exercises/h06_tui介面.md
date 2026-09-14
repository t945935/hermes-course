# H6 實作紀錄：TUI 介面

> 完成日期：2026-09-14 ｜ 執行：`hermes --tui`（tmux 中）

## 實測畫面（capture）
- 啟動橫幅：Session e4d21f2c（每 session 一 ID）
- **Available Tools** 面板（可摺疊）：
  - browser: browser_vault_enter_code, browser_vault_fill, …+3
  - browser-use: browser_exec
  - clarify: clarify
  - code_execution: execute_code
  - delegation: delegate_task
  - file: patch, read_file, search_files, write_file
  - memory: memory
  - other: tool_call, tool_describe, tool_search
  - 另有 5 個 toolsets（…+5）
- **Available Skills (54) in 11 categories**（預設收合 ▸）
- 狀態列：`─ ready │ solar pro4:free │ 5s │ 1 session`
- 輸入列：`❯ Ask me anything…`
- 底部：`25 tools · 54 skills · /help for commands`

## 官方文件重點（tui.md）
| 特性 | 說明 |
|---|---|
| 啟動 | `hermes --tui`；`HERMES_TUI=1` 環境變數；config `display.interface: tui` |
| 續接 | `hermes --tui -c` / `-r <session>` / `--resume latest` |
| 非阻塞輸入 | 可先打字排隊，session ready 後自動送出 |
| 摺疊橫幅 | Tools(開)/Skills/System Prompt/MCP Servers（▸▾ 切換） |
| 進階 | 滑鼠選擇、`/skin`、`/personality` 即時換主題 |

## 驗收自評
✅ 了解 TUI 是「官方建議的互動介面」
✅ 能說出橫幅四個可摺疊區塊
✅ 知道啟動三式：`--tui` 旗標 / 環境變數 / config 預設
✅ 實際看到 tools/skills 面板與就緒狀態列

## 附註
- TUI 與 Classic CLI 共用同一 agent/session/斜線指令（不同皮、同一引擎）
- capture-pane 有替代畫面（alternate screen），截圖容易拿到空白——用 `-S` 取歷史列即可