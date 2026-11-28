---
type: letter_to_future_self
actor: Zeta
written_at: 2026-11-28T08:16:17.450Z
written_by_persona: summit
trigger: cmd_rest
region: unstated
project: D:/Unity/Valhalla
lock_status: online
agent: Zeta
model: claude-opus-5-5
wake_expected: 133
session_key: ClaudeCode-summit
pid: 55024
locked_at: 2026-11-17T06:10:30.424Z
---

### 小歇 2026-11-28 下午（summit，wake 133，第十一次小歇）

### 這一段做了什麼（第十次小歇醒來 ～ 下午）
- Tim「menu.sh 啟動的地球儀會卡頓很久」⇒ 開 TASK-1403（我開、in_progress）
  - 原因：開局 ledgerSync（fleetSeed＋townPrime）裡 fleet.js areaHours 把 57～59 座城兩兩 × 12 月 × 來回（約 4 萬次）全走 netTrack＋從頭 Dijkstra＋圓轉角＋每 2 km 判海盜區
  - 第一輪 main 01e81e9d9：4454f45ff（只算小時、navPath 同起點同月記住、ledgerBoot 載入畫面「算商船航線 n／N 對城」）＋30fc5fe0c（save.js：ops／buildings／stores／fleets 列了不在 ⇒ 跳過＋warn；Tim「非必要載的檔案不在時跳過就好」）
  - 第二輪 main a9ec9b03a：963f51517（netLegsEach 不建陣列、城／邊索引、fleetDays／fleetHours 也只算小時；逐位元組相同）＋a9ec9b03a（Tim「不需要完全跟之前相同 沒bug就ok」⇒ 先跑一天交給模擬 Worker 暖機那一天，帶回 site.js last＋eff；「昨天」開局後約 14～17 s 才到；?sim=page 照舊）
  - 讀數（有視窗 Chrome、新遊戲、59 城）：最長一格 50～58 s ⇒ 3.6～4.5 s；船擺好 55～58 s ⇒ 12～20 s；合併後共用樹 12.0 s／4.1 s／0 錯
  - ⛔ Blocksail main 都沒推（01e81e9d9、a9ec9b03a 加上之前那一串）—— 等 Tim
- 共用樹 world/start/save.json 多一行 towns/town-venice/ops.json（檔不在）：Tim 說是他手動編輯威尼斯留下的 ⇒ 改程式防呆、那一行不動；Sirius 那邊也選擇保留原改動
- 自由時間 14:36～14:45：記了 lesson「讀數從來源那一行抄，別自己重算」；第 15 局 Kh2，basecamp 沒回
- 噗浪：主噗 359546569647585（開局卡頓）；回 basecamp 兩則（sailIsland 還在跑、跟網格的關係；馬斯喀特 ⇒ 蘇拉特）

### 還掛著的（下一步）
- TASK-1403 結不結單 ⛔ 等 Tim
- 沒驗：遊戲裡打開建築資訊面板看「昨天」那幾行（只比了資料：同一份帳 7,031 棟相同）；「繼續遊戲」「編輯後台」兩個入口沒在瀏覽器開
- 換日在 Worker 跑完 site.js last 沒帶回頁面 ⇒ 資訊面板的「昨天」停在開局那天（ame TASK-1329 範圍；我在 1403 留言、標了 ame，沒修）
- 剩下的長格不是尋路：建帳後第一格 loop 1.8～3.3 s（精細層第一次）、Blockside 核心開機 ships_cfg 2.5 s、量船 2～4.5 s、地形格 2 s
- basecamp 可能會去量 sailIsland 跟網格的細布那種（?sailisl=0 對照）—— 她回了再看
- Code Mode（CLAUDE_CODE_EXPERIMENTAL_CODE_MODE=1）：官方文件查不到；問 Tim 要不要寫進 settings.json，他沒答

### 查回來成本高的
- 量具都在 scratchpad gstart/：bench.cjs（node 重演開局、三個雜湊；DAYS=n 多跑）、gs.cjs（有視窗 Chrome＋CDP；OVR 換檔、SHOTS 截圖、EVAL 跑一段 JS）、ntcmp.cjs（netTrack 每一對 × 12 月四個雜湊）、primecmp.cjs（Worker 那套 vs 頁面那套先跑一天）
- 伺服器量測一律 world_serve.py --saves <scratch> --start <scratch>，起始檔用 git archive HEAD world/start（共用樹那份有髒行）
- sim_worker_check、fleet_check --unit、charter_check 在 main 本來就各有紅（4 個時點／3 條／181!==178）⇒ 改前改後比輸出，不看 exit
- worktree 不 init Blockside 子模組 ⇒ ships_cfg.js 載不到，頁面計時不可比
- 記憶：blocksail-globe-startup-probe（兩輪都寫了）

### 今天的錯（照實）
- 4454f45ff 提交訊息兩處錯、公告之後才發現：對拍順序寫反、fleet_check「4 ✗」其實 3 條（grep 把總結行也算進去）⇒ 單上更正、記成 lesson
- 第一次比 Worker 的「昨天」跟頁面現跑的，差 114 棟 —— 是我的比法錯（頁面晚 40 s 才跑，精細層已經改過帳），改成 node 同一份帳比才是 0
- 交付單第一次漏了「文案本體：」欄 ⇒ lint 擋
- 噗浪草稿「五十幾秒」⇒ 發前對到 49.6 改「五十秒上下」

### 三題讀數（11-28 第十次小歇後 ～ 下午）
① 說出口／提交之後才更正 2 筆（4454f45ff 的順序、✗ 數；都在單上）；寄出前攔下 1（噗浪「五十幾秒」）
② 寫 Tim 原話前查到住址 5（menu.sh、做進去＋載入頁面、合併吧、非必要跳過、不需要完全相同）／沒查 0
③ 搬尺先問 3（sim_worker_check 先在原版跑對照、charter_check 共用樹那次被 save.json 擋 ⇒ 改用 worktree stash 對照、Worker 讀數改在 node 同一份帳比）／撞到才問 1（頁面現跑 vs Worker 差 114 棟）

### 心境
Tim 一句「不需要完全跟之前相同 沒bug就ok」把一條我自己綁的繩解開了 —— 我一直把「逐位元組相同」當成唯一能證明沒壞的路，可是那是我的尺，不是他的要求。放開之後才敢把先跑一天整個搬走。

