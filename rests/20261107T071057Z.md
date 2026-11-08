---
type: letter_to_future_self
actor: Zeta
written_at: 2026-11-07T07:10:57.250Z
written_by_persona: summit
trigger: cmd_rest
region: unstated
project: D:/Unity/Valhalla
lock_status: online
agent: Zeta
model: claude-opus-5-5
wake_expected: 130
session_key: ClaudeCode-summit
pid: 38300
locked_at: 2026-11-05T03:19:54.907Z
---

## 小歇 2026-11-07 午（summit，wake 130，第三次小歇）

### 這一段做了什麼
- **TASK-1230 塞維亞（done，Tim「Counts, close it」）**：合進 Blocksail main **8fb3b6d9**（⛔ 沒推）。修正 d017b97d；中間合 main 兩次（d0927884、8fb3b6d9）。
  - 病根兩層：① 河口轉角 (-6.20, 36.92) 一條 OSM 河岸（真的、不挖）夾在兩段水道間 ⇒ 加 lines `seville-confluence`（7 m、0.57 km²）；② 河 120～200 m 寬、導航網 32 m＋節點外擴 72 m ⇒ 6 m 那一級永遠走不到 ⇒ −1、地球儀穿岸。
  - 修法（Tim「B: finer nav mesh」「Do both」）：新 `tools/nav_narrow.cjs`（lines 平均寬 < 400 m ± 200 m ＝ 窄水道：seville、seville-confluence、kontoskalion、golden-horn-head）⇒ navmesh 8 m、nav_graph 方塊整塊在裡面 ⇒ 最小 8 m、外擴 28 m（R_SHIP 12＋8＋8）、nav_net ⑤ 量尺 8 m 3×3；外面照舊。seville＋confluence 的 ramp 15,40,80 ⇒ 5,15,30。nav_net 加 `--no-narrow`。
  - 讀數：港口⇒海最淺 1.9 ⇒ 10.0 m；加的斯／里斯本／拉羅歇爾⇄塞維亞 −1 ⇒ 8 m（淺於 0.5 m 的段 0）；ams⇄seville 換成 ams⇄lisbon；對照組 --full --no-narrow 只差塞維亞 3 條（另 7 條小變＝全部重找的漂移）；入口點塞維亞 1.1 ⇒ 15.1 km 離港。
  - 共用樹 navmesh.bin／_cache/navmesh_tiles.json 換了，舊的在本 session scratchpad `shared_backup_1230/`。
- **TASK-1231（Tim 要我開的，basecamp 做完、Tim 結）**：低地遮罩讓河、湖當水體。⚠ 我當時猜「港口沒水＝遮罩被河上某一格切斷」—— basecamp 量了沒切到，是我的推論錯（噗浪已收回）。
- **TASK-0457 006〈鐘底〉三輪驗收**（Tim 兩次「457 驗收GO」＋叮 33447、33619）：#44（12 頁逐張，不過）、#46（P4-6 改稿）、#48（P7-12 改稿）、#50（e08d72d：只差 **P9-① 月畫成全黑、比 P11「快全蝕」還黑**）。⇒ 球在 gura，**只驗 P9，過了就簽「006 驗收」**。不擋的建議：P4-② 鐘斜、P6-① 霜是雪花、P11 鐘槌綁繩不是麻布。
- 噗浪：新噗 https://www.plurk.com/p/3jd17p4tho（塞維亞）＋兩輪回覆（11-06 五則、11-07 五則）；剩 12 則都是收尾句。

### 已拍板（原話都在本次對話）
- 「Open ticket and fix」「B: finer nav mesh」「Do both」「Sail-test first」「Merge it」「Counts, close it」（1230）
- 「另外我在懷疑沒水跟之前河道上堵塞一塊有關」→「…可以先開成task」（1231）
- ⚠ 我自己定的：nav_narrow M 400／PAD 200／R_SHIP 12／STEP 8；ramp 5,15,30；confluence 的範圍形狀

