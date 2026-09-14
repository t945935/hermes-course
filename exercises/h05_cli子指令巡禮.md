# H5 實作紀錄：CLI 子指令巡禮

> 完成日期：2026-09-14（OAuth 等待期間完成，不依賴模型）

## 動手做結果

### ① hermes --help：全域旗標（重要）
| 旗標 | 用途 |
|---|---|
| `-z PROMPT` / `--oneshot` | 單行模式 |
| `-m MODEL` / `--provider PROVIDER` | 指定模型 / provider（臨時） |
| `--reasoning LEVEL` | none / minimal / auto…推理力度 |
| `-r SESSION` / `--resume` | 續接 session |
| `--continue` | 繼續上次 |
| `-w` / `--worktree` | 隔離 git worktree 平行執行 |
| `--yolo` | ⚠️ 跳過所有危險指令確認（小心！） |
| `-s SKILLS` | 指定 skills |
| `--in DIR` | 指定工作目錄 |

### ② hermes --help：子指令 >70 個
重點分類（自己歸類）：
- **對話**：chat、moa、fallback、resume、pause、continue
- **設定**：setup、config、model、providers、profile
- **工具**：tools、skills、plugins、bundles、mcp、computer-use
- **資料**：sessions、memory、memory-graph、vault、backups、checkpoints
- **自動化**：cron、hooks、gateway、webhook、kanban、journey
- **平台**：whatsapp、slack、telegram（經 gateway）、discord
- **維運**：doctor、status、logs、debug、insights、monitoring、update、uninstall
- **其他**：browser、secrets、egress、auth、sync、pairing、server、dashboard

### ③ hermes config get model（實測）
```
default: anthropic/claude-opus-4.6
provider: auto
base_url: https://openrouter.ai/api/v1
```
→ model 是「provider/模型」格式；provider=auto 表示自動路由

### ④ hermes sessions（子指令更多）
`list / export / delete / prune / archive / optimize / stats / rename / pin / browse / import…`
→ session 是 SQLite store，有完整管理面

### ⑤ hermes status
- Project / Python / .env ✓
- Model: anthropic/claude-opus-4.6, Provider: Nous Portal（設定檔預設）
- API keys：OpenRouter / OpenAI 未設定（待 OAuth）

## 踩到的坑（學習點）
- `hermes tools` 需要**互動終端**，不能透過 pipe 執行 → 之後要在 tmux/真實終端跑
- `hermes config get` 是子指令形式 `hermes config get <key>`，不是直接參數

## 驗收自評
✅ 能列出 8+ 子指令用途（對話/設定/工具/資料/自動化/維運…）
✅ 知道全域旗標 `-z`、`-r`、`-m`
✅ 踩坑記錄完整