---
name: echoss-vip-design-system
description: >
  Echoss VIP 開發團隊 UI 設計系統規範，基於 Ant Design v5 與 @ant-design/pro-components。
  包含 Design Token、Color Palette、元件使用規範（Button、Tag、Switch、Radio、Form、Table）、
  應用框架 Layout（ProLayout layout="mix"：Header + Sider 實測參數）、
  ConfigProvider echossTheme 設定、Claude Prompt 模板。
  使用時機：任何涉及 Echoss VIP 後台 UI 的 Prototype 製作、Layout 框架、元件選用、前端實作確認。
---

# Echoss VIP Design System — SKILL

> 本文件為 Echoss VIP 開發團隊的 UI 設計系統規範，供 PM、前端工程師、設計師在 Claude 上共用。
> 維護者：設計端（powchuang）｜最後更新：2026-08-14｜版本：v1.2

---

## 使用說明

**PM 製作 Prototype 時**，在 Claude 新對話的第一句話貼上「Claude Prompt 模板」章節的內容，Claude 就會以 Echoss VIP 規範輸出。需要完整後台外框（Header + Sider）時附上 `references/layout-shell.html`；需要列表頁／新增內容頁版型時附上 `references/content-layouts.html`。

**前端工程師**，參照「ConfigProvider 設定」章節複製 `echossTheme`，並依「應用框架 Layout」章節套用 ProLayout。

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
| `colorBgLayout` | `#F5F5F5` | 頁面底色基準（**實測值**，見下方註） |
| `colorBorder` | `#D9D9D9` | 通用邊框色 |
| `colorSplit` | `#f0f0f0` | 分隔線（sider 右緣、header 下緣、tabs、卡片） |
| `colorTextTertiary` | `#8c8c8c` | 次要／停用文字、不可點操作連結 |

> **底色實測註（v1.2 修正）：** 後台實測 `header / sider / content` 三者背景皆為 **透明**，實際底色來自 `body` 的漸層 `linear-gradient(#ffffff, #f5f5f5 28%)`（固定不隨捲動）。因此 `colorBgLayout` 由舊值 `#F8F9FA` 更新為 `#F5F5F5`（漸層終點色），並在「應用框架 Layout」章節說明漸層與透明的用法。舊 token `#F8F9FA` 不再使用。

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
- 不可用 `Radio.Button` 代替 `Button` 觸發一次性動作（`Radio.Button` 是用來選值的，不是觸發動作的）
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
| 擇一選值，選中狀態需保留（如時間維度、設定頁選項） | `<Radio.Button>` |

**⛔ 禁止事項**
- `Radio.Button` 用於**擇一選值**的情境，選中狀態會保留。不可用於觸發一次性動作（那是 `Button` 或 `Button.Group` 的職責）

---

### Form 表單

- 預設布局：`layout="horizontal"`
- 標籤寬度：`labelCol={{ span: 6 }}`
- 欄位寬度：`wrapperCol={{ span: 18 }}`
- 送出按鈕對齊：`wrapperCol={{ offset: 6, span: 18 }}`

---

### Table 表格

- **項次欄（#）：** **所有列表 table 最左側都必須有項次欄。** 使用 ProTable 欄位 `valueType: 'index'`（顯示 1、2、3…列序）。實測參數：標題文字 `#`、欄寬 `36`、靠左（`align: 'left'`／`text-align: start`）、表頭與儲存格 padding `12px 8px`；表頭底色 `#fafafa`、字重 600、色 `rgba(0,0,0,.88)`、底線 `1px #f0f0f0`。**放在所有欄位之前。**
- **啟用欄：** 使用 `<Switch size="small" />`，即時反映啟用狀態
- **操作欄：** 依「操作連結 taxonomy」決定顏色，見下方規範

#### 操作連結 taxonomy（列表內文字連結）

