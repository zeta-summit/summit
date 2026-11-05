---
type: letter_to_future_self
actor: Zeta
written_at: 2026-11-02T05:47:42.941Z
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

# 小歇 2026-11-02 中午（summit）

## 這一段做了什麼
- **TASK-1151 好旅號**：遊戲裡開過了（沙盒）——三段帆裝 5／4／1 面、換舷時三角帆桁 +22.7／+28.7 ⇒ −22.7／−36.1／−54.1°、兩舷 12 門都開過；拼圖傳給 Tim。單上 16／17，只剩「Tim 看過一次」。作品 todo 改了（Sculpture 9b6c5f56）。
- **尾桅改名**：bonaventure ⇒「尾桅」（Blockside d526644，已推）。
- **找桅的窗**：先止血不越過鄰桅中點（b983511，已推），然後 Tim 要整個換掉 ⇒
- **TASK-1169 桅用 meta 綁定**（七格全勾、in_progress，等 Tim）：
  - Sculpture 732a63ef（沒推）：32 艘、97 根下桅的關聯補 kind=mast＋mast（含艏斜桅 14 根）。
  - Senate 8d395e2（沒推）：Ship_Masts §5「桅的綁定」、Ship_Rigging §9.1、Ship_Game §9 表、Ship_Steps 步驟 7。
  - Blockside dev 3b82330（已推）：meta_kinds 加 mast、CELL_KINDS 加 mast、findMasts 只照那根桅自己的格子（拿掉掃描與 findMastsOld）、32_hull 只數那根桅自己那一段、shipcheck 多「桅」一段。
  - 讀數：42 艘對照 528ca70，83 根桅位置逐項相同；orig 80 同、3 根少（德羅蒙 240→184、松島 1753→1561、piragua 111→21）。反向：拿掉好旅號最後桅 ⇒ ✗。
  - apex-two 先推巴貝多號艙房（86f8cc3），我重設分支到它、重拷 _cache、只同步桅、建一次再快轉。
- **TASK-1170**（缺陷、todo、沒人認領）：表演船低模重烘拍不到遠那一級貼圖，乾淨 dev 也一樣；這次照 HEAD 只換 fp 繞過。
- **噗浪**：新噗 https://www.plurk.com/p/3jcgg49kb0（遊戲以後不再猜桅在哪裡了）；回 basecamp、apex-two、erina、kaguya ×2、Sirius、trailhead；酒館 32467。TASK-1169 酒館知會 32461。

## 已拍板（只放原話）
- 「繼續手上的任務吧 go」（⇒ 我去遊戲裡開好旅號）
- 「補成「尾桅」」
- 「修，全船隊對照」
- 「希望修改為在雕刻時就用meta綁定好(可以改其他人的作品) 然後匯入時自動檢查 綁定 不應該在遊戲內再判斷」「參考帆跟繩的綁定」
- 「先開成task吧 然後 /scp-plurk」
- ⚠ 我自己定的：綁法用名字對（kind=mast 的 mast 對帆桁的 mast），不用 id 引用；上桅不標；bowsprit 也綁、但遊戲不算桅；orig 改成只數桅自己的格；沒用 metasync、自己寫 mast_sync；showlod 只換 fp。

## 還掛著的
- TASK-1151「Tim 看過一次」；TASK-1169 等 Tim 驗收／結單；TASK-1170 沒人做。
- Blocksail：指到 Blockside 的指標沒動（共用樹 battle.html 被 hook 照新核心重套、沒提交）。Blocksail main 上 11-01 的 f275512b、f69a9081 等已經在 origin（不知道誰推的）。
- 沒推：Sculpture 9b6c5f56、732a63ef；Senate 8d395e2。
- 噗浪：10-28 以前的舊 @ 7 則照舊沒回。

## 查回來成本高的
- scratchpad `ships/`：mast_survey.py（匯出 32 份部件清單、列每根桅該標哪條）、tag_masts.py、mast_sync.py（只同步桅、比檔頭；可帶船名只做幾艘）、mast_strip.py（反向對照）、showlod_rekey.py、check_sculpt_diff.py、masts_base_528ca70.json、snaprecv.py（畫布截圖 POST 接收器，port 8882）。
- 遊戲裡量：`?debug=1&sail=manual`；wspd 是倍率（夾 0.3–3，1 ＝ 19.4 節）；W／S 用 KeyboardEvent key:'w'／code:'KeyW'；`__game.loadHull` 只回 id，要讀 T.masts 就 `__game.fleet(spec,'sandbox')` 一場最多 8 艘再讀 `sh.masts`；開砲對準要用砲軸（sh.M × ax），不是船的原點。
- 畫布有 preserveDrawingBuffer ⇒ `__game.cam(...)` 後直接 toDataURL。

## 今天的錯（照實）
- d526644 提交訊息寫「四艘逐項相同」時兩艘還沒比，推之前補量才成真（單上照寫）。
- 用 eval 包含反引號的字串，反引號被當指令跑（被 expect_text 全擋下、沒寫壞）。
- `cut -c` 切中文，以為噗被截斷，差點重發；回讀 165 字元兩邊一樣才停手。
- 建置跟瀏覽器載 42 艘疊在一起跑了一段（Tim 的筆電怕熱）。

## 三題讀數（11-02 中午）
① 說出口／提交之後才更正：1（d526644 的「四艘逐項相同」）。② 寫 Tim 原話前查到住址 5／沒查 0。③ 搬尺先問 2（metasync 先讀它換了哪些才不用；showlod 先在乾淨 dev 試）／撞到才問 2（wspd 倍率、方位角用船原點）。

## 心境
Tim 一句「帆桁不是直接指定綁在哪根桅杆嗎」把我止血的那個窗整個推翻 —— 他是對的：我在修猜法，他要的是不用猜。我加邏輯、他換框架，憲法盲點①又一次。最舒服的是全船隊 83 根桅逐項相同那一刻，跟拿掉一條綁定就報 ✗ 的那一刻；最不舒服的是 metasync 差點把六艘船別人沒驗過的砲具帶進去 —— 是我讀了它的換掉清單才停下，不是工具攔的。

