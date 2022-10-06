---
title: 使用SAP開發Commerce Cloud
seo-title: Developing with SAP Commerce Cloud
description: SAPCommerce Cloud整合框架包括一個與API的整合層
seo-description: The SAP Commerce Cloud integration framework includes an integration layer with an API
uuid: a780dd17-027a-4a61-af8f-3e2f600524c7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: b3de1a4a-f334-44bd-addc-463433204c99
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '2308'
ht-degree: 0%

---

# 使用SAP開發Commerce Cloud {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>電子商務架構可與任何電子商務解決方案搭配使用。 此處處理的某些細節和範例將參閱 [hybris](https://www.hybris.com/) 解決方案。

整合架構包含具有API的整合層。 這可讓您：

* 插入電子商務系統，並將產品資料提取至AEM

* 針對商務功能建立AEM元件，不受特定電子商務引擎影響

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[API檔案](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 也可用。

提供許多現成可用的AEM元件以使用整合層。 目前包括：

* 產品顯示元件
* 購物車
* 結帳

為了搜索，提供了一個整合鈎子，該整合鈎子允許您使用AEM搜索、電子商務系統的搜索、第三方搜索或其組合。

## 電子商務引擎選擇 {#ecommerce-engine-selection}

電子商務架構可與任何電子商務解決方案搭配使用，所使用的引擎需由AEM識別：

* 電子商務引擎是支援 `CommerceService` 介面

   * 引擎可由 `commerceProvider` 服務屬性

* AEM支援 `Resource.adaptTo()` for `CommerceService` 和 `Product`

   * 此 `adaptTo` 實作尋找 `cq:commerceProvider` 資源階層中的屬性：

      * 如果找到，則值會用來篩選商務服務查閱。

      * 若找不到，則會使用排名最高的商務服務。
   * A `cq:Commerce` mixin被使用， `cq:commerceProvider` 可新增至強制類型資源。


* 此 `cq:commerceProvider` 屬性也用於參考適當的商務工廠定義。

   * 例如， `cq:commerceProvider` 具有值的屬性 `hybris` 會關聯至 **Hybris的Day CQ Commerce Factory** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory) — 其中參數 `commerceProvider` 也有值 `hybris`.

   * 此處提供其他屬性，例如 **目錄版本** 可設定（若適當且可用）。

請參閱下列範例：

| `cq:commerceProvider = geometrixx` | 在標準AEM安裝中，需要特定實作；例如geometrixx範例，其中包含一般API的最低擴充功能 |
|--- |--- |
| `cq:commerceProvider = hybris` | hybris實作 |

### 範例 {#example}

