# 日序 Daymark

個人行程與任務管理系統，部署於 GitHub Pages，使用 Firebase Authentication（Google 登入）與 Cloud Firestore 雲端同步資料。

**線上預覽：** https://yning13.github.io/1106-/

## 功能特色

- **今日總覽儀表板**：一眼掌握今日行程數、待辦任務、已完成數與任務步驟進度
- **行程管理**：支援固定行程、排程任務、未排程待辦三種類型，可設定每週重複
- **日曆 / 週曆切換**：日檢視與週檢視自由切換，快速瀏覽一週安排
- **任務進度追蹤**：每項任務可設定總步驟數與已完成步驟，顯示進度條
- **本週完成率**：側邊欄顯示本週任務完成率統計
- **AI 智慧填入**：透過 Google Gemini API，用自然語言描述即可自動辨識類型、日期、時間並填入表單
- **5 色主題切換**：紫、藍、綠、橘、粉五種主題色彩
- **深色模式**：一鍵切換深色 / 亮色模式，偏好設定自動儲存於本機
- **響應式設計**：支援桌面與手機瀏覽

## 技術架構

| 項目 | 技術 |
|------|------|
| 前端 | 純 HTML / CSS / JavaScript（單頁應用） |
| 部署 | GitHub Pages |
| 認證 | Firebase Authentication（Google 登入） |
| 資料庫 | Cloud Firestore（asia-east1） |
| AI | Google Gemini API（gemini-3.8-flash） |

## Firestore 資料結構

- 使用者資料存放於 `users/{uid}/items/{itemId}`
- Firestore 規則只允許使用者存取自己的項目
- 已登入時，新增、編輯、刪除會同步到 Firestore；未登入時暫存於本機
- 首次登入且 Firestore 尚無資料時，會將本機資料遷移至該使用者的 Firestore 子集合

## 設定檔

- `firebase-runtime/firebase-config.js`：Firebase Web App 設定
- `firebase-runtime/gemini-config.js`：Gemini API Key 設定（請參考 `gemini-config.example.js`）
- `firestore.rules`：Firestore 安全規則

## 部署

Firestore 規則可用 Firebase CLI 部署：

```sh
firebase deploy --only firestore
```
