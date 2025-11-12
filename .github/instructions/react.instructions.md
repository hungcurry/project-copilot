---
description: 'ReactJS 開發標準與最佳實踐'
applyTo: '**/*.jsx, **/*.tsx, **/*.js, **/*.ts, **/*.css, **/*.scss'
---

# ReactJS 開發指引

依據官方文件 https://react.dev，建構高品質 ReactJS 應用程式，採用現代模式、Hooks 與最佳實踐。

## 專案背景
- 使用最新版 React（React 19+）
- 以 TypeScript 強化型別安全（如適用）
- 預設採用函式型元件與 Hooks
- 遵循 React 官方風格指南與最佳實踐
- 採用現代建構工具（Vite、Create React App 或自訂 Webpack）
- 實作元件組合與重用模式

## 開發標準

### 架構
- 主要採用函式型元件與 Hooks
- 優先使用元件組合而非繼承
- 依功能或領域組織元件，便於擴展
- 明確區分展示型與容器型元件
- 以自訂 Hook 重用有狀態邏輯
- 建立清晰的元件階層與資料流

### TypeScript 整合
- 使用 TypeScript 介面定義 props、state、元件
- 為事件處理器與 refs 定義正確型別
- 適時實作泛型元件
- `tsconfig.json` 啟用嚴格模式
- 善用 React 內建型別（如 `React.FC`, `React.ComponentProps` 等）
- 建立元件變體與狀態的聯集型別

### 元件設計
- 遵循單一職責原則
- 命名具描述性且一致
- 以 TypeScript 或 PropTypes 驗證 props
- 元件設計可測試且可重用
- 保持元件精簡，聚焦單一功能
- 採用組合模式（render props、children 為函式）

### 狀態管理
- 使用 `useState` 管理本地狀態
- 複雜邏輯採用 `useReducer`
- 跨元件樹共享狀態用 `useContext`
- 複雜應用可考慮 Redux Toolkit、Zustand
- 正規化狀態資料結構
- 伺服器狀態管理建議用 React Query 或 SWR

### Hooks 與 Effect
- `useEffect` 正確設置依賴陣列，避免無限迴圈
- Effect 需實作清理函式，防止記憶體洩漏
- 需時用 `useMemo`、`useCallback` 優化效能
- 建立自訂 Hook 重用有狀態邏輯
- 遵守 Hook 規則（僅於頂層呼叫）
- 用 `useRef` 操作 DOM 或儲存可變值

### 樣式設計
- 使用 CSS Modules、Styled Components 或現代 CSS-in-JS
- 響應式設計採行 mobile-first
- CSS class 命名遵循 BEM 或類似規則
- 用 CSS 變數（custom properties）實作主題
- 保持間距、字型、色彩系統一致
- 確保無障礙性（ARIA 屬性、語意 HTML）

### 效能優化
- 適時用 `React.memo` 元件記憶化
- 用 `React.lazy`、`Suspense` 實現程式碼分割
- Tree shaking、動態匯入優化 bundle
- 合理使用 `useMemo`、`useCallback` 避免不必要重渲染
- 大型清單可用虛擬捲動
- 用 React DevTools 分析效能瓶頸

### 資料取得
- 建議用 React Query、SWR、Apollo Client 等現代資料取得函式庫
- 實作載入、錯誤、成功狀態
- 處理競態條件與請求取消
- 樂觀更新提升使用者體驗
- 實作快取策略
- 處理離線與網路錯誤

### 錯誤處理
- 用 Error Boundary 處理元件層級錯誤
- 資料取得需有錯誤狀態
- 錯誤情境提供備用 UI
- 適當記錄錯誤便於除錯
- 處理 effect 與事件處理器的非同步錯誤
- 提供有意義的錯誤訊息給使用者

### 表單與驗證
- 表單輸入採用受控元件
- 表單驗證建議用 Formik、React Hook Form
- 正確處理送出與錯誤狀態
- 表單需有無障礙設計（label、ARIA 屬性）
- 驗證可用 debounce 提升體驗
- 處理檔案上傳與複雜表單情境

### 路由
- 用 React Router 實現前端路由
- 支援巢狀路由與路由保護
- 正確處理路由參數與查詢字串
- 路由懶載入分割程式碼
- 實作正確導覽模式與返回鍵處理
- 實作麵包屑與導覽狀態管理

### 測試
- 用 React Testing Library 撰寫元件單元測試
- 測試元件行為而非實作細節
- 測試框架建議用 Jest
- 複雜元件互動可寫整合測試
- 適當 mock 外部依賴與 API
- 測試無障礙功能與鍵盤操作

### 安全性
- 過濾使用者輸入防止 XSS
- 渲染前驗證與跳脫資料
- 外部 API 皆用 HTTPS
- 實作正確認證與授權模式
- 不將敏感資料存於 localStorage 或 sessionStorage
- 使用 CSP（Content Security Policy）標頭

### 無障礙設計
- 正確使用語意 HTML 元素
- 實作 ARIA 屬性與角色
- 所有互動元件支援鍵盤操作
- 圖片需有 alt 文字，icon 有描述
- 色彩對比需達標
- 用螢幕閱讀器與輔助工具測試

## 實作流程
1. 規劃元件架構與資料流
2. 建立專案結構與資料夾組織
3. 定義 TypeScript 介面與型別
4. 實作核心元件與樣式
5. 加入狀態管理與資料取得邏輯
6. 實作路由與導覽
7. 加入表單處理與驗證
8. 實作錯誤處理與載入狀態
9. 增加元件與功能測試覆蓋率
10. 優化效能與 bundle 大小
11. 確保無障礙合規
12. 增加文件與程式註解

## 其他指引
- 元件命名用 PascalCase，函式用 camelCase
- commit 訊息具意義，保持乾淨 git 歷史
- 實作程式碼分割與懶載入
- 複雜元件與自訂 Hook 用 JSDoc 註解
- 用 ESLint、Prettier 保持格式一致
- 定期更新依賴並檢查安全性
- 依不同部署階段設置環境參數
- 用 React Developer Tools 除錯與效能分析

## 常見模式
- 高階元件（HOC）處理橫切關注
- Render props 元件組合
- Compound 元件實作相關功能
- Provider 模式共享 context 狀態
- 容器/展示型元件分離
- 自訂 Hook 抽取重用邏輯