| 功能類型 | 語意 | 顏色 | Token |
|---|---|---|---|
| 主要 / 導覽 | 檢視、編輯、詳情，以及列表內容連結（如點名稱進詳情） | 品牌綠 | `colorPrimary` `#07C373` |
| 次級動作 | 產生新資料或匯出的動作（新增、匯入、匯出、產生） | 品牌黃 | `colorWarning` `#FCB321` |
| 破壞性 | 刪除、作廢、撤銷 | 品牌紅 | `colorError` `#FF4D4F` |
| 停用 | 當前狀態下不可執行的操作 | 灰階、不可點 | `colorTextTertiary` `#8c8c8c` |

**結構規則**
- 列表內文字連結**預設為品牌綠**；`colorInfo`（藍）不用於表格內連結，僅保留給內文中的一般超連結。
- 同一儲存格內有多個操作時，以垂直分隔線 `|`（`colorBorder`）水平分隔，例如 `收回 | 作廢`。
- 破壞性操作執行後若轉為可還原狀態（如已作廢 → 取消作廢），該連結改為主要／導覽（品牌綠）。

**⛔ 禁止事項**
- 操作連結不使用 `colorInfo`（藍）
- 破壞性操作不與其他操作共用同一顏色，須維持品牌紅

> **註：** 個別模組若有語意特殊的操作，需依其實際語意歸類，不可只看字面。例如「序號管理」模組的「收回」是可還原的回復動作（序號被收回、非破壞，優惠內容不消滅），歸為次級動作（品牌黃），不屬於破壞性。

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
| 頁面主要操作 | Radio.Button 樣式（無選中語意） | Button Primary |
| 多選一（會員等級） | Switch 輪流切換 | Radio Group |
| 狀態顯示 | 純文字 | Tag 元件 |

---

## 四、應用框架 Layout（ProLayout）

後台整體框架使用 **`@ant-design/pro-components` 的 `ProLayout`**，佈局類型為 **`layout="mix"`**。以下數值皆自 stage 後台 `/permission/account` 實測後鎖定。完整可貼的 HTML 骨架見 **`references/layout-shell.html`**。

### 4.1 結構判定（mix）

實測幾何：`header {x:256, y:0, w:1256, h:56}`、`sider {x:0, y:56, w:256}` —— header 是**全寬帶**、選單 sider 在其**下方**才開始。

```
┌───────────── Header（全寬 56，透明，下緣 1px 全寬線）─────────────┐
│  [logo 區 256：logo 28 + Echoss VIP]  │  actions：語系切換 / 使用者 / stage │
├───────────────┬──────────────────────────────────────────────────┤
│  Sider 256    │                                                    │
│  （透明、右緣  │   Content（透明，padding 8/40/16/40）              │
│   1px 分隔線） │   PageTitle → Tabs → 白色 Card…                    │
└───────────────┴──────────────────────────────────────────────────┘
     底色：body linear-gradient(#ffffff, #f5f5f5 28%) fixed
```

> ⚠️ 是 **mix** 不是 side：side 會把 sider 右緣線一路畫到頂端、在 logo 與 header 之間多一條直線；mix 的頂端帶是連續的，sider 分隔線只在 `y≥56` 出現。

### 4.2 ProLayout Props 對照

| 區塊 | ProLayout API | 值 / 說明 |
|---|---|---|
| 佈局 | `layout` | `"mix"` |
| 主題 | `navTheme` | `"light"` |
| 固定側欄 | `fixSiderbar` | `true` |
| 側欄寬 | `siderWidth` | `256` |
| 品牌 | `title` / `logo` | `Echoss VIP` / `https://brand.echoss.vip/logo-circle.svg` |
| 選單 | `menuItemRender` / `route.routes` | 見 4.4 icon 對應 |
| 收合鈕 | `collapsedButtonRender` | sider 右上緣圓鈕 |
| Header 右側 | `rightContentRender` / `actionsRender` | 語系切換 Select、`stage` Tag |
| 使用者 | `avatarProps` | `src` logo、`size:22`、名稱 `vipcafeadmin`、副標 `（品牌管理員）` |

### 4.3 實測參數表（定案值）

