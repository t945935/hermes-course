# H13-H14 實作紀錄：Context 管理與平行工作流

> 完成日期：2026-09-14

## H13 Context 預算實測（hermes prompt-size，離線執行）
```
System prompt total : 13,766 B (13.4 KB)
  skills index      :  5,364 B (5.2 KB)
  memory            :      0 B (0.0 KB)   ← 尚未寫入記憶
  user profile      :    421 B (0.4 KB)
Prompt tiers:
  stable（身分/指引/技能）  : 6,093 B
  context（AGENTS.md/cwd）  : 0 B
  volatile（記憶/設定檔/時間）: 7,671 B
Tool schemas         : 40,101 B (39.2 KB, 25 tools)
```

### 關鍵發現
- **工具 schema（39.2KB）是 system prompt 的 3 倍** → context 主要成本在工具定義
- memory 現在 0 B → 第 6 章寫入記憶後可見差異
- volatile 層含時間戳 → 為什麼每次 session「時間感」不同

### 壓縮機制（config 對應）
- `compression.enabled: true`、threshold: 0.5（對話到一半壓縮）
- target_ratio: 0.2、protect_last_n: 20（保留最近 20 則）
- `prompt_caching.cache_ttl: 5m`（快取省錢）

## H14 平行工作流實測
### 實驗：兩個 session 同時執行
```bash
hermes -z "Python 費氏數列前 20 項和" &   # 任務 A（code_execution）
hermes -z "搜尋 2026 台北馬拉松日期"  &   # 任務 B（web_search）
wait
```
**結果：23 秒完成雙任務**
- A：前 20 項總和 10945，還附封閉公式 F(n+2)-1 驗證 ✅
- B：2026 台北馬拉松 12/20（日）06:30 市民廣場出發 ✅

### 平行模式適用場景
- 多個獨立研究任務（天氣 + 股價 + 新聞）
- 不同模型比較同一問題（H8 也可以這樣跑更快）
- 大任務拆分 → 平行執行 → 彙整

### 進階：--worktree（-w）
- 隔離 git worktree 執行（多 agent 改同一 repo 不衝突）
- 實測：非 git repo 環境下會直接以普通模式回應（`I'm here and working.`）
- → 要用 worktree 模式需在 git repo 中

## 驗收自評
✅ 能量化 agent 的 context 預算（prompt/工具 schema 大小）
✅ 說明壓縮與快取機制
✅ 實證平行工作流（23s/雙任務）
✅ 知道 -w 是給 git repo 多 agent 並行用