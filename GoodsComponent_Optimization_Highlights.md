
# 商品卡元件優化重點

以下為「必須優化」的重點區塊，請派遣人員依此進行優化作業。

---

## 1. 元件拆分與程式結構

- 將大型 `Goods` 元件拆分為：
  - `GoodsItem`：最外層 `<li>` 容器與事件處理
  - `GoodsImageSlider`：Swiper 與單張圖片 fallback
  - `GoodsInfoBlock`：商品名稱、標籤、出版社／作者、價格、評價
  - `GoodsActions`：加入購物車、追蹤按鈕、銷售量

---

## 2. 效能優化

- **避免重建陣列**  
  - 刪除 `const goodsList = [...props.goodsInfoList]`  
  - 改用 `useMemo`：  
    ```ts
    const goodsList = useMemo(() => props.goodsInfoList, [props.goodsInfoList])
    ```
- **配合 React.memo**  
  - 把 `onGoodsClick`、`atAddToCart` 用 `useCallback` 包裝，確保 props 穩定
- **條件載入 Swiper**  
  - 單張圖片時不載入 Swiper，改為直接 `<img loading="lazy" />`
- **圖片懶載入**  
  - 在所有 `<img>` 標籤加上 `loading="lazy"`

---

## 3. 移除 Inline Style

- **背景圖**  
  - 將 `style={{ backgroundImage: 'url(...)' }}` 移至 CSS class 或 SCSS
- **JSX style 物件**  
  - 改用 `className` + CSS／SCSS，減少執行時物件建立

---

## 4. 邏輯搬移到 Utility

- **函式抽出**  
  - `publisherLink`、`authorLink`、`categorizeGoodsTag`、`categorizeIconTag` 都搬到 `/utils/`  
- **簡化條件判斷**  
  - 將 `isShowPublisherBlock` 改寫為單行判斷

---

## 5. 渲染與 JSX 優化

- **小元件化**  
  - 把 map 內過長 JSX 拆成小元件
- **動態 class 處理**  
  - 使用 `classnames` 或 helper 來組裝複雜 className
- **移除匿名 inline function**  
  - 改成透過 `useCallback` 定義 handler，再在 JSX 中使用

---

## 6. 減少 DOM 查詢

- **避免 document.querySelectorAll**  
  - 透過 props 或 ref 傳遞 `goodsIndex`，避免在 React 裡查詢 DOM

---

請依優先順序：先進行架構拆分與效能優化，再依序處理樣式、工具函式、渲染細節與 DOM 查詢重構。
