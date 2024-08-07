---
title: 開發（一般）
description: 整合架構包含具有API的整合層，可讓您為電子商務功能建立AEM元件。
contentOwner: Guillaume Carlino
exl-id: 1138a548-d112-4446-b0e1-b7a9ea7c7604
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 0%

---

# 開發（一般）{#developing-generic}

>[!NOTE]
>
>[API檔案](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation)也可供使用。

整合架構包含具有API的整合層。 這可讓您建置電子商務功能的AEM元件（不受特定電子商務引擎影響）。 它也可讓您使用內部CRX資料庫或插入電子商務系統，並將產品資料提取到AEM中。

提供幾個現成的AEM元件，以供使用整合層。 目前包括：

* 產品顯示元件
* 購物車
* 促銷活動和憑單
* 目錄和章節藍圖
* 結帳
* 搜尋

針對搜尋，整合勾點可讓您使用Adobe Experience Manager (AEM)搜尋、協力廠商搜尋或其組合。

## 電子商務引擎選擇 {#ecommerce-engine-selection}

電子商務架構可搭配任何電子商務解決方案使用，使用的引擎必須由AEM識別 — 即使使用AEM通用引擎亦然：

* 電子商務引擎是支援`CommerceService`介面的OSGi服務

   * 引擎可由`commerceProvider`服務屬性區分

* AEM支援`CommerceService`和`Product`的`Resource.adaptTo()`

   * `adaptTo`實作會在資源的階層中尋找`cq:commerceProvider`屬性：

      * 如果找到，則會使用值來篩選商務服務查閱。
      * 如果找不到，則會使用排名最高的商務服務。

   * 已使用`cq:Commerce` mixin，以便將`cq:commerceProvider`新增到強型別資源。

* `cq:commerceProvider`屬性也用來參考適當的商務工廠定義。

   * 例如，值為Geometrixx的`cq:commerceProvider`屬性與&#x200B;**Day CQ Commerce Factory for Geometrixx-Outdoors** (`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`)的OSGi設定相關，其中引數`commerceProvider`也具有值`geometrixx`。
   * 您可以在此處設定其他屬性（若適當且可提供）。

在標準AEM安裝中，需要特定實施，例如：

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | geometrixx範例；這包含一般API的最低擴充功能 |

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
>您可以使用CRXDE Lite檢視這在AEM一般實作的產品元件中受到如何處理的問題：
>
>`/apps/geometrixx-outdoors/components/product`

### 工作階段處理 {#session-handling}

儲存與客戶購物車相關資訊的工作階段。

**CommerceSession**：

* 擁有&#x200B;**購物車**

   * 執行新增/移除/等
   * 在購物車上執行各種計算；

     `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* 擁有&#x200B;**訂單**&#x200B;資料的持續性：

  `CommerceSession.getUserContext()`

* 可使用`updateOrder(Map<String, Object> delta)`擷取/更新傳遞詳細資料
* 擁有&#x200B;**付款**&#x200B;處理連線
* 擁有&#x200B;**履行**&#x200B;連線

### 架構 {#architecture}

#### 產品和變體的架構 {#architecture-of-product-and-variants}

單一產品可以有多個變數，例如可能因顏色和/或大小而異。 產品必須定義哪些屬性會驅動變化；Adobe字詞這些&#x200B;*變化軸*。

不過，並非所有屬性都是變數軸。 變化也可能會影響其他屬性；例如，價格可能取決於大小。 購物者無法選取這些屬性，因此不會視為變數軸。

每個產品和/或變體由資源表示，因此將1:1對應到存放庫節點。 必然結果是，特定產品和/或變體可由其路徑唯一識別。

任何產品資源都可以以`Product API`表示。 產品API中的大部分呼叫都是變動專用（雖然變動可能會繼承來自上階的共用值），但也有列出變動集（`getVariantAxes()`、`getVariants()`等）的呼叫。

>[!NOTE]
>
>實際上，變數座標軸是由`Product.getVariantAxes()`傳回的任何專案所決定：
>
>* 對於一般實作，AEM會從產品資料( `cq:productVariantAxes`)中的屬性讀取它
>
>雖然產品（一般）可以有許多變體軸，但現成可用的產品元件僅處理兩個變體：
>
>1. `size`
>1. 再加一個
>
>   此額外變體是透過產品參考的`variationAxis`屬性選取的(Geometrixx Outdoors通常為`color`)。

#### 產品參考與PIM資料 {#product-references-and-pim-data}

一般而言：

* PIM資料位於`/etc`下

* `/content`下的產品參考。

產品變數和產品資料節點之間必須是1:1對應。

產品參考也必須針對呈現的每個變數有一個節點，但不需要呈現所有變數。 例如，如果產品有S、M、L等變數，則產品資料可能是：

```shell
etc
  commerce
    products
      shirt
        shirt-s
        shirt-m
        shirt-l
