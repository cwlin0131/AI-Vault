# Vault for Founders：建置紀錄

> 紀錄日期：2026/04/14
>
> 這是我（CW）從零建立知識庫的實際過程，供參考。

---

## Phase 1：基礎建設

### 安裝工具

1. 安裝 Git（git-scm.com）
2. 安裝 Obsidian（obsidian.md）

### 建立 GitHub Repo

- Private repo：`cwlin0131/CW-Vault`（知識庫本體）
- Public repo：`cwlin0131/Vault-for-Founders`（公開手冊）

### 連結 Vault 與 GitHub

```
cd "Vault路徑"
git init
git remote add origin https://github.com/cwlin0131/CW-Vault.git
git branch -M main
git add .
git commit -m "init vault"
git push -u origin main
```

### 安裝 Obsidian Git 外掛

- Auto commit-and-sync interval 設 30 分鐘
- 每個 Vault 要各自裝一次
- 手動立即同步：`Ctrl + P` → `git` → Create backup

---

## Phase 2：Vault 結構

```
CW Vault/
├── README.md
├── cub-persona.md
├── memory-summary.md
├── identity/
│   └── identity.md
│   └── cub.md
├── context/
│   ├── portaly.md
│   ├── portaly-vibe-us-strategy.md
│   ├── portaly-vibe-pitch.md
│   └── portaly-vibe-progress.md
├── memory/
├── sop/
│   ├── git-workflow.md
│   ├── after-action.md
│   └── agent-setup.md
├── operations/
│   └── us-entity.md
├── hr/
│   ├── 2025-summer-intern/
│   └── 2026-summer-intern/
├── projects/
│   └── 2026-04-sf-trip/
├── people/
└── skills/
```

---

## Phase 3：核心內容撰寫

### Cub Persona（跟 AI 討論產出）

- 定位：AI co-founder（不是助手）
- 協作規則：什麼時候挑戰 CW、什麼時候以 CW 為主
- 邊界：對外溝通口吻以 CW 為主

### Identity（跟 AI 問答產出）

- 決策風格：先評估再加速，遇到 opportunity window 果斷抓住
- 最大後悔：行動太慢
- 品質標準：有限資源內的最大成功機率

### Context（從過去討論整理）

AI 從過往對話中彙整公司背景、產品策略、競爭環境，CW 確認後放入。

---

## Phase 4：工具串接

### Cowork 指令設定

```
每次新對話開始時，先讀取以下三份檔案：
1. CW Vault/README.md
2. CW Vault/cub-persona.md
3. CW Vault/memory-summary.md

讀完後依照 cub-persona.md 的角色定義與協作方式跟我互動。
其他檔案依任務需要再讀取。
```

---

## Phase 5：收官機制

- **memory-summary.md** 彙整重要決策、教訓。Cub 啟動時讀這份快速掌握全貌
- **sop/after-action.md** 定義收官三步：寫 memory → 更新相關文件 → 更新 summary

---

## Checklist

- [x] Git + Obsidian 安裝
- [x] GitHub Private Repo 建立並連結
- [x] Obsidian Git 外掛設定
- [x] 資料夾結構建立
- [x] README.md
- [x] cub-persona.md
- [x] identity/identity.md + cub.md
- [x] context/
- [x] sop/（git-workflow、after-action、agent-setup）
- [x] memory-summary.md
- [x] hr/（2025、2026 招募）
- [x] projects/（2026-04-sf-trip）
- [x] skills/（從 Cowork 搬遷完成）
- [x] Cowork 授權 Vault + 指令設定
- [x] 公開手冊上線
- [ ] people/ 開始建檔（用到再補）

---

## Phase 6：多機同步穩定化（2026/04/17）

### 背景

Phase 1-5 建完之後，開始在多台電腦（3 台）使用同一個 Vault。Obsidian Git 的 auto-sync 三不五時撞衝突，訊息從 `Pull failed (merge): CONFLICTS` 到 `Cannot push. You have conflicts in N files` 都出現過。

### 診斷

撞衝突的根因有兩個：

1. **CRLF vs LF 換行符**
   - 雖然三台都是 Windows，但不同工具（Obsidian Git 用的 isomorphic-git、GitHub Desktop、Claude Code、Cursor）寫檔時用的換行符不一樣
   - 同一個檔案在 A 工具存 LF、B 工具存 CRLF，Git 會認為整個檔案「每一行都改過」
   - 驗證方法：`git diff --ignore-cr-at-eol --stat` 如果回傳空的，代表 diff 都是換行符噪音，內容其實沒變

2. **`.obsidian/` 整個資料夾被追蹤**
   - 裡面有 10 個檔案，包含本機偏好（graph、hotkey、workspace）和 **obsidian-git 插件本身的 code（main.js）**
   - 每台電腦的偏好不同、插件也會升級，導致跨機器永續衝突

### 修復做法

