---
title: 開發（通用）
seo-title: Developing (generic)
description: 整合框架包括帶有API的整合層，允許您為電AEM子商務功能構建元件
seo-description: The integration framework includes an integration layer with an API, allowing you to build AEM components for eCommerce capabilities
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: 1138a548-d112-4446-b0e1-b7a9ea7c7604
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 0%

---

# 開發（通用）{#developing-generic}

>[!NOTE]
>
>[API文檔](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 的上界。

該整合框架包括具有API的整合層。 這允許您構AEM建電子商務功能的元件（獨立於您的特定電子商務引擎）。 它還允許您使用內部CRX資料庫或插入電子商務系統並將產品資料拉入AEM。

提供了多個現成元件AEM以使用整合層。 目前，這些是：

* 產品顯示元件
* 購物車
* 促銷和憑單
* 目錄和分區藍圖
* 簽出
* 搜尋

為了搜索，提供了允許您使用搜索、第AEM三方搜索或其組合的整合鈎子。

## 電子商務引擎選擇 {#ecommerce-engine-selection}

電子商務框架可以與任何電子商務解決方案一起使用，所使用的引擎需要由AEM — 即使使用通用引AEM擎：

* 電子商務引擎是OSGi服務，支援 `CommerceService` 介面

   * 引擎可由 `commerceProvider` 服務屬性

* AEM支 `Resource.adaptTo()` 為 `CommerceService` 和 `Product`

   * 的 `adaptTo` 實施查找 `cq:commerceProvider` 資源層次結構中的屬性：

      * 如果找到，則使用該值篩選商業服務查找。
      * 如果找不到，則使用排名最高的商務服務。
   * A `cq:Commerce` 使用混合，因此 `cq:commerceProvider` 可以添加到強類型資源中。


* 的 `cq:commerceProvider` 屬性亦用於參考適當之商業工廠定義。

   * 例如， `cq:commerceProvider` 值geometrixx的屬性將與的OSGi配置相關 **Day CQ Commerce Factory for Autdoors(Day CQ Commerce Factory for AutdoorsGeometrixx商廠)** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`) — 參數的位置 `commerceProvider` 也有值 `geometrixx`。
   * 此處可以配置其他屬性（如果適當且可用）。

在標準安AEM裝中，需要具體實施，例如：

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | 幾何線示例；這包括對通用API的最小擴展 |

### 範例 {#example}

```shell
/etc/commerce/products/geometrixx-outdoors
+ cq:commerceProvider = geometrixx
  + adobe-logo-shirt
    + cq:commerceType = product
    + price = 12.50
  + adobe-logo-shirt_S
    + cq:commerceType = variant
    + size = S
  + adobe-logo-shirt_XL
    + cq:commerceType = variant
    + size = XL
    + price = 14.50
```

>[!NOTE]
>
>使用CRXDE Lite，您可以查看在通用實現的產品元件中如何處理AEM該問題：
>
>`/apps/geometrixx-outdoors/components/product`

### 會話處理 {#session-handling}

儲存與客戶購物車相關的資訊的會話。

的 **商務會話**:

* 擁有 **購物車**

   * 執行添加/刪除/等
   * 在購物車上執行各種計算；

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* 擁有的持久性 **訂單** 資料：

   `CommerceSession.getUserContext()`

* 可以使用 `updateOrder(Map<String, Object> delta)`
* 還擁有 **付款** 處理連接
* 還擁有 **完成** 連接

### 架構 {#architecture}

#### 產品和變型的體系結構 {#architecture-of-product-and-variants}

一個產品可以有多種變化；例如，它可能因顏色和/或大小而異。 產品必須定義驅動變化的屬性；我們 *變型軸*。

但是，並非所有屬性都是變型軸。 變動也會影響其他物業；例如，價格可能取決於規模。 這些屬性不能由購物者選擇，因此不被視為變型軸。

每個產品和/或變型都由資源表示，因此將1:1映射到儲存庫節點。 這是一個推論，即特定產品和/或變型可以通過其路徑唯一地標識。

任何產品資源都可以由 `Product API`。 產品API中的大多數調用都是特定於變體的（儘管變體可能從祖先繼承共用值），但也有一些調用列出了變體集( `getVariantAxes()`。 `getVariants()`等)。

>[!NOTE]
>
>實際上，變數軸由任何 `Product.getVariantAxes()` 返回：
>
>* 對於一般實AEM現，請從產品資料中的屬性中讀取它( `cq:productVariantAxes`)
>
>雖然產品（通常）可以有許多變型軸，但出廠預裝產品元件僅處理兩個：
>
>1. `size`
>1. 再加一個

>
>   通過 `variationAxis` 產品引用的屬性(通常 `color` Geometrixx Outdoors)。

#### 產品參考和PIM資料 {#product-references-and-pim-data}

總的來說：

* PIM資料位於 `/etc`

* 產品參考 `/content`。

產品變體和產品資料節點之間必須有1:1的映射。

產品引用還必須為所呈現的每個變體具有一個節點 — 但不要求顯示所有變體。 例如，如果產品有S、M、L變體，則產品資料可能是：

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

儘管「大而高」目錄可能只有：

```shell
content
  big-and-tall
    shirt
      shirt-l
```

最後，不需要使用產品資料。 可以將所有產品資料放在目錄中的引用下；但是，如果不複製所有產品資料，就不能真的擁有多個目錄。

**API**

#### com.adobe.cq.commerce.api.Product介面 {#com-adobe-cq-commerce-api-product-interface}

```java
public interface Product extends Adaptable {

    public String getPath();            // path to specific variation
    public String getPagePath();        // path to presentation page for all variations
    public String getSKU();             // unique ID of specific variation

    public String getTitle();           // shortcut to getProperty(TITLE)
    public String getDescription();     // shortcut to getProperty(DESCRIPTION)
    public String getImageUrl();        // shortcut to getProperty(IMAGE_URL)
    public String getThumbnailUrl();    // shortcut to getProperty(THUMBNAIL_URL)

    public <T> T getProperty(String name, Class<T> type);

    public Iterator<String> getVariantAxes();
    public boolean axisIsVariant(String axis);
    public Iterator<Product> getVariants(VariantFilter filter) throws CommerceException;
}
```

#### com.adobe.cq.commerce.api.VariantFilter  {#com-adobe-cq-commerce-api-variantfilter}

```java
/**
 * Interface for filtering variants and AxisFilter provided as common implementation
 *
 * The <code>VariantFilter</code> is used to filter variants,
 * e.g. when using {@link Product#getVariants(VariantFilter filter)}.
 */
public interface VariantFilter {
    public boolean includes(Product product);
}

/**
 * A {@link VariantFilter} for filtering variants by the given
 * axis and value. The following example returns a list of
 * variant products that have a value of <i>blue</i> on the
 * <i>color</i> axis.
 *
 * <p>
 * <code>product.getVariants(new AxisFilter("color", "blue"));</code>
 */
public class AxisFilter implements VariantFilter {

    private String axis;
    private String value;

    public AxisFilter(String axis, String value) {
        this.axis = axis;
        this.value = value;
    }

    /**
     * {@inheritDoc}
     */
    public boolean includes(Product product) {
        ValueMap values = product.adaptTo(ValueMap.class);

        if(values != null) {
            String v = values.get(axis, String.class);

            return v != null && v == value;
        }

        return false;
    }
}
```

* **常規儲存機制**

   * 產品節點不是非結構化的。
   * 產品節點可以是：

      * 一個引用，其中產品資料儲存在其他位置：

         * 產品引用包含 `productData` 屬性，它指向產品資料(通常位於 `/etc/commerce/products`)。
         * 產品資料是分層的；product屬性是從product資料節點的祖先繼承的。
         * 產品引用還可以包含本地屬性，這些屬性會覆蓋其產品資料中指定的屬性。
      * 產品本身：

         * 沒有 `productData` 屬性。
         * 本地保存所有屬性（不包含productData屬性）的產品節點直接從其自己的祖先繼承產品屬性。


* **通AEM用產品結構**

   * 每個變型必須有其自己的葉節點。
   * 產品介面既表示產品，也表示變型，但相關儲存庫節點是特定的。
   * 產品節點描述產品屬性和變型軸。

#### 範例 {#example-1}

```shell
+ banyan_shirt
    - cq:commerceType = product
    - cq:productAttributes = [jcr:title, jcr:description, size, price, color]
    - cq:productVariantAxes = [color, size]
    - jcr:title = Banyan Shirt
    - jcr:description = Flowery, all-cotton shirt.
    - price = 14.00
    + banyan_shirt_s
        - cq:commerceType = variant
        - size = S
        + banyan_shirt_s_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_s_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_m
        - cq:commerceType = variant
        - size = M
        + banyan_shirt_m_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_m_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_l
        - cq:commerceType = variant
        - size = L
        + banyan_shirt_l_red
            - cq:commerceType = variant
            - color = red
        + banyan_shirt_l_blue
            - cq:commerceType = variant
            - color = blue
    + banyan_shirt_xl
        - cq:commerceType = variant
        - size = XL
        - price = 18.00
```

#### 購物車的建築 {#architecture-of-the-shopping-cart}

**元件**

* 購物車由 `CommerceSession:`

   * 的 `CommerceSession` 執行添加、刪除等。
   * 的 `CommerceSession` 還在購物車上執行各種計算。
   * 的 `CommerceSession` 還應用已觸發到購物車的憑證和促銷。

* 雖然與購物車不直接相關，但 `CommerceSession` 還必須提供目錄定價資訊(因為它擁有定價

   * 定價可能有幾個修改量：

      * 數量折扣。
      * 不同的貨幣。
      * 免增值稅和免增值稅。
   * 修飾符完全是開放式的，具有以下介面：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**儲存空間**

* 儲存空間

   * 在通AEM用情況下， [ClientContext](/help/sites-administering/client-context.md)

**個人化**

* 個性化應始終通過 [ClientContext](/help/sites-administering/client-context.md)。
* ClientContext `/version/` 建立Cart:

   * 應使用 `CommerceSession.addCartEntry()` 的雙曲餘切值。

* 以下說明了ClientContext車中的購物車資訊示例：

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### 結帳體系結構 {#architecture-of-checkout}

**購物車和訂單資料**

的 `CommerceSession` 擁有三個元素：

1. **購物車內容**

   購物車內容架構由API固定：

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **定價**

   定價方案也由API固定：

   ```java
       public String getCartPreTaxPrice();
       public String getCartTax();
       public String getCartTotalPrice();
       public String getOrderShipping();
       public String getOrderTotalTax();
       public String getOrderTotalPrice();
   ```

1. **訂單詳細資料**

   但是，訂單詳細資訊 *不* 由API修復：

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**發運計算**

* 訂單通常需要提供多個發運選項（和價格）。
* 價格可能基於訂單的項目和詳細資訊，如重量和/或交貨地址。
* 的 `CommerceSession` 具有對所有依賴項的訪問權限，因此可以以與產品定價類似的方式處理它：

   * 的 `CommerceSession` 擁有發運定價。
   * 使用 `updateOrder(Map<String, Object> delta)` 以檢索/更新交貨詳細資訊。

### 搜索定義 {#search-definition}

遵循標準服務API模型，電子商務項目提供了一組可由單個商務引擎實現的與搜索相關的API。

>[!NOTE]
>
>目前，只有hybris引擎實現現成的搜索API。
>
>但是，搜索API是通用的，可由每個CommerceService單獨實現。
>
>因此，儘管出廠提供的通用實現並未實現此API，但您可以擴展它並添加搜索功能。

電子商務項目包含預設搜索元件，位於：

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

這利用搜索API查詢所選商業引擎(請參閱 [電子商務引擎選擇](#ecommerce-engine-selection)):

#### 搜索API {#search-api}

核心項目提供了幾個通用/幫助程式類：

1. `CommerceQuery`

   用於描述搜索查詢（包含有關查詢文本、當前頁、頁面大小、排序和所選小平面的資訊）。 所有實現搜索API的電子商務服務都將接收此類實例以執行其搜索。 A `CommerceQuery` 可以從請求對象( `HttpServletRequest`)。

1. `FacetParamHelper`

   是提供一種靜態方法的實用程式類 —  `toParams`  — 用於生成 `GET` 來自facets清單的參數字串和一個切換的值。 這在UI端非常有用，在UI端，您需要為每個方面的每個值顯示一個超連結，這樣當用戶按一下該超連結時，就會切換各個值（即，如果選擇了它，則會從查詢中刪除它，否則會添加）。 這將考慮處理多個/單值小平面、覆蓋值等的所有邏輯。

搜索API的入口點是 `CommerceService#search` 返回 `CommerceResult` 的雙曲餘切值。 有關本主題的詳細資訊，請參閱API文檔。

### 開發促銷和憑單 {#developing-promotions-and-vouchers}

* 憑單:

   * 憑單是基於頁面的元件，使用網站控制台建立/編輯並儲存在以下位置：

      `/content/campaigns`

   * 憑證供應：

      * 憑證代碼（由購物者輸入購物車）。
      * 憑證標籤（在購物者將其輸入購物車後顯示）。
      * 升級路徑（定義憑證應用的操作）。
   * 憑單沒有其自己的開/關日期/時間，但使用其父市場活動的日期/時間。
   * 外部商務引擎也可以提供憑證；這些要求至少以下幾項：

      * 憑證代碼
      * 安 `isValid()` 方法
   * 的 **憑證** 元件(C) `/libs/commerce/components/voucher`)提供：

      * 憑證管理的呈現者；這顯示購物車中當前的任何憑證。
      * 用於管理（添加/刪除）憑證的編輯對話框（表單）。
      * 在購物車中添加/刪除憑單所需的操作。



