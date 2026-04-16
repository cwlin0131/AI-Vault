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

*最後更新：2026/04/14*
