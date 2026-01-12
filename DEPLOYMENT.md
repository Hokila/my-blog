# Blog 部署指南

本文件說明如何將您的 Hugo blog 部署到各種平台。

## 部署前準備

### 1. 建立 GitHub Repository

```bash
cd /home/ubuntu/my-blog
git init
git add .
git commit -m "Initial commit: Hugo blog with Mainroad theme and Giscus"
gh repo create my-blog --public --source=. --remote=origin
git push -u origin master
```

或者使用 `main` 作為主分支：

```bash
git branch -m master main
gh repo create my-blog --public --source=. --remote=origin
git push -u origin main
```

### 2. 更新 baseURL

在部署前，記得更新 `config.toml` 中的 `baseURL`：

```toml
baseURL = 'https://yourusername.github.io/my-blog/'  # GitHub Pages
# 或
baseURL = 'https://your-site.netlify.app/'  # Netlify
# 或
baseURL = 'https://your-site.vercel.app/'  # Vercel
```

## 部署選項

### 選項 1: GitHub Pages（推薦）

#### 使用 GitHub Actions 自動部署

1. **確認工作流程檔案存在**
   
   檔案已經建立在 `.github/workflows/hugo.yml`

2. **推送到 GitHub**
   
   ```bash
   git add .
   git commit -m "Add GitHub Actions workflow"
   git push
   ```

3. **設定 GitHub Pages**
   
   - 前往 repository 的 **Settings** → **Pages**
   - Source 選擇 **GitHub Actions**
   - 等待工作流程完成（可在 Actions 標籤查看進度）

4. **訪問您的網站**
   
   網站會發布在 `https://yourusername.github.io/repository-name/`

#### 注意事項

- 如果使用 `main` 分支，確認 `hugo.yml` 中的分支名稱正確
- 首次部署可能需要幾分鐘
- 後續推送會自動觸發重新部署

### 選項 2: Netlify

#### 方法 A: 透過 Git 連接（推薦）

