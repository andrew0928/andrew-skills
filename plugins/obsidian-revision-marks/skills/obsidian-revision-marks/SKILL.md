---
name: obsidian-revision-marks
description: "Mark revisions inline using Obsidian comment syntax (%%...%%) when editing existing Obsidian markdown files, so the user can review every change before accepting. Use whenever revising, restructuring, adjusting, or reorganizing existing Obsidian markdown content — outlines, notes, drafts, articles, talk decks. Triggers on words like 調整, 修訂, 重新檢視, 改一下, 重新組織, revise, adjust, restructure, reorganize. Do NOT use when creating brand-new files from scratch, when the user explicitly says 直接改 不用標記, or when working on non-Obsidian markdown (the %%...%% syntax won't auto-hide there)."
---

# Obsidian 修訂標記慣例

當使用者請我調整、修訂、重新檢視既有的 Obsidian markdown 文件時, 用 Obsidian 註解語法 `%%...%%` 標記修訂範圍, 讓使用者可以清楚對照變更後再決定是否接受。

## 為什麼用這個慣例

- `%%...%%` 是 **Obsidian 原生註解語法, 閱讀模式自動隱藏** — 簡報/輸出/預覽乾淨
- 不跟 highlight `==...==` 衝突 (使用者的 vault 已將 `==` 用於其他用途)
- 編輯模式清楚可見, 可全文搜尋 `%%[` 一次找出所有修訂處
- 接受變更後可用 regex 一次清除, 留下乾淨版本

## 標記語法

### 1. 改寫的行 — 保留原文方便對照

```
新內容 %%[改] 原: "原文" - 改寫理由%%
```

範例:
```
- AI 重新定義 BizDevOps 的執行平衡 %%[改] 原: "AI 改變了哪些流程與作業方法?" - 標題正面化%%
```

### 2. 新增的單行 — 描述目的

```
新增的內容 %%[新增] 新增理由%%
```

範例:
```
- 瓶頸轉移到「架構師的邊界規劃能力」+「Core Context 的管理品質」 %%[新增] 預告答案, 收斂到後續兩大主軸%%
```

### 3. 新增的整段 (多行) — 用開始/結束 marker 包住

```
%%[新增段落 開始] 簡述新增理由%%
段落內容
更多內容
%%[新增段落 結束]%%
```

範例:
```
%%[新增段落 開始] 獨立 Harness Engineering section - 主軸命名%%
Harness Engineering - 從工程師擴大到架構師

- 業界已經有成熟的 harness 框架...
- ...
%%[新增段落 結束]%%
```

### 4. 擬刪除的內容 — 保留原文, 標記擬刪除

不要直接刪除原文 (使用者看不到刪了什麼)。標記擬刪除, 由使用者確認後再清除:

```
原本的行 %%[擬刪除] 理由%%
```

或整段:
```
%%[擬刪除 開始] 理由%%
原段落
%%[擬刪除 結束]%%
```

## 標記要點

| 原則 | 說明 |
|---|---|
| 每個標記附「為什麼」 | 簡短即可 — 讓使用者直接判斷是否接受, 不用回頭問 |
| 不要逐字描述變更 | 一句話交代意圖即可 (改了哪幾個字使用者一看就知道) |
| 改寫類保留原文 | 用 `原: "..."` 格式 — 方便對照 |
| 新增類描述目的 | 為什麼需要這條 — 方便取捨 |
| 標記放行尾 | 避免影響原文閱讀, 集中在行末 |
| 新段落用開始/結束 | 一行標記容易遺漏範圍, 開始/結束 marker 清楚框住範圍 |

## 收尾流程

調整完成後, 給使用者一份完整摘要:

1. **變動摘要表格** — 各區域變動類型 (改/新增/移動)
2. **標記慣例提醒** — 閱讀模式自動隱藏, 編輯模式可見
3. **清除標記的方式**:
   - VS Code / 編輯器 regex 取代: 搜尋 `%%\[[^%]*?%%` 取代為空字串 (注意 macOS sed 要加 -E)
   - Obsidian 內 `Ctrl+F` (或 `Cmd+F`) 搜 `%%[` 逐一檢視
   - 或寫成簡單 script:
     ```bash
     sed -i.bak -E 's/%%\[[^%]*?%%//g' file.md
     ```

## 何時不適用

- **建立全新檔案** — 沒有原文需要對照, 直接寫即可
- **純粹追加內容** — 不影響既有結構時, 直接寫入並告訴使用者位置即可
- **使用者明確說「直接改, 不用標記」** — 尊重指示
- **非 Obsidian 的 markdown 檔案** — `%%...%%` 在標準 markdown 渲染器會以原文顯示, 不會隱藏

## 工作流程

1. **理解使用者要調整什麼** — 先讀檔, 釐清範圍
2. **規劃改動** — 列出每處要動的地方與理由
3. **執行 Edit** — 每次修改都附上對應的 `%%...%%` 標記
4. **摘要報告** — 表格列出所有變動、提醒標記慣例、附清除方式
5. **等使用者確認** — 不要主動清除標記, 讓使用者自己決定哪些接受

## 與其他 skills 的關係

- 搭配 `obsidian:obsidian-markdown` 使用: 那個 skill 處理 wikilinks/callouts/properties 等 Obsidian 語法, 此 skill 專注於修訂工作流程
- 不取代 git diff: 此 skill 是給「還沒 commit, 還在跟使用者協作調整中」的階段使用, commit 後的版本應該清掉所有修訂標記
