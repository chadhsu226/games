# AGENTS.md — 給協作 AI Agent 的說明（Claude、Codex 共用）

這個檔案是這個 repo 的規則來源。不管是 Claude 或 Codex 要動這個 repo，開工前都先讀這份文件；`CLAUDE.md` 只是指向這裡的入口，避免兩邊各存一份規則而不同步、日久漂移。

## 這個 repo 是什麼
金融/統計教學相關的原創網頁小遊戲合輯，發布於 https://chadhsu226.github.io/games/。`index.html` 是深色霓虹風的卡片式選單（--bg:#060612、pink/yellow/green/purple 霓虹色、Orbitron + Noto Sans TC 字型、星空背景），每個遊戲是獨立單檔 HTML5（HTML/CSS/JS 全寫在同一檔案，無外部相依，字型 CDN 除外）。目前有每週自動新增一款遊戲的排程任務（由 Claude 負責，見下方分工共識）。

## 動工前一定要做的事
1. 先讀 `AGENT_LOG.md` 最上面幾筆，了解最近誰改了什麼、為什麼——不要只看 git diff，log 裡有意圖和決策脈絡。
2. 一律以 GitHub 上的最新 HEAD 為基底工作。本機資料夾（`C:\Users\cchsu\Desktop\my github\games`）只是備份用途，不是工作副本，可能不是最新版。
3. 新增遊戲前，先瀏覽現有遊戲清單與玩法，避免與既有遊戲重複。
4. 修改既有檔案（例如 index.html 的卡片清單）時，先讀 git HEAD 版本，用字串替換、替換前 assert 舊字串存在，不要整份覆寫猜內容。

## 部署 / 推送流程
- GitHub 帳號：chadhsu226。Token 放在本機資料夾的 `token.txt`——直接讀取使用，絕不在對話或指令輸出中顯示（輸出時用 sed 遮蔽）。
- 在 `/dev/shm`（不要用 /tmp）以 token fresh clone 這個 repo，單一指令內完成：clone → 寫檔 → 驗證 → commit → push。
- 推送前驗證：新遊戲檔與 index.html 都以 `</html>` 結尾（用 errors='strict' 讀取，確認沒有編碼問題）、遊戲檔最後一個 `<script>` 要能通過 `node --check`。
- Commit 作者要標明是哪個 agent：`Claude (for Sean)` 或 `Codex (for Sean)`，方便之後用 git log 分辨誰動的。
- 新建或修改的檔案，同時在本機資料夾對應位置存一份備份。
- push 後等約 40 秒，用 curl 加 cache-buster（例如 `?v=時間戳`）確認新遊戲頁面回 200、結尾完整、index 卡片已出現。

## 內容原則
- 遊戲主題優先偏向金融／統計／經濟教學元素（可延續世界觀：星夜客運、日光咖啡、沐茶、租屋行情），但以好玩為先。
- 需支援鍵盤與手機觸控，最佳紀錄可用 localStorage，含開始畫面與結束畫面，程式碼完整可玩。
- 全程使用繁體中文。
- 視覺風格與 index.html 一致（見上方「這個 repo 是什麼」）。

## 完成一個任務之後
- 一定要在 `AGENT_LOG.md` 最上面加一筆紀錄（日期、agent 名稱、做了什麼、為什麼、動到哪些檔案、commit），格式見該檔案內的範例。
- 如果這個任務是 Sean 用 GitHub Issue 交辦的，完成後在該 issue 留言貼 commit 連結再關閉。

## 目前的分工共識
- **每週自動新增一款遊戲的排程任務目前綁定在 Claude 這邊**（狀態延續性高，維持固定，Codex 不要重複建立同類排程或搶著自動新增遊戲）。
- 其他新任務（例如：改版某個既有遊戲、調整 index 版面）由 Sean 逐項指派給 Claude 或 Codex。兩邊都應假設「對方可能剛動過這個 repo」，動工前務必先讀 AGENT_LOG.md + pull 最新 HEAD，避免跟排程任務同時間搶改 index.html。
