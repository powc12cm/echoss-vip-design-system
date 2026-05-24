# Echoss VIP Design System

Echoss VIP 開發團隊的 UI 設計系統規範，基於 Ant Design v5 + 品牌客製化 Token。

## 用途

供 PM、前端工程師、設計師在 Claude 上共用，確保所有 Prototype 與實作的元件視覺一致。

## 包含內容

- **Design Tokens** — 色碼、字型、間距、圓角完整對照表
- **Color Palette** — Primary / Warning / Error / Info 各 10 階色盤
- **元件規範** — Button、Tag、Switch、Radio、Form、Table 統一用法
- **ConfigProvider 設定** — 前端直接複製套用的 `echossTheme`
- **Claude Prompt 模板** — PM 開新對話直接貼上使用
- **版本紀錄** — Changelog

## 快速使用

### PM

開啟 Claude 新對話，將 `SKILL.md` 中「Claude Prompt 模板」章節的內容整段複製貼入，即可讓 Claude 以 Echoss VIP 規範輸出 Prototype。

### 前端工程師

參照 `SKILL.md` 中「ConfigProvider 設定」章節，複製 `echossTheme` 到專案套用：

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

- UI Framework：Ant Design v5
- 品牌主色：`#07C373`
- 字型：Noto Sans TC
- 基礎圓角：6px

## 版本

**v1.0** — 2026-05-25 初始發佈
