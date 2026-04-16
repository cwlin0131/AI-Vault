# Memory Scaling 指南 — 當記憶開始爆量

> 你的 Vault 用了三個月，memory-summary.md 從 30 行長到 200 行。Agent 每次啟動讀完要花很久，還常常被舊資訊誤導。這份指南講的是怎麼處理這個階段。

---

## 問題：單一檔案撐不住

`memory-summary.md` 設計上是「每次啟動必讀的精華版」。但隨著決策累積，你會遇到：

- **太長** — Agent 讀完要消耗大量 token，拖慢回應
- **太雜** — 三個月前的決策和今天的焦點混在一起，Agent 難以判斷優先級
- **太舊** — 已完成的項目還留著，誤導 Agent 的判斷
- **改不動** — 每次更新都怕刪掉還重要的東西

這不是你的問題，是架構的問題。一個檔案同時當「索引」和「內容」，遲早會撞牆。

---

## 解法：兩層記憶

把 `memory-summary.md` 拆成兩層：

```
memory-summary.md        ← 索引層（≤50 行）：只放指標，不放內容
memory/
├── active-focus.md      ← 當前焦點（1-3 件事）
├── decisions/
│   ├── 2026-01_product-pivot.md
│   └── 2026-03_pricing-change.md
├── lessons.md           ← 累積的教訓
├── patterns.md          ← Agent 觀察到的模式
└── archive/             ← 已完成、已過期的決策
```

### 索引層：memory-summary.md

改成純路由表，每行一個指標，不超過 50 行：

```markdown
# Memory Summary

> 最後更新：2026/04/15
> 這是索引，不是內容。Agent 讀完這份，決定要不要開 memory/ 裡的檔案。

## 當前焦點
→ [memory/active-focus.md](memory/active-focus.md)

## 重要決策（按時間倒序，最新在前）
- [2026-03 定價調整](memory/decisions/2026-03_pricing-change.md) — B2B 轉 PLG，月費從 $29 降到 $9
- [2026-01 產品轉向](memory/decisions/2026-01_product-pivot.md) — 從 dashboard 轉 API-first

## 教訓
→ [memory/lessons.md](memory/lessons.md)

## 我的模式
→ [memory/patterns.md](memory/patterns.md)

## 歸檔（已完成 / 已過期）
→ [memory/archive/](memory/archive/)
```

### 內容層：memory/*.md

每個檔案只負責一件事，用 frontmatter 標記時效：

```markdown
---
updated: 2026-03-20
status: active        # active / archived
tags: [pricing, strategy]
summary: B2B 轉 PLG 定價策略，月費 $29→$9
---

# 2026-03 定價調整

## 背景
（略）

## 決策
（略）

## 結果
（略）
```

---

## 什麼時候搬到兩層

不需要一開始就用兩層。判斷標準：

| 狀態 | 行動 |
|------|------|
| memory-summary.md < 50 行 | 維持現狀，不用動 |
| memory-summary.md 50-100 行 | 考慮拆分，但不急 |
| memory-summary.md > 100 行 | 該拆了，Agent 效率開始下降 |
| Agent 開始回答過期資訊 | 立刻拆，不要等 |

---

## 記憶衰減：什麼該留、什麼該歸檔

不是所有記憶都永遠重要。定期問自己：

**留在 active：**
- 正在進行的專案相關決策
- 反覆驗證仍成立的教訓
- Agent 需要每次都知道的偏好

**移到 archive：**
- 已完成專案的決策紀錄（結果已知，不影響當前判斷）
- 被後續決策覆蓋的舊決策
- 超過 6 個月且沒被引用過的項目

**歸檔不是刪除。** 檔案還在 `memory/archive/`，Agent 有需要時可以回去查。但不會每次啟動都讀。

---

## Agent 輔助清洗

在 `agent-persona.md` 加入這段，讓 Agent 主動幫你維護記憶：

```markdown
## 記憶維護
- 每次讀完 memory-summary.md，如果發現超過 50 行，提醒我做一次清洗
- 發現已完成的項目還在 active 區，建議我歸檔
- 新增決策紀錄後，主動更新 memory-summary.md 的索引
- 歸檔時告訴我你歸檔了什麼，讓我確認
```

---

## 跟 after-action 的配合

after-action 流程（收官三步）產出的 memory 紀錄，直接寫進 `memory/decisions/`。然後在 `memory-summary.md` 加一行索引指標。

這樣收官流程不會讓 summary 膨脹 — 膨脹的是 `memory/` 資料夾（那邊不怕多），summary 只多一行。

---

## 這套方法的來源

這個兩層記憶架構來自實際運營 AI 多代理系統（19 個 Agent、50+ 記憶檔案）超過 6 個月的經驗。當 memory index 檔案長到 200 行時，我們發現：

1. Agent 讀完 index 就已經消耗大量 context window
2. 舊資訊和新焦點混在一起，Agent 優先級判斷失準
3. 每次手動清洗都要花 30 分鐘以上，導致越來越少做

拆成索引層 + 內容層後，index 壓到 50 行以內，Agent 啟動效率提升，維護成本也降低。

---

*最後更新：2026/04/16*