1. **登入 Netlify**
   
   前往 [netlify.com](https://www.netlify.com/) 並登入

2. **New site from Git**
   
   - 點擊 "Add new site" → "Import an existing project"
   - 選擇 GitHub 並授權
   - 選擇您的 blog repository

3. **配置建置設定**
   
   - Build command: `hugo`
   - Publish directory: `public`
   - 點擊 "Deploy site"

4. **設定自訂網域（可選）**
   
   - 在 Site settings → Domain management 中設定

#### 方法 B: 使用 Netlify CLI

```bash
# 安裝 Netlify CLI
npm install -g netlify-cli

# 登入
netlify login

# 初始化並部署
cd /home/ubuntu/my-blog
netlify init
netlify deploy --prod
```

#### Netlify 配置檔（可選）

建立 `netlify.toml`：

```toml
[build]
  publish = "public"
  command = "hugo"

[build.environment]
  HUGO_VERSION = "0.120.0"

[context.production.environment]
  HUGO_ENV = "production"
```

### 選項 3: Vercel

#### 方法 A: 透過 Git 連接

1. **登入 Vercel**
   
   前往 [vercel.com](https://vercel.com/) 並登入

2. **Import Project**
   
   - 點擊 "Add New..." → "Project"
   - 選擇 GitHub repository
   - Vercel 會自動偵測 Hugo

3. **配置設定**
   
   - Framework Preset: Hugo
   - Build Command: `hugo`
   - Output Directory: `public`
   - 點擊 "Deploy"

#### 方法 B: 使用 Vercel CLI

```bash
# 安裝 Vercel CLI
npm install -g vercel

# 部署
cd /home/ubuntu/my-blog
vercel
```

### 選項 4: Cloudflare Pages

1. **登入 Cloudflare**
   
   前往 [pages.cloudflare.com](https://pages.cloudflare.com/)

2. **Create a project**
   
   - 連接 GitHub repository
   - 選擇您的 blog repository

3. **配置建置設定**
   
   - Framework preset: Hugo
   - Build command: `hugo`
   - Build output directory: `public`
   - 環境變數: `HUGO_VERSION` = `0.120.0`

4. **部署**
   
   點擊 "Save and Deploy"

### 選項 5: 自架伺服器

#### 使用 Nginx

1. **建置網站**
   
   ```bash
   cd /home/ubuntu/my-blog
   hugo
   ```

2. **複製到伺服器**
   
   ```bash
   scp -r public/* user@your-server:/var/www/html/
   ```

3. **配置 Nginx**
   
   ```nginx
   server {
       listen 80;
       server_name yourdomain.com;
       root /var/www/html;
       index index.html;
       
       location / {
           try_files $uri $uri/ =404;
       }
   }
   ```

## 持續部署

### 自動化工作流程

使用 GitHub Actions（已配置）：
- 推送到 main/master 分支自動觸發部署
- 可在 Actions 標籤查看部署狀態

### 手動部署

```bash
# 1. 更新內容
hugo new post/new-article.md
# 編輯文章...

# 2. 測試
hugo server -D

# 3. 提交並推送
git add .
git commit -m "Add new article"
git push

# 4. 等待自動部署完成
```

## 部署後檢查清單

- [ ] 網站可以正常訪問
- [ ] 所有頁面正確顯示
- [ ] 圖片和靜態資源載入正常
- [ ] Giscus 評論系統正常運作
- [ ] RSS feed 可以訪問
- [ ] Sitemap 正確生成
- [ ] 手機版顯示正常
- [ ] 設定 Google Analytics（可選）
- [ ] 設定自訂網域（可選）
- [ ] 設定 HTTPS（大部分平台自動提供）

## 常見問題

### CSS 樣式沒有載入

確認 `config.toml` 中的 `baseURL` 設定正確。

### 404 錯誤

檢查：
1. 部署的目錄是否為 `public`
2. `baseURL` 是否正確
3. 檔案路徑是否正確

### Giscus 評論不顯示

1. 確認已部署到實際網站（本地環境不會顯示）
2. 檢查 repository 是公開的
3. 確認 Giscus App 已安裝

### 建置失敗

檢查：
1. Hugo 版本是否正確
2. 主題是否正確安裝（submodule）
3. 查看建置日誌的錯誤訊息

## 效能優化

### 圖片優化

```bash
# 使用 Hugo 的圖片處理功能
# 在 content 中使用相對路徑
```

### 啟用快取

大部分平台會自動配置 CDN 和快取。

### 壓縮資源

Hugo 已經在建置時進行了最小化（使用 `--minify` 選項）。

## 監控和分析

### Google Analytics

在 `config.toml` 中加入：

```toml
googleAnalytics = "G-XXXXXXXXXX"
```

### Cloudflare Analytics

如果使用 Cloudflare Pages，會自動提供分析功能。

## 備份

定期備份：
1. GitHub repository（自動備份）
2. `blog_comment` repository 的 Discussions（評論資料）

## 更新流程

```bash
# 1. 拉取最新變更
git pull

# 2. 更新主題
git submodule update --remote --merge

# 3. 測試
hugo server -D

# 4. 提交並推送
git add .
git commit -m "Update theme"
git push
```

## 相關資源

- [Hugo 官方文件 - Hosting & Deployment](https://gohugo.io/hosting-and-deployment/)
- [GitHub Pages 文件](https://docs.github.com/en/pages)
- [Netlify 文件](https://docs.netlify.com/)
- [Vercel 文件](https://vercel.com/docs)
- [Cloudflare Pages 文件](https://developers.cloudflare.com/pages/)

## 需要協助？

如有任何問題：
1. 查看平台的建置日誌
2. 檢查 Hugo 文件
3. 在 GitHub Issues 尋求幫助
4. 查看 Mainroad 主題文件

祝您部署順利！🚀
