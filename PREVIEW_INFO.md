# Blog 預覽資訊

## 測試結果

✅ Hugo blog 已成功建立並運行
✅ Mainroad 主題已正確安裝和配置
✅ 文章頁面正常顯示
✅ 側邊欄功能正常（Recent Posts、Categories、Tags、Social）
✅ 目錄（Table of Contents）功能正常
✅ Giscus 評論系統已整合（需要配置 GitHub repository 後才會顯示）

## 當前狀態

- **首頁**: 顯示文章列表和側邊欄
- **文章頁面**: 包含完整內容、目錄、標籤、以及評論區域（待配置）
- **主題**: Mainroad - 簡潔優雅的設計
- **語言**: 繁體中文

## 注意事項

頁面底部顯示警告訊息：
> WARNING: Authorbox is activated, but [Author] parameters are not specified.

這是因為啟用了作者資訊框但沒有設定作者資料。如果需要顯示作者資訊，可以在 config.toml 中加入：

```toml
[Author]
  name = "您的名字"
  bio = "您的簡介"
  avatar = "img/avatar.png"
```

或者在 config.toml 中將 `authorbox = false` 以關閉作者資訊框。
