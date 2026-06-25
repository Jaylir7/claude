# 手機收集箱 → Obsidian 知識庫

這個倉庫專門用來做**手機端的資訊收集**，之後在電腦上把這些內容抓下來、
整理進你的 Obsidian (OB) 知識庫。所有手機收集的內容都集中在 **`mobile/`** 資料夾底下。

## 工作流程

```
📱 手機                          ☁️ GitHub                  💻 電腦
─────────                       ──────────                 ─────────
在 mobile/inbox/ 新增筆記  ──→   push           ──→   pull 下來
                                                      整理進 Obsidian Vault
                                                      歸檔後可清空 mobile/inbox/
```

## 目錄說明

手機收集的內容都放在 `mobile/` 底下：

| 資料夾 | 用途 |
|--------|------|
| `mobile/inbox/`      | 手機隨手丟進來的草稿、未整理的筆記、連結、靈感 |
| `mobile/attachments/`| 圖片、PDF、語音等附件 |
| `mobile/templates/`  | 筆記範本，方便手機快速建立格式一致的筆記 |

## 在手機上怎麼用

1. 用任何能編輯 GitHub 的 App（GitHub 官方 App、Working Copy、a-Shell、
   或直接用瀏覽器）開這個倉庫。
2. 在 `mobile/inbox/` 下新增 `.md` 檔（可參考 `mobile/templates/note.md` 的格式）。
3. Commit & Push。

## 在電腦上怎麼用

```bash
git pull
```

把 `mobile/inbox/` 裡的內容整理、搬進 Obsidian Vault 後，
可以清空 `mobile/inbox/`（保留 `.gitkeep`）再 commit，保持收集箱乾淨。

## 命名建議

筆記檔名建議用日期開頭，方便排序：`2026-06-25-想法標題.md`