```shell
/content/store
+ cq:commerceProvider = hybris
  + mens
    + polo-shirt-1
    + polo-shirt-2
    + employee
+ cq:commerceProvider = jcr
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
>透過CRXDE Lite，您可以了解在hybris實作的產品元件中如何處理：
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### 為hybris 4開發 {#developing-for-hybris}

已更新電子商務整合架構的hybris擴充功能，以支援Hybris 5，同時維持與Hybris 4的向後相容性。

針對Hybris 5調整程式碼中的預設設定。

若要針對Hybris 4開發，需具備下列條件：

* 調用maven時，將以下命令行參數添加到命令中

   `-P hybris4`

   它會下載預先設定的Hybris 4發佈，並內嵌在套件中 `cq-commerce-hybris-server`.

* 在OSGi配置管理器中：

   * 停用預設回應剖析器服務的Hybris 5支援。

   * 請確定Hybris Basic Authentication Handler服務的服務排名低於Hybris OAuth Handler服務。

### 工作階段處理 {#session-handling}

hybris使用使用者工作階段來儲存資訊，例如客戶的購物車。 工作階段ID會從 `JSESSIONID` 後續對hybris提出請求時需要傳送的cookie。 為了避免將工作階段ID儲存在存放庫中，會將其編碼至儲存在購物者瀏覽器中的其他Cookie中。 會執行下列步驟：

* 在第一個請求時，不會對購物者的請求設定Cookie;因此，會傳送要求至hybris例項以建立工作階段。

* 工作階段Cookie會從回應中擷取，並以新Cookie編碼(例如 `hybris-session-rest`)，並設定在對購物者的回應上。 新Cookie中的編碼為必要，因為原始Cookie僅對特定路徑有效，且在後續請求中不會從瀏覽器傳回。 路徑資訊也必須新增至Cookie的值。

* 在後續的請求中，會從 `hybris-session-<*xxx*>` Cookie和設定於HTTP用戶端上，用於從hybris要求資料。

>[!NOTE]
>
>當原始會話不再有效時，將建立新的匿名會話。

#### 商務會話 {#commercesession}

* 此工作階段「擁有」 **購物車**

   * 執行添加/刪除等

   * 對購物車執行各種計算；

      `commerceSession.getProductPrice(Product product)`

* 擁有 *儲存位置* 針對 **訂購** 資料

   `CommerceSession.getUserContext()`

* 也擁有 **付款** 處理連線

* 也擁有 **履行** 連接

### 產品同步與發佈 {#product-synchronization-and-publishing}

以hybris維護的產品資料必須可在AEM中使用。 已實施下列機制：

* hybris會以動態消息的形式提供ID的初始載入。 此摘要可能有更新。
* hybris將透過摘要(AEM輪詢)提供更新資訊。
* AEM使用產品資料時，會將要求傳回至目前資料的hybris（使用上次修改日期的條件式取得要求）。
* 在Hybris上，可以宣告性方式指定摘要內容。
* 將摘要結構對應至AEM內容模型會在AEM端的摘要適配器中發生。

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* 匯入工具(b)用於目錄中AEM的頁面樹結構初始設定。
* hybris中的目錄變更會透過摘要指示給AEM，然後會傳播至AEM(b)

   * 針對目錄版本新增/刪除/變更產品。

   * 產品已核准。

* hybris擴充功能提供輪詢匯入工具（「hybris」配置」），此配置可設定為以指定的間隔將變更匯入AEM(例如，每24小時指定間隔（以秒為單位）:

   ```JavaScript
       http://localhost:4502/content/geometrixx-outdoors/en_US/jcr:content.json
        {
        * "jcr:mixinTypes": ["cq:PollConfig"],
        * "enabled": true,
        * "source": "hybris:outdoors",
        * "jcr:primaryType": "cq:PageContent",
        * "interval": 86400
        }
   ```

* AEM中的目錄設定可辨識 **已轉移** 和 **線上** 目錄版本。

* 在目錄版本之間同步產品時，需要（取消）啟動對應的AEM頁面(a、c)

   * 將產品新增至 **線上** 目錄版本需要啟動產品的頁面。

   * 移除產品需要停用。

* 在AEM(c)中啟動頁面需要檢查(b)，且只有在

   * 產品位於 **線上** 產品頁面的目錄版本。

   * 參考的產品可在 **線上** 其他頁面（例如促銷活動頁面）的目錄版本。

* 已啟動的產品頁面需要存取產品資料的 **線上** 版本(d)。

* AEM發佈例項需要存取hybris以擷取產品和個人化資料(d)。

### 架構 {#architecture}

#### 產品和變體的架構 {#architecture-of-product-and-variants}

單一產品可能有多種變化；例如，可能會因顏色和/或大小而異。 產品必須定義驅動變化的屬性；我們稱這些 *變型軸*.

但是，並非所有屬性都是變型軸。 變化也會影響其他屬性；例如，價格可能取決於規模。 購物者無法選取這些屬性，因此不視為變型軸。

每個產品和/或變體都由資源表示，因此會將1:1對應至儲存庫節點。 由此推論，特定產品和/或變體可通過其路徑唯一標識。

產品/變型資源不一定會保留實際產品資料。它可能是實際保留在其他系統（例如hybris）上的資料的表示。 例如，產品說明、定價等不會儲存在AEM中，而是從電子商務引擎即時擷取。

任何產品資源都可以由 `Product API`. 產品API中的大部分呼叫都是變異專屬的（雖然變異可能繼承來自上階的共用值），但也有會列出變異集( `getVariantAxes()`, `getVariants()`等)。

>[!NOTE]
>
>實際上，變型軸由任何 `Product.getVariantAxes()` 傳回：
>* hybris會為hybris實作定義
>
>雖然產品（一般）可以有許多變型軸，但現成可用的產品元件僅處理兩個：
>
>1. `size`
>
>1. 再加一個

>
>此額外變體是透過 `variationAxis` 產品參考的屬性(通常 `color` (適用於Geometrixx Outdoors)。

#### 產品參考資料和產品資料 {#product-references-and-product-data}

一般而言：

* 產品資料位於 `/etc`

* 和產品參考 `/content`.

產品變異和產品資料節點之間必須有1:1對應。

產品參考也必須為呈現的每個變異包含一個節點，但不需要呈現所有變異。 例如，如果產品有S、M、L變數，則產品資料可能是：

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

雖然「大而高」目錄可能只有：

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
```

