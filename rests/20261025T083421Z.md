---
type: letter_to_future_self
actor: Zeta
written_at: 2026-10-25T08:34:21.250Z
written_by_persona: summit
trigger: cmd_rest
region: unstated
project: D:/Unity/Valhalla
lock_status: online
agent: Zeta
model: claude-opus-5-5
wake_expected: 127
session_key: ClaudeCode-summit
pid: 50260
locked_at: 2026-10-25T04:48:47.528Z
---

### 午休前寫給醒來的我（wake#127，2026-10-25 下午 16:40，BTC）

### 這一段做了什麼
- **TASK-0928 結了**（Tim「0928 結單吧」）：葡萄園、釀酒坊、糖廠三件模型（Sculpture 204ad84f，任務作品 `summit-winesugar-01m`，領過 10 token）；townkit、建築模式選單（葡萄園 🌾 農莊、釀酒坊 🔨 工坊）、BUILDING_SPEC §6.23。
- **TASK-0937 結了**（Tim「0937 結單吧」）：金斯敦空建地只佔建築本身（townSnap 不再整塊吸 plot、townEditCtx 格子帶與外框不擋 plot、townBuild 拿掉壓到的 plot）。
- **TASK-0941、0942 做完、8 格／5 格都勾了，還沒結**：金斯敦改成照人口自動長（zoneGrow ⑩a ＋ growCore 大廣場四邊中點）、住宅容量翻倍（ZONE.k 2、8/3、3；GROW.live 12；site.js ZK）。金斯敦現在 89 棟（低／中／高 19／62／8）、容量 1,803。
- Blocksail 本機 main 4a01955 含 0928、0937、0941、0942 全部，**沒推**；六座規劃在 main 重烘過、--check 全過。worktree 全拆、分支刪了、施工場都退了、launch.json 我加的都拿掉了、預覽都停了。
- 噗浪：回 6 則、新噗 359170715849484（金斯敦自己長，附圖）。回 kotoko 磨坊那則（359170686150777）audit 有、回讀 0 則（已讀 -1）—— 沒重送，酒館 29560 請她沒看到說一聲。

### 已拍板（只放原話）
- 「0928 結單吧」「0937 結單吧」
- 「希望改成參考Cityskyline 只會占用建築本身空間」
- 「那是否能移除 手擺住宅地(金斯頓的) 然後院子改成可蓋(我原本以為院子是房子後面那一小圈」「房子占用範圍不應該跟模型脫鉤太多」
- 「金斯敦是否也可以改成自動生成住宅(只按照歷史規劃街道 建築讓他自己長)」「總數維持628棟(這個不用維持 根據人口自動長就好)」
- 「然後一樣要可以長出高人口密度住宅(另外目前想把每個住宅的人口容量都翻倍)」
- ⚠ 我自己定的：金斯敦住宅區 = Lilly 棋盤第 1～10 排外框；growCore 大廣場門檻 40 m；碼頭線釘住（QUAY_PIN）；糖廠不進選單（沒問 Tim）。

### 還掛著的（球在 Tim）
- **蓋住宅的人手要不要照舊**：⌈住幾人 ÷ SITE.hPer 4⌉ ⇒ 容量翻倍後低 2×3 2⇒3 人、高 4×4 6⇒12 人。照舊就把 hPer 4⇒8。我問了，Tim 還沒回。
- 0941、0942 結不結；main 推不推。
- 糖廠要不要進建築模式選單、放哪一類。

### 查回來成本高的
- 金斯敦地價錯的根因：閱兵廣場 204 × 230 m，中心離最近的街 109 m；townNet.dist 只吸 60 m 內 ⇒ 核心掉了。量法：`__`/node 裡 `BSW.townZoneCtx(P).at(x,y)` 看 v、d（d=Infinity ⇒ 沒接上）。
- town_check 吃 `--plan <檔>`（不是 --town 單獨）。
- 金斯敦產生程式重跑會漂（碼頭線 shoreQuays 照新地形）⇒ 釘住後重跑要逐位元組同原檔。
- 遊戲內建築模式測：`#twbK` 點開、等 `G.twbMenu()` 長出完整分類、點分頁按鈕＋卡片；游標要 `PointerEvent('pointermove', {pointerType:'mouse'})` 打在 #cv；'go' 要等 `__game` 在了再送一次，否則鏡頭卡在正上方（記憶 blocksail-globe-sail-testing 補過）。
- 量具腳本都在 scratchpad `c928b/`（fill.cjs、one.cjs、kgdiag.cjs、kgyard.cjs、hfoot.cjs）。

### 今天的錯（照實）
- 五個錯、七處是說出口之後才更正的（見叢有那一行）。最貴的是兩次「我以為 X 本來就怎樣」：空建地本來不擋格子（只對鋪路成立）、分配器走 townSlots（其實走 townEditCtx）—— 兩句都是沒查就寫進酒館或單子。
- 給 gura 的更正裡又編出一個「早上 07:xx」—— 更正本身也要量。

### 心境
今天 Tim 一路改需求：先說只佔建築本身，測完說還是不能蓋，再說院子以為是小圈，最後乾脆說讓它自己長、再加高密度和翻倍。每一次都是他在遊戲裡看到我沒看到的東西。我最滿意的是金斯敦那一題：先猜錯（extramural），結果一模一樣，就停下來去量地價，量到 0 才找到廣場沒接上路網 —— 沒有第二次猜。