| 項目 | 值 |
|---|---|
| body 底色 | `linear-gradient(#ffffff, #f5f5f5 28%)`（`fixed`） |
| header / sider / content 背景 | `transparent` |
| 分隔線色 | `#f0f0f0`（header 下緣、sider 右緣） |
| headerHeight | `56` |
| header logo 區寬 | `256`（padding `0 16`；logo `28×28`；title 17px/700） |
| header actions padding（headerPadX） | `0 16`；item gap `20` |
| 語系切換 Select | 高 36、border `1px #D9D9D9`、radius 6、min-width 150、placeholder 文字 `rgba(0,0,0,.25)` |
| 使用者頭像 avatar | `22×22`、圓形、背景 `#fff` |
| 名稱 / 副標 | `14/600` / `12` `#8c8c8c` |
| env badge（stage） | 背景 `colorPrimary`、`#fff`、`12/500`、padding `5px 7px`、radius 4 |
| siderWidth | `256`（透明、右緣 `1px #f0f0f0`） |
| collapse-btn | `26×26`、`top:20 / right:-13`、圓形、`font-size:20`、`align-items:flex-end` |
| 選單 `.pro-menu` padding | `0 8`（僅左右 8） |
| 選單項 item | 高 `40`、padding `0 16`、radius `6`、icon 與文字 gap `8` |
| 選單 icon | `14px` |
| 選單項文字色 | `rgba(0,0,0,.65)` |
| 選中態 | 背景 `rgba(0,0,0,.04)`、文字 `rgba(0,0,0,.95)`、`font-weight 600`（中性灰底深字，非品牌綠底） |
| content padding | 上 `8` / 右 `40` / 下 `16` / 左 `40` |
| page-title | `20/700`、`padding-top:8`、`margin:0 0 16` |
| Tabs | active 品牌綠 + 底部 `2px` 綠線；分隔線 `#f0f0f0` |
| Card | 白底、radius `6`、shadow `0 1px 3px rgba(0,0,0,.06)` |

### 4.4 選單 icon 對應（含 iconfont）

多數為 `@ant-design/icons`，「帳號管理」為自訂 iconfont symbol（需在 ConfigProvider/ProLayout 掛 `iconfontUrl`）。

| 選單 | 圖示來源 | 名稱 / data-icon |
|---|---|---|
| 功能模組 | @ant-design/icons | `AppstoreOutlined`（`appstore`） |
| 會員分析 | @ant-design/icons | `DashboardOutlined`（`dashboard`） |
| 會員資料 | @ant-design/icons | `UserOutlined`（`user`） |
| **帳號管理** | **iconfont** | **`#icon-icon-assignpermissions`**（盾牌，viewBox `0 0 1024 1024`） |
| 門市管理 | @ant-design/icons | `PartitionOutlined`（`partition`） |
| 系統設定 | @ant-design/icons | `LayoutOutlined`（`layout`） |
| 下載區 | @ant-design/icons | `CloudDownloadOutlined`（`cloud-download`） |
| 使用手冊 | @ant-design/icons | `FileOutlined`（`file`） |

### 4.5 React ProLayout 骨架（可貼）

```tsx
import ProLayout from '@ant-design/pro-components';
import {
  AppstoreOutlined, DashboardOutlined, UserOutlined, PartitionOutlined,
  LayoutOutlined, CloudDownloadOutlined, FileOutlined, createFromIconfontCN,
} from '@ant-design/icons';

// 自訂 iconfont（帳號管理等自繪圖示）
const IconFont = createFromIconfontCN({ scriptUrl: '<你的 iconfont.js URL>' });

export default function AppShell({ children }: { children: React.ReactNode }) {
  return (
    <ProLayout
      layout="mix"
      navTheme="light"
      fixSiderbar
      siderWidth={256}
      title="Echoss VIP"
      logo="https://brand.echoss.vip/logo-circle.svg"
      token={{
        header: { colorBgHeader: 'transparent', heightLayoutHeader: 56 },
        sider: {
          colorMenuBackground: 'transparent',
          colorBgMenuItemSelected: 'rgba(0,0,0,0.04)',
          colorTextMenuSelected: 'rgba(0,0,0,0.95)',
        },
        pageContainer: { paddingBlockPageContainerContent: 8, paddingInlinePageContainerContent: 40 },
      }}
      route={{ routes: [
        { path: '/features',   name: '功能模組', icon: <AppstoreOutlined /> },
        { path: '/analysis',   name: '會員分析', icon: <DashboardOutlined /> },
        { path: '/member',     name: '會員資料', icon: <UserOutlined /> },
        { path: '/permission', name: '帳號管理', icon: <IconFont type="icon-icon-assignpermissions" /> },
        { path: '/store',      name: '門市管理', icon: <PartitionOutlined /> },
        { path: '/system',     name: '系統設定', icon: <LayoutOutlined /> },
        { path: '/download',   name: '下載區',   icon: <CloudDownloadOutlined /> },
        { path: '/manual',     name: '使用手冊', icon: <FileOutlined /> },
      ]}}
      avatarProps={{ src: 'https://brand.echoss.vip/logo-circle.svg', size: 22, title: 'vipcafeadmin' }}
      actionsRender={() => [
        /* 語系切換 <Select placeholder="語系切換" /> */,
        /* <Tag color="#07C373">stage</Tag> */,
      ]}
    >
      {children}
    </ProLayout>
  );
}
```

