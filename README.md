#### 網址: https://github.com/github/awesome-copilot

### (一).Prompts（提示檔案）- .prompt.md
用途：特定任務的快速指令
比喻：就像預設好的快捷指令或範本
使用方式：用 / 指令主動呼叫

特色：
✅ 你主動呼叫它 /vue /react
✅ 用於特定、一次性的任務
✅ 像是「幫我做某件事」的按鈕

![螢幕擷取畫面 2025-11-12 111832](https://hackmd.io/_uploads/HJxn2dWg-g.png)



實際例子：
```jsx=
---
mode: agent
---
# 產生readme

當你需要建立 README 檔案時，產生包含專案描述、安裝步驟、使用方法的完整文件。

**使用場景**：
/create-readme
/create-test
/explain-error
/write-doc
```



### (二).Instructions（指示）- .instructions.md
用途：自動套用的編碼標準和規則
比喻：就像背景自動執行的規則引擎
使用方式：自動偵測檔案類型並套用

特色：
✅ 自動觸發，不用手動呼叫
✅ 持續性地影響特定類型的檔案
✅ 像是「在背景監督你的程式碼風格」


實際例子：
```jsx=
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
```

### (三).Chat Modes（模式）- .chatmode.md
用途：切換 AI 的角色和專業領域
比喻：就像換一個專家來跟你對話
使用方式：用Agent 選特定角色

![螢幕擷取畫面 2025-11-12 111953](https://hackmd.io/_uploads/Hk21pd-lbx.png)


特色：
✅ 改變 AI 的「專業身份」
✅ 用於需要特定專業知識的對話
✅ 像是「找不同領域的專家諮詢」

實際例子：
```jsx=
---
description: "檢視程式碼品質與最佳實踐的遵循度。"
tools: ["usages", "vscodeAPI", "problems", "fetch", "githubRepo", "search"]
---

# 程式碼審查模式

你是一位經驗豐富的資深開發者，正在進行徹底的程式碼審查。你的職責是檢視程式碼的品質、最佳實踐，以及是否遵循[專案標準](../copilot-instructions.md)，但不直接修改程式碼。

## 分析重點

- 分析程式碼品質、架構與最佳實踐
- 識別潛在的錯誤、安全問題或效能問題
- 評估無障礙性與使用者體驗考量
- 評估可維護性與可讀性
```
