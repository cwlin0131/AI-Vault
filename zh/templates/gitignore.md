# .gitignore 模板（Obsidian Vault 版）

> 最後更新：2026/04/17

## 這是什麼

`.gitignore` 是 Git 的標準設定檔，放在 Vault 根目錄。它告訴 Git「這些檔案不要追蹤」，避免把本機專屬的設定、快取、垃圾檔上傳到 repo。

## 為什麼需要

Obsidian 會在 Vault 裡產生一個 `.obsidian/` 資料夾，放你的**本機偏好設定**（graph 視圖、hotkey、已裝插件、workspace 分頁狀態等）。這些東西：

- **不應該跨電腦分享**——每台電腦有自己的設定
- **會被插件自動修改**——造成跨機器持續衝突的主因之一
- **包含插件本身的 code**（例如 `obsidian-git/main.js`）——插件升級時會產生大改動

作業系統也會產生垃圾檔（`.DS_Store`、`Thumbs.db`）不應該進 repo。

**不設 `.gitignore` → `.obsidian/` 被追蹤 → 永遠撞衝突。**

## 怎麼用

1. 在 Vault 根目錄建一個檔案叫 `.gitignore`（注意開頭的點）
2. 把下面「設定內容」整段貼進去、存檔
3. 如果 `.obsidian/` 之前已被 Git 追蹤，執行：
   ```bash
   git rm -r --cached .obsidian/
   git commit -m "chore: stop tracking .obsidian/ (local settings)"
   ```
4. 這不會刪掉你硬碟上的 `.obsidian/` 資料夾，只是讓 Git 從此忽略它

## 設定內容

```
# Obsidian 本地設定 (app 設定、插件、hotkey、graph、workspace 等)
# 跨電腦不 share，每台電腦各自管理
.obsidian/

# macOS
.DS_Store

# Windows
Thumbs.db
desktop.ini

# 編輯器暫存
*.swp
*.swo
*~
.vscode/
.idea/
```

## 如果你想保留部分 Obsidian 設定跨機器同步

最常見是**想同步 hotkey 或已裝插件清單**。兩個做法：

**做法 A：完全不 ignore（不推薦）**
刪掉 `.gitignore` 裡的 `.obsidian/` 那行。代價是高頻衝突，不值得。

**做法 B：選擇性忽略（進階）**
改成只忽略 workspace 跟插件本體，保留設定檔：
```
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.obsidian/plugins/*/main.js
.obsidian/plugins/*/styles.css
.obsidian/cache
```
這樣仍保留 `hotkeys.json`、`community-plugins.json` 等設定檔同步。

**建議大多數人直接忽略整個 `.obsidian/`**，hotkey 重設一次 30 秒，換來的是穩定性。

## 備註

- 做完之後 **所有協作電腦都要 pull 一次**，新規則才會在各機器生效
- 搭配 `.gitattributes`（見同資料夾對應模板）一起用，才完整解決多機同步問題