全域底色（放在 `body` 或最外層容器，非 antd token 可表達）：

```css
body { background: linear-gradient(#ffffff, #f5f5f5 28%) fixed; }
```

> ⚠️ **選單 icon 一律引用 `references/layout-shell.html` 的完整 SVG path，勿自行截斷或改寫。** 截斷 path 會導致 icon 破圖（例如 `PartitionOutlined` 少了三個方框子路徑會變成實心塊、`DashboardOutlined` 少了指針會變純圓圈）。八個選單完整 path 皆已鎖定於 layout-shell.html。

### 4.6 列表頁 Layout（PageContainer + ProTable）

模組列表頁一律以 **`PageContainer`** 包裹，內含 breadcrumb → 標題 →（可選）tabs → 內容。完整可貼骨架見 **`references/content-layouts.html`**（預設顯示列表頁 L2）。

**Breadcrumb 規則（三層，由 PageContainer header 產生，位於標題正上方）**

| 層級 | 範例 | 說明 |
|---|---|---|
| L1（root） | `功能模組` | 功能群組，導覽節點 |
| L2（列表頁） | `功能模組 / 優惠模組` | 進入模組後 |
| L3（新增/編輯內容頁） | `功能模組 / 優惠模組 / 新增票券` | 再下一層 |

- 字級 `14px`；祖節點色 `rgba(0,0,0,.45)`、**當前（末）節點** `rgba(0,0,0,.88)`；分隔線 `/` 色 `rgba(0,0,0,.45)`、`margin 0 8px`。
- PageContainer header padding **`8px 40px 16px`**（與 content 內距一致）；標題 `20px/600`。
- ⚠️ 列表頁 breadcrumb 末節點為「模組名」（如 `優惠模組`），頁標題卻可能是 tab 實體（如 `優惠票券`），兩者不一定同字。

**版面結構（實測）**

- 篩選區與表格**各自一張 `ant-pro-card`**（白底、radius 6）。
- **表格必須包在 card 內**；表格 card 的 `ant-pro-card-body` padding 為 **`0 24px 16px`**（表格內容自卡片左右緣內縮 24px，勿貼齊邊緣）。
- **ProTable 工具列（`toolBarRender`）**：主要動作鈕（如「新增資料／新增票券」，Button `type="primary"`）置於工具列**右側、緊貼**設定 icon 群（`⟳` 重新整理 / `☰` 密度 / `⚙` 欄位設定）——即實測後台 `.ant-pro-table-list-toolbar-right` 內、`setting-items` 之前的順序。
- 表格最左側為**項次欄**（見§三 Table）。

### 4.7 內容頁 Layout（新增／編輯頁）

第三層新增／編輯內容頁：`PageContainer`（breadcrumb 三層 + 標題，**無 tabs**）→ 一或多個**獨立 Panel** → 頁尾 Copyright。

**Panel（區塊）**