```

雖然「大而高」目錄可能只有：

```shell
content
  big-and-tall
    shirt
      shirt-l
```

最後，不需要使用產品資料。 您可以將所有產品資料放置在目錄中的參照下；但這樣一來，您就無法在不複製所有產品資料的情況下擁有多個目錄。

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
 * for example, when using {@link Product#getVariants(VariantFilter filter)}.
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

* **一般儲存機制**

   * 產品節點nt：unstructured。
   * 產品節點可以是：

      * 具有儲存在其他位置的產品資料的參考：

         * 產品參考包含`productData`屬性，指向產品資料（通常在`/etc/commerce/products`下）。
         * 產品資料為階層式；產品屬性繼承自產品資料節點的祖先。
         * 產品參考也可以包含本機屬性，這些屬性會覆寫產品資料中指定的屬性。

      * 產品本身：

         * 沒有`productData`屬性。
         * 在本機持有所有屬性（且不包含productData屬性）的產品節點，會直接從自己的祖先繼承產品屬性。

* **AEM-generic產品結構**

   * 每個變體都必須有自己的葉節點。
   * 產品介面同時代表產品與變體，但相關的存放庫節點會針對具體專案而有所不同。
   * product節點會說明產品屬性和變體軸。

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

#### 購物車的架構 {#architecture-of-the-shopping-cart}

**元件**

* 購物車屬於`CommerceSession:`

   * `CommerceSession`執行新增、移除等動作。
   * `CommerceSession`也會在購物車上執行各種計算。
   * `CommerceSession`也會套用已引發購物車的憑單和促銷活動。

* 雖然不直接與購物車相關，但`CommerceSession`也必須提供目錄定價資訊（因為它擁有定價）

   * 訂價可能有數個修正因子：

      * 數量折扣。
      * 不同的貨幣。
      * 應付VAT且免付VAT。

   * 修飾詞使用以下介面為開放式：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`

**儲存空間**

* 儲存空間

   * 在AEM一般案例中，購物車儲存在[ClientContext](/help/sites-administering/client-context.md)中

**Personalization**

* 一律透過[ClientContext](/help/sites-administering/client-context.md)推動個人化。
* 在所有情況下都會建立購物車的ClientContext`/version/`：

   * 應該使用`CommerceSession.addCartEntry()`方法來新增產品。

* 以下說明ClientContext購物車中的購物車資訊範例：

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### 結帳架構 {#architecture-of-checkout}

**購物車與訂單資料**

`CommerceSession`擁有三個元素：

1. **購物車內容**

   購物車內容結構已由API修正：

   ```java
       public void addCartEntry(Product product, int quantity);
       public void modifyCartEntry(int entryNumber, int quantity);
       public void deleteCartEntry(int entryNumber);
   ```

1. **定價**

   API也會修正此定價結構：

   ```java
       public String getCartPreTaxPrice();
       public String getCartTax();
       public String getCartTotalPrice();
       public String getOrderShipping();
       public String getOrderTotalTax();
       public String getOrderTotalPrice();
   ```

1. **訂單詳細資料**

   但是，訂單詳細資料&#x200B;*不是*&#x200B;由API修正：

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**送貨計算**

* 訂購單通常必須提供多種送貨選項（和價格）。
* 價格可能會以訂單的專案和詳細資訊為依據，例如重量和/或交貨地址。
* `CommerceSession`具有所有相依性的存取權，因此可將其視為類似產品定價的方式：

   * `CommerceSession`擁有送貨定價。
   * 使用`updateOrder(Map<String, Object> delta)`擷取/更新傳遞詳細資料。

### 搜尋定義 {#search-definition}

遵循標準服務API模型，電子商務專案提供一組可由個別商務引擎實作的搜尋相關API。

>[!NOTE]
>
>目前，只有Hybris引擎會實作立即可用的Search API。
>
>不過，搜尋API是通用的，可由每個CommerceService個別實作。
>
>因此，雖然提供的現成通用實作不會實作此API，但您可以擴充此API並新增搜尋功能。

電子商務專案包含中的預設搜尋元件：

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

