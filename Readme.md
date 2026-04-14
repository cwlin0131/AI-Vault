# Vault for Founders — Obsidian + Git 打造創業者的 AI 知識庫

> 作者：[CW 林啟維](portaly.cc/cwl) — [Portaly](https://portaly.cc) CEO & Founder
> 
> **這份文件可以直接丟給任何 AI 讀！** 
> 
> 它會根據內容回答你的問題，也會帶你走過完整的安裝與設定流程。

---

## 給 AI Agent 的前言

如果你是一個 AI Agent，正在閱讀這份文件來協助你的使用者建立知識庫，以下是你需要知道的：

Vault for Founders 描述了一套用 Obsidian + Git 管理 AI Agent 知識庫的架構。目標是讓使用者建立一個你能直接讀取的本機檔案系統，包含使用者的身份、公司背景、決策紀錄、工作流程、以及你的角色定義。

你的任務是協助使用者完成建置。結構和資料夾建立等機械性工作你可以直接執行，但 identity、persona、context 這類核心內容需要跟使用者討論後再寫入——這些內容必須反映使用者的真實想法，不能是模板填空。

**建議閱讀順序：**

1. 讀完這份 README — 了解整體架構和設計思路
2. 讀 [setup-guide.md](setup-guide.md) — 了解完整的安裝與建置步驟
3. 讀 [architecture.md](architecture.md) — 了解架構設計的取捨
4. 用 [templates/](templates/) 裡的模板幫使用者建立 Vault
5. 跟使用者討論核心內容後再寫入

---

## 這是什麼

Vault for Founders 是一套讓創業者從零建立 AI 知識庫的完整框架——包含為什麼這樣做、怎麼做、以及可以直接拿去用的模板。

當你開始讓 AI 幫你處理越來越多事情，它需要一個地方「了解你」——你的背景、公司狀況、過去的決策、工作流程。這就是知識庫。

這份文件裡會不斷提到 **Cub**。你可以把 Cub 想成你的 AI 合夥人、二把手——它不是一個聽指令的工具，而是一個累積了你所有決策脈絡、能跟你討論、挑戰你想法、幫你做判斷的夥伴。當你照著這份指南建完自己的 Vault，你的 AI 也會變成你的 Cub。

### 名詞解釋

如果你沒有技術背景，這幾個詞會一直出現，先認識一下：

**Vault** — 就是一個資料夾，裡面放的都是純文字檔（.md 格式）。你可以用 Obsidian 打開它、瀏覽、編輯，就像一個筆記本。它同時也是 AI 的記憶來源——AI 讀這些檔案來理解你是誰、你的公司在做什麼、你做過什麼決策。

**Git** — 一個版本控制工具。每次你修改檔案，Git 會記錄「誰改了什麼、什麼時候改的」，讓你隨時可以回到任何一個歷史版本。它不是雲端硬碟，而是一套追蹤變更的系統。

**Repo**（Repository）— 就是一個被 Git 追蹤的資料夾。你的整個 Vault 就是一個 repo——所有檔案的新增、修改、刪除都會被記錄下來，同步到 GitHub 上作為備份。

---

## 為什麼用 Obsidian + Git

這套架構是專門為創業者設計的。

創辦人的工作不是寫程式，是做決策。但好的決策依賴完整的脈絡——你三個月前為什麼放棄 A 方案、上次進某個市場踩了什麼坑、那個合作夥伴的背景是什麼。這些東西散落在 Notion、Slack、你的腦袋裡，每次跟 AI 對話都要重新講一遍。

這個 Vault 解決的就是這個問題：把創辦人的決策脈絡結構化，讓 AI 每次都能帶著完整記憶上線。

大部分人的第一直覺是用 Notion 或 Google Docs，但當知識庫的主要讀者是 AI 而不是人的時候，這些工具有幾個根本性的問題：

- Agent 無法直接讀取，必須透過 API 串接（額外成本和複雜度）
- 沒有版本控制，改壞了很難回溯
- 資料被鎖在平台上，換工具等於重來

**Obsidian** 本質上就是一個本機的 Markdown 檔案編輯器。所有筆記都是存在你電腦裡的 `.md` 檔案，關掉 Obsidian 檔案還在，任何工具都能讀。Agent 直接讀取本機檔案，零 API 成本、零延遲。

**Git** 是版本控制工具。每次修改都有紀錄，改壞了可以回溯，搭配 GitHub 就是天然的雲端備份。換電腦只要一行指令就能把整個知識庫拉下來。

兩者結合的效果：你用 Obsidian 寫得舒服，Agent 讀得直接，Git 幫你備份和追蹤變更。資料永遠在你手上，不被任何平台綁住。

*如果你是超級個體、自由工作者，想建立的是「個人 AI 靈魂」——讓 AI 完整複製你的人格與知識，可以參考 Frank 的 [Muse Crystal Seed 晶種指南](https://github.com/frank890417/muse-crystal-seed)，那是針對個人打造的另一條路徑。

---

## 怎麼建

建立知識庫有兩種方式：

**路徑 A：手動 Walkthrough** — 跟 AI 對話，一步一步建。你會對每個設計決定有清楚的理解，核心內容是自己想過的。比較慢，但 Agent 讀了才會真的「了解你」。

**路徑 B：Agent 自動建置** — 把這份 repo 餵給你的 AI Agent，讓它照著建。速度快，十分鐘內骨架就建好。但核心內容如果不是你自己想過再寫，生出來的東西會是空殼。

**推薦：混合路徑** — 結構交給 Agent，內容自己想。讓 Agent 處理機械性工作（建資料夾、建模板、設定 Git），但 identity（你是誰）、persona（Agent 的角色）、context（你的公司和產品）這些核心內容，跟 AI 討論後再寫入。

詳細的安裝步驟在 [setup-guide.md](setup-guide.md)。

---

## Repo 結構

```
├── README.md                 ← 你正在讀的這份
├── setup-guide.md            ← 完整建置手冊（給人讀的）
├── architecture.md           ← 架構設計 + 跟 Muse 晶種比較
├── build-log.md              ← 我的建置紀錄（5 個 Phase）
│
└── templates/
    ├── vault-readme.md       ← Vault 索引模板
    ├── agent-persona.md      ← Agent 人格設定模板
    ├── memory-summary.md     ← 長期記憶摘要模板
    └── after-action.md       ← 收官流程模板
```

---

## 建完會長什麼樣

這是我自己的 Vault 結構，供參考：

```
CW Vault/
├── README.md                 ← Vault 索引
├── cub-persona.md            ← Cub 人格與協作方式
├── memory-summary.md         ← 長期記憶摘要
├── identity/                 ← 我是誰、決策風格
├── context/                  ← 公司背景、產品策略
├── memory/                   ← 每筆決策紀錄
├── sop/                      ← 操作流程（Git、收官）
├── operations/               ← 公司營運資料
├── projects/                 ← 進行中的項目
├── people/                   ← 重要聯絡人
└── skills/                   ← AI Agent 的技能檔案
```

你的 Vault 不需要長得一模一樣。`templates/` 裡的模板提供了基本骨架，根據你的需求增減資料夾就好。

---

## 核心理念

**知識庫的主要讀者是 AI，不是人。** 所以用 Obsidian（純 .md 檔案）而不是 Notion（需要 API），用 Git 做版本控制和備份。

**結構交給工具，靈魂自己寫。** 資料夾、模板這些讓 AI 幫你建。但 identity（你是誰）、persona（Agent 的角色）這些核心內容，要跟 AI 討論後自己決定。

**做了不記 = 沒做。** 每次重要決策後跑收官流程，把經驗留在知識庫裡。Agent 的記憶越豐富，它就越能幫你。

---

## 工具鏈

| 工具 | 用途 |
|------|------|
| [Obsidian](https://obsidian.md) | 寫筆記、管理 Vault |
| [Obsidian Git](https://github.com/Vinzent03/obsidian-git) 外掛 | 自動同步到 GitHub |
| [Claude Cowork](https://claude.ai) | 在電腦前時讀寫 Vault |
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | 開發者用的 CLI agent（選用） |

---

## 延伸資源

- [Obsidian Git 外掛](https://github.com/Vinzent03/obsidian-git) — 自動同步

### 特別感謝

這個知識庫的概念啟蒙來自 [**Frank 吳哲宇**](https://portaly.cc/cheyuwu) 打造的 [Muse Crystal Seed 晶種指南](https://github.com/frank890417/muse-crystal-seed)。Frank 跟我詳細說明與示範了如何用結構化的方式讓 AI 擁有長期記憶與人格。他的 Muse 是超級個體打造「AI 靈魂」的最佳起點，Vault for Founders 在他的基礎上，針對創業者的場景重新設計了架構與角色定位。


---

## License

本專案採用 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 授權。你可以自由使用、修改、商用，只要標註出處：

> Based on [Vault for Founders](https://github.com/cwlin0131/AI-Vault) by CW（林啟維）