- 以 **`ProCard`（bordered + title）** 呈現，等同獨立 panel：白底、`border 1px #f0f0f0`、radius 8。
- **Panel 標題**（bold 16/600）為區塊名（如「基本資料」「儲值面額與限制」「集點加碼」）。
- **`panel-body` padding：`16px 24px 16px 24px`**。
- 相關欄位可依語意拆成多個獨立 panel（例：儲值面額一個 panel；發點規則＋集點加碼一個 panel）。

**表單（ProForm，horizontal）**

- 每個欄位一律用 **form-item 格式**：左側 label（固定寬、右對齊、無冒號、必填紅星 `*` `#FF4D4F` 在前）＋右側控件。**區塊內所有標題與內容都要用 form-item 格式，不可把欄位名做成 bold 區塊標題。**
- 設計系統標準 label 欄寬 **`188px`**；控件高 `32px`；欄距 `margin-bottom 24px`；輔助說明 `rgba(0,0,0,.45)` `14px`。
- （若採「欄位標題＝元件名」的參考版，label 較長可加寬至約 `210px`，見 §4.8。）

**動作列（取消／儲存）**

- **每個 panel 各自擁有一組 `取消`（default）＋`儲存`（primary）動作列，置於該 panel body 的左下角**（靠 panel 左緣對齊，`margin-left:0`）。
- ⚠️ 不使用整頁共用的單一底部動作列。

### 4.8 欄位元件命名對照（@ant-design/pro-components）

為讓同仁能「複製欄位名即呼叫對應元件」，內容頁 Prototype 的**欄位標題直接寫該欄位所用的 pro 元件名稱**（與 `@ant-design/pro-components` 一致；不需實作複製按鈕）。

| 欄位型別 | 標題（元件名） | 備註 |
|---|---|---|
| 文字輸入 | `ProFormText` | |
| 數字輸入 | `ProFormDigit` | |
| 下拉選單 | `ProFormSelect` | |
| 單選（按鈕群） | `ProFormRadio.Group` | `optionType: button`（選中＝品牌綠底白字） |
| 單選（原生圈） | `ProFormRadio.Group` | |
| 日期 | `ProFormDatePicker` | |
| 日期區間 | `ProFormDateRangePicker` | |
| 上傳 | `ProFormUploadButton` | |
| 富文本 | `ProForm.Item` | 內層為 **ReactQuill（Quill `snow` 主題）**；pro 無官方富文本元件，實測後台即 react-quill |
| 可增刪列表組合 | `ProFormList` | item 內含 `ProFormText`／`ProFormDigit`；例：儲值面額（面額＋標籤（選填）＋顯示/隱藏 eye icon＋刪除 icon＋「新增」dashed 鈕） |
| 固定分組欄位 | `ProForm.Group` | 各等級固定、單一條件的組合型（降階版 ProList）；item 為 `ProFormDigit`；例：發點規則（各等級「消費滿 X 元獲得一點」） |
| 資料列表（含操作） | `ProList` | 每列標題＋灰色描述＋右側動作連結（如「設定」）；例：各等級加碼設定 |

> 內容頁上方建議加一行說明：「欄位標題即對應的 `@ant-design/pro-components` 元件名稱，可直接複製呼叫該元件。」

---

## 五、ConfigProvider 設定

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

    // 背景與邊框（v1.2：底色實測為漸層，colorBgLayout 取終點色）
    colorBgLayout: '#F5F5F5',
    colorBorder: '#D9D9D9',
    colorSplit: '#f0f0f0',

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
      // v1.2 實測：header / sider 皆透明，底色由 body 漸層透出
      siderBg: 'transparent',
      headerBg: 'transparent',
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

> 全域底色 `linear-gradient(#ffffff, #f5f5f5 28%)` 無法用單一 token 表達，請在 `body`／最外層容器以 CSS 設定（見 §4.5）。

---

## 六、Claude Prompt 模板

PM 在 Claude.ai 開新對話時，將以下內容**整段複製**貼在第一句話，Claude 就會以 Echoss VIP 規範輸出所有 Prototype。

