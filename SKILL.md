# Echoss VIP Design System — SKILL

> 本文件為 Echoss VIP 開發團隊的 UI 設計系統規範，供 PM、前端工程師、設計師在 Claude 上共用。
> 維護者：設計端（powchuang）｜最後更新：2026-05-25｜版本：v1.0

---

## 使用說明

**PM 製作 Prototype 時**，在 Claude 新對話的第一句話貼上「Claude Prompt 模板」章節的內容，Claude 就會以 Echoss VIP 規範輸出。

**前端工程師**，參照「ConfigProvider 設定」章節複製 `echossTheme` 到專案中套用。

**設計師維護更新**，直接編輯此檔案後推送到 GitHub，團隊下次使用即取得最新版本。

---

## 一、Design Tokens

所有 Token 直接對應 antd v5 ConfigProvider。

### 色彩 Color

| Token | 色碼 | 用途 |
|---|---|---|
| `colorPrimary` | `#07C373` | 品牌主色、Primary Button、Switch on |
| `colorLink` | `#1BAA6D` | 連結文字、Anchor |
| `colorSuccess` | `#07C373` | 成功狀態（同 Primary） |
| `colorWarning` | `#FCB321` | 警示狀態、Warning Alert |
| `colorError` | `#FF4D4F` | 錯誤、Danger Button、Error Alert |
| `colorInfo` | `#1A9CFF` | 資訊提示、Info Alert |
| `colorBgLayout` | `#F8F9FA` | 頁面整體背景 Layout |
| `colorBorder` | `#D9D9D9` | 通用邊框色 |

### 字型 Typography

| Token | 值 | 用途 |
|---|---|---|
| `fontFamily` | `Noto Sans TC, sans-serif` | 全域字型 |
| `fontSize` | `14px` | 基礎字型大小 |
| `fontSizeSM` | `12px` | 輔助說明、Tag、Badge |
| `fontSizeLG` | `16px` | 小標、卡片標題 |
| `fontWeightStrong` | `600` | 粗體 |

### 尺寸與間距 Spacing

| Token | 值 | 用途 |
|---|---|---|
| `borderRadius` | `6px` | 基礎圓角（目前後台實際值） |
| `borderRadiusLG` | `8px` | 大圓角（Card、Modal） |
| `borderRadiusSM` | `4px` | 小圓角（Tag、Badge） |
| `controlHeight` | `32px` | 預設控件高度 |
| `controlHeightLG` | `40px` | Large 控件高度 |
| `controlHeightSM` | `24px` | Small 控件高度 |
| `paddingXS` | `8px` | 最小內距 |
| `paddingSM` | `12px` | 小內距 |
| `paddingMD` | `20px` | 中內距 |
| `paddingLG` | `24px` | 大內距 |
| `paddingXL` | `32px` | 超大內距 |

---

## 二、Color Palette

由 `@ant-design/colors` 的 `generate()` 函數從品牌色推算，每組 1～10 階，數字越小色越淡、越大色越深。

### Primary 主色 — #07C373

| 階 | 色碼 | 用途 |
|---|---|---|
| 1 | `#e6fff0` | 元件背景最淡色（colorPrimary-bg） |
| 2 | `#a6f5c8` | Hover 背景（colorPrimary-bg-hover） |
| 3 | `#79e8ad` | 邊框（colorPrimary-border） |
| 4 | `#4fdb95` | Hover 邊框（colorPrimary-border-hover） |
| 5 | `#29cf81` | Hover 狀態（colorPrimary-hover） |
| **6** | **`#07C373`** | **品牌主色（colorPrimary）** |
| 7 | `#009c5d` | Active 狀態（colorPrimary-active） |
| 8 | `#00754a` | 深色強調 |
| 9 | `#004f35` | 文字色（colorPrimary-text） |
| 10 | `#00291d` | 最深色 |

### Warning 警示色 — #FCB321

| 階 | 色碼 |
|---|---|
| 1 | `#fffced` |
| 2 | `#fff3c4` |
| 3 | `#ffe89c` |
| 4 | `#ffda73` |
| 5 | `#ffc94a` |
| **6** | **`#FCB321`** |
| 7 | `#d68e11` |
| 8 | `#b06c05` |
| 9 | `#8a4e00` |
| 10 | `#633500` |

