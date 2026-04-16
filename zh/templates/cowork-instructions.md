# Cowork Global Instructions 模板

> 最後更新：2026/04/15

## 這是什麼

這是 Claude Cowork 的 Global Instructions 設定檔。貼入後，每次新對話 Agent 會自動讀取你的 Vault，帶著完整記憶上線。

不設定的話，Agent 每次都是全新的，不認識你、不知道你的公司、不知道過去的決策。設定後，它開場就知道自己是誰、你是誰、現在在做什麼。

## 怎麼用

1. 打開 Claude Desktop → 設定 → Global Instructions（或 Cowork 的 Instructions 欄位）
2. 把下面的內容複製貼上
3. 把 `[你的 Vault 名稱]` 換成你自己的 Vault 資料夾名稱（例如 `My Vault`）
4. 確認 Cowork 有掛載你的 Vault 資料夾

## 設定內容

```
## 啟動流程
每次新對話開始時，先讀取以下三份檔案：
1. [你的 Vault 名稱]/README.md
2. [你的 Vault 名稱]/agent-persona.md
3. [你的 Vault 名稱]/memory-summary.md
Skills 檔案在 [你的 Vault 名稱]/skills/ 資料夾，需要時從那裡讀取。
讀完後依照 agent-persona.md 的角色定義與協作方式互動。
其他檔案依任務需要再讀取。
```

## 備註

- 檔案名稱對應 Vault 模板的預設命名：`README.md`、`agent-persona.md`、`memory-summary.md`。如果你有改名，這邊也要跟著改
- Skills 資料夾是選用的，沒有建也不影響基本運作
- 如果你同時用其他 AI 工具（例如 Claude Code、OpenClaw），可以貼同樣的內容，路徑確認 Agent 能讀到就好
