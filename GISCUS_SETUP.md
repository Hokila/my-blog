# Giscus 評論系統設定指南

## ✅ 設定完成！

您的 blog 已經成功整合 Giscus 評論系統，所有配置都已完成。

## 當前配置

- **Repository**: `Hokila/blog_comment`
- **Repository ID**: `R_kgDOQ4JV2Q`
- **Category**: `Announcements`
- **Category ID**: `DIC_kwDOQ4JV2c4C02n5`
- **Mapping**: `pathname` (使用頁面路徑)
- **Theme**: `preferred_color_scheme` (跟隨使用者系統偏好)
- **Language**: `zh-TW` (繁體中文)

## 已完成的設定步驟

✅ **步驟 1**: 確認 `Hokila/blog_comment` repository 為公開狀態  
✅ **步驟 2**: 啟用 repository 的 Discussions 功能  
✅ **步驟 3**: 安裝 Giscus App 到 repository  
✅ **步驟 4**: 取得 repository ID 和 category ID  
✅ **步驟 5**: 更新 `config.toml` 配置檔

## 如何使用

### 本地測試

**注意**：Giscus 評論系統在本地開發環境（`hugo server`）中**不會顯示**，這是正常的。評論系統只會在部署到實際網站後才能正常運作。

### 部署後使用

1. 將 blog 部署到 GitHub Pages、Netlify、Vercel 或其他平台
2. 訪問您的網站上的任何文章頁面
3. 頁面底部會自動顯示 Giscus 評論框
4. 訪客可以使用 GitHub 帳號登入並留言

### 管理評論

所有評論都會儲存在 GitHub Discussions 中：
- 前往 https://github.com/Hokila/blog_comment/discussions
- 在 **Announcements** 分類下可以看到所有文章的討論串
- 您可以在這裡管理、編輯、刪除評論

## 配置說明

### 對應方式 (Mapping)

當前使用 `pathname` 對應方式，表示：
- 每個頁面的路徑會對應到一個 Discussion
- 例如：`/post/my-first-post/` 會建立一個標題包含該路徑的 Discussion

### 主題 (Theme)

當前使用 `preferred_color_scheme`，表示：
- 評論框會自動跟隨使用者的系統深色/淺色模式偏好
- 如果想固定使用特定主題，可以改為 `light` 或 `dark`

### 分類 (Category)

使用 `Announcements` 分類的好處：
- 只有 repository 維護者和 giscus bot 可以建立新的 discussion
- 防止垃圾訊息
- 保持 discussions 的整潔

## 進階設定

### 更改主題

編輯 `config.toml` 中的 `theme` 參數：

```toml
theme = "light"  # 固定淺色主題
theme = "dark"   # 固定深色主題
theme = "preferred_color_scheme"  # 跟隨系統偏好（當前設定）
```

### 更改對應方式

編輯 `config.toml` 中的 `mapping` 參數：

```toml
mapping = "pathname"  # 使用頁面路徑（當前設定，推薦）
mapping = "url"       # 使用完整 URL
mapping = "title"     # 使用頁面標題
mapping = "og:title"  # 使用 OpenGraph 標題
```

### 停用評論系統

如果想暫時停用 Giscus，將 `enable` 設為 `false`：

```toml
[Params.giscus]
  enable = false
```

### 在特定文章停用評論

在文章的 front matter 中加入：

```yaml
---
title: "文章標題"
comments: false
---
```

## 部署建議

### GitHub Pages

1. 使用提供的 `.github/workflows/hugo.yml` 工作流程
2. 推送到 GitHub 後會自動建置和部署
3. 在 repository 設定中啟用 GitHub Pages

### Netlify

1. 連接您的 GitHub repository
2. Build command: `hugo`
3. Publish directory: `public`
4. 自動部署

### Vercel

1. Import GitHub repository
2. Framework Preset: Hugo
3. 自動偵測並部署

## 疑難排解

### 評論框沒有顯示

1. 確認已部署到實際網站（本地環境不會顯示）
2. 檢查瀏覽器控制台是否有錯誤訊息
3. 確認 repository 是公開的
4. 確認 Giscus App 已正確安裝

### 無法留言

1. 確認訪客已登入 GitHub
2. 確認 Giscus App 有權限存取 repository
3. 檢查 repository 的 Discussions 功能是否啟用

### Discussion 沒有自動建立

1. 確認使用的對應方式正確
2. 確認 category 設定正確
3. 嘗試手動在 GitHub Discussions 中建立一個測試討論

## 相關連結

- [Giscus 官方網站](https://giscus.app/zh-TW)
- [Giscus GitHub Repository](https://github.com/giscus/giscus)
- [您的評論 Repository](https://github.com/Hokila/blog_comment)
- [您的 Discussions](https://github.com/Hokila/blog_comment/discussions)
- [Giscus 進階用法](https://github.com/giscus/giscus/blob/main/ADVANCED-USAGE.md)

## 技術細節

### 實際配置代碼

您的 blog 使用以下配置（已整合到 `layouts/partials/giscus.html`）：

```html
<script src="https://giscus.app/client.js"
        data-repo="Hokila/blog_comment"
        data-repo-id="R_kgDOQ4JV2Q"
        data-category="Announcements"
        data-category-id="DIC_kwDOQ4JV2c4C02n5"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="preferred_color_scheme"
        data-lang="zh-TW"
        crossorigin="anonymous"
        async>
</script>
```

### 檔案結構

```
my-blog/
├── layouts/
│   └── partials/
│       ├── comments.html  # 評論系統整合（覆寫主題）
│       └── giscus.html    # Giscus 配置模板
└── config.toml            # 包含 Giscus 參數設定
```

## 享受您的 Blog！

現在您的 blog 已經完全設定好了，包括：
- ✅ Hugo 靜態網站生成器
- ✅ Mainroad 優雅主題
- ✅ Giscus 評論系統（完整配置）
- ✅ GitHub Actions 自動部署

開始寫作並與讀者互動吧！🎉
