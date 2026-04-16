# [你的名字] Vault

這是 [你的名字] 的個人知識庫，供 AI Agent（[Agent 名字]）讀取使用。

---

## 資料夾結構

```
/
  README.md              ← 你正在讀的這份
  agent-persona.md       ← Agent 的人格設定與協作方式
  memory-summary.md      ← 長期記憶摘要

  /identity              ← 你是誰、價值觀、決策風格
  /context               ← 工作背景、產品現況、策略方向
  /memory                ← 重要決策紀錄、會議結論
  /sop                   ← 操作流程
  /projects              ← 各項目的狀態
  /people                ← 重要聯絡人背景
  /skills                ← Agent 的技能檔案
```

## Agent 閱讀順序

1. 讀這份 README（了解整體結構）
2. 讀 `agent-persona.md`（了解自己的角色與協作方式）
3. 讀 `memory-summary.md`（掌握近期重要事項）
4. 依任務需要，讀對應資料夾的內容

## 維護原則

- 一個事實只寫在一個地方（Single Source of Truth）
- 建新檔案前先搜尋有沒有現有的
- 每份文件開頭標注最後更新日期
- 敏感資訊（API key、密碼等）不進這個 repo
