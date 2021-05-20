---
title: 開發（一般）
seo-title: 開發（一般）
description: 整合架構包含具有API的整合層，可讓您建立AEM元件以利電子商務功能
seo-description: 整合架構包含具有API的整合層，可讓您建立AEM元件以利電子商務功能
uuid: 393bb28a-9744-44f4-9796-09228fcd466f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '1886'
ht-degree: 0%

---

# 開發（一般）{#developing-generic}

>[!NOTE]
>
>[也提](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 供API檔案。

整合架構包含具有API的整合層。 這可讓您建立AEM元件，以利使用電子商務功能（不受您特定電子商務引擎影響）。 它也可讓您使用內部CRX資料庫，或插入電子商務系統，並將產品資料提取至AEM。

提供許多現成可用的AEM元件以使用整合層。 目前包括：

* 產品顯示元件
* 購物車
* 促銷活動和憑單
* 目錄和章節藍圖
* 結帳
* 搜尋

為了搜尋，提供整合鈎點，可讓您使用AEM搜尋、第三方搜尋(類似Search&amp;Promote)或其組合。

## 電子商務引擎選擇{#ecommerce-engine-selection}

電子商務架構可與任何電子商務解決方案搭配使用，所使用的引擎需由AEM識別，即使使用AEM通用引擎亦然：

* 電子商務引擎是支援`CommerceService`介面的OSGi服務

   * 引擎可由`commerceProvider`服務屬性區分

* AEM支援`CommerceService`和`Product`的`Resource.adaptTo()`

   * `adaptTo`實作會在資源的階層中尋找`cq:commerceProvider`屬性：

      * 如果找到，則值會用來篩選商務服務查閱。
      * 若找不到，則會使用排名最高的商務服務。
   * 使用`cq:Commerce` mixin，可將`cq:commerceProvider`新增至強類型資源。


* `cq:commerceProvider`屬性還用於參考相應的商務工廠定義。

   * 例如，具有值geometrixx的`cq:commerceProvider`屬性將與&#x200B;**Day CQ Commerce Factory for Geometrixx-Outdoors**(`com.adobe.cq.commerce.hybris.impl.GeoCommerceServiceFactory`) — 其中參數`commerceProvider`也具有`geometrixx`值的OSGi設定相互關聯。
   * 此處可設定其他屬性（若適用且可用）。

在標準AEM安裝中，需要特定實作，例如：

|  |  |
|---|---|
| `cq:commerceProvider = geometrixx` | geometrixx範例；這包括一般API的最低擴充功能 |

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
>透過CRXDE Lite，您可以了解在AEM一般實作的產品元件中如何處理：
>
>`/apps/geometrixx-outdoors/components/product`

### 會話處理{#session-handling}

存放客戶購物車相關資訊的工作階段。

**CommerceSession**:

* 擁有&#x200B;**購物車**

   * 執行添加/刪除等
   * 對購物車執行各種計算；

      `commerceSession.getProductPriceInfo(Product product, Predicate filter)`

* 擁有&#x200B;**order**&#x200B;資料的持續性：

   `CommerceSession.getUserContext()`

* 可使用`updateOrder(Map<String, Object> delta)`擷取/更新傳送詳細資料
* 還擁有&#x200B;**payment**&#x200B;處理連接
* 還擁有&#x200B;**fulfillment**&#x200B;連接

### 架構 {#architecture}

#### 產品和變型的架構{#architecture-of-product-and-variants}

單一產品可能有多種變化；例如，可能會因顏色和/或大小而異。 產品必須定義驅動變化的屬性；我們將這些&#x200B;*變體軸*&#x200B;定義。

但是，並非所有屬性都是變型軸。 變化也會影響其他屬性；例如，價格可能取決於規模。 購物者無法選取這些屬性，因此不視為變型軸。

每個產品和/或變體都由資源表示，因此會將1:1對應至儲存庫節點。 由此推論，特定產品和/或變體可通過其路徑唯一標識。

任何產品資源都可以用`Product API`表示。 產品API中的大部分呼叫都是變異專用的（雖然變異可能繼承來自上階的共用值），但也有列出變異集（`getVariantAxes()`、`getVariants()`等）的呼叫。

>[!NOTE]
>
>實際上，變型軸由`Product.getVariantAxes()`返回的內容決定：
>
>* 針對一般實作AEM會從產品資料中的屬性讀取(`cq:productVariantAxes`)
>
>
雖然產品（一般）可以有許多變型軸，但現成可用的產品元件僅處理兩個：
>
>1. `size`
>1. 再加一個

>
>   
此附加變體是透過產品參考的`variationAxis`屬性選取的(對於Geometrixx Outdoors，通常為`color`)。

#### 產品參考和PIM資料{#product-references-and-pim-data}

一般而言：

* PIM資料位於`/etc`下

* `/content`下的產品參考。

產品變異和產品資料節點之間必須有1:1對應。

產品參考也必須為呈現的每個變異包含一個節點，但不需要呈現所有變異。 例如，如果產品有S、M、L變數，則產品資料可能是：

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

最後，不需要使用產品資料。 您可以將所有產品資料放在目錄中的參考下；但是，如果不複製所有產品資料，就無法真正擁有多個目錄。

**API**

#### com.adobe.cq.commerce.api.Product介面{#com-adobe-cq-commerce-api-product-interface}

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

* **一般儲存機制**

   * 產品節點不是非結構化的。
   * 產品節點可以是：

      * 參考，其中產品資料儲存在其他位置：

         * 產品參考包含`productData`屬性，指向產品資料（通常位於`/etc/commerce/products`下）。
         * 產品資料是分層的；產品屬性繼承自產品資料節點的祖先。
         * 產品參考也可包含本機屬性，這會覆寫其產品資料中指定的屬性。
      * 產品本身：

         * 沒有`productData`屬性。
         * 在本地保留所有屬性（且不包含productData屬性）的產品節點會直接從自己的祖先繼承產品屬性。


* **AEM — 一般產品結構**

   * 每個變體都必須有自己的葉節點。
   * 產品介面既代表產品和變體，也代表相關存放庫節點，但節點是特定的。
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

#### 購物車架構{#architecture-of-the-shopping-cart}

**元件**

* 購物車歸`CommerceSession:`所有

   * `CommerceSession`執行添加、刪除等操作。
   * `CommerceSession`也會對購物車執行各種計算。
   * `CommerceSession`也會套用已引發購物車的憑單和促銷活動。

* `CommerceSession`不直接與購物車相關，但還必須提供目錄定價資訊（因為它擁有定價）

   * 定價可能有幾個修改量：

      * 數量折扣。
      * 不同的貨幣。
      * 免增值稅和免增值稅。
   * 修飾元完全開放，介面如下：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**儲存**

* 儲存

   * 在AEM-generic案例中，購物車儲存在[ClientContext](/help/sites-administering/client-context.md)中

**個性化**

* 個人化應一律透過[ClientContext](/help/sites-administering/client-context.md)來驅動。
* 所有情況下，都會建立購物車的ClientContext`/version/`:

   * 應使用`CommerceSession.addCartEntry()`方法新增產品。

* 以下說明ClientContext車中的購物車資訊範例：

![chlimage_1-33](/help/sites-developing/assets/chlimage_1-33a.png)

#### 結帳架構{#architecture-of-checkout}

**購物車和訂購資料**

`CommerceSession`擁有三個元素：

1. **購物車內容**

   購物車內容結構已由API修正：

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

   不過，訂單詳細資料是由API修正的&#x200B;*not*:

   ```java
       public void updateOrderDetails(Map<String, String> orderDetails);
       public Map<String, String> getOrderDetails();
       public void submitOrder();
   ```

**運費計算**

* 訂單通常需要提供多種運送選項（和價格）。
* 價格可能基於訂單的項目和詳細資訊，例如重量和/或交貨地址。
* `CommerceSession`可存取所有相依性，因此可以以與產品定價類似的方式處理：

   * `CommerceSession`擁有運費定價。
   * 使用`updateOrder(Map<String, Object> delta)`來擷取/更新傳送詳細資料。

### 搜索定義{#search-definition}

遵循標準服務API模型，電子商務專案提供一組可由個別商務引擎實作的搜尋相關API。

>[!NOTE]
>
>目前，只有hybris引擎會立即實作搜尋API。
>
>不過，搜尋API是通用的，可由每個CommerceService個別實作。
>
>因此，雖然提供的現成通用實作不會實作此API，但您可以擴充它，並新增搜尋功能。

電子商務項目包含預設搜索元件，位於：

`/libs/commerce/components/search`

![chlimage_1-34](/help/sites-developing/assets/chlimage_1-34a.png)

這利用搜尋API來查詢選取的商務引擎（請參閱[電子商務引擎選取項目](#ecommerce-engine-selection)）:

#### 搜尋API {#search-api}

核心專案提供數個一般/協助程式類別：

1. `CommerceQuery`

   用於描述搜索查詢（包含有關查詢文本、當前頁、頁面大小、排序和選定刻面的資訊）。 所有實作搜尋API的電子商務服務都會收到此類別的例項，以執行其搜尋。 可以從請求物件(`HttpServletRequest`)實例化`CommerceQuery`。

1. `FacetParamHelper`

   是實用程式類，提供一種靜態方法 — `toParams` -，用於從Facet清單和一個切換的值生成`GET`參數字串。 這在UI端很實用，您需要針對每個面向的每個值顯示超連結，這樣當使用者點按超連結時，就會切換個別值（亦即，如果選取了該值，則會從查詢中移除，否則會新增）。 這會處理處理多/單值Facet、覆寫值等的所有邏輯。

搜尋API的入口點是傳回`CommerceResult`物件的`CommerceService#search`方法。 如需本主題的詳細資訊，請參閱API檔案。

### 開發促銷和憑單{#developing-promotions-and-vouchers}

* 憑單:

   * 憑單是以頁面為基礎的元件，使用網站控制台建立/編輯，並儲存在以下位置：

      `/content/campaigns`

   * 憑單供應：

      * 憑單代碼（由購物者輸入購物車）。
      * 憑單標籤（在購物者將其輸入購物車後顯示）。
      * 促銷路徑（定義憑證套用的動作）。
   * 憑單沒有自己的開啟和關閉日期/時間，而是使用其父促銷活動的憑證。
   * 外部商務引擎也可以提供憑單；這些要求至少：

      * 憑單代碼
      * `isValid()`方法
   * **憑證**&#x200B;元件(`/libs/commerce/components/voucher`)提供：

      * 憑證管理的轉譯者；這顯示當前購物車中的任何憑單。
      * 用於管理（添加/刪除）憑證的編輯對話框（表單）。
      * 向購物車添加/從購物車中刪除憑單所需的操作。



* 促銷活動:

   * 促銷活動是以頁面為基礎的元件，會透過網站主控台建立/編輯，並儲存於下列位置：

      `/content/campaigns`

   * 促銷活動提供：

      * 優先順序
      * 升級處理程式路徑
   * 您可以將促銷活動連結至促銷活動，以定義其開啟/關閉日期/時間。
   * 您可以將促銷活動連結至體驗，以定義其區段。
   * 未與體驗連結的促銷活動不會自行引發，但仍可由憑單引發。
   * 升級元件(`/libs/commerce/components/promotion`)包含：

      * 促銷管理的推薦者和對話
      * 用於呈現和編輯升級處理程式專用的配置參數的子元件
   * 提供兩個升級處理程式：

      * `DiscountPromotionHandler`，此變數會套用購物車範圍的絕對或百分比折扣
      * `PerfectPartnerPromotionHandler`，如果合作夥伴產品也在購物車中，則會套用產品絕對或百分比折扣
   * ClientContext`SegmentMgr`解析區段，ClientContext`CartMgr`解析促銷活動。 每個至少會觸發一個已解析區段的促銷活動。

      * 引發的促銷活動會透過AJAX呼叫傳回至伺服器，以重新計算購物車。
      * 「引發的促銷活動」（和新增的憑單）也會顯示在「ClientContext」面板中。




通過`CommerceSession` API可以添加/刪除購物車中的憑單：

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

這樣，`CommerceSession`將負責檢查憑證是否存在以及是否可應用。 這可能適用於只有在滿足特定條件時才可應用的憑證；例如，當購物車總價大於$100時)。 如果憑證因任何原因無法應用，`addVoucher`方法將引發異常。 此外，`CommerceSession`還負責在添加/刪除憑單後更新購物車的價格。

`Voucher`是類似Bean的類，包含以下項的欄位：

* 憑單代碼
* 簡短說明
* 參考指示折扣類型和值的相關促銷

提供的`AbstractJcrCommerceSession`可以使用憑單。 類`getVouchers()`返回的憑單是`cq:Page`包含jcr:content節點的實例，該節點具有以下屬性（其中包括）:

* `sling:resourceType` （字串） — 這必須  `commerce/components/voucher`

* `jcr:title` （字串） — 憑證說明
* `code` （字串） — 用戶必須輸入的代碼，才能應用此憑證
* `promotion` （字串） — 要套用的促銷活動；例如  `/content/campaigns/geometrixx-outdoors/article/10-bucks-off`

促銷活動處理常式是可修改購物車的OSGi服務。 購物車將支援將在`PromotionHandler`介面中定義的多個鈎點。

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

提供三個升級處理程式：

* `DiscountPromotionHandler` 套用購物車範圍絕對或百分比折扣
* `PerfectPartnerPromotionHandler` 如果產品合作夥伴也在購物車中，則套用產品絕對或百分比折扣
* `FreeShippingPromotionHandler` 適用免運費
