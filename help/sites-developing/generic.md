---
title: 開發（一般）
seo-title: 開發（一般）
description: 整合架構包含具有API的整合層，可讓您建立適用於電子商務功能的AEM元件
seo-description: 整合架構包含具有API的整合層，可讓您建立適用於電子商務功能的AEM元件
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: d8ee3b57-633a-425e-bf36-646f0e0bad52
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16

---


# 開發（一般）{#developing-generic}

>[!NOTE]
>
>[另外也提供](/help/sites-developing/ecommerce.md#api-documentation) API檔案。

整合架構包含具有API的整合層。 這可讓您建立適用於電子商務功能的AEM元件（不受您的特定電子商務引擎影響）。 它也可讓您使用內部CRX資料庫，或插入電子商務系統，並將產品資料提取至AEM。

提供許多現成可用的AEM元件，以使用整合層。 目前有：

* 產品顯示元件
* 購物車
* 促銷和憑證
* 目錄和章節藍圖
* 結帳
* 搜尋

針對搜尋，提供整合掛接，可讓您使用AEM搜尋、協力廠商搜尋（例如Search&amp;Promote）或其組合。

## 電子商務引擎選擇 {#ecommerce-engine-selection}

電子商務架構可與任何電子商務解決方案搭配使用，所使用的引擎需由AEM識別——即使使用AEM一般引擎：

* 電子商務引擎是支援介面的OSGi服 `CommerceService` 務

   * 引擎可由服務屬性 `commerceProvider` 區分

* AEM支援 `Resource.adaptTo()` 與 `CommerceService``Product`

   * 實 `adaptTo` 施會在資源的 `cq:commerceProvider` 層次結構中查找屬性：

      * 如果找到，則使用該值來篩選商務服務查閱。
      * 如果找不到，則會使用排名最高的商務服務。
   * 使 `cq:Commerce` 用混合素，以便 `cq:commerceProvider` 將其添加到強型資源。


* 該 `cq:commerceProvider` 屬性也用於參考相應的商務工廠定義。

   * 例如，具 `cq:commerceProvider` 有值geometrixx的屬性會關聯至Day CQ Commerce Factory for Geometrixx-Outdoors **(** )的OSGi組態，其中`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`參數也有值 `commerceProvider``geometrixx`。
   * 您可在此處設定其他屬性（若適用且可用）。

在標準AEM安裝中，需要特定實作，例如：

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | geometrixx範例；這包括一般API的最低擴充功能 |

### 例如 {#example}

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
>使用CRXDE Lite，您就可以在AEM一般實作的產品元件中看到如何處理這些問題：
>
>`/apps/geometrixx-outdoors/components/product`

### 作業處理 {#session-handling}

儲存客戶購物車相關資訊的作業。

CommerceSession ****:

* 擁有購 **物車**

   * 執行添加／刪除／等
   * 對購物車執行各種計算；

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* 擁有訂單資 **料** :

   `CommerceSession.getUserContext()`

* 可使用 `updateOrder(Map<String, Object> delta)`
* 也擁有付款 **處理** 連線
* 也擁有履約 **連線** 。

### 建築 {#architecture}

#### 產品和變型的架構 {#architecture-of-product-and-variants}

單一產品可以有多種變化；例如，可能因顏色和／或大小而異。 產品必須定義哪些屬性驅動變化；我們用變 *型軸來定義*。

但是，並非所有屬性都是變型軸。 變化也會影響其他屬性；例如，價格可能取決於規模。 購物者無法選取這些屬性，因此不視為變型軸。

每個產品和／或變體都由資源表示，因此將1:1映射到儲存庫節點。 由此推論，特定產品和／或變體可以通過其路徑唯一標識。

任何產品資源都可以用 `Product API`。 產品API中的大部分呼叫都是變數特定的（雖然變數可能繼承祖先的共用值），但也有呼叫會列出變數集( `getVariantAxes()`、 `getVariants()`等等)。

>[!NOTE]
>
>實際上，變型軸由任何返回項 `Product.getVariantAxes()` 決定：
>
>* 對於一般實作，AEM會從產品資料中的屬性中讀取它( `cq:productVariantAxes`)
>
>
雖然產品（一般而言）可以有許多變型軸，但現成的產品元件只能處理兩個：
>
>1. `size`
   >
   >
1. 再加一個
   >   此額外變數是透過產品參 `variationAxis` 考的屬性選取(通常 `color` 適用於Geometrixx Outdoors)。
>



#### 產品參考與PIM資料 {#product-references-and-pim-data}

一般而言：

* PIM資料位於 `/etc`

* 產品參考 `/content`。

產品變化與產品資料節點之間必須有1:1的對應。

產品參考也必須為每個呈現的變化提供一個節點——但不需要顯示所有的變化。 例如，如果產品有S、M、L變數，則產品資料可能是：

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

雖然「高大」目錄可能只有：

```shell
content
  big-and-tall
    shirt
      shirt-l
```

最後，不需要使用產品資料。 您可以將所有產品資料放在目錄的參考之下；但是，若不複製所有產品資料，就無法真正擁有多個型錄。

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

#### com.adobe.cq.commerce.api.VariantFilter {#com-adobe-cq-commerce-api-variantfilter}

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

* **通用儲存機制**

   * 產品節點為nt:unstructured。
   * 產品節點可以是：

      * 參考，其中產品資料儲存在其他位置：

         * 產品參考包 `productData` 含屬性，其指向產品資料(通常在 `/etc/commerce/products`下)。
         * 產品資料是分層的；產品屬性繼承自產品資料節點的祖先。
         * 產品參考也可以包含局部屬性，這些屬性會覆寫其產品資料中指定的屬性。
      * 產品本身：

         * 沒有屬 `productData` 性。
         * 在本機保存所有屬性（且不包含productData屬性）的產品節點會直接從其祖先繼承產品屬性。


* **AEM-generic產品結構**

   * 每個變型都必須有自己的葉節點。
   * 產品介面既代表產品，也代表變型，但相關儲存庫節點是特定的。
   * 產品節點描述產品屬性和變型軸。

#### 例如 {#example-1}

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

#### 購物車的架構 {#architecture-of-the-shopping-cart}

**元件**

* 購物車歸 `CommerceSession:`

   * 執行 `CommerceSession` 添加、刪除等操作。
   * 此外 `CommerceSession` ，還會對購物車執行各種計算。
   * 此外， `CommerceSession` 還會套用已觸發至購物車的憑單和促銷。

* 雖然不直接與購物車相關，但 `CommerceSession` 必須提供目錄定價資訊（因為它擁有定價）

   * 定價可能有數種修飾詞：

      * 數量折扣。
      * 不同的貨幣。
      * 適用增值稅且免加值稅。
   * 這些修飾元是完全開放的，具有下列介面：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**儲存**

* 儲存

   * 在AEM-generic案例中，購物車儲存在 [ClientContext中](/help/sites-administering/client-context.md)

**個性化**

* 個人化應一律透過 [ClientContext推動](/help/sites-administering/client-context.md)。
* 購物車 `/version/` 的ClientContext會在所有情況下建立：

   * 應使用方法添加產 `CommerceSession.addCartEntry()` 品。

* 以下說明ClientContext購物車中購物車資訊的範例：

![chlimage_1-33](assets/chlimage_1-33a.png)

#### 結帳的架構 {#architecture-of-checkout}

**購物車和訂購資料**

The owns `CommerceSession` the three elements:

1. **購物車內容**

   購物車內容結構由API修正：

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **定價**

   API也會修正定價結構：

   ```java
       public String getCartPreTaxPrice();
       public String getCartTax();
       public String getCartTotalPrice();
       public String getOrderShipping();
       public String getOrderTotalTax();
       public String getOrderTotalPrice();
   ```

1. **訂單詳細資料**

   但是，訂單詳細資 *料* ,API並未修正：

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**發運計算**

* 訂單通常需要提供多種運送選項（和價格）。
* 價格可能根據訂單的項目和詳細資訊，例如重量和／或交貨地址。
* The `CommerceSession` has access to all the dependiences, so the it can as simaly as approduct pricing:

   * 該公司 `CommerceSession` 擁有運費定價。
   * 使用 `updateOrder(Map<String, Object> delta)` 擷取／更新傳送詳細資訊。

### 搜尋定義 {#search-definition}

遵循標準服務API模型，電子商務專案提供一組可由個別商務引擎實施的搜尋相關API。

>[!NOTE]
>
>目前，只有hybris引擎會立即建置搜尋API。
>
>不過，搜尋API是通用的，可由每個CommerceService個別實作。
>
>因此，雖然提供的通用實作現成不實作此API，但您可以擴充它並新增搜尋功能。

電子商務專案包含預設搜尋元件，位於：

`/libs/commerce/components/search`

![chlimage_1-34](assets/chlimage_1-34a.png)

這可使用搜尋API來查詢選取的商務引擎(請參閱 [電子商務引擎選擇](#ecommerce-engine-selection)):

#### 搜尋API {#search-api}

核心專案提供數個通用／輔助類別：

1. `CommerceQuery`

   用於描述搜索查詢（包含有關查詢文本、當前頁、頁面大小、排序和選定刻面的資訊）。 所有實作搜尋API的電子商務服務都會收到此類的例項，以執行其搜尋。 可 `CommerceQuery` 以從請求物件( `HttpServletRequest`)實例化。

1. `FacetParamHelper`

   是提供一種靜態方法的實用程式類 `toParams` 別——用於從刻面和一個切 `GET` 換的值清單中生成參數字串。 這在UI端很有用，您需要針對每個Facet的每個值顯示超連結，如此當使用者按一下超連結時，就會切換個別值（例如，如果選取該值，則會從查詢中移除，否則會新增）。 這會處理處理多／單值刻面、覆寫值等所有邏輯。

搜尋API的入口點是傳回 `CommerceService#search` 物件的方 `CommerceResult` 法。 如需此主題的詳細資訊，請參閱API檔案。

### 開發促銷和憑證 {#developing-promotions-and-vouchers}

* 憑單:

   * 優惠券是以頁面為基礎的元件，可透過網站主控台建立／編輯，並儲存於：

      `/content/campaigns`

   * 憑單供應：

      * 優惠券代碼（由購物者輸入到購物車中）。
      * 優惠券標籤（在購物者將其輸入購物車後顯示）。
      * 促銷路徑（用來定義憑證套用的動作）。
   * 憑單沒有自己的開／關日期／時間，但使用其父促銷活動。
   * 外部商務引擎也可以提供憑證；這些要求至少：

      * 優惠券代碼
      * 一種方 `isValid()` 法
   * 憑 **單元** ( `/libs/commerce/components/voucher`)提供：

      * 憑證管理的轉譯器；這會顯示購物車中目前的任何憑單。
      * 用於管理（添加／刪除）憑單的編輯對話框（表單）。
      * 在購物車中新增／移除憑單所需的動作。



* 促銷活動:

   * 促銷是以頁面為基礎的元件，使用網站主控台建立／編輯，並儲存在：

      `/content/campaigns`

   * 促銷提供：

      * 優先順序
      * 促銷處理常式路徑
   * 您可以將促銷活動連結至促銷活動，以定義其開／關日期／時間。
   * 您可以將促銷活動與體驗連結，以定義其細分。
   * 與體驗無關的促銷活動不會自行引發，但仍可以透過優惠券引發。
   * 升級元件( `/libs/commerce/components/promotion`)包含：

      * 促銷管理的轉譯者和對話方塊
      * 子元件，用於渲染和編輯特定於升級處理程式的配置參數
   * 兩個升級處理常式會從方塊中提供：

      * `DiscountPromotionHandler`，這套用整個購物車的絕對或百分比折扣
      * `PerfectPartnerPromotionHandler`，如果合作夥伴產品也在購物車中，則套用產品絕對或百分比折扣
   * ClientContext會解 `SegmentMgr` 析區段，而ClientContext會解 `CartMgr` 析促銷。 每個至少受限於一個已解決群體的促銷活動都會引發。

      * 引發的促銷活動會透過AJAX呼叫傳回伺服器，以重新計算購物車。
      * 引發的促銷活動（和新增的憑證）也會顯示在ClientContext面板中。




從購物車新增／移除優惠券是透過 `CommerceSession` API完成：

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

這樣，該代 `CommerceSession` 表負責檢查憑證是否存在以及是否可以套用。 這可能是針對只有在符合特定條件時才能使用的憑證；例如，當購物車總價格大於$100時)。 如果憑單因任何原因無法套用， `addVoucher` 方法會擲回例外。 此外， `CommerceSession` 在新增／移除優惠券後，還負責更新購物車的價格。

是 `Voucher` 一個類似Bean的類，包含以下欄位：

* 優惠券代碼
* 簡短說明
* 參考指示折扣類型和值的相關促銷

提供 `AbstractJcrCommerceSession` 的可以申請憑證。 類別傳回的憑單是 `getVouchers()` 包含jcr:content節 `cq:Page` 點的例項，其中包含下列屬性：

* `sling:resourceType` （字串）-這必須是 `commerce/components/voucher`

* `jcr:title` （字串）-用於優惠券的說明
* `code` （字串）-使用者必須輸入的代碼，才能套用此憑單
* `promotion` （字串）-要套用的促銷；例如， `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

促銷處理常式是可修改購物車的OSGi服務。 購物車將支援在介面中定義的數個勾 `PromotionHandler` 點。

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

3個升級處理常式現成可用：

* `DiscountPromotionHandler` 套用購物車的絕對或百分比折扣
* `PerfectPartnerPromotionHandler` 如果產品合作夥伴也在購物車中，則套用產品絕對或百分比折扣
* `FreeShippingPromotionHandler` 套用免運費

