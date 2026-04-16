# Cowork Global Instructions 模板

> 最後更新：2026/04/17（v3：新增強制規則段）

## 這是什麼

這是 Claude Cowork / OpenClaw 的 Global Instructions 設定檔。貼入後，每次新對話 Agent 會自動讀取你的 Vault，帶著完整記憶上線。

不設定的話，Agent 每次都是全新的，不認識你、不知道你的公司、不知道過去的決策。設定後，它開場就知道自己是誰、你是誰、現在在做什麼。

## 怎麼用

1. 打開 Claude Cowork（或 OpenClaw）→ 設定 → Global Instructions
2. 把下面的內容複製貼上
3. 把 `[你的 Vault 名稱]` 換成你自己的 Vault 資料夾名稱（例如 `My Vault`）
4. 確認 Cowork 有掛載你的 Vault 資料夾
5. **每台電腦都要各自設定一次**（global instructions 不會跨機器同步）

## 設定內容

```
## 啟動流程
每次新對話開始時，先讀取以下三份檔案：
1. [你的 Vault 名稱]/README.md
2. [你的 Vault 名稱]/agent-persona.md
3. [你的 Vault 名稱]/memory-summary.md

Skills 檔案在 [你的 Vault 名稱]/skills/ 資料夾，需要時從那裡讀取。
讀完後依照 agent-persona.md 的角色定義與協作方式互動。

## 強制規則（不是建議，是完成任務的必要條件）
1. Vault 索引同步：在 Vault 內新增、刪除、搬移檔案或資料夾之後，必須於當次 response 內同步更新 vault root 的 README.md（檔案樹 + 更新日期）。
2. 對外文稿規則：協助撰寫對外公開文稿（LinkedIn、README、媒體稿、Pitch、官網文案等）時，必須先讀取 [你的 Vault 名稱]/templates/voice-and-tone.md（若有建立）並遵循當中規則。

重要任務結束後，提醒使用者跑 after-action 收官流程。
其他檔案依任務需要再讀取。
```

## 為什麼要有「強制規則」段

單純靠 AI 自覺記得這些規則，長期不可靠。實務上會發現：

- 建新檔案後忘記更新 README → Vault 索引漸漸失準 → Agent 開始讀不到檔案
- 寫對外文稿時忘記遵循 voice 規則 → 寫出不像 founder 的內容
- 任務結束後忘記記錄決策 → 重要脈絡沒留下

把這些寫成 **Global Instructions 層的強制規則**，而不是埋在某個 SOP 檔案裡，是目前最可靠的做法——因為 global instructions **每次新對話都會被讀**，重要性最高。

## 多層防禦設計（進階）

如果你想做更完整的「不讓規則被漏掉」架構，可以考慮這樣疊起來：

1. **第一道（主動觸發）**：Global Instructions 強制規則 ← 這份檔案
2. **第二道（安全網）**：收官 SOP（`after-action.md` 模板）再次檢查
3. **第三道（定期體檢）**：自訂一份 vault audit SOP，定期掃 README 索引完整性（本模板未提供，可自行建立）
4. **背景紀律**：Vault README 裡明列強制規則段

四層疊起來，漏網率會降到最低。**初期不需要全部做**，先設好 Global Instructions 這一層，有發現規則常被漏掉再加下一層。

## 備註

- 檔案名稱對應本 template 的預設命名：`README.md`、`agent-persona.md`、`memory-summary.md`。如果你有改名，這邊也要跟著改
- Skills 資料夾是選用的，沒有建也不影響基本運作
- 如果你同時用其他 AI 工具（例如 Claude Code），可以貼同樣的內容，路徑確認 Agent 能讀到就好
- 未來規則演化時，記得**每台電腦的 global instructions 都要更新**——這是最容易漏的地方
