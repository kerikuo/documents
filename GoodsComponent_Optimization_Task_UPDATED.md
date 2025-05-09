
# 商品卡元件優化任務說明

## 🔧 任務名稱：商品卡元件結構與效能優化

### 🧾 背景說明
目前 `src/components/mobile/goods/index.tsx` 為商品卡主元件，整體功能完整但過於龐大，包含 UI 呈現、邏輯處理、埋點追蹤等，建議進行重構與優化，提升元件的可讀性、可維護性與效能表現。

---

### ✅ 任務目標
1. 拆分原始 `Goods` 元件為多個子元件（依照功能區塊）
2. 優化圖片載入與 Swiper 使用邏輯
3. 清除非必要 inline style 與搬移邏輯 function 至 utils

---

### 📂 作業範圍

#### 1. 子元件拆分（以功能為主）

| 子元件名稱         | 功能描述                            |
|------------------|-----------------------------------|
| `GoodsItem`      | 包裝每筆商品卡的主要邏輯              |
| `GoodsImageSlider` | 處理 Swiper 與圖片標籤顯示邏輯       |
| `GoodsTagGroup`  | 顯示商品標籤（如 店⁺、預購、免運券等）與 icon |
| `GoodsPriceBlock`| 顯示價格、市價、3P 價格資訊等         |
| `GoodsPublisherInfo` | 出版社／作者區塊                 |
| `GoodsActionButtons` | 加入購物車與愛心追蹤按鈕區域        |

> 每個子元件請放在 `/components/mobile/goods/components/` 中，並設有 `index.tsx` 檔。

---

#### 2. 效能優化
- 商品圖如 `imgTypeUrlArray.length < 2`，則改為單張圖片，不使用 Swiper。
- `<img>` 標籤請補上 `loading="lazy"`。
- `goodsList` 改用 `useMemo` 包裝，避免 React.memo 失效：
  ```tsx
  const goodsList = useMemo(() => props.goodsInfoList, [props.goodsInfoList])
  ```

---

#### 3. 追蹤邏輯（排除處理）

> 本區塊屬於 momowa 埋點追蹤邏輯，請勿調整  
> `onGoodsClick` 函式內已有明確標記 `// 👉 埋點邏輯開始` ~ `// 👉 埋點邏輯結束`  
> 派遣人員不需修改這段程式，若需協助請通知負責人處理

---

#### 4. 邏輯搬移與樣式優化
- `categorizeGoodsTag` 與 `categorizeIconTag` 搬至 `@/utils/goodsTagHelper.ts`
- 將 inline `style={{ backgroundImage: 'url(...)' }}` 改為使用 class + CSS 寫法，統一樣式於 SCSS 或 Tailwind（依原專案規範處理）。

---

### 🧪 驗收條件
- 商品卡畫面呈現不變（可用 mock 資料或現有 `props` 驗證）
- 新元件有基本 prop 驗證（interface）
- 僅使用 TypeScript + React（不引入額外套件）
- 可透過 Storybook 或 `Search` 頁面正常渲染並互動

---

### 📎 附加資料
- 原始檔案位置：`/src/components/mobile/goods/index.tsx`
- 使用的 interface 來自：`@/utils/model`
- 若需協助確認資料型態可詢問原開發人員
