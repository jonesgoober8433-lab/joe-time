# 開啟「email 找回活動」：Firebase 後台設定（約 5 分鐘）

網頁程式已經支援。沒完成下面設定前，網站照常使用；只是 email 驗證信寄不出去、雲端備份會失敗（本機「我的活動」清單不受影響）。

## 1. 開啟 email 連結登入
1. Firebase 後台，專案 `joe-time` → **Authentication** → **Sign-in method**
2. 點 **Email/Password** → 打開第一個開關「Email/Password」→ 再打開 **「Email link (passwordless sign-in)」** → 儲存

## 2. 加入授權網域
1. Authentication → **Settings** → **Authorized domains**
2. 新增 `jonesgoober8433-lab.github.io`（`localhost` 通常已經有）

## 3. 更新 Firestore 規則（先比對再貼）
1. Firestore Database → **Rules**
2. **先把目前的規則存一份備份**（複製貼到記事本），再和本資料夾的 `firestore.rules` 比對
3. 確認沒問題後，貼上 `firestore.rules` 的內容 → **發布**

這份規則的重點：
- `events`：維持用連結讀寫；禁止列出全部活動、禁止刪除
- `users/{uid}/events`：只有登入的本人能讀寫，別人讀不到你的管理連結

## 4. （建議）把信改成中文
Authentication → **Templates** → **Email link sign-in**：可改寄件人名稱與主旨，例如「喬時間 驗證信」。

## 注意
- 驗證信可能進垃圾信件匣。
- Firebase 免費方案對每個 email 每天可寄的驗證信次數有限（約數封）。
