# H3 實作紀錄：Provider 設定 + 第一次真實對話

> 完成日期：2026-09-14

## 過程
1. `hermes setup --portal` 啟動 OAuth 登入（tmux 中執行）
2. 使用者於瀏覽器完成 Nous Portal 授權
3. 模型選擇：**upstage/solar-pro4:free**（免費，$0/Mtok）
4. 設定完成：login ✓ + model ✓

## 驗證結果
- `hermes doctor` → `✓ Nous Portal auth (logged in)`
- `hermes config get model` →
  ```
  default: upstage/solar-pro4:free
  provider: nous
  base_url: https://inference-api.nousresearch.com/v1
  ```

## 第一次真實對話（H3 驗收）
> 問：用一句話介紹你自己，並列出你能幫我做的 3 類事情

> 答：我是 Solar Pro4，由韓國 Upstage AI 開發的語言模型；我能幫你做的三類事：搜尋與整理資訊（網頁搜尋、頁面提取）、處理文件與數據（讀寫檔案、操作 Excel/Word/PDF 等）、以及協助開發與除錯（執行程式碼、檢查程式庫、排查問題）。

## 踩到的坑（學習點）
- WSL 系統 Chrome 缺 `libnspr4.so`，`setup --portal` 自動開瀏覽器失敗 → **不影響**授權，手動開 URL 即可
- 裝置代碼有時效（約 5-10 分鐘），過期需重啟流程
- tmux server 在流程中意外終止過 2 次 → 之後用 `hermes doctor` 驗證最終狀態，不要只看 tmux 畫面

## 驗收自評
✅ 完成一次真實對話
✅ 知道 provider = nous、模型格式 = provider/模型名
✅ 知道免費模型與計費模型的差別（看 `hermes model` 選單的價格欄）