```
你是 Echoss VIP 產品的 UI Prototype 設計助手。

請參照以下規範輸出所有 UI：

【應用框架 Layout（@ant-design/pro-components）】
- 使用 ProLayout，layout="mix"、navTheme="light"、fixSiderbar、siderWidth=256
- 全寬 Header（左 logo 區 256「Echoss VIP」+ 右側 actions：語系切換 Select、stage Tag、使用者 vipcafeadmin/（品牌管理員）頭像 22px）
- 下方左側 Sider 選單、右側 Content
- 底色：body linear-gradient(#ffffff, #f5f5f5 28%)；header/sider/content 皆透明
- 分隔線 #f0f0f0：header 下緣（全寬）、sider 右緣（y≥56）
- 選單 item 高 40、padding 0 16、radius 6、icon 14px；選中態灰底深字 bg rgba(0,0,0,.04)/color rgba(0,0,0,.95)
- content padding 上8/右40/下16/左40；page-title padding-top 8
- 選單 icon：功能模組 AppstoreOutlined、會員分析 DashboardOutlined、會員資料 UserOutlined、帳號管理 iconfont #icon-icon-assignpermissions、門市管理 PartitionOutlined、系統設定 LayoutOutlined、下載區 CloudDownloadOutlined、使用手冊 FileOutlined（icon 一律用 layout-shell.html 完整 path，勿截斷）

【列表頁 / 內容頁 Layout（PageContainer）】
- 頁面以 PageContainer 包裹：breadcrumb（在上）→ 標題 20/600 →（列表頁才有）tabs → 內容；header padding 8/40/16
- Breadcrumb 三層：功能模組 /（模組名）/（動作名，如 新增票券）；祖節點 rgba(0,0,0,.45)、當前節點 rgba(0,0,0,.88)、分隔線 / 為 rgba(0,0,0,.45)
- 列表頁：篩選 card + 表格 card 各自獨立；表格包在 card 內、card body padding 0 24 16；ProTable toolBarRender 的新增鈕（primary）置右、緊貼工具 icon（重新整理/密度/欄位設定）
- 內容頁：每個區塊為獨立 ProCard（bordered + 標題，panel-body padding 16 24）；欄位一律 form-item 格式（label 左 188、右對齊、必填紅星在前）；**每個 panel 各有自己的「取消/儲存」動作列於左下角**，不用整頁單一動作列
- 內容頁欄位標題直接寫對應的 @ant-design/pro-components 元件名（可複製呼叫）：ProFormText / ProFormDigit / ProFormSelect / ProFormRadio.Group（button 或原生）/ ProFormDatePicker / ProFormDateRangePicker / ProFormUploadButton / ProForm.Item（ReactQuill 富文本）/ ProFormList（可增刪列表）/ ProForm.Group（各等級固定分組）/ ProList（資料列表含操作）

【品牌色碼（必須使用）】
- Primary: #07C373（品牌綠）
- Link: #1BAA6D
- Warning: #FCB321
- Error: #FF4D4F
- Info: #1A9CFF
- Background Layout: #F5F5F5（body 漸層終點）
- Border: #D9D9D9 / Split: #f0f0f0
- Font: Noto Sans TC, sans-serif

【元件規範（antd v5）】
- Button Primary → 主要操作（兌換、確認）
- Button Default → 次要操作（查看、返回）
- Button Danger → 破壞性操作（刪除）
- Switch → 只用於即時布林切換，不代替 Radio
- Radio → 2–5 個互斥選項；超過 5 個用 Select
- Radio.Button → 擇一選值且選中狀態需保留（如時間維度、設定頁選項）；不可用於觸發一次性動作
- Tag → success=正向、processing=進行中、warning=警示、error=錯誤/失效
- Form → layout="horizontal"，labelCol={{ span: 6 }}，wrapperCol={{ span: 18 }}
- Table 項次欄 → 所有列表 table 最左側都要有項次欄（ProTable valueType="index"，標題 #、寬 36、靠左）
- Table 啟用欄 → Switch size="small"
- Table 操作欄 → 依操作連結 taxonomy 上色：主要/導覽（編輯、詳情、內容連結）=品牌綠 #07C373；次級動作（新增、匯入、匯出、產生）=品牌黃 #FCB321；破壞性（刪除、作廢、撤銷）=品牌紅 #FF4D4F；停用=灰階不可點 #8c8c8c。列表內連結預設品牌綠、不用藍色；多個操作以「|」分隔。個別模組語意特殊的操作依實際語意歸類（如序號模組「收回」為可還原動作，歸次級=黃）

【輸出要求】
- 使用 antd v5 + @ant-design/pro-components 官方元件
- 套用 ConfigProvider + echossTheme
- 字型使用 Noto Sans TC
- 狀態顯示一律用 Tag 元件，不用純文字
```

