# H70-H77 實作紀錄：Provider 與部署

> 完成日期：2026-09-14

## 認證池（hermes auth）
```
copilot (1 credentials):  #1 gh auth token (api_key, gh_cli)
nous   (1 credentials):  #1 t945935@gmail.com (oauth, device_code) ←
```
- 多 provider 多 credential 集中管理；可新增/移除/重置 cooldown/設定輪替策略
- 目前：nous（主）、copilot gh token（輔）

## 部署面總覽（實測各入口）
| 入口 | 用途 | 實測 |
|---|---|---|
| `hermes serve` | JSON-RPC/WebSocket 後端（port 9119），desktop 與遠端客戶端連接 | headless，不開瀏覽器 |
| `hermes desktop` / `gui` | Electron 桌面 app（會 build 打包） | WSL 建議跳過 |
| `hermes proxy` | OpenAI-compatible 代理：本地 HTTP 把請求轉給 OAuth provider | ✓ nous ready |
| `hermes gateway` | 訊息平台 + cron 中樞（第 8/9 章） | 未啟動 |
| `hermes lsp` | write_file/patch 後的語義診斷服務 | ✓ enabled, document 模式 |

### proxy 實測
```
[nous] Nous Portal — ready (bearer expires 2026-09-14T05:10:12+00:00)
[xai ] xAI Grok OAuth — not logged in
```
- 外部 app 指到 proxy 即可用公開 bearer token，proxy 換成真實憑證轉發

### LSP 實測
```
enabled: True, wait_mode: document, wait_timeout: 5s, active clients: none
```
- 支援語言伺服器清單用 `hermes lsp list`；`install` 可裝 binary

## 多模型架構
### MoA（Mixture of Agents，hermes moa）
```
Default: default
Reference models:
  1. openai-codex:gpt-5.5
  2. openrouter:deepseek/deepseek-v4-pro
Aggregator: openrouter:anthropic/claude-opus-4.8
```
- 概念：多個 reference 模型各答一次 → aggregator 彙整
- 目前 Active in config: (off)——需要的話 `hermes moa configure` 開啟

### Fallback（hermes fallback）
- 目前無設定；加語法 `hermes fallback add`（選 provider+model）
- 用途：主模型 rate-limit/超載/連線錯誤時依序嘗試

## 更新與同步（銜接第 16 章）
- `hermes update --check` / `--plan`：先查先看，不變更
- `hermes update`：git pull + 重裝依賴；支援 --no-backup/--backup/--force/--branch
- `hermes sync`：技能跨裝置同步（status/pull/push/now/enable/disable/device/propose）；組織可共享技能

## 驗收自評
✅ 看懂認證池與可用 credentials
✅ 分得清 serve/proxy/gateway/desktop/lsp 五個部署面
✅ 理解 MoA 與 fallback 鏈的多模型架構
✅ 知道更新/同步入口（update/sync）與安全旗標