### Error 錯誤色 — #FF4D4F

| 階 | 色碼 |
|---|---|
| 1 | `#fff2f0` |
| 2 | `#ffccc7` |
| 3 | `#ffa39e` |
| 4 | `#ff7875` |
| **5** | **`#FF4D4F`** |
| 6 | `#f5222d` |
| 7 | `#d9363e` |
| 8 | `#b32430` |
| 9 | `#8c1523` |
| 10 | `#660e1b` |

### Info 資訊色 — #1A9CFF

| 階 | 色碼 |
|---|---|
| 1 | `#e6f8ff` |
| 2 | `#bdebff` |
| 3 | `#94dbff` |
| 4 | `#6bc9ff` |
| 5 | `#42b4ff` |
| **6** | **`#1A9CFF`** |
| 7 | `#0b79d9` |
| 8 | `#0059b3` |
| 9 | `#00418c` |
| 10 | `#002c66` |

---

## 三、元件規範

所有元件基於 **antd v5** 官方元件庫。

### Button 按鈕

| Type | API | 用途 |
|---|---|---|
| Primary | `type="primary"` | 主要操作：兌換、確認、送出 |
| Default | `type="default"` | 次要操作：查看、返回、取消 |
| Danger | `danger={true}` | 破壞性操作：刪除 |
| Text | `type="text"` | 輕重操作、內嵌在卡片中 |
| Link | `type="link"` | 頁面內輔助連結 |

**⛔ 禁止事項**
- 不可用 `Radio.Button` 代替 `Button` 觸發操作
- 不可用純文字連結代替按鈕操作

---

### Tag 標籤

| 色彩 | API | 語意 |
|---|---|---|
| 預設 | `color` 省略 | 一般狀態、分類 |
| 成功 | `color="success"` | 正向狀態：VIP、已啟用 |
| 處理中 | `color="processing"` | 進行中、鑽石卡 |
| 警示 | `color="warning"` | 即將到期 |
| 錯誤 | `color="error"` | 已失效、已停用 |

**⛔ 禁止事項**
- 狀態一律用 Tag 顯示，不用純文字或背景色塊

---

### Switch 開關

**正確用法：** 只用於「即時生效的布林值切換」
- 通知開關
- 功能啟用 / 停用
- 列表中的「啟用」欄：使用 `<Switch size="small" />`

**⛔ 禁止事項**
- 不可用 Switch 代替 Radio 做選擇
- 不可用 Switch 代替 Checkbox 做多選

---

### Radio 單選

| 情境 | 用法 |
|---|---|
| 2～5 個互斥選項 | `<Radio.Group>` |
| 超過 5 個 | 改用 `<Select>` |
| 分組顯示切換（如時間維度） | `<Radio.Button>` |

**⛔ 禁止事項**
- `Radio.Button` 只用於分組顯示切換，不可觸發操作

---

### Form 表單

- 預設布局：`layout="horizontal"`
- 標籤寬度：`labelCol={{ span: 6 }}`
- 欄位寬度：`wrapperCol={{ span: 18 }}`
- 送出按鈕對齊：`wrapperCol={{ offset: 6, span: 18 }}`

---

### Table 表格

- **啟用欄：** 使用 `<Switch size="small" />`，即時反映啟用狀態
- **刪除欄：** 使用 `<DeleteOutlined />` 圖示 + 「刪除」文字
- 不可用「停用」文字代替「刪除」

---

### Badge 徽章

| 狀態 | API | 用途 |
|---|---|---|
| `success` | `status="success"` | 啟用中 |
| `processing` | `status="processing"` | 處理中 |
| `error` | `status="error"` | 停用 |
| `warning` | `status="warning"` | 待審核 |
| `default` | `status="default"` | 草稿 |

---

### 歷史不一致用法統一規範