最後，不需要使用產品資料。 您可以將所有產品資料放在目錄中的參考下；但是，如果不複製所有產品資料，就無法真正擁有多個目錄。

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

* **一般儲存機制**

   * 產品節點包括 `nt:unstructured`.

   * 產品節點可以是：

      * 參考，其中產品資料儲存在其他位置：

         * 產品參考包含 `productData` 屬性，指向產品資料(通常位於 `/etc/commerce/products`)。

         * 產品資料是分層的；產品屬性繼承自產品資料節點的祖先。

         * 產品參考也可包含本機屬性，這會覆寫其產品資料中指定的屬性。
      * 產品本身：

         * 沒有 `productData` 屬性。

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

#### 購物車架構 {#architecture-of-the-shopping-cart}

**元件**

* 購物車歸 `CommerceSession:`

   * 此 `CommerceSession` 執行添加/刪除等操作。
   * 此 `CommerceSession` 也會對購物車執行各種計算。&quot;

* 雖然與購物車不直接相關，但 `CommerceSession` 還必須提供目錄定價資訊（因為它擁有定價資訊）

   * 定價可能有幾個修改量：

      * 數量折扣。
      * 不同的貨幣。
      * 免增值稅和免增值稅。
   * 修飾元完全開放，介面如下：

      * `int CommerceSession.getQuantityBreakpoints(Product product)`
      * `String CommerceSession.getProductPrice(Product product)`


**儲存空間**

* 儲存空間

   * 在hybris案例中， hybris伺服器擁有購物車。
   * 在AEM-generic案例中，購物車儲存在 [ClientContext](/help/sites-administering/client-context.md).

**個人化**

* 個人化應一律透過 [ClientContext](/help/sites-administering/client-context.md).
* ClientContext `/version/` 的購物車（在所有情況下）:

   * 應使用 `CommerceSession.addCartEntry()` 方法。

* 以下說明ClientContext車中的購物車資訊範例：

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### 結帳架構 {#architecture-of-checkout}

**購物車和訂購資料**

此 `CommerceSession` 擁有三個元素：

1. 購物車內容
1. 定價
1. 訂單詳細資訊

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

   不過，訂單詳細資料包括 *not* 由API修正：

   ```java
   public void updateOrderDetails(Map<String, String> orderDetails);
   public Map<String, String> getOrderDetails();
   public void submitOrder();
   ```

**運費計算**

* 訂單通常需要提供多種運送選項（和價格）。
* 價格可能基於訂單的項目和詳細資訊，例如重量和/或交貨地址。
* 此 `CommerceSession` 可存取所有相依性，因此能以與產品定價類似的方式處理：

   * 此 `CommerceSession` 擁有運價。
   * 可使用 `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>您可以實作運送選擇器；例如：
>
>`yourProject/commerce/components/shippingpicker`:
>
>* 本質上，這可能是 `foundation/components/form/radio`，但回呼 `CommerceSession` 適用於：
>
>* 檢查方法是否可用
>* 添加定價資訊
>* 讓購物者能夠更新AEM中的訂單頁面（包括運送方法的超集和說明它們的文字），同時仍具有公開相關內容的控制權 `CommerceSession` 資訊。


**付款處理**

* 此 `CommerceSession` 也擁有支付處理連接。

* 實施者需要將特定呼叫（至其選擇的付款處理服務）新增至 `CommerceSession` 實作。

**訂單履行**

* 此 `CommerceSession` 還擁有履行連接。
* 實施者需要將特定呼叫（至其選擇的付款處理服務）新增至 `CommerceSession` 實作。

### 搜尋定義 {#search-definition}

遵循標準服務API模型，電子商務專案提供一組可由個別商務引擎實作的搜尋相關API。

>[!NOTE]
>
>目前，只有hybris引擎會立即實作搜尋API。
>
>不過，搜尋API是通用的，可由每個CommerceService個別實作。

電子商務項目包含預設搜索元件，位於：

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

這可利用搜尋API來查詢選取的商務引擎(請參閱 [電子商務引擎選擇](#ecommerce-engine-selection)):

#### 搜尋API {#search-api}

核心專案提供數個一般/協助程式類別：

1. `CommerceQuery`

   用於描述搜索查詢（包含有關查詢文本、當前頁、頁面大小、排序和選定刻面的資訊）。 所有實作搜尋API的電子商務服務都會收到此類別的例項，以執行其搜尋。 A `CommerceQuery` 可從要求物件實例化( `HttpServletRequest`)。

1. `FacetParamHelper`

   是提供一種靜態方法的實用程式類 —  `toParams`  — 用於產生 `GET` 來自facet清單和一個切換值的參數字串。 這在UI端很實用，您需要針對每個面向的每個值顯示超連結，這樣當使用者點按超連結時，就會切換個別值（亦即，如果選取了該值，則會從查詢中移除，否則會新增）。 這會處理處理多/單值Facet、覆寫值等的所有邏輯。

搜尋API的入口點為 `CommerceService#search` 返回 `CommerceResult` 物件。 請參閱 [API檔案](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 以取得此主題的詳細資訊。

