# Copilot Instructions for SDD-shop-web

## 🏗️ 專案架構概覽
- 本專案為 Vue 3 + Vite 商店網站，採用 Composition API 與模組化組件設計。
- 主要目錄結構：
  - `src/components/`：所有 UI 組件（如 Header, Footer, ProductCard, ProductList, Home, About, Contact）
  - `src/assets/products.js`：商品資料來源，前端假資料陣列
  - `src/router/index.js`：路由設定，負責頁面切換與 props 傳遞
  - `src/App.vue`：全域佈局，包含 Header、Footer 及 `<router-view />`
  - `src/main.js`：應用程式入口，掛載 Vue 並注入 router

## ⚡️ 開發與建置流程
- 開發啟動：`npm run dev`（Vite 快速啟動，預設 http://localhost:5173）
- 建置生產：`npm run build`（產生 dist/ 目錄）
- 預覽建置：`npm run preview`
- 無測試框架，無自動化測試腳本

## 🧩 關鍵設計模式與慣例
- 所有組件皆採用 `<script setup>`，推薦使用 Composition API 寫法
- 商品資料透過 props 傳遞至 `ProductList`，再分發給 `ProductCard`
- 路由 props 實作範例：
  ```js
  // src/router/index.js
  {
    path: '/products',
    name: 'Products',
    component: ProductList,
    props: { products: products }
  }
  ```
- 響應式設計：CSS 皆採用 scoped 樣式，並針對不同螢幕尺寸設計
- Swiper 輪播整合於 `ProductList.vue`，斷點設計如下：
  ```js
  const breakpoints = {
    800: { slidesPerView: 3 },
    600: { slidesPerView: 3 },
    400: { slidesPerView: 2 },
  }
  ```
- Header 組件含響應式選單與搜尋框，手機版自動切換漢堡選單

## 🔗 外部依賴與整合
- 主要依賴：`vue`, `vue-router`, `swiper`, `@vitejs/plugin-vue`, `vite`
- 無後端 API 整合，所有資料皆為前端假資料
- 無 SSR、無 Vuex/Pinia 狀態管理

## 📝 其他注意事項
- 請遵循現有組件命名與 props 傳遞慣例
- 新增頁面請於 `src/components/` 建立，並於 `src/router/index.js` 註冊
- 若需擴充商品資料，請編輯 `src/assets/products.js`
- 請勿引入未經討論的全新架構或大型依賴

---


### AI Agent 專用補充
- 請優先參考本檔案，勿採用未明確規範的「最佳實踐」或自訂流程。
- 只需維護前端假資料，不需串接 API。
- 若需新增組件，請依現有命名規則與 props 傳遞模式。
- 若遇不明確或遺漏之處，請回報以便補充。

如有不明確或遺漏之處，請回報以便補充！