| 情境 | ❌ 過去錯誤用法 | ✅ 統一規範 |
|---|---|---|
| 啟用/停用功能 | Radio 選「啟用」「停用」 | Switch 元件 |
| 頁面主要操作 | Radio.Button 樣式 | Button Primary |
| 多選一（會員等級） | Switch 輪流切換 | Radio Group |
| 狀態顯示 | 純文字 | Tag 元件 |
| 刪除操作按鈕 | 「停用」文字 | `DeleteOutlined` + 「刪除」 |

---

## 四、ConfigProvider 設定

前端工程師將以下內容存為 `src/theme/echoss-theme.ts`，在 `App.tsx` 最外層包上 `<ConfigProvider>` 即可全局套用 Echoss VIP 品牌色。

```typescript
// src/theme/echoss-theme.ts
export const echossTheme = {
  token: {
    // 品牌色
    colorPrimary: '#07C373',
    colorLink: '#1BAA6D',
    colorSuccess: '#07C373',
    colorWarning: '#FCB321',
    colorError: '#FF4D4F',
    colorInfo: '#1A9CFF',

    // 背景與邊框
    colorBgLayout: '#F8F9FA',
    colorBorder: '#D9D9D9',

    // 字型
    fontFamily: "'Noto Sans TC', sans-serif",
    fontSize: 14,

    // 圓角
    borderRadius: 6,
    borderRadiusLG: 8,
    borderRadiusSM: 4,

    // 控件尺寸
    controlHeight: 32,
    controlHeightLG: 40,
    controlHeightSM: 24,
  },
  components: {
    Layout: {
      siderBg: '#fff',
      headerBg: '#fff',
    },
  },
};
```

```tsx
// src/App.tsx
import { ConfigProvider } from 'antd';
import { echossTheme } from './theme/echoss-theme';

export default function App() {
  return (
    <ConfigProvider theme={echossTheme}>
      {/* 你的應用內容 */}
    </ConfigProvider>
  );
}
```

---

## 五、Claude Prompt 模板

PM 在 Claude.ai 開新對話時，將以下內容**整段複製**貼在第一句話，Claude 就會以 Echoss VIP 規範輸出所有 Prototype。

```
你是 Echoss VIP 產品的 UI Prototype 設計助手。

請參照以下規範輸出所有 UI：

【品牌色碼（必須使用）】
- Primary: #07C373（品牌綠）
- Link: #1BAA6D
- Warning: #FCB321
- Error: #FF4D4F
- Info: #1A9CFF
- Background Layout: #F8F9FA
- Border: #D9D9D9
- Font: Noto Sans TC, sans-serif

【元件規範（antd v5）】
- Button Primary → 主要操作（兌換、確認）
- Button Default → 次要操作（查看、返回）
- Button Danger → 破壞性操作（刪除）
- Switch → 只用於即時布林切換，不代替 Radio
- Radio → 2–5 個互斥選項；超過 5 個用 Select
- Radio.Button → 只用於分組顯示切換，不可觸發操作
- Tag → success=正向、processing=進行中、warning=警示、error=錯誤/失效
- Form → layout="horizontal"，labelCol={{ span: 6 }}，wrapperCol={{ span: 18 }}
- Table 啟用欄 → Switch size="small"
- Table 刪除欄 → DeleteOutlined + 「刪除」

【輸出要求】
- 使用 antd v5 官方 React 元件
- 套用 ConfigProvider + echossTheme
- 字型使用 Noto Sans TC
- 狀態顯示一律用 Tag 元件，不用純文字
```

---

## 六、版本紀錄

### v1.0 — 2026-05-25

**初始建立**
- 建立 Design System 基礎架構
- 定義完整 Design Token（色彩、字型、間距、圓角）
- 建立元件統一規範：Button、Tag、Switch、Radio、Form、Table
- 輸出 `echossTheme` ConfigProvider 設定
- 建立 Claude Prompt 模板供團隊使用
- 寫入 Notion MCP，支援設計師直接在 Notion 維護
- 發佈至 GitHub

**貢獻者：** powchuang（設計端）

---

## 更新說明

設計師更新規範時：
1. 直接編輯此 `SKILL.md` 對應章節
2. Commit 並 push 到 GitHub
3. 團隊下次使用 Claude 時即取得最新版本

不需要通知任何人，自動生效。