* 促銷活動:

   * 「升級」是一個基於頁面的元件，使用「網站」控制台建立/編輯，並儲存在以下位置：

      `/content/campaigns`

   * 促銷供應：

      * 優先順序
      * 升級處理程式路徑
   * 您可以將促銷與市場活動連接，以定義其開/關日期/時間。
   * 您可以將促銷與體驗相連，以定義其細分市場。
   * 與體驗無關的促銷不會自行啟動，但仍然可以通過憑單啟動。
   * 升級元件( `/libs/commerce/components/promotion`)包含：

      * 提升管理的呈現者和對話
      * 用於呈現和編輯特定於升級處理程式的配置參數的子元件
   * 提供兩個升級處理程式：

      * `DiscountPromotionHandler`，它應用購物車範圍的絕對或百分比折扣
      * `PerfectPartnerPromotionHandler`，如果合作夥伴產品也在購物車中，則應用產品絕對折扣或百分比折扣
   * ClientContext `SegmentMgr` 解析段和ClientContext `CartMgr` 解決促銷。 將觸發每個受至少一個已解析段約束的促銷。

      * 已激發的促銷通過呼叫將返AJAX回伺服器以重新計算購物車。
      * 激發的促銷（和添加的憑單）也顯示在ClientContext面板中。




從購物車添加/刪除憑單是通過 `CommerceSession` API:

