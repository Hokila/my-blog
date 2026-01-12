# 我的個人 Blog

這是一個使用 Hugo 和 Mainroad 主題建立的個人部落格，並整合了 Giscus 評論系統。

## 技術架構

- **靜態網站生成器**: [Hugo](https://gohugo.io/) v0.92.2
- **主題**: [Mainroad](https://github.com/Vimux/Mainroad)
- **評論系統**: [Giscus](https://giscus.app/) (基於 GitHub Discussions)

## 專案結構

```
my-blog/
├── archetypes/          # 內容模板
├── content/             # 文章內容
│   └── post/           # 文章目錄
├── data/               # 資料檔案
├── layouts/            # 自訂佈局模板
│   └── partials/       # 部分模板
│       ├── comments.html  # 評論系統整合
│       └── giscus.html    # Giscus 配置
├── static/             # 靜態資源
├── themes/             # 主題目錄
│   └── mainroad/       # Mainroad 主題
├── config.toml         # Hugo 配置檔
├── GISCUS_SETUP.md    # Giscus 設定指南
└── README.md          # 本文件
```

## 快速開始

### 本地開發

1. 啟動開發伺服器：
   ```bash
   hugo server -D
   ```

2. 開啟瀏覽器訪問 `http://localhost:1313`

### 建立新文章

```bash
hugo new post/my-new-post.md
```

編輯 `content/post/my-new-post.md` 檔案，將 `draft: true` 改為 `draft: false` 以發布文章。

### 建置網站

```bash
hugo
```

建置完成的靜態檔案會輸出到 `public/` 目錄。

## Giscus 評論系統設定

Giscus 評論系統已整合到本 blog 中，但需要您完成配置才能啟用。

詳細設定步驟請參考 [GISCUS_SETUP.md](GISCUS_SETUP.md)。

### 快速設定步驟

1. 建立或使用現有的公開 GitHub repository
2. 在 repository 中啟用 Discussions 功能
3. 安裝 [Giscus App](https://github.com/apps/giscus)
4. 前往 [giscus.app](https://giscus.app/zh-TW) 取得配置資訊
5. 更新 `config.toml` 中的 `[Params.giscus]` 區塊

## 部署

本 blog 可以部署到以下平台：

- **GitHub Pages**: 使用 GitHub Actions 自動部署
- **Netlify**: 連接 GitHub repository 自動部署
- **Vercel**: 支援 Hugo 的快速部署
- **Cloudflare Pages**: 免費且快速的部署選項

### GitHub Pages 部署範例

1. 建立 `.github/workflows/hugo.yml`
2. 推送到 GitHub
3. 在 repository 設定中啟用 GitHub Pages

## 配置說明

主要配置檔案為 `config.toml`，包含以下設定：

- **基本設定**: 網站標題、語言、URL
- **主題設定**: Mainroad 主題參數
- **側邊欄設定**: 小工具配置
- **Giscus 設定**: 評論系統參數

## 自訂化

### 修改樣式

在 `static/css/` 目錄下建立自訂 CSS 檔案。

### 修改佈局

在 `layouts/` 目錄下覆寫主題模板。

### 新增頁面

```bash
hugo new about.md
```

## 相關資源

- [Hugo 官方文件](https://gohugo.io/documentation/)
- [Mainroad 主題文件](https://github.com/Vimux/Mainroad)
- [Giscus 官方網站](https://giscus.app/zh-TW)
- [Hugo 主題市場](https://themes.gohugo.io/)

## 授權

- Blog 內容：由作者保留所有權利
- Hugo：Apache License 2.0
- Mainroad 主題：MIT License
- Giscus：MIT License

## 聯絡方式

如有任何問題或建議，歡迎透過 GitHub Issues 或評論系統聯繫。
