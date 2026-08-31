# Firebase 安全同步設定

MoneyCan 現在會在雲端權限不可用時保留本機資料，不會再把已有資料顯示成空白。

## 目前狀態

- `wallets` 和 `transactions` 可讀取，因此舊存錢資料可正常恢復。
- `settings`、`ledgerAccounts`、`ledgerTransactions`、`ledgerSettlements` 和 `ledgerTransfers` 目前會被 Firestore 規則拒絕。
- 新帳本在權限完成前以瀏覽器本機資料為主。
- 使用者目前選擇先不加入登入，因此同一裝置可完整使用；真正的跨裝置家庭同步仍保留到登入階段處理。

## 正式上線前

1. 在 Firebase Authentication 啟用一種登入方式（建議 Google）。
2. 將家庭成員的 Firebase UID 加入 `authorizedUsers/{uid}`。
3. 將 `firestore.rules.example` 複製為 `firestore.rules` 後部署。
4. 確認登入後才可讀寫家庭帳本。

`firestore.rules.example` 預設拒絕未登入或未授權使用者。在網站尚未加入登入畫面前，不要直接部署這份規則，否則現有網站會全部切換為本機模式。
