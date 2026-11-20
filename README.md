# 日序 Daymark

個人行程與任務管理前端，使用 Firebase Authentication 登入，並以 Cloud Firestore 儲存登入使用者的行程與任務。

## Firestore

- Standard `(default)` 資料庫，位置為 `asia-east1`（台灣）。
- 使用者資料存放於 `users/{uid}/items/{itemId}`，Firestore 規則只允許使用者存取自己的項目。
- 已登入時，新增、編輯、刪除與進度變更會同步到 Firestore；未登入時暫存於本機。
- 首次登入且 Firestore 尚無資料時，會把舊版 `daymark-v1` 本機資料遷移至該使用者的 Firestore 子集合。
- Web App 設定位於 `firebase-runtime/firebase-config.js`；此設定供瀏覽器使用，資料存取權由 `firestore.rules` 控制。

`firebase.json`、`firestore.rules` 與 `firestore.indexes.json` 可用 Firebase CLI 部署：

```sh
firebase deploy --only firestore
```
