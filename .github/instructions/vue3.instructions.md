---
description: 'VueJS 3 開發標準與最佳實踐（使用 Composition API 與 TypeScript）'
applyTo: '**/*.vue, **/*.ts, **/*.js, **/*.scss'
---

# VueJS 3 開發指引

本文件提供使用 Composition API、TypeScript 與現代化最佳實踐，建立高品質 VueJS 3 應用的開發準則。

## 專案背景
- 預設使用 Vue 3.x 的 Composition API  
- 採用 TypeScript 以確保型別安全  
- 使用單檔元件（`.vue`），並採 `<script setup>` 語法  
- 使用現代建構工具（建議使用 Vite）  
- 應用狀態管理使用 Pinia  
- 遵循官方 Vue 風格指南與最佳實踐  

## 開發標準

### 架構
- 優先使用 Composition API（`setup` 函式與 composables），取代 Options API  
- 依功能或領域組織元件與 composable，方便擴展  
- 將以 UI 為主的元件（展示用）與以邏輯為主的元件（容器）分離  
- 將可重複使用的邏輯提取到 `composables/` 目錄中的函式  
- 以領域為單位結構化 Pinia 的 store 模組，明確定義 actions、state 與 getters  

### TypeScript 整合
- 在 `tsconfig.json` 啟用 `strict` 模式以最大化型別安全  
- 使用 `defineComponent` 或 `<script setup lang="ts">` 搭配 `defineProps` 與 `defineEmits`  
- 使用 `PropType<T>` 定義具型別的 props 與預設值  
- 以介面或型別別名（type alias）定義複雜的 props 與 state 結構  
- 為事件處理器、refs、`useRoute`/`useRouter` 鉤子定義型別  
- 在適用情況下使用泛型元件與 composable  

### 元件設計
- 遵循單一職責原則（Single Responsibility Principle）  
- 元件名稱採 PascalCase，檔名使用 kebab-case  
- 保持元件小而專注於單一功能  
- 使用 `<script setup>` 簡化語法並提升效能  
- 以 TypeScript 驗證 props，僅在必要時使用執行期檢查  
- 優先使用 slot 與 scoped slot 實現彈性組合  

### 狀態管理
- 使用 Pinia 管理全域狀態：以 `defineStore` 定義 store  
- 對於簡單的區域狀態，使用 `ref` 或 `reactive`  
- 以 `computed` 建立衍生狀態  
- 在處理複雜資料結構時保持狀態正規化（normalized）  
- 將非同步邏輯放入 Pinia 的 actions  
- 使用 store 外掛實現持久化或偵錯功能  

### Composition API 模式
- 建立可重用的 composable（例如 `useFetch`、`useAuth`）  
- 使用 `watch` 與 `watchEffect` 並精確指定依賴  
- 在 `onUnmounted` 或 `watch` 的清理回呼中釋放副作用  
- 謹慎使用 `provide`/`inject` 進行深層依賴注入  
- 使用 `useAsyncData` 或第三方工具（如 Vue Query）進行非同步資料處理  

### 樣式
- 在元件層級使用 `<style scoped>` 或 CSS Modules  
- 建議採用工具優先框架（如 Tailwind CSS）以加速開發  
- 採 BEM 或功能導向命名規範命名 class  
- 使用 CSS 變數進行主題與設計變數管理  
- 採行 mobile-first 響應式設計（使用 CSS Grid 或 Flexbox）  
- 確保樣式具備可及性（對比度、焦點狀態）  

### 效能優化
- 以動態匯入與 `defineAsyncComponent` 實現延遲載入  
- 使用 `<Suspense>` 處理非同步元件載入回退  
- 對靜態內容使用 `v-once` 或 `v-memo`  
- 使用 Vue DevTools 的效能分析工具進行剖析  
- 避免不必要的監聽器，優先使用 `computed`  
- 使用 Vite 的 Tree-shaking 與最佳化機制移除未用代碼  