```java
/**
 * Apply a voucher to this session's cart.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void addVoucher(String code) throws CommerceException;

/**
 * Remove a voucher that was previously added with {@link #addVoucher(String)}.
 *
 * @param code the voucher's code
 * @throws CommerceException
 */
public void removeVoucher(String code) throws CommerceException;

/**
 * Get a list of vouchers that were added to this cart via {@link #addVoucher(String)}.
 *
 * @throws CommerceException
 */
public List<Voucher> getVouchers() throws CommerceException;
```

這邊， `CommerceSession` 負責檢查憑證是否存在以及是否可以應用。 這可能適用於只有滿足特定條件才能應用的憑單；例如，當購物車總價格大於$100時)。 如果憑證因任何原因無法應用， `addVoucher` 方法將引發異常。 另外， `CommerceSession` 負責在添加/刪除憑證後更新購物車的價格。

的 `Voucher` 是類似Bean的類，它包含以下欄位：

* 憑證代碼
* 簡短描述
* 引用指示折扣類型和值的相關促銷

的 `AbstractJcrCommerceSession` 可以應用憑單。 類返回的憑證 `getVouchers()` 是 `cq:Page` 包含jcr:content節點，該節點具有以下屬性（其中包括）:

* `sling:resourceType` （字串） — 這需要 `commerce/components/voucher`

