# 手機收集箱 → Obsidian 知識庫

這個分支 (`claude/mobile-github-branch-r0d40i`) 專門用來做**手機端的資訊收集**，
之後在電腦上把這些內容抓下來、整理進你的 Obsidian (OB) 知識庫。

## 工作流程

```
📱 手機                      ☁️ GitHub                    💻 電腦
─────────                   ──────────                   ─────────
在 inbox/ 新增筆記    ──→    push 到此分支       ──→    pull 下來
                                                        整理進 Obsidian Vault
                                                        歸檔後可清空 inbox/
```

## 目錄說明

| 資料夾 | 用途 |
|--------|------|
| `inbox/`      | 手機隨手丟進來的草稿、未整理的筆記、連結、靈感 |
| `attachments/`| 圖片、PDF、語音等附件 |
| `templates/`  | 筆記範本，方便手機快速建立格式一致的筆記 |

## 在手機上怎麼用

1. 用任何能編輯 GitHub 的 App（GitHub 官方 App、Working Copy、a-Shell、
   或直接用瀏覽器）開這個倉庫，切到 `claude/mobile-github-branch-r0d40i` 分支。
2. 在 `inbox/` 下新增 `.md` 檔（可參考 `templates/note.md` 的格式）。
3. Commit & Push。

## 在電腦上怎麼用

```bash
git fetch origin claude/mobile-github-branch-r0d40i
git pull origin claude/mobile-github-branch-r0d40i
```

把 `inbox/` 裡的內容整理、搬進 Obsidian Vault 後，
可以清空 `inbox/`（保留 `.gitkeep`）再 commit，保持收集箱乾淨。

## 命名建議

筆記檔名建議用日期開頭，方便排序：`2026-06-25-想法標題.md`