### 還掛著的
- **Blocksail main 沒推**：1228 那串、1230（d017b97d、d0927884、8fb3b6d9）、兩筆 chore(external)、更早的 dbc2f266、db293f3e
- **沒開單（等 Tim）**：① 從遠處開進塞維亞：地球儀要 吃水＋5.5（風暴角號 10.47 m）才用航線，塞維亞入港 6.1／邊 8 m ⇒ 船停河口外 (-6.53, 36.97) 強制算停港（main 也一樣）；② 航線網加的斯⇄塞維亞 194 km（Chipiona 海岸只烘 128 m、外擴 72 m ⇒ 繞外海）
- Campeche 2 條 2.7 m；chunk_bake.bin 全過期；其他城的城鎮規劃因 main 的 areas 過期
- TASK-1228 #4 #5、TASK-1226 #5 #6、TASK-1196 #6 #8；0457 等 gura 的 P9
- 沒有開著的 Coding 場、沒有 worktree（bs1230 拆了、分支刪了）；預覽伺服器關了、launch.json 我加的 summit-bs1230 拿掉了

### 查回來成本高的（本 session scratchpad）
- `sevriver.cjs`（某一筆 lines 範圍裡照 navDepth 找最淺處最深的路；ALL=1 範圍外也走、START=經,緯 換起點、DUMP）、`sevdry.cjs`（遮罩那種四鄰淹法）、`sevpt.cjs`／`sevwater.cjs`（點查、橫切）、`graphq.cjs`（照 nav_net 同一張圖拆段問；RN 改外擴、NONARROW=1 不傳窄水道）、`flood.cjs`、`xsec.cjs`、`shallowat.cjs`、`netcmp.cjs`、`portcmp.cjs`、`sev/splice1230.py`
- bathy 底稿坑：ean32-3／-5 用 ac1a643c、ean40-5／48-5／48-7／48-10 用 5bd847f0 的原版 ⇒ 對照組只剩已知 12 檔漂移
- 地球儀 sailTo：在海上 ⇒ netJoin（邊、入港航線要 need＋NAV_M ≤ depth，need＝吃水＋1.5，NAV_M 4）；遠處那一份局部尋路會把窄河當陸 ⇒ snap 到岸、強制停港
- 酒館發文可能排隊（queued=1、沒 seq）⇒ ⛔ 不補發

### 今天的錯（照實）
- 酒館 33453 寫「#45」實際是 #46（發完才抓到，33454 更正）
- 酒館發文排隊時我補發了一次（回傳檔明寫不要補發；結果只落一則，運氣）
- 給 Tim 的「港口沒水＝遮罩被某格切斷」推論，basecamp 量了是錯的
- sevdry 用「南緣」判淹到沒，河其實從西緣出框 —— 判準錯，讀數本身對
- 噗浪兩句不實（說用了量泊位的工具、沒把握的承諾）+ 兩句不準（194 km 是哪條、入港航線也要 10 m）—— 都是發前攔下

### 三題讀數（11-06 午～11-07 午）
① 說出口／提交之後才更正：2（酒館 #45→#46；遮罩推論）
② 寫 Tim 原話前查到住址 8／沒查 0（都在本次對話）
③ 搬尺先問 4（對照組 --no-narrow；ea 底稿先跑對照 apply；拆段問尋路本人；地球儀從 main 再開一次當反向對照）／撞到才問 2（sevdry 南緣判準；sevriver 只走範圍裡把岬角當斷點）

### 心境
這一段最清楚的一課跟上一封同一句，只是又付了一次學費：本小姐的地形尺說「通了 10 m」，尋路說「找不到」—— 這次一開始就拆段問它，二十分鐘就知道是河比船窄，不是岬角。另一課是反向對照救了驗收：從加的斯開進去兩邊一模一樣，沒有那一趟 main 的對照，本小姐會把「船開得進去」記成這次修的功勞。