* `jcr:title` （字串） — 用於憑證的說明
* `code` （字串） — 用戶必須輸入的代碼才能應用此憑證
* `promotion` （字串） — 要應用的升級；例如 `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

促銷處理程式是修改購物車的OSGi服務。 該購物車將支援在 `PromotionHandler` 。

```java
/**
 * Apply promotion to a cart line item. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @param cartEntry The cart line item
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyCartEntryPromotion(CommerceSession commerceSession,
                                         Promotion promotion, CartEntry cartEntry)
    throws CommerceException;

/**
 * Apply promotion to an order. The method returns a discount
 * <code>PriceInfo</code> instance or <code>null</code> if no discount
 * was applied.
 * @param commerceSession The commerce session
 * @param promotion The configured promotion
 * @return A discounted <code>PriceInfo</code> or <code>null</code>
 */
public PriceInfo applyOrderPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

public PriceInfo applyShippingPromotion(CommerceSession commerceSession, Promotion promotion)
    throws CommerceException;

/**
 * Allows a promotion handler to define a custom, author-oriented message for a promotion.
 * The {@link com.adobe.cq.commerce.common.promotion.PerfectPartnerPromotionHandler}, for instance,
 * uses this to list the qualifying pairs of products in the current cart.
 * @param commerceSession
 * @param promotion
 * @return A message to display
 * @throws CommerceException
 */
public String getMessage(SlingHttpServletRequest request, CommerceSession commerceSession, Promotion promotion) throws CommerceException;

/**
 * Informs the promotion handler that something under the promotions root has been edited, and the handler
 * should invalidate any caches it might be keeping.
 */
public void invalidateCaches();
```

提供了三個升級處理程式：

* `DiscountPromotionHandler` 應用購物車範圍的絕對折扣或百分比折扣
* `PerfectPartnerPromotionHandler` 如果產品合作夥伴也在購物車中，則應用產品絕對折扣或百分比折扣
* `FreeShippingPromotionHandler` 應用免費運送