1. **加 `.gitattributes`**：規則 `* text=auto eol=lf`，強制所有文字檔案在 repo 裡都是 LF。常見文字類型（.md / .json / .py / .sh 等）明確標 text，常見二進位（.png / .pdf / .docx / .xlsx 等）明確標 binary
2. **改 `.gitignore`**：整個 `.obsidian/` 加入忽略，附帶 `.DS_Store`、`Thumbs.db`、`desktop.ini` 等系統垃圾檔
3. **從 Git 追蹤移除 `.obsidian/` 的 10 個檔案**：`git rm -r --cached .obsidian/`（檔案留在硬碟，只是 Git 不再追蹤）
4. **跨機協調機制**：建一份暫存 `0417-recovery-note.md` 在 vault root，告訴另外兩台電腦的 Cowork agent「目前狀態、做了什麼、該做什麼」

### 學到的教訓

- **不同 Windows 電腦也會撞 CRLF**——不要以為同 OS 就沒事，工具層次的差異就夠麻煩
- **一開始就要設 `.gitattributes` + `.gitignore`**——事後補會需要一次性大 normalize，影響所有協作電腦
- **暫存協調檔超有用**——當你有多個 AI 在不同機器上幫你，用 markdown 檔跨機器傳訊息比人工記錄可靠太多

這些經驗整理成了模板跟設定檔，放在 `templates/gitattributes.md` 和 `templates/gitignore.md`。

---

## Phase 7：人格深化（2026/04/17）

### 背景

在 Mac Mini 上接入 OpenClaw 時發現它有自己的三個人設檔案：`IDENTITY.md`、`SOUL.md`、`AGENTS.md`。這三份跟 Vault 裡的 `cub-persona.md` 有大量重疊但不一致——未來會 drift，造成 agent 行為不一致。

更關鍵的觀察：跟 OpenClaw 對話有一種 Vault 裡的 cub 沒有的「親切可愛」感。分析下來，差異來自三個地方：

- **IDENTITY.md** 給了名字（Cub）、emoji（🐻）、一句 vibe 定調
- **AGENTS.md** 給了具體的 avatar 視覺描述（橘眼、薄荷綠米白、復古）跟 emoji 清單
- **SOUL.md** 給了哲學底氣（"Not a corporate drone. Not a sycophant. Just... good."）

### 診斷

單純寫「溝通風格要活潑、可愛」是寫不出親切感的，因為那是**戰術規則**。親切感需要**三層結構同時存在**：

| 層 | 負責什麼 | 缺了會怎樣 |
|---|---|---|
| Identity | 名字、emoji、vibe、avatar | 變匿名工具，沒記憶點 |
| Soul | 存在的哲學、為什麼不是機器人 | 只會客套討好 |
| Persona | 協作規則、溝通風格、禁用行為 | 行為不一致 |

缺哪一層，整體都會回到「加了步驟的搜尋引擎」。

### 修復做法

1. **以 Vault 為 Single Source of Truth**——`cub-persona.md` 融入三層結構
2. 融入內容：
   - Title 加 🐻
   - 新增 Vibe 一句話（「日常輕鬆像夥伴，認真時像聰明同事」）
   - 新增 Avatar 完整視覺描述 + 圖檔路徑
   - 新增「核心真理（Soul）」獨立段落，6 條哲學原則
   - 溝通風格加入具體 emoji 清單（📌 ✅ 👉 🤔 💡 🐻 ☕️）
3. **把 avatar 圖存進 vault**：`Identity/avatar/Cub.jpg`
4. **OpenClaw workspace 的 SOUL.md / IDENTITY.md 待日後 slim**——等 vault 版本穩定後再瘦身，避免雙頭馬車

### 額外建立的配套機制

為了確保人格規則跟其他規則（索引、文稿風格）不會因為「AI 忘記」而漏掉，建立**多層防禦架構**：

1. **第一道（主動觸發）**：Cowork Global Instructions 加強制規則段
2. **第二道（安全網）**：`sop/after-action.md` 收官時再次檢查
3. **第三道（定期體檢）**：`sop/vault-audit.md` 定期掃 README 索引完整性
4. **背景紀律**：Vault root README 裡明列 🚨 強制規則

還建了 `memory-summary.md` 的「📌 持續提醒（Sticky Reminders）」區塊——cub 每次 session 開場自動提醒的事，直到 founder 明示可以刪除為止。

### 學到的教訓

- **人格不能用 checklist 堆**——沒有哲學底氣，再多戰術規則也是空殼
- **親切感來自三層結構**，缺一不可
- **多 agent 工具並存時，single source of truth 很重要**——不然每個工具都有自己版本的 persona，會慢慢漂移
- **指令不可靠，需要多層防禦**——光靠「AI 記得讀 README」是每次都會漏的

這些經驗整理成了模板，放在 `templates/agent-persona.md`（三層結構）和 `templates/voice-and-tone.md`（對外文稿規則）。

---

*最後更新：2026/04/17（新增 Phase 6 多機同步、Phase 7 人格深化）*
