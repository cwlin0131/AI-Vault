# Vault for Founders：建置手冊

> 從零開始建立 Obsidian + Git 知識庫的完整流程，適合非技術背景的人操作。

---

## 事前準備

你需要：
- 一台電腦（Windows / Mac 都可以）
- GitHub 帳號（https://github.com 免費註冊）

---

## 第一步：安裝 Git

到 https://git-scm.com 下載安裝。

安裝過程中「Adjusting your PATH environment」選擇 **Git from the command line and also from 3rd-party software**（通常是預設選項），其他一路 Next。

安裝完成後，**關掉所有已開的終端機視窗**，重新開一個新的 cmd（`Win + R` → 輸入 `cmd` → Enter），確認安裝成功：

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

在 Obsidian 裡建立以下資料夾（可以手動建，也可以讓 AI 幫你建）：

```
/
  README.md              ← Vault 索引，Agent 第一個讀的檔案
  agent-persona.md       ← Agent 的角色定位與協作方式
  memory-summary.md      ← 長期記憶摘要，每次啟動必讀
  /identity              ← 你是誰、價值觀、決策風格
  /context               ← 公司背景、產品現況、策略方向
  /memory                ← 重要決策紀錄、會議結論
  /sop                   ← 操作流程
  /operations            ← 公司營運資料
  /projects              ← 各項目的狀態
  /people                ← 重要聯絡人背景
```

核心檔案說明：

**README.md** 是 Agent 的導覽地圖，列出資料夾結構、閱讀順序、維護原則。

**agent-persona.md** 是 Agent 的靈魂。定義它的角色、跟你的協作方式、溝通風格、行為邊界。這份檔案決定了 Agent 是一個「照指令做事的工具」還是「能跟你討論的夥伴」。

**memory-summary.md** 是長期記憶的精華版。Agent 每次啟動讀完這份，就能在幾秒內掌握你當前的焦點、重大決策、教訓。

模板可以在 [templates/](templates/) 資料夾裡找到。

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

*最後更新：2026/04/14*
