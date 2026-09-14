# 🤝 讀者參與指南（CONTRIBUTING）

歡迎一起讓《Hermes Agent 100 小時》更好。這是一本「真人在真實環境學習」的書——你踩到的坑，就是下一版要修的內容。

## 你可以做什麼

### 1. 回報勘誤（最簡單、最有用）
在 [Issues › 勘誤回報](https://github.com/t945935/hermes-course/issues/new?template=01-errata.yml) 貼出：
- 出錯位置（章節/小時）
- 原文 vs 應該是什麼
- 你的 Hermes 版本（`hermes --version`）

### 2. 直接修書稿（PR）
書稿原始碼在 [`00-book/hermes-agent-100-hours.md`](00-book/hermes-agent-100-hours.md)，是純 Markdown。

**流程**：
1. Fork 本倉庫
2. 改 `00-book/` 下的檔案
3. 開 PR 時**引用對應 Issue**（如有）
4. 維護者審閱後合併，修正會進入下一版 EPUB

### 3. 建議新內容
用 [Issues › 內容建議](https://github.com/t945935/hermes-course/issues/new?template=02-suggestion.yml) 提出。評估標準：
- 多數讀者會碰到？
- 與現有進度線（入門→進階→開發）一致？
- 有明確驗收標準？

## 書稿寫作規範（改稿前必讀）

| 原則 | 說明 |
|---|---|
| 每節 1 小時 | 新單元請維持「動手做／內容重點／驗收」三欄結構 |
| 版本免責 | 具體數字、指令若隨版本變化，加「以你的版本為準」 |
| 不臆測 | 沒實測過的行為不要寫進去；寫了就要能跑 |
| 實作優先 | 每個知識點都要能動手驗證 |

## 溝通守則

- **問題先查**：先看 [Discussions Q&A](https://github.com/t945935/hermes-course/discussions) 是否已有解答
- **一個 Issue 一件事**：方便追蹤與關閉
- **友善**：大家都是來學的，保持禮貌

## 標籤說明

| 標籤 | 用途 |
|---|---|
| `errata` | 書稿錯誤（最高優先） |
| `bug` | 書中指令/行為失效 |
| `suggestion` | 內容改進提案 |
| `question` | 讀者問題 |
| `version-drift` | 因 Hermes 版本更新而失效的內容 |

感謝你花時間讓這本書更好 🚀