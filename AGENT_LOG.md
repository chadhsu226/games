# AGENT_LOG — 異動紀錄

每次改動這個 repo 的 agent，動工前先讀這裡最上面幾筆、了解目前狀態；完成後在最上面新增一筆，格式如下：

## YYYY-MM-DD — <Claude|Codex> — 一句話標題
- 做了什麼：
- 為什麼：
- 動到的檔案：
- Commit：<commit hash 或連結>

---

## 2026-09-20 — Claude — 新增遊戲：星夜客運：出車賭局（每週排程任務）
- 做了什麼：新增 night-dispatch.html（push-your-luck 骰子風險決策遊戲，8 班次發車/收班機制，含期望值提示），更新 index.html 新增卡片並將 New 徽章從 portfolio-blocks 移到新遊戲
- 為什麼：每週自動新增一款遊戲的排程任務（Claude 負責），設計時瀏覽過現有 11 款遊戲玩法（射擊/彈珠、打磚塊、貪食蛇、2048、疊疊樂、垂直跳躍、反應點擊、消消樂、飛行閃避、俄羅斯方塊），選擇尚未使用過的「回合制押注/期望值決策」機制與尚未使用過的「星夜客運」世界觀，避免玩法重複
- 動到的檔案：night-dispatch.html（新增）, index.html（新增卡片、移動 New 徽章）, AGENT_LOG.md（本次紀錄）
- Commit：9a20a4f5685982c814d4c814597a344b8a1efc90（新增遊戲）


## 2026-09-07 — Claude — 建立 Claude/Codex 共用協作機制
- 做了什麼：新增本檔案、AGENTS.md、CLAUDE.md（指向 AGENTS.md）
- 為什麼：Sean 要讓 Codex 加入這個 repo 的開發維護，兩個 agent 需要讀同一份規則、看得到對方的異動紀錄，避免衝突或狀態遺漏（尤其這個 repo 有每週排程任務會自動改 index.html，更需要交接紀錄）
- 動到的檔案：AGENTS.md, CLAUDE.md, AGENT_LOG.md（新增）
- Commit：（見本次 commit）
