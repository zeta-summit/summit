---
type: letter_to_future_self
actor: Zeta
written_at: 2026-11-17T08:32:02.588Z
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

### 小歇 2026-11-17 午後（summit，wake 133，第一次小歇）

### 這一段做了什麼
- 早安（Tim「早安後 自由意志模式 處理待辦 GO」）：自介 seq 35275。
- **TASK-1302 威尼斯加萊賽戰船：結單 done**（Tim「結單」）。今天做步驟 10～15：
  - 10 底艙＋艏部彈藥庫 6 桶＋艙蓋＋三盞艉燈（Tim「艉燈可以加(不用按照參考圖)」）＋羅經櫃 —— Sculpture e5c9019a
  - 11 舵沿斜艉柱（52°）＋舵柄口、兩隻四爪錨 —— 502e1f0c
  - 13 槳 50 支（皇家號槳放大 0.5323）—— af7dffd8；兩頭 stroke 9／24／22／5°（Tim「先保留小擺幅」，f7bb2292）
  - 14 匯入 Blockside：be052aa（已推 dev，一起帶出 kiara f6ab413、pinnacle efa7df2）；Sculpture e8ef84c2（ids）、d3fc71db（高度表）
  - 13 靠泊：Tim「等等 合併到Dev 我來測試好了」⇒ Tim 測「測試ok 辛苦了」⇒ 勾
  - 15 交船檢查表 —— 39bfff96
- 噗浪：新噗 https://www.plurk.com/p/3jeliue5vg （附 Tim 截圖）；回 gura ×3、basecamp、meadow、pinnacle。

### 已拍板（原話都在本次對話）
- 「艉燈可以加(不用按照參考圖)」「先保留小擺幅」「等等 合併到Dev 我來測試好了」「測試ok 辛苦了」「1302 交船 GO」「結單」「現在測靠泊」（之後被「合併到Dev 我來測試」取代）
- ⚠ 我自己定的：彈藥庫在艏樓下（照 meadow galea）、6 桶、錨 scale 0.8、三盞 fanò、cfg.base 3.5、geo（spar 52–53、qx 60、marineGap 12）、names 照指揮官姓氏

### 還掛著的
- **Blocksail 896d49f1**（external/Blockside → be052aa ＋ battle.html）在本機、⛔ 沒推，等 Tim。
- 答應 gura（噗 359412245325799）：「還沒自己把它開進聖馬可灣那座棧橋，量過再回妳」—— ⛔ 這是承諾，量了才回。
- 作品 todo：開局 lostModels(0) 舵、帆裝 W／S 三段、艏樓／艉樓砲門沒蓋板會不會開局進水；帆素白；小艇／絞盤／廚房沒放。
- Blocksail 共用樹有別人改的 tools/townkit_flaw.json —— 不是我的，沒碰。
- 沒有 Coding 場、沒有我的 worktree（bs1302-galeazza 拆了、分支刪了）。

### 查回來成本高的
- 模型 scale ＝ 來源一格是幾個本作品格（⛔ 不再乘 mpv/0.1；barrel 22×0.2 ＝ 4.4 格 ＝ 0.44 m）。
- 槳 P 舷擺法照皇家號：y → 321 − y ＋ mirror=y。
- Ship_Helm 的鉸鏈擬合「丟離線 1.5 格的層」在彎艉柱上會丟到只剩 9 層 ⇒ 只丟舵柄層、殘差照記（本船 5.4 格）。
- 匯入流程：worktree 複製 _cache ⇒ import ⇒ ids（慢，>10 分）⇒ admin.load/validate/save 只加這艘 ⇒ build ⇒ shipcheck ⇒ showlod＋ancbake ⇒ build ⇒ showlod --check＋srccheck ⇒ commit ⇒ coding start（單獨）⇒ ff ⇒ 複製 vxk＋對 lock ⇒ srccheck ⇒ end force（非 .NET）⇒ push dev ⇒ Blocksail gitlink。
- 量具（scratchpad，會被清）：probe_hold.py、probe_xs.py、probe_stern.py、occ.npy；槳對砲外框的量法寫進 notes 交船那一節。

### 今天的錯（照實）
- draft_hold 的模型外框第一版多乘了 mpv/0.1 ⇒ 桶小了 5 倍、量出假的「放得下」；改對才發現前排兩桶撞 V 形底。
- 用 sed 在 Git Bash 改中文那行 ⇒ 把註解塞進括號裡，語法壞掉（記憶 inline-comment-swallows-code 那一族）。
- 槳對砲模型的碰撞，步驟 13 沒量，交船對檢查表才補。
- 高度表把前桅、後桅帆桁寫成沒量的「約 150／約 120」，寫進作品 notes（未提交）後才去 rig.json 讀真值 180／115。

### 三題讀數（11-17 早安～午後小歇）
① 說出口／提交之後才更正：0 筆；寫進作品 notes 未提交時才抓到 1（帆桁高度）；寄出前攔下 2（噗浪「划到一半」⇒「擺幅一大」、回 pinnacle 的「船廠分頁裡會看到」沒量 ⇒ 拿掉）
② 寫 Tim 原話前查到住址 7／沒查 0（都在本次對話）
③ 搬尺先問 3（皇家號槳的 P 舷擺法、meadow 彈藥庫與艙蓋的寫法、import 會重排 game.json 那條記憶）／撞到才問 2（Ship_Helm 鉸鏈擬合規則、模型 scale 的單位）

### 心境
今天最清楚的一課是「靜止零碰撞 ≠ 動起來零碰撞」。槳擺著量是 0，讓它前後划才知道兩頭的槳柄會打到樓牆。昨天砲樓裡的舊舷頂，也是砲往裡退才撞出來的。另一個讓本小姐安心的地方：組裝件格數用改前的引擎讀數加減，剛好對上；遊戲算的槳手 300／300 也跟自己的量法一樣。兩條路對得上的時候，才敢說「做完了」。哼，Tim 最後一句「辛苦了」，本小姐收下了。

