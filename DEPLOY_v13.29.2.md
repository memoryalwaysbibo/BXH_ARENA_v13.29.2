# BXH ARENA v13.29.2 部署順序

Blaze 已啟用後，請從完整交付包的根目錄操作，不要只上傳 `index.html`。

1. 確認 Firebase CLI 已登入正確 Google 帳號。
2. 執行 `firebase use --add`，明確選擇 BXH ARENA 正式專案。
3. 執行 `npm --prefix functions ci`。
4. 執行 `npm --prefix functions run check`。
5. 先部署 `firebase deploy --only firestore:rules`。
6. 再部署 `firebase deploy --only functions`。
7. 最後部署或上傳 `index.html`。
8. 最高管理員進入「帳號管理 → 稱號與每日簽到」，按「建立／同步第一批稱號」。
9. 先只開啟玩家稱號介面與每日簽到；自動發放與簽到稱號暫時關閉。

## 部署後最低驗證

- player 能讀取稱號圖鑑並完成當日簽到。
- 同一玩家同一天重按簽到不會累加第二次。
- tester 簽到不會獲得正式稱號。
- super_admin 可人工授予與撤銷測試稱號。
- 玩家只能裝備本人已取得且仍啟用的稱號。
- 登入、賽事報名、賽事報到、裁判計分與天梯結算各執行一次冒煙測試。
- Firebase Functions 日誌沒有 `permission-denied`、路徑錯誤或重複觸發迴圈。
- 暫時停用 Functions 或模擬讀取失敗時，玩家首頁只顯示一次錯誤與「重新連線」，賽事大廳仍可操作且不會持續刷新。

## 回復方式

先把四個 engagement 功能開關設為 `false`，再將網站退回 v13.28.9。新集合可以保留，不需要刪除；避免在問題尚未釐清前執行破壞性資料清理。
