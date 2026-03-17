# 部落格修改指南（優先維持原框架）

這份指南是給日常維護用，目標是：
- 快速改內容
- 盡量不碰 `themes/`
- 保持可升級、可部署

---

## 1) 修改原則（先看）

1. 優先改外層檔案，不直接改 `themes/`：
   - `hugo.toml`
   - `config/_default/params.yml`
   - `content/`
   - `data/`
   - `layouts/`（只有設定做不到時才用）
2. 新功能先用「設定」完成，最後才考慮 layout override。
3. 每次改完至少跑：
   - `hugo --minify`
4. 發佈前確認本地：
   - `hugo serve`

---

## 2) 常見需求與對應檔案

- 改網站標題 / 語言 / 預設語系
  - `hugo.toml`

- 改 bio（側欄簡介）、社群連結、主題功能開關
  - `config/_default/params.yml`
  - 常改欄位：`description`、`social`、`sidebar`、`player`、`injector`

- 改「關於我」
  - `content/about.md`

- 改首頁封面圖 / avatar / favicon
  - `static/images/banner.webp`
  - `static/avatar/avatar.webp`
  - `static/favicon.ico`
  - 路徑設定在 `config/_default/params.yml`

- 改隨機文章封面池
  - `data/covers.yml`

---

## 3) 新增文章

### 建議做法
在 `content/post/` 新增一個 markdown，例如：
- `content/post/2026-03-my-note.md`

最小可用 front matter：

```md
---
title: "文章標題"
date: 2026-03-17T20:00:00+08:00
draft: false
tags: ["tag1"]
categories: ["blog"]
description: "一句簡短摘要（可選）"
---

正文寫在這裡。
```

### 草稿流程
- 開發中可用 `draft: true`
- 準備上線再改 `draft: false`

---

## 4) 刪除文章

最簡單就是刪除對應檔案：
- `content/post/xxx.md`

如果只是暫時不想顯示，改成：
- `draft: true`

---

## 5) 功能開關（以不破壞框架為主）

主要都在 `config/_default/params.yml`：

- 留言系統：`giscus` / `waline` / `disqus` 等
- 搜尋：`algolia_search.enable`
- 動效：`animation.enable`、`firework.enable`
- 音樂：`player.aplayer.enable`、`player.meting.enable`
- PJAX：`pjax.enable`
- Live2D：`live2d.enable`

建議：
1. 一次只改一個功能。
2. 改完立刻 `hugo --minify`。
3. 若怪問題出現，先回退最後一個開關。

---

## 6) 你目前專案的建議修改路線

### 優先走設定層
先嘗試：
- `hugo.toml`
- `config/_default/params.yml`
- `content/*`
- `data/*`

### 只有設定做不到時，才用 `layouts/` override
例如：
- 插入 YouTube iframe 到特定位置
- 調整某區塊輸出順序

做法是新增對應檔到：
- `layouts/partials/...`

不直接改 `themes/hugo-theme-reimu/...`

---

## 7) 本地預覽與上線

### 本地預覽
```bash
hugo serve
```

### 建置檢查
```bash
hugo --minify
```

### 提交與推送
```bash
git add .
git commit -m "docs: update blog content/settings"
git push origin main
```

推送後會觸發你目前的 GitHub Actions 部署流程。

---

## 8) 變更前快速檢查清單

- 是否改到 `themes/`？（若有，先停）
- 是否只是想改文案/開關，卻用了 layout override？
- `hugo --minify` 是否通過？
- 手機版與桌機版是否都看過一次？
- 是否有不必要檔案被加入版本控制？

