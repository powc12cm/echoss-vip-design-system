# Echoss VIP Design System

Echoss VIP 開發團隊的 UI 設計系統規範，基於 Ant Design v5 + @ant-design/pro-components + 品牌客製化 Token。

## 用途

供 PM、前端工程師、設計師在 Claude 上共用，確保所有 Prototype 與實作的元件視覺、後台框架、頁面版型一致。

## 包含內容

- **Design Tokens** — 色碼、字型、間距、圓角完整對照表
- **Color Palette** — Primary / Warning / Error / Info 各 10 階色盤
- **元件規範** — Button、Tag、Switch、Radio、Form、Table（含**項次欄**）統一用法
- **應用框架 Layout** — ProLayout `layout="mix"`：Header + Sider 的實測參數、props 對照、選單 icon 對應（含 iconfont）
- **列表頁 Layout** — PageContainer + breadcrumb 三層規則、篩選/表格雙 card、ProTable 工具列（新增鈕靠右）
- **內容頁 Layout** — 獨立 Panel（ProCard）+ ProForm form-item 格式 + 每個 panel 各自的動作列
- **欄位元件命名對照** — 內容頁欄位標題＝對應的 `@ant-design/pro-components` 元件名，供同仁複製呼叫
- **ConfigProvider 設定** — 前端直接複製套用的 `echossTheme`
- **Claude Prompt 模板** — PM 開新對話直接貼上使用
- **版本紀錄** — Changelog

## 檔案結構

- `SKILL.md` — 設計系統規範主檔（Claude 上共用）
- `index.html` — 視覺展示頁（色彩／Token／元件／Layout 預覽）
- `references/layout-shell.html` — 後台外框 Layout（mix）完整可貼骨架（Header + Sider）；`index.html` 以 iframe 內嵌預覽
- `references/content-layouts.html` — 列表頁（L2）＋ 新增內容頁（L3）完整可貼骨架（PageContainer / ProTable 項次欄 / ProForm 獨立 panel）

## 快速使用

### PM

開啟 Claude 新對話，將 `SKILL.md` 中「Claude Prompt 模板」章節的內容整段複製貼入，即可讓 Claude 以 Echoss VIP 規範輸出 Prototype。需要完整後台外框時附上 `references/layout-shell.html`；需要列表／內容頁版型時附上 `references/content-layouts.html`。

### 前端工程師

參照 `SKILL.md` 中「ConfigProvider 設定」章節，複製 `echossTheme` 到專案套用；後台框架依「應用框架 Layout」章節套用 ProLayout（`layout="mix"`）：

```tsx
import { ConfigProvider } from 'antd';
import { echossTheme } from './theme/echoss-theme';

<ConfigProvider theme={echossTheme}>
  <App />
</ConfigProvider>
```

列表頁 / 內容頁依「列表頁 Layout」「內容頁 Layout」章節：列表用 `PageContainer` + `ProTable`（最左側加 `valueType:'index'` 項次欄、`toolBarRender` 新增鈕靠右）；新增/編輯頁用 `PageContainer` + 多個獨立 `ProCard` panel + `ProForm`（form-item 格式，每個 panel 各自的取消/儲存動作列）。

### 設計師維護更新

直接編輯 `SKILL.md` 對應章節，commit 並 push，團隊下次使用即自動取得最新版本。

> ⚠️ 選單 icon 一律引用 `references/layout-shell.html` 的完整 SVG path，勿自行截斷（截斷會破圖）。

## 技術規格

- UI Framework：Ant Design v5 + @ant-design/pro-components
- 後台框架：ProLayout `layout="mix"`（Header 56 / Sider 256）
- 頁面容器：PageContainer（breadcrumb 三層 + 標題 + tabs）
- 品牌主色：`#07C373`
- 頁面底色：`linear-gradient(#ffffff, #f5f5f5 28%)`（header/sider/content 透明）
- 字型：Noto Sans TC
- 基礎圓角：6px（card 6 / panel 8）
- 富文本：ReactQuill（Quill `snow` 主題）

## 版本

- **v1.2** — 2026-08-14　合併發布：新增「應用框架 Layout（ProLayout mix）」章節與展示頁、底色 token 修正（`colorBgLayout` → `#F5F5F5`、新增 `colorSplit`、header/sider 透明）；並併入頁面層規範——Table 項次欄、breadcrumb 三層、列表頁／內容頁 Layout、欄位元件命名對照、新增 `references/content-layouts.html`
- **v1.1** — 2026-07-06　Table 操作連結 taxonomy 正式化
- **v1.0** — 2026-05-25　初始發佈

> 完整 Changelog 見 `SKILL.md` 的「版本紀錄」章節。
