
# Goods Component 優化任務說明文件

## 🔧 目的
優化 `src/components/mobile/goods/index.tsx` 中的 `Goods` 商品卡元件，提升程式碼可讀性、模組化程度與未來維護性。

---

## 📁 任務範圍

| 範圍 | 說明 |
|------|------|
| ✅ 包含 | 組件內部邏輯重構、UI 區塊拆分、樣式與條件簡化、命名優化 |
| ❌ 不含 | 埋點邏輯 (`sendMomowaTrackEvent` 等)、API 呼叫行為 |

---

## 📌 優化項目與執行說明

### 1. 組件拆分
**目的：** 簡化主元件內容，增加模組可重用性。

| 區塊功能             | 拆出成元件名                     |
|----------------------|----------------------------------|
| 商品圖片與輪播區     | `GoodsImageArea.tsx`             |
| 商品資訊欄（標題、tag）| `GoodsMetaInfo.tsx`              |
| 商品價格區塊         | `GoodsPriceInfo.tsx`             |
| 商品作者／出版社區塊 | `GoodsPublishInfo.tsx`           |
| 加入購物車／追蹤區   | `GoodsActionButtons.tsx`         |

> 📁 路徑建議：`/components/mobile/goods/blocks/`

---

### 2. 抽出邏輯函式
**目的：** 把與 UI 無關的邏輯抽出，便於單元測試與維護。

| 函式                      | 移動至                          |
|---------------------------|----------------------------------|
| `categorizeGoodsTag()`     | `utils/goodsTagUtils.ts`         |
| `categorizeIconTag()`      | `utils/goodsTagUtils.ts`         |
| `isShowMarketPrice()`      | `utils/goodsPriceUtils.ts`       |
| `publisherLink()`、`authorLink()` | `utils/bookLinkUtils.ts`   |

---

### 3. 樣式與 className 優化
**目的：** 減少冗長條件與重複判斷。

- 引入 `classnames` 套件簡化 class 條件語法。
- 將 `props.goodsShowType === 'chessboardType'` 結果儲存為變數，例如：

```ts
const isChessboard = props.goodsShowType === 'chessboardType'
```

- 將背景圖樣式抽成變數：

```ts
const backgroundImageStyle = {
  backgroundImage: `url(${
    isChessboard ? goods.edmCardBackgroundUrl : goods.edmListBackgroundUrl
  })`
}
```

---

### 4. 抽離硬編碼字串
**目的：** 增加文字維護與多語系支援的彈性。

請建立 `constants/goodsText.ts` 並將下列字串抽出：

```ts
export const GOODS_TEXT = {
  AD: 'Ad',
  ADULT: '18禁',
  EDM_BUTTON: '立即前往',
  AUTHOR: '作者',
  PUBLISHER: '出版社'
}
```

---

### 5. 商品標籤樣式邏輯改用映射表
**目的：** 增加可擴充性與可讀性。

請將原本硬編碼的 tag 判斷：

```ts
if (content === '預') {...}
```

改寫成：

```ts
const goodsTagMap = new Map<string, TagStyleInfo>([
  ['預', { theme: Theme.orange, addonStyle: 'bg-orange-500', type: 'solid' }],
  ...
])
```

---

## 🧪 驗收標準

| 項目                             | 驗收方式 |
|----------------------------------|----------|
| 元件是否已依功能拆分             | 每個功能元件單獨呈現 |
| 是否使用 classnames 優化樣式條件 | `className` 寫法簡潔清楚 |
| 是否抽出重複邏輯至 utils         | 所有 `tag/icon` 判斷不再出現在元件中 |
| 執行後頁面功能不變               | 手動測試原功能無破壞 |

---

## 📦 附註

- 重構後請 **保留原本的 props 傳入結構**，不要改動元件的使用介面。
- 拆出的 utils 函式應提供型別，並附上註解。
