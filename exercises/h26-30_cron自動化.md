# H26-H30 實作紀錄：Cron 自動化

> 完成日期：2026-09-14

## H26 核心機制：Cron 需要 gateway 才會自動觸發
```
⚠ Gateway is not running — jobs won't fire automatically.
   hermes gateway install      # 使用者服務
   sudo hermes gateway install --system  # Linux 開機服務
   hermes gateway              # 前景執行
```
- **排程 ≠ 自動執行**：job 排好了，但要有常駐 gateway 才會 fire
- config `cron.catch_up_missed: true`（錯過排程會補跑）

## H27 建立 job（實測）
```bash
hermes cron create "0 17 * * *" "產生今日天氣摘要並存入 ~/hermes-course/exercises/daily-weather.md" --name weather-demo --paused
```
- schedule 支援自然語言（`30m`、`every 2h`）或 cron 五欄位（`0 17 * * *`）
- 選項：--deliver（telegram/discord…）、--skill、--script、--model、--continuity、--paused
- 建立成功：`Created job: 5764ad3eedad`
- ⚠️ 同名 job 會衝突（resume 時要求用 job ID）— 我用 ID 解掉

## H28 生命週期管理（全實測）
| 動作 | 指令 | 結果 |
|---|---|---|
| 列出 | `hermes cron list` | ✓ 顯示 schedule/next run/deliver |
| 暫停 | `hermes cron pause` | — |
| 恢復 | `hermes cron resume 5764ad3eedad` | ✓ Next run: 17:00+08:00 |
| 立即執行 | `hermes cron run tick-test` | ✓ **Ran now: succeeded**（run 是立即執行！） |
| 刪除 | `hermes cron remove tick-test` | ✓ Removed |
| 診斷 | `hermes cron doctor` / `incidents` / `notepad` | 健康檢查/失敗事件/持久 KV |

## H29 執行記錄（hermes cron runs）
```
2c492dcb…  completed  job=11545def9d3e  source=direct  2026-09-14T12:25:18
```
- 每個 job 每次執行有獨立 run ID（durable execution）
- source=direct（手動觸發）vs 排程自動觸發

## H30 實戰案例（保留中）
`weather-demo`：「每天 17:00 產生天氣摘要存檔」— 目前 active
- 待使用者決定是否 `hermes gateway install` 讓它真正自動化

## 驗收自評
✅ 會建立/暫停/恢復/執行/刪除 cron job
✅ 知道 gateway 常駐服務的必要性與安裝方式
✅ 看懂執行記錄（run ID / source）
✅ 理解 catch_up_missed 補跑機制