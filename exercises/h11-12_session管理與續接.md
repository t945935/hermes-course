# H11-H12 實作紀錄：Session 管理與續接

> 完成日期：2026-09-14

## H11 Session 管理
### 統計（hermes sessions stats）
```
Total sessions: 9 ｜ Total messages: 44 ｜ Database size: 0.5 MB
```
→ 資料庫是 SQLite（WAL 模式），所有 session 統一存放

### 匯出（hermes sessions export）
| 格式 | 指令 | 結果 |
|---|---|---|
| JSONL | `sessions export --format jsonl --session-id <ID> <dir>/` | ✓ 20KB 檔案 |
| Markdown | `sessions export --format md --session-id <ID> <dir>/` | ✓ 6 則訊息，檔名自動帶標題 |

→ 支援格式：jsonl / md / qmd / html / trace
→ 支援豐富過濾：--older-than、--model、--min-tokens、--min-cost…（可當稽核工具）

## H12 續接與命名
### 指定 session 續接（-r）
```bash
hermes -r 20260914_121340_bb3fd6 -z "我喜歡的語言是哪個？"
```
→ 回覆「你的首選程式語言是 Python。」＝跨 session 上下文延續 ✅

### 改名（sessions rename）
```bash
hermes sessions rename <session_id> "新標題"
```
→ `Session '...' renamed to: H4-我的Python偏好` ✅（支援中文標題）

### 續接三式整理
| 指令 | 效果 |
|---|---|
| `hermes --continue` | 續接最新 session |
| `hermes --resume <ID>` / `-r <ID>` | 續接指定 session |
| `hermes --resume latest` | 續接最近一次 |

## 驗收自評
✅ 會查 session 統計、匯出 JSONL/MD
✅ 會改名、會用 -r 指定續接指定對話
✅ 認知「session = 上下文單位，資料庫集中管理」