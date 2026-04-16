# .gitattributes 模板

> 最後更新：2026/04/17

## 這是什麼

`.gitattributes` 是 Git 的標準設定檔，放在 Vault 根目錄。它告訴 Git「每個檔案要怎麼處理」，特別是**換行符規則**。

## 為什麼需要

當你開始在多台電腦、多個工具之間同步同一個 Vault（例如 Obsidian Git、GitHub Desktop、Claude Code、Cursor），不同工具對「換行符」的處理方式不一樣：

- Mac / Linux 預設用 **LF**（`\n`）
- Windows 預設用 **CRLF**（`\r\n`）

肉眼看起來一樣，但對 Git 是不同內容。任何一個工具換了格式，其他電腦 pull 下來就會看到「整個檔案都被改了」的假 diff，進而引發合併衝突。

**不裝 `.gitattributes` → 多機同步遲早撞衝突。**

## 怎麼用

1. 在你的 Vault 根目錄建一個檔案叫 `.gitattributes`（注意開頭的點）
2. 把下面「設定內容」整段貼進去、存檔
3. 第一次加入時執行：
   ```bash
   git add .gitattributes
   git commit -m "chore: add .gitattributes (enforce LF line endings)"
   ```
4. 可選：若 repo 已有大量檔案是 CRLF 格式，執行 `git add --renormalize .` 一次性轉成 LF

## 設定內容

```
# 強制所有文字檔案使用 LF 換行符，避免跨電腦、跨工具的換行符衝突
# 設定後請執行一次：git add --renormalize .

* text=auto eol=lf

# 明確標記為文字 (使用 LF)
*.md       text eol=lf
*.txt      text eol=lf
*.json     text eol=lf
*.js       text eol=lf
*.ts       text eol=lf
*.py       text eol=lf
*.yml      text eol=lf
*.yaml     text eol=lf
*.xml      text eol=lf
*.html     text eol=lf
*.css      text eol=lf
*.sh       text eol=lf
.gitignore text eol=lf
.gitattributes text eol=lf

# 二進位檔案，不做換行符轉換
*.png      binary
*.jpg      binary
*.jpeg     binary
*.gif      binary
*.ico      binary
*.svg      binary
*.pdf      binary
*.docx     binary
*.pptx     binary
*.xlsx     binary
*.zip      binary
*.gz       binary
*.woff     binary
*.woff2    binary
*.ttf      binary
*.otf      binary
*.mp3      binary
*.mp4      binary
*.mov      binary
```

## 備註

- 這份設定以 **Markdown 知識庫為主要場景**。如果你的 Vault 有特殊檔案類型，自行增補
- 做完之後 **所有協作電腦都要 pull 一次**，新規則才會在各機器生效
- 舊檔案可能顯示「一次性大改動」，那是 normalize 動作，不是內容真的變了
