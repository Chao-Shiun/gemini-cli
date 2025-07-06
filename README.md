# Gemini CLI

[![Gemini CLI CI](https://github.com/google-gemini/gemini-cli/actions/workflows/ci.yml/badge.svg)](https://github.com/google-gemini/gemini-cli/actions/workflows/ci.yml)

![Gemini CLI 螢幕截圖](./docs/assets/gemini-screenshot.png)

本儲存庫包含 Gemini CLI，這是一個命令列 AI 工作流程工具，可連接您的工具、理解您的程式碼並加速您的工作流程。

透過 Gemini CLI，您可以：

- 在 Gemini 的 1M token 內容視窗內外查詢和編輯大型程式碼庫。
- 使用 Gemini 的多模態功能，從 PDF 或草圖生成新的應用程式。
- 自動化操作任務，例如查詢提取請求或處理複雜的 rebase。
- 使用工具和 MCP 伺服器連接新功能，包括[使用 Imagen、Veo 或 Lyria 進行媒體生成](https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia)。
- 使用內建於 Gemini 的 [Google 搜尋](https://ai.google.dev/gemini-api/docs/grounding)工具來支援您的查詢。

## 快速入門

1.  **先決條件：** 確保您已安裝 [Node.js 20](https://nodejs.org/en/download) 或更高版本。
2.  **執行 CLI：** 在您的終端機中執行以下指令：

    ```bash
    npx https://github.com/google-gemini/gemini-cli
    ```

    或使用以下指令安裝：

    ```bash
    npm install -g @google/gemini-cli
    gemini
    ```

3.  **選擇顏色主題**
4.  **驗證：** 出現提示時，使用您的個人 Google 帳戶登入。這將授予您使用 Gemini 每分鐘最多 60 次模型請求和每天 1,000 次模型請求的權限。

您現在已準備好使用 Gemini CLI！

### 使用 Gemini API 金鑰：

Gemini API 提供免費方案，使用 Gemini 1.5 Pro 每天可發出 [100 次請求](https://ai.google.dev/gemini-api/docs/rate-limits#free-tier)，您可以控制使用哪個模型，並能存取更高的速率限制（需付費方案）：

1.  從 [Google AI Studio](https://aistudio.google.com/apikey) 產生金鑰。
2.  在您的終端機中將其設定為環境變數。將 `YOUR_API_KEY` 替換為您產生的金鑰。

    ```bash
    export GEMINI_API_KEY="YOUR_API_KEY"
    ```

3.  （可選）在 API 金鑰頁面上將您的 Gemini API 專案升級為付費方案（將自動解鎖[第 1 級速率限制](https://ai.google.dev/gemini-api/docs/rate-limits#tier-1)）。

有關其他驗證方法，包括 Google Workspace 帳戶，請參閱[驗證](./docs/cli/authentication.md)指南。

## 範例

CLI 執行後，您可以開始從您的 shell 與 Gemini 互動。

您可以從一個新目錄開始一個專案：

```sh
cd new-project/
gemini
> 幫我寫一個 Gemini Discord 機器人，它會使用我將提供的 FAQ.md 檔案來回答問題
```

或處理現有專案：

```sh
git clone https://github.com/google-gemini/gemini-cli
cd gemini-cli
gemini
> 給我昨天所有變更的摘要
```

### 後續步驟

- 學習如何[從原始碼貢獻或建置](./CONTRIBUTING.md)。
- 探索可用的 **[CLI 指令](./docs/cli/commands.md)**。
- 如果您遇到任何問題，請參閱**[疑難排解指南](./docs/troubleshooting.md)**。
- 如需更全面的文件，請參閱[完整文件](./docs/index.md)。
- 查看一些[熱門任務](#popular-tasks)以獲得更多靈感。

### 專案結構

Gemini CLI 是一個使用 npm workspaces 管理的 monorepo。主要目錄及其用途概述如下：

| 路徑 | 說明 |
| --- | --- |
| `packages/cli` | Gemini CLI 的主要進入點和使用者介面。此套件負責呈現互動式提示並處理使用者輸入。 |
| `packages/core` | 包含核心邏輯，包括可用工具的實作、與 Gemini API 互動的服務以及遙測。 |
| `docs/` | 所有專案文件，包括指南、架構概觀和指令參考。 |
| `scripts/` | 用於建置、測試和其他開發相關任務的 Node.js 指令碼集合。 |
| `integration-tests/` | 驗證 CLI 功能及其與各種工具和服務整合的端對端測試。 |
| `.github/` | GitHub 的設定，包括 CI/CD 工作流程（在 `workflows/` 中）、問題範本和提取請求範本。 |
| `eslint-rules/` | 用於維護整個專案程式碼品質和一致性的自訂 ESLint 規則。 |
| `esbuild.config.js` | esbuild 的設定，用於將應用程式打包以供生產環境使用。 |
| `tsconfig.json` | 專案的根 TypeScript 設定檔。 |
| `package.json` | 定義專案的相依性、指令碼和 workspaces。 |

### 疑難排解

如果您遇到問題，請前往[疑難排解](docs/troubleshooting.md)指南。

## 熱門任務

### 探索新的程式碼庫

首先 `cd` 進入現有或新複製的儲存庫並執行 `gemini`。

```text
> 描述此系統架構的主要部分。
```

```text
> 有哪些安全機制？
```

### 使用您現有的程式碼

```text
> 為 GitHub 問題 #123 實作初稿。
```

```text
> 幫我將此程式碼庫遷移到最新版本的 Java。從一個計畫開始。
```

### 自動化您的工作流程

使用 MCP 伺服器將您的本機系統工具與您的企業協作套件整合。

```text
> 幫我製作一個投影片，顯示過去 7 天的 git 歷史記錄，並按功能和團隊成員分組。
```

```text
> 為牆面顯示器製作一個全螢幕 Web 應用程式，以顯示我們互動最頻繁的 GitHub 問題。
```

### 與您的系統互動

```text
> 將此目錄中的所有影像轉換為 png，並根據 exif 資料中的日期重新命名。
```

```text
> 按支出月份整理我的 PDF 發票。
```

### 解除安裝

有關解除安裝說明，請前往[解除安裝](docs/Uninstall.md)指南。

## 服務條款和隱私權聲明

有關適用於您使用 Gemini CLI 的服務條款和隱私權聲明的詳細資訊，請參閱[服務條款和隱私權聲明](./docs/tos-privacy.md)。