這會使用搜尋API來查詢選取的商務引擎（請參閱[電子商務引擎選擇](#ecommerce-engine-selection)）：

#### 搜尋API {#search-api}

核心專案提供了幾個通用/協助程式類別：

1. `CommerceQuery`

   用於描述搜尋查詢（包含有關查詢文字、目前頁面、頁面大小、排序和所選多面的資訊）。 所有實作搜尋API的電子商務服務都會收到此類別的執行個體，以執行其搜尋。 可從要求物件( `HttpServletRequest`)具現化`CommerceQuery`。

1. `FacetParamHelper`

   是一個公用程式類別，它提供一個靜態方法 — `toParams` — 用來從Facet清單和一個切換值產生`GET`引數字串。 這在UI端相當實用，您需要顯示每個Facet之每個值的超連結，如此當使用者按一下超連結時，就會切換個別值。 也就是說，如果選取它，它會從查詢中移除，否則會新增。 這會負責處理多個/單一值Facet、覆寫值等作業的所有邏輯。

搜尋API的進入點是傳回`CommerceResult`物件的`CommerceService#search`方法。 請參閱API檔案，以取得有關本主題的詳細資訊。

### 開發促銷活動和憑單 {#developing-promotions-and-vouchers}

* 憑單：

   * 憑單是使用Websites主控台建立/編輯並儲存在下的頁面型元件：

     `/content/campaigns`

   * 憑單供給：

      * 憑單代碼（由購物者輸入購物車中）。
      * 憑單標籤（購物者將其輸入購物車後顯示）。
      * 促銷活動路徑（定義憑單套用的動作）。

   * 憑單沒有自己的開啟和結束日期/時間，但會使用父行銷活動的日期/時間。
   * 外部商務引擎也可以提供憑單；這些至少需要：

      * 憑單代碼
      * `isValid()`方法

   * **憑單**&#x200B;元件( `/libs/commerce/components/voucher`)提供：

      * 憑單管理的轉譯器；這會顯示目前購物車中的任何憑單。
      * 用於管理（新增/移除）憑單的編輯對話方塊（表單）。
      * 在購物車中新增/移除憑單所需的動作。

* 促銷活動：

   * 促銷活動是使用Websites主控台建立/編輯的頁面型元件，並儲存在下列位置：

     `/content/campaigns`

   * 促銷供應：

      * 優先順序
      * 推進處理常式路徑

   * 您可以將促銷活動連結至促銷活動，以定義其開啟/關閉日期/時間。
   * 您可以將促銷活動連結至體驗，以定義其區段。
   * 未連線至體驗的促銷活動不會自行引發，但仍可由憑單引發。
   * Promotion元件( `/libs/commerce/components/promotion`)包含：

      * 推進管理的轉譯器和對話方塊
      * 用於呈現和編輯升級處理常式專屬之組態引數的子元件

   * 現成提供兩個提升處理常式：

      * `DiscountPromotionHandler`，適用於整個購物車的絕對折扣或百分比折扣
      * `PerfectPartnerPromotionHandler`，如果合作夥伴產品也在購物車中，則套用產品絕對折扣或百分比折扣

   * ClientContext`SegmentMgr`會解析區段，而ClientContext`CartMgr`會解析促銷活動。 至少會引發一個已解析區段的促銷活動。

      * 已引發的促銷活動會透過AJAX呼叫傳回至伺服器，以重新計算購物車。
      * 已引發的促銷活動（以及新增的憑單）也會顯示在「ClientContext」面板中。

新增/移除購物車的憑單是透過`CommerceSession` API完成：

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

如此一來，`CommerceSession`便負責檢查憑單是否存在，以及憑單是否可以套用。 這可能適用於只有在符合特定條件時才能套用的憑單。 例如，當購物車總價大於$100時。 如果由於任何原因無法套用憑單，`addVoucher`方法會擲回例外狀況。 此外，新增/移除憑單後，`CommerceSession`負責更新購物車的價格。

`Voucher`是Bean型類別，包含下列欄位：

* 憑單代碼
* 簡短說明
* 參考指出折扣型態與值的相關促銷

提供的`AbstractJcrCommerceSession`可以套用憑單。 類別`getVouchers()`傳回的憑單是`cq:Page`的執行個體，包含具有下列屬性（等等）的jcr：content節點：

* `sling:resourceType` （字串） — 這必須是`commerce/components/voucher`

* `jcr:title` （字串） — 憑單說明
* `code` （字串） — 使用者必須輸入以套用此憑單的代碼
* `promotion` （字串） — 要套用的促銷活動；例如，`/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

促銷活動處理常式是修改購物車的OSGi服務。 購物車支援`PromotionHandler`介面中定義的數個勾點。

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

提供三個立即可用的促銷活動處理常式：

* `DiscountPromotionHandler`套用購物車範圍的絕對或百分比折扣
* 如果產品合作夥伴也在購物車中，`PerfectPartnerPromotionHandler`會套用產品絕對折扣或百分比折扣
* `FreeShippingPromotionHandler`套用免運費
