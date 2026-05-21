# LS Medal

Lost Saga 勳章資料查詢網頁。以卡片方式列出勳章的屬性數值，並可依系列篩選、依數值排序，方便比較與選配。

## 功能

- **勳章列表**：以卡片呈現名稱、圖示與八項屬性
- **系列篩選**：全部、憤怒、月光
- **排序**：預設、攻擊力、防禦力、移動速度、減少跌傷、武器／盔甲／頭盔／披風技能（由高到低）
- **屬性顯示**：正數為綠色、負數為紅色、零為灰色

每張卡片包含：

| 屬性 | 說明 |
|------|------|
| 武器技能 | 武器相關技能加成 |
| 盔甲技能 | 盔甲相關技能加成 |
| 頭盔技能 | 頭盔相關技能加成 |
| 披風技能 | 披風相關技能加成 |
| 攻擊力 | 攻擊數值 |
| 防禦力 | 防禦數值 |
| 移動速度 | 移速加成 |
| 減少跌傷 | 跌落傷害減免 |

目前資料共 **59** 枚勳章（憤怒系列 + 月光系列）。

## 技術棧

- [React](https://react.dev/) 19
- [Vite](https://vite.dev/) 8
- [TypeScript](https://www.typescriptlang.org/)
- [Tailwind CSS](https://tailwindcss.com/) 4
- [React Router](https://reactrouter.com/) 7
- [Lucide React](https://lucide.dev/)（圖示）

## 專案結構

```
ls_medal/
├── index.html              # 進入點
├── src/
│   ├── main.tsx            # React 掛載與 Router
│   ├── App.tsx             # 路由設定
│   ├── Medal.tsx           # 主頁：篩選、排序、列表
│   ├── components/
│   │   └── Card.tsx        # 單張勳章卡片
│   ├── data/
│   │   └── LsMedalData.ts  # 勳章資料（由 CSV 產生）
│   ├── assets/images/      # 勳章圖片（檔名為小寫英文名或原名小寫 .png）
│   └── scripts/
│       ├── LsMedalData.csv # 原始資料表
│       └── convert.cjs     # CSV → TypeScript 轉換腳本
└── dist/                   # 建置輸出（npm run build）
```

## 環境需求

- [Node.js](https://nodejs.org/)（建議 18 以上）
- npm

## 安裝與執行

```bash
# 安裝依賴
npm install

# 開發模式（預設 http://localhost:5173）
npm run dev

# 建置正式版
npm run build

# 預覽建置結果
npm run preview
```

開啟網站後，首頁即為勳章列表（路徑 `/`）。舊路徑 `/ls_medal` 會自動導向首頁。

## 更新勳章資料

1. 編輯 `src/scripts/LsMedalData.csv`
2. 確認對應圖片已放在 `src/assets/images/`，檔名為 `{勳章名稱小寫}.png`
3. 在專案根目錄執行轉換腳本：

```bash
node src/scripts/convert.cjs
```

會重新產生 `src/data/LsMedalData.ts`。完成後重新執行 `npm run dev` 或 `npm run build` 即可看到更新。

### CSV 欄位

`id`, `category`, `name`, `weaponSkill`, `armorSkill`, `helmetSkill`, `cloakSkill`, `attack`, `defense`, `moveSpeed`, `fallDamageReduction`

- `category` 僅支援：`憤怒`、`月光`
- `name` 需與圖片檔名對應（轉換時會以小寫比對 `.png`）

## 部署說明

`vite.config.ts` 中 `base` 設為 `'./'`，建置後的 `dist/` 可直接放在子目錄或靜態主機，無需額外設定根路徑。

若使用 GitHub Pages 等靜態託管，上傳 `dist/` 內容即可。

## 授權

本專案為私人用途之資料整理工具。遊戲相關名稱、圖像版權屬原權利人所有。
