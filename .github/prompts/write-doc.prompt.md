---
mode: agent
---
# 撰寫文件（Write Documentation）

## 指令（Prompt）範本
你是一位資深技術寫手與工程師，請根據下面輸入的「功能資訊」產出一份完整的技術文件（Markdown 格式），內容要能直接放進專案的 `docs/` 或 `prompts/` 資料夾。文件要簡潔、有條理，包含範例程式碼、輸入輸出欄位、錯誤碼與處理建議、相依性、版本紀錄與維護者資訊。請依指示產生適合開發者閱讀的技術文件。

### 必要輸入（請提供）
- 功能或模組名稱（name）
- 功能簡述（short_description） — 一行描述為何需要此功能
- 使用場景（use_cases） — 列出 1~3 個常見場景
- API 或介面規格（如果有）：
  - 路徑 / 方法（例如：`POST /api/v1/tasks`）
  - 請求參數（name、type、required、description、example）
  - 回傳格式（status、data schema、error examples）
- 前置需求（prerequisites） — 例如：需登入、需某 service、需特定權限或環境變數
- 相依性（dependencies） — 例如：其他微服務、資料庫、第三方 API、npm 套件
- 權限／安全考量（auth） — 若需 token、scope、OAuth 等請說明
- 常見錯誤（errors） — 錯誤碼與說明、可能原因、處理建議
- 範例程式碼語言（至少一種，建議 JS/TS 或 curl）
- 維護者（owner）與聯絡方式
- 版本（version）與變更紀錄（可選）
- 額外說明（notes，可選）

### 產出格式（Markdown）
文件應包含以下章節（若部分輸入缺少，仍保留章節但標記為 TODO）：

1. 標題（包含功能名稱、版本）
2. 概覽（1~3 段，含 short_description、主要 use_cases）
3. 前置條件（prerequisites / setup）
4. 快速開始（Quick Start）  
   - 最少一個能立刻執行的範例（可用 curl / JS）
5. API 規格 / 介面（Endpoints / Methods）  
   - 對每個 endpoint 提供：描述、路徑、HTTP 方法、請求範例、參數表格、回應範例（成功與錯誤）
6. 行為描述（流程步驟、狀態機、重要邏輯或副作用）
7. 錯誤處理（Error codes & handling）
8. 範例（Usage examples）：至少一個真實可用範例（含輸入輸出）
9. 相依性與相容性（dependencies / compatible versions）
10. 性能與安全注意事項（performance / security）
11. 測試建議（unit / integration / e2e 測試重點）
12. 維護與版本紀錄（owner、contact、CHANGELOG 範例）
13. FAQ 或已知限制（optional）
14. Appendix（資料結構或、schema 的完整 JSON 範例）

### 內容品質要求
- 清楚明確：使用者能照著 Quick Start 操作成功。
- 可執行範例：範例程式碼可直接執行（或只需少量替換參數）。
- 一致性：參數名稱、範例與表格需一致。
- 可讀性：條列化、表格化說明欄位與範例。
- 標準化：HTTP 狀態碼與錯誤碼遵循一般慣例（2xx 成功、4xx 用戶端錯誤、5xx 伺服器錯誤）。

---

## 範例輸入（示範）
> 使用者可以給出如下 JSON（或自由文字）作為輸入，幫助生成文件。

```json
{
  "name": "Create Task",
  "short_description": "建立任務並回傳任務 ID",
  "use_cases": [
    "使用者在 UI 建立待辦任務",
    "系統自動排程建立背景任務"
  ],
  "api": {
    "path": "/api/v1/tasks",
    "method": "POST",
    "request": [
      {"name": "title", "type": "string", "required": true, "description": "任務標題"},
      {"name": "dueDate", "type": "string (ISO8601)", "required": false, "description": "到期日"},
      {"name": "ownerId", "type": "string", "required": true, "description": "指派使用者 ID"}
    ],
    "response": {
      "200": {"status": "success", "data": {"taskId": "string"}},
      "400": {"status": "error", "error": {"code": "BadRequest", "message": "invalid input"}}
    }
  },
  "prerequisites": ["Authenticated user", "UserService reachable"],
  "dependencies": ["UserService v2+", "Postgres 13+"],
  "auth": "Bearer token required (scope: tasks:create)",
  "examples": ["curl example or JS example"],
  "owner": "team-todo / todo-owner@example.com",
  "version": "1.0.0"
}