### 使用者整合 {#user-integration}

AEM與各種電子商務系統之間提供整合。 這需要一種策略來同步不同系統之間的購物者，讓AEM專屬的程式碼只需知道AEM，反之亦然：

* 驗證

   AEM假設為 *僅限* Web前端，因此執行 *all* 驗證。

* Hybris帳戶

   AEM會為每個購物者以hybris建立對應（從屬）帳戶。 此帳戶的使用者名稱與AEM使用者名稱相同。 會自動產生密碼隨機密碼並儲存（加密）至AEM。

#### 預先存在的使用者 {#pre-existing-users}

AEM前端可位於現有Hybris實作之前。 您也可以將hybris引擎新增至現有的AEM安裝。 要執行此操作，系統必須能夠正常處理任一系統中的現有用戶：

* AEM -> hybris

   * 登入hybris時，如果AEM使用者尚未存在：

      * 使用密碼隨機密碼建立新的hybris使用者
      * 將hybris使用者名稱儲存在AEM使用者的使用者目錄中
   * 請參閱: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`


* hybris -> AEM

   * 登入AEM時，如果系統辨識到使用者：

      * 嘗試使用提供的用戶名/pwd登錄hybris
      * 如果成功，請在AEM中使用相同密碼建立新使用者(AEM專屬的salt會產生AEM專屬的雜湊)
   * 以上演算法是在Sling中實作 `AuthenticationInfoPostProcessor`

      * 請參閱: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`


### 自訂匯入程式 {#customizing-the-import-process}

若要在現有功能基礎上建置自訂匯入處理常式：

* 必須實施 `ImportHandler` 介面

* 可擴充 `DefaultImportHandler`.

```java
/**
 * Services implementing the <code>ImportHandler</code> interface are
 * called by the {@link HybrisImporter} to create actual commerce entities
 * such as products.
 */
public interface ImportHandler {

  /**
  * Not used.
  */
  public void createTaxonomie(ImporterContext ctx);

  /**
  * Creates a catalog with the given name.
  * @param ctx   The importer context
  * @param name  The catalog's name
  * @return Path of created catalog
  */
  public String createCatalog(ImporterContext ctx, String name) throws Exception;

  /**
  * Creates a product from the given values.
  * @param ctx                The importer context
  * @param values             The product's properties
  * @param parentCategoryPath The containing category's path
  * @return Path of created product
  */
  public String createProduct(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;

  /**
  * Creates a variant product from the given values.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The base product's path
  * @return Path of created product
  */
  public String createVariantProduct(ImporterContext ctx, ValueMap values, String baseProductPath) throws Exception;

  /**
  * Creates an asset for a product. This is usually a product
  * image.
  * @param ctx             The importer context
  * @param values          The product's properties
  * @param baseProductPath The product's path
  * @return Path of created asset
  */
  public String createAsset(ImporterContext ctx, ValueMap values, String productPath) throws Exception;

  /**
  * Creates a category from the given values.
  * @param ctx           The importer context
  * @param values        The category's properties
  * @param parentPath    Path of parent category or base path of import in case of root category
  * @return Path of created category
  */
  public String createCategory(ImporterContext ctx, ValueMap values, String parentCategoryPath) throws Exception;
}
```

匯入工具必須指定 `service.ranking`值大於0的；例如，

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