### 資料請求
- 使用 composable（如 `useFetch`）或 Vue Query 等函式庫  
- 明確處理 loading、error、success 狀態  
- 在元件卸載或參數變更時取消過期請求  
- 實作樂觀更新並在失敗時回滾  
- 快取回應並採背景重新驗證（background revalidation）  

### 錯誤處理
- 使用全域錯誤處理器（`app.config.errorHandler`）捕捉未預期錯誤  
- 使用 `try/catch` 包裹風險邏輯並提供友善提示  
- 在元件內使用 `errorCaptured` 建立局部錯誤邊界  
- 優雅顯示錯誤 UI 或提示訊息  
- 將錯誤上報至外部監控服務（如 Sentry、LogRocket）  

### 表單與驗證
- 使用 VeeValidate 或 @vueuse/form 等函式庫  
- 使用受控的 `v-model` 綁定管理表單值  
- 使用防抖（debounce）於輸入或失焦事件進行驗證  
- 在 composable 處理檔案上傳與多步驟表單邏輯  
- 確保無障礙：標籤關聯、錯誤提示與焦點管理  

### 路由
- 使用 Vue Router 4 搭配 `createRouter` 與 `createWebHistory`  
- 實現巢狀路由與按需載入  
- 使用導航守衛（`beforeEnter`、`beforeEach`）保護路由  
- 在 `setup` 內使用 `useRoute` 與 `useRouter` 進行導覽  
- 妥善處理查詢參數與動態路由段  
- 透過 route meta 設定麵包屑資料  

### 測試
- 使用 Vue Test Utils 與 Jest 撰寫單元測試  
- 測試行為而非內部實作  
- 使用 `mount` 或 `shallowMount` 進行元件隔離  
- 模擬全域插件（如 router、Pinia）  
- 使用 Cypress 或 Playwright 撰寫端對端測試  
- 整合 axe-core 進行可及性測試  

### 安全性
- 避免使用 `v-html`，若需使用需嚴格消毒  
- 使用 CSP 標頭防止 XSS 與注入攻擊  
- 在模板與指令中驗證與轉義資料  
- API 請求全數使用 HTTPS  
- 將敏感 Token 儲存在 HTTP-only Cookie，而非 localStorage  

### 無障礙設計（Accessibility）
- 採用語意化 HTML 元素與 ARIA 屬性  
- 管理模態視窗與動態內容的焦點  
- 為互動元件提供鍵盤導覽支援  
- 為圖片與圖示添加有意義的 `alt` 文本  
- 確保顏色對比符合 WCAG AA 標準  

## 實作流程
1. 規劃元件與 composable 架構  
2. 使用 Vue 3 + TypeScript 初始化 Vite 專案  
3. 定義 Pinia stores 與 composable  
4. 建立核心 UI 元件與版面配置  
5. 整合路由與導覽邏輯  
6. 實作資料請求與狀態邏輯  
7. 建立表單與驗證及錯誤狀態  
8. 加入全域錯誤處理與回退 UI  
9. 編寫單元與端對端測試  
10. 優化效能與打包體積  
11. 確保無障礙符合標準  
12. 文件化元件、composable 與 store  

## 額外指引
- 遵循官方 Vue 風格指南（vuejs.org/style-guide）  
- 使用 ESLint（`plugin:vue/vue3-recommended`）與 Prettier 維持一致性  
- 撰寫具意義的 commit 訊息並保持整潔歷史  
- 定期更新相依套件並檢查安全性  
- 使用 JSDoc/TSDoc 為複雜邏輯添加註解  
- 使用 Vue DevTools 進行偵錯與效能分析  

## 常見模式
- 使用無渲染（Renderless）元件與 scoped slot 提供彈性 UI  
- 以 provide/inject 建立複合元件（Compound Components）  
- 使用自訂指令處理跨元件邏輯  
- 使用 Teleport 實現模態與浮層  
- 以插件系統（plugin）提供全域功能（i18n、分析工具等）  
- 透過 composable factory 建立可參數化邏輯  

