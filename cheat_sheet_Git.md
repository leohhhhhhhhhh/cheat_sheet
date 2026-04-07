#  Git & GitHub 

##  一、 專案開工：連結 GitHub 遠端倉庫
*在本地建好資料夾，想要連到 GitHub 新建立的 Repository 時。*

1. **初始化資料夾**: `git init`
2. **暫存所有檔案**: `git add .`
3. **提交第一個存檔**: `git commit -m "Initial commit"`
4. **設定主分支名稱**: `git branch -M main`
5. **連結遠端地址**: `git remote add origin https://github.com/你的帳號/倉庫名.git`

---

##  二、 日常開發：修改與同步
*當寫完程式、改完筆記，要傳上雲端備份時。*

1. **查看狀態**: `git status`
2. **加入準備清單**: `git add .` (或 `git add 檔案名稱`)
3. **正式存檔標籤**: `git commit -m "feat: 這裡寫你改了什麼"`
4. **推送到雲端**: `git push`
   >  **注意**：第一次推送請用 `git push -u origin main`，之後只要打 `git push`。

---

##  三、 疑難排解：同步報錯與衝突處理

### 1. 報錯：`Updates were rejected / fetch first`
**原因**：雲端有你本地沒有的檔案（如 README.md），導致進度不一致。

####  選項 A：使用 Rebase
將你的修改「接」在雲端進度之後，保持直線。
```bash
git pull origin main --rebase
git push -u origin main
```
####  選項 B：使用 Merge
將兩邊進度揉合，會產生一個 Merge Commit。
```bash
git pull origin main --no-rebase #如果跳出 Vim 視窗，輸入 :wq 按 Enter 退出即可
git push
```
---
##  四、 常用指令

1. **查看狀態**: `git status`
2. **查看歷史紀錄**: `git log --oneline`
3. **查看目前分支**: `git branch`
4. **強制覆蓋雲端**: `git push -f`
5. **改了哪幾行程式碼**: `git diff` (跳出按q)
