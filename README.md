# Echoss VIP Design System

Echoss VIP 開發團隊的 UI 設計系統規範，基於 Ant Design v5 + @ant-design/pro-components + 品牌客製化 Token。

## 用途

供 PM、前端工程師、設計師在 Claude 上共用，確保所有 Prototype 與實作的元件視覺、後台框架一致。

## 包含內容

- **Design Tokens** — 色碼、字型、間距、圓角完整對照表
- **Color Palette** — Primary / Warning / Error / Info 各 10 階色盤
- **元件規範** — Button、Tag、Switch、Radio、Form、Table 統一用法
- **應用框架 Layout** — ProLayout `layout="mix"`：Header + Sider 的實測參數、props 對照、選單 icon 對應（含 iconfont）
- **ConfigProvider 設定** — 前端直接複製套用的 `echossTheme`
- **Claude Prompt 模板** — PM 開新對話直接貼上使用
- **版本紀錄** — Changelog

## 檔案結構

- `SKILL.md` — 設計系統規範主檔（Claude 上共用）
- `index.html` — 視覺展示頁（色彩／Token／元件／Layout 預覽）
- `references/layout-shell.html` — 後台 Layout（mix）完整可貼骨架；`index.html` 以 iframe 內嵌預覽

## 快速使用

### PM

開啟 Claude 新對話，將 `SKILL.md` 中「Claude Prompt 模板」章節的內容整段複製貼入，即可讓 Claude 以 Echoss VIP 規範輸出 Prototype。需要完整後台框架時，附上 `references/layout-shell.html`。

### 前端工程師

參照 `SKILL.md` 中「ConfigProvider 設定」章節，複製 `echossTheme` 到專案套用；後台框架依「應用框架 Layout」章節套用 ProLayout（`layout="mix"`）：

```tsx
import { ConfigProvider } from 'antd';
import { echossTheme } from './theme/echoss-theme';

<ConfigProvider theme={echossTheme}>
  <App />
</ConfigProvider>
```

### 設計師維護更新

直接編輯 `SKILL.md` 對應章節，commit 並 push，團隊下次使用即自動取得最新版本。

## 技術規格

- UI Framework：Ant Design v5 + @ant-design/pro-components
- 後台框架：ProLayout `layout="mix"`（Header 56 / Sider 256）
- 品牌主色：`#07C373`
- 頁面底色：`linear-gradient(#ffffff, #f5f5f5 28%)`（header/sider/content 透明）
- 字型：Noto Sans TC
- 基礎圓角：6px

## 版本

- **v1.2** — 2026-08-12　新增「應用框架 Layout（ProLayout mix）」章節與展示頁；底色 token 修正（`colorBgLayout` → `#F5F5F5`、新增 `colorSplit`、header/sider 透明）
- **v1.1** — 2026-07-06　Table 操作連結 taxonomy 正式化
- **v1.0** — 2026-05-25　初始發佈

> 完整 Changelog 見 `SKILL.md` 的「版本紀錄」章節。
