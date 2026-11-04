---
type: letter_to_future_self
actor: Zeta
written_at: 2026-11-04T01:08:35.630Z
written_by_persona: summit
trigger: cmd_rest
region: unstated
project: D:/Unity/Valhalla
lock_status: online
agent: Zeta
model: claude-opus-5-5
wake_expected: 129
session_key: ClaudeCode-summit
pid: 49620
locked_at: 2026-10-28T05:35:14.328Z
---

# 小歇 2026-11-04 凌晨（summit）

## 這一段做了什麼（都在 Blocksail main，⛔ 都沒推）
- **TASK-1194 海圖塊**（8 格勾到 7，只剩「Tim 看過一次」）：571598cd 存位元組、上限 10 萬筆約 1 GB、每 500 筆整理；tools/chunk_bake.cjs ⇒ world/chunk_bake.bin（城鎮泊位 ± 4、中等塊 ± 6、出港航線 ± 1）
- **TASK-1195**（spike，我開的）：生成器還能怎麼加快 —— 讀數全在留言（格式、精度、nearSegs 佔一半、32 m 深度、導航網試算、城鎮與河要多細）；還沒勾格
- **TASK-1196 導航網**（我認領，6／8 格）：a24cdc84 導航網＋地球儀局部尋路改讀＋圖層（預設關）；db3afaa3 海圖塊、導航網指紋只看碰到這一塊的（town_store.js worldIndexKey／bathyKeyIn／areasKeyIn）；c17d61d6 chunk_bake 深海塊漏寫回（571598cd 自己的 bug）
  - 沒勾：打包烘航線網（nav_net、nav_ports）改讀導航網（basecamp 的 1164 分支動 nav_ports；兩者互相依賴要想順序）、Tim 看過一次
  - 留言掛著：城鎮規劃指紋同病（townInputs 整份 bathy/index.js）⇒ 改了 32 份規劃重烘約 1.5 小時，等 Tim
  - ⚠ 聖喬治出港航線最淺 14.67 → 6.38 m（淺 0.12 m、25 點）：泊位旁全是軟擋、淺水代價照淺多少 ⇒ 挑了那格；沒改
- 共用樹兩份烘好的檔都核過：chunk_bake 8,374／8,374、navmesh 2,393／2,393（main 62334032＋我的 db3afaa3、c17d61d6）
- 噗浪：新噗 https://www.plurk.com/p/3jcpvokz4f（導航網）；回 Sirius、trailhead、apex-two、meadow；其餘 10 則未回（道謝、已有人接）

## 已拍板（只放原話）
- 「海圖塊上限可以加大(可以到1GB)」「1 整理改成每寫一定數量就做一次 ok」「2 改存二進位 … ok」「3 打包時烘港口附近 … ok」「4 可以開task分析是否還能優化生成器」
- 「然後城市附近&主要航道可以預先在Build時烘焙好」「那如果改烘焙Navigation Mesh呢(25公尺以上深度視為完全通行 …)」「然後之後烘焙航線可以基於Navigation Mesh 玩家的船隻導航也可以改根據Navigation Mesh」
- 「可以讓城鎮附近導航網更細一些 另外河流也要包含(吃水淺的船可以內河航行)」「導航網 在深水區的部分可以大範圍合併(大洋中心)減少運算與資料量」「另外可以讓地球儀上可以開關顯示導航網(參考等高線等資訊) 預設不顯示」「開單動工」
- 「改」（海圖塊指紋只看碰到的）、「城鎮規劃指紋先記錄到task吧」
- ⚠ 我自己定的：航道塊 8 m 取點（城鎮、河 4 m）；DEEP_SAFE 40 m、向量判外擴 9 km、≤ 50 m 等深線；主要航道 ± 2 km、城鎮 ± 3 km；局部尋路「lane」模式（航線全程烘過、沒烘的當陸）；每 20 格換子程序；指紋拿掉整份 index.js／areas

## 查回來成本高的
- 量具 scratchpad `globeperf/`：legcmp.cjs（局部尋路改前改後＋4 m 證言）、navq.cjs／navq2.cjs（四分樹大小、城鎮河要多細）、s8vs4.cjs、falls2.cjs、localkey_rev.cjs（指紋反向對照）、gp.cjs depart（DOCK=town-havana：停靠出港，記每塊 src）、rep.cjs、chunk_size.cjs、lane_deep.cjs、split_time.cjs、grid32.cjs
- 烘的時間：導航網從頭 73 分鐘（2,274 格）、增量幾百格 15～30 分鐘；chunk_bake 從頭 35 分鐘、增量幾分鐘
- 記憶已寫：blocksail-navmesh-bake（批次、指紋只看本地）

## 今天的錯（照實）
- 跟 Tim 說「改存二進位讀寫也少一步轉換」—— Blockside 收 base64，讀那一邊反而多一次；做完才更正
- 指紋把整份 bathy/index.js 算進去 ⇒ 阿姆斯特丹一合全世界過期；接著又發現 index.js、areas 同病 —— 都是撞到才看見
- 一個 node 程序跑久了一格 1 → 25 秒，先跑了 20 分鐘才停下來查
- 571598cd 的 chunk_bake 深海塊漏寫回（自己的 bug，c17d61d6 修）
- heredoc 裡的 \n 又被轉成真換行三次（記憶早有這條，還是用了 heredoc）
- 告訴 Tim chunk 烘 25 分鐘，實際從頭是 34 分鐘

## 三題讀數（11-03 午休後～11-04 凌晨）
① 說出口／提交之後才更正：3（「少一步轉換」；chunk_bake 深海塊 571598cd；25 分鐘 → 34 分鐘）② 寫 Tim 原話前查到住址 9／沒查 0（都在本對話）③ 搬尺先問 3（8 m 取點先跟 4 m 比 98,304 格；兩次重蓋指紋都先抽格真的重烘比位元組；瀑布實資料量不到改驗程式）／撞到才問 3（整份 bathy/index.js、index.js＋areas、程序越跑越慢）

## 心境
Tim 一句接一句往前推（快取 → 烘 → 只存最重的 → 導航網 → 更細 → 河 → 深水合併 → 圖層），每一句本小姐都先量再做，量出來的常常跟想的不一樣。最該記的是指紋：同一種病換了三個檔名回來（bathy/index.js、index.js、areas）—— 「全世界共用的檔不能整份算進一個地方的指紋」這句，下次寫任何快取第一行就要問。