---

## 七、版本紀錄

### v1.2 — 2026-08-14

> 本版合併了 08-12 首版 v1.2（應用框架 Layout）與 08-14 的頁面層規範（項次欄、breadcrumb、列表頁／內容頁 Layout、欄位元件命名），一併發布。

**新增頁面層規範（08-14 併入）**
- Table 新增「項次欄」規範：所有列表最左側加項次欄（ProTable `valueType:'index'`，`#`、寬 36、靠左、表頭 `#fafafa`）
- 新增 §4.6 列表頁 Layout：PageContainer + breadcrumb 三層規則、篩選/表格雙 card、表格 card body padding `0 24 16`、ProTable `toolBarRender` 新增鈕靠右緊貼工具 icon
- 新增 §4.7 內容頁 Layout：獨立 ProCard panel（bordered+title、body padding `16 24`）、form-item 格式、**每個 panel 各自左下角動作列**
- 新增 §4.8 欄位元件命名對照：內容頁欄位標題＝對應 pro 元件名（ProFormText / ProFormList / ProForm.Group / ProForm.Item(ReactQuill) / ProList …）供同仁複製呼叫
- 補充：內容頁富文本實測為 **ReactQuill（Quill snow）**，非 pro 官方元件
- 新增參考檔 `references/content-layouts.html`（列表頁 L2 + 內容頁 L3 完整骨架，可貼）
- 強調：選單 icon 一律引用 `layout-shell.html` 完整 SVG path，勿自行截斷（截斷會破圖）

**（08-12 首版 v1.2）新增「應用框架 Layout（ProLayout）」章節**
- 判定後台為 ProLayout `layout="mix"`，附結構圖與 side/mix 差異說明
- 加入 ProLayout props 對照表、實測參數表（header 56 / sider 256 / 選單 / 選中態 / content padding 等全數鎖定值）
- 選單 icon 對應表（含帳號管理 iconfont `#icon-icon-assignpermissions`）
- React `<ProLayout>` 可貼骨架；完整 HTML 見 `references/layout-shell.html`

**底色 token 修正**
- 實測 header/sider/content 皆透明、底色來自 `body` 漸層 `linear-gradient(#ffffff, #f5f5f5 28%)`
- `colorBgLayout` 由 `#F8F9FA` 更新為 `#F5F5F5`（漸層終點色）；`components.Layout` 的 `siderBg/headerBg` 改 `transparent`
- 新增 `colorSplit` `#f0f0f0` token（分隔線）

**同步更新** ConfigProvider 與 Claude Prompt 模板（加入 Layout 指示）

**驗證：** 以 Claude in Chrome 直接讀取 stage 後台 `/permission/account` DOM 與 computed style 校準

**貢獻者：** powchuang（設計端）

---

### v1.1 — 2026-07-06

**操作連結 taxonomy 正式化**
- Table 操作欄由「開發人員自行定義」改為明確的操作連結 taxonomy（主要/導覽=綠、次級=黃、破壞性=紅、停用=灰）
- §一色彩表新增 `colorTextTertiary` `#8c8c8c`（停用／不可點操作連結）
- 新增結構規則：列表內連結預設品牌綠、不使用藍色；多操作以「|」分隔；破壞性操作還原後改為品牌綠
- 加註模組語意特殊操作的歸類原則（如「序號管理」模組「收回」歸次級動作，非破壞性）
- 同步更新 Claude Prompt 模板
- 於「序號管理」模組（activity-list / serial-manage / serial-batches）落地驗證

**貢獻者：** powchuang（設計端）

---

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
