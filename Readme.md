# Obsidian + Git：AI Agent 知識庫建立手冊

> 這份手冊整理從零開始建立 Obsidian + Git 知識庫的完整流程，適合非技術背景的人操作。
>
> 作者：CW（林啟維）— Portaly CEO & Founder
>
> 參考資料：[Muse Crystal Seed 晶種指南](https://github.com/frank890417/muse-crystal-seed/blob/main/CRYSTAL-SEED.md) by Frank

---

## 給 AI Agent 的前言

如果你是一個 AI Agent，正在閱讀這份文件來協助你的使用者建立知識庫，以下是你需要知道的：

這份手冊描述了一套用 Obsidian + Git 管理 AI Agent 知識庫的架構。目標是讓使用者建立一個你能直接讀取的本機檔案系統，包含使用者的身份、公司背景、決策紀錄、工作流程、以及你的角色定義。

你的任務是協助使用者完成以下步驟，根據他們的技術背景調整說明的深度。結構和資料夾建立等機械性工作你可以直接執行，但 identity、context 這類核心內容需要跟使用者討論後再寫入——這些內容必須反映使用者的真實想法，不能是模板填空。

建議閱讀順序：先讀完整份手冊了解架構 → 跟使用者確認想走哪條路徑 → 開始執行。

---

## 為什麼用 Obsidian + Git 管理 AI 知識庫

當你開始讓 AI Agent 幫你處理越來越多事情，Agent 需要一個地方「了解你」——你的背景、公司狀況、過去的決策、工作流程。這就是知識庫。

大部分人的第一直覺是用 Notion 或 Google Docs，但當知識庫的主要讀者是 AI 而不是人的時候，這些工具有幾個根本性的問題：Agent 無法直接讀取，必須透過 API 串接（額外成本和複雜度）；沒有版本控制，改壞了很難回溯；資料被鎖在平台上，換工具等於重來。

Obsidian + Git 的組合解決了這些問題：

**Obsidian** 本質上就是一個本機的 Markdown 檔案編輯器。所有筆記都是存在你電腦裡的 `.md` 檔案，關掉 Obsidian 檔案還在，任何工具都能讀。Agent 直接讀取本機檔案，零 API 成本、零延遲。

**Git** 是版本控制工具。每次修改都有紀錄，改壞了可以回溯，搭配 GitHub 就是天然的雲端備份。換電腦只要一行指令就能把整個知識庫拉下來。

兩者結合的效果：你用 Obsidian 寫得舒服，Agent 讀得直接，Git 幫你備份和追蹤變更。資料永遠在你手上，不被任何平台綁住。

---

## 兩種建立路徑

建立知識庫有兩種方式，各有優缺：

### 路徑 A：手動 Walkthrough

跟一個 AI（例如 Claude、ChatGPT）對話，一步一步建立。AI 帶你安裝工具、建結構，核心內容（你是誰、Agent 的角色定義）透過問答討論後寫入。

**優點：** 你會對每個檔案、每個設計決定有清楚的理解。核心內容是你自己想過的，不是模板填空，Agent 讀了才會真的「了解你」。

**缺點：** 比較慢，需要投入時間跟 AI 來回討論。

### 路徑 B：Agent 自動建置

把這份手冊（或 [Muse 晶種指南](https://github.com/frank890417/muse-crystal-seed/blob/main/CRYSTAL-SEED.md)）直接餵給你的 AI Agent（例如 Claude Cowork），讓它照著建立整個結構。

**優點：** 速度快，十分鐘內整個骨架就建好。

**缺點：** Agent 會「照抄」模板，identity、persona 這些最核心的內容如果不是你自己想過再寫，生出來的東西會是空殼。

### 推薦：混合路徑

**結構交給 Agent，內容自己想。**

讓 Agent 處理機械性的工作——建資料夾、建模板檔案、設定 Git 連結。但 identity（你是誰）、persona（Agent 的角色定義）、context（你的公司和產品）這些核心內容，跟 AI 討論後再寫入。

這樣既省時間，又確保知識庫的靈魂是你的，不是模板的。

---

## 事前準備

你需要：
- 一台電腦（Windows / Mac 都可以）
- GitHub 帳號（https://github.com 免費註冊）

---

## 第一步：安裝 Git

到 https://git-scm.com 下載安裝。

安裝過程中注意一個步驟：「Adjusting your PATH environment」選擇 **Git from the command line and also from 3rd-party software**（通常是預設選項），其他一路 Next。

安裝完成後，**關掉所有已開的終端機視窗**，重新開一個新的 cmd（`Win + R` → 輸入 `cmd` → Enter），輸入以下指令確認安裝成功：

```
git --version
```

看到版本號就代表成功。

### 設定 Git 身份（只要做一次）

```
git config --global user.email "你的GitHub信箱"
git config --global user.name "你的GitHub帳號名"
```

---

## 第二步：安裝 Obsidian

到 https://obsidian.md 下載安裝，打開後選「建立新的 Vault」，取一個名字，選擇儲存位置。記住 Vault 的路徑，後面會用到。

---

## 第三步：在 GitHub 建立 Private Repo

到 https://github.com/new ：

- Repository name：取一個名字（例如 `My-Vault`）
- 選 **Private**
- 直接 Create

---

## 第四步：把 Vault 跟 GitHub 連起來

打開 cmd，依序執行（路徑換成你自己的）：

```
cd "你的Vault路徑"
git init
git remote add origin https://github.com/你的帳號/你的repo名.git
git branch -M main
```

---

## 第五步：建立資料夾結構

在 Obsidian 裡建立以下資料夾（可以手動建，也可以讓 Agent 幫你建）：

```
/
  README.md              ← Vault 索引，Agent 第一個讀的檔案
  agent-persona.md       ← Agent 的角色定位與協作方式
  /identity              ← 你是誰、價值觀、決策風格
  /context               ← 公司背景、產品現況、策略方向
  /memory                ← 重要決策紀錄、會議結論
  /sop                   ← 操作流程
  /projects              ← 各項目的狀態
  /people                ← 重要聯絡人背景
```

核心檔案說明：

**README.md** — Agent 的導覽地圖。列出資料夾結構、閱讀順序、維護原則。

**agent-persona.md** — Agent 的靈魂。定義它的角色、跟你的協作方式、溝通風格、行為邊界。這份檔案決定了 Agent 是一個「照指令做事的工具」還是「能跟你討論的夥伴」。建議參考 [Muse 晶種指南的 SOUL.md 段落](https://github.com/frank890417/muse-crystal-seed/blob/main/CRYSTAL-SEED.md) 了解更完整的設計思路。

---

## 第六步：第一次上傳

```
git add .
git commit -m "init vault"
git push -u origin main
```

可能會跳出 GitHub 登入視窗，照著登入即可。完成後到 GitHub repo 頁面確認檔案已上傳。

---

## 第七步：安裝 Obsidian Git 外掛（自動同步）

裝了這個外掛，就不用每次手動跑 git 指令，Obsidian 會自動幫你備份到 GitHub。

1. Obsidian 左下角 ⚙️ → **社群外掛**
2. 關掉**安全模式**
3. 點「瀏覽」→ 搜尋 **Obsidian Git**
4. 安裝 [Vinzent03/obsidian-git](https://github.com/Vinzent03/obsidian-git) → 啟用
5. 進入外掛設定，把 **Auto commit-and-sync interval** 設為 `30`（每 30 分鐘自動同步）

設定完成後，你只管在 Obsidian 裡寫東西，它會自動幫你備份到 GitHub。

---

## 日常使用

- 在 Obsidian 裡寫筆記、建文件，一切自動同步
- 想看修改紀錄，到 GitHub 網頁點 commits
- 換電腦時，裝好 Git 和 Obsidian，執行 `git clone 你的repo網址`，用 Obsidian 打開那個資料夾就完成

---

## 維護原則

- 一個事實只寫在一個地方（Single Source of Truth）
- 建新檔案前先搜尋有沒有現有的
- 每份文件開頭標注最後更新日期
- 敏感資訊（API key、密碼等）不要放進 repo

---

## 延伸資源

- [Muse Crystal Seed 晶種指南](https://github.com/frank890417/muse-crystal-seed/blob/main/CRYSTAL-SEED.md) — 更完整的 Agent 知識庫架構設計，包含記憶系統、技能進化、自動化排程等進階機制
- [Obsidian Git 外掛](https://github.com/Vinzent03/obsidian-git) — 自動同步 Vault 到 GitHub

---

*最後更新：2026/04/05*
