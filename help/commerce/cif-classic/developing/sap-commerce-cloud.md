---
title: 使用SAPCommerce Cloud開發
seo-title: Developing with SAP Commerce Cloud
description: SAPCommerce Cloud整合框架包括帶有API的整合層
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

# 使用SAPCommerce Cloud開發 {#developing-with-sap-commerce-cloud}

>[!NOTE]
>
>該電子商務框架可以與任何電子商務解決方案一起使用。 此處介紹的某些細節和示例將參考 [碎片](https://www.hybris.com/) 解決方案。

該整合框架包括具有API的整合層。 這允許您：

* 插入電子商務系統並將產品資料拉入AEM

* 構建AEM獨立於特定電子商務引擎的商務功能元件

![chlimage_1-11](/help/sites-developing/assets/chlimage_1-11a.png)

>[!NOTE]
>
>[API文檔](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 的上界。

提供了多個現成元件AEM以使用整合層。 目前，這些是：

* 產品顯示元件
* 購物車
* 簽出

為了搜索，提供了一個整合鈎子，它AEM允許您使用搜索、電子商務系統的搜索、第三方搜索或其組合。

## 電子商務引擎選擇 {#ecommerce-engine-selection}

電子商務框架可以與任何電子商務解決方案一起使用，所使用的引擎需要通過以下方式AEM識別：

* 電子商務引擎是OSGi服務，支援 `CommerceService` 介面

   * 引擎可由 `commerceProvider` 服務屬性

* AEM支 `Resource.adaptTo()` 為 `CommerceService` 和 `Product`

   * 的 `adaptTo` 實施查找 `cq:commerceProvider` 資源層次結構中的屬性：

      * 如果找到，則使用該值篩選商業服務查找。

      * 如果找不到，則使用排名最高的商務服務。
   * A `cq:Commerce` 使用混合，因此 `cq:commerceProvider` 可以添加到強類型資源中。


* 的 `cq:commerceProvider` 屬性亦用於參考適當之商業工廠定義。

   * 例如， `cq:commerceProvider` 具有值的屬性 `hybris` 將與OSGi配置相關 **Hybris的Day CQ Commerce Factory** (com.adobe.cq.commerce.hybris.impl.HybrisServiceFactory) — 其中參數 `commerceProvider` 也有值 `hybris`。

   * 這裡還有其它屬性，例如 **目錄版本** 可以配置（如果適當且可用）。

請參閱以下示例：

| `cq:commerceProvider = geometrixx` | 在標準安AEM裝中需要具體實施；例如，geometrixx示例，該示例包括對通用API的最小擴展 |
|--- |--- |
| `cq:commerceProvider = hybris` | Hybris實現 |

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
>使用CRXDE Lite，您可以查看如何在用於混合實現的產品元件中處理該問題：
>
>`/apps/geometrixx-outdoors/components/hybris/product/product.jsp`

### 為碎石4開發 {#developing-for-hybris}

電子商務整合框架的擴展已經更新，以支援Hybris 5，同時保持與Hybris 4的向後相容。

代碼中的預設設定將針對Hybris 5進行調整。

為Hybris 4開發，需要以下內容：

* 調用maven時，將以下命令行參數添加到命令

   `-P hybris4`

   它下載預配置的Hybris 4發行版，並將其嵌入捆綁包中 `cq-commerce-hybris-server`。

* 在OSGi配置管理器中：

   * 禁用Hybris 5對預設響應分析器服務的支援。

   * 確保Hybris Basic Authentication Handler服務的服務等級低於Hybris OAuth Handler服務。

### 會話處理 {#session-handling}

hybris使用用戶會話來儲存諸如客戶購物車之類的資訊。 會話ID從中的hybris返回 `JSESSIONID` 曲奇需要隨後向hybris發出請求。 為避免將會話ID儲存在儲存庫中，會話ID會被編碼到儲存在購物者瀏覽器中的另一cookie中。 執行以下步驟：

* 在第一個請求中，顧客的請求中沒有設定cookie;因此向hybris實例發送請求以建立會話。

* 會話cookie從響應中提取，用新cookie編碼(例如， `hybris-session-rest`)，並設定對購物者的回應。 需要使用新Cookie進行編碼，因為原始Cookie僅對特定路徑有效，否則在後續請求中不會從瀏覽器返回。 還必須將路徑資訊添加到cookie的值中。

* 在隨後的請求中，從 `hybris-session-<*xxx*>` 在HTTP客戶端上設定cookie和set，該客戶端用於從hybris請求資料。

>[!NOTE]
>
>當原始會話不再有效時，將建立新的匿名會話。

#### 商務會話 {#commercesession}

* 此會話「擁有」 **購物車**

   * 執行添加/刪除/等

   * 在購物車上執行各種計算；

      `commerceSession.getProductPrice(Product product)`

* 擁有 *儲存位置* 為 **訂單** 資料

   `CommerceSession.getUserContext()`

* 還擁有 **付款** 處理連接

* 還擁有 **完成** 連接

### 產品同步和發佈 {#product-synchronization-and-publishing}

需要在中提供以混合形式維護的產品數AEM據。 已實施以下機制：

* 初始ID負載由混合物作為飼料提供。 此源可以有更新。
* hybris將通過feed（輪詢）提供最AEM新資訊。
* 當使AEM用產品資料時，它將將當前資料的請求發送回hybris（使用上次修改日期的條件獲取請求）。
* 在混合物中，可以以聲明性方式指定飼料內容物。
* 將饋送結構映射到AEM內容模型時，會在側面的饋送適配器AEM中發生。

![chlimage_1-12](/help/sites-developing/assets/chlimage_1-12a.png)

* 導入程式(b)用於目錄中的頁面樹結構的初始AEM設定。
* 通過飼料將雜碎中的目AEM錄變化指示給，然後這些變化傳播AEM到(b)

   * 產品已添加/刪除/更改目錄版本。

   * 產品已批准。

* hybris擴展提供輪詢導入程式（「hybris」方案），該導入程式可配置為按指定的間隔(例如，每24小時指定間隔（以秒為單位）將更改導入：

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

* 識別中的目錄配AEM置 **已轉移** 和 **線上** 目錄版本。

* 在目錄版本之間同步產品將需要（取消）激AEM活相應頁(a、c)

   * 將產品添加到 **線上** 目錄版本需要激活產品頁。

   * 刪除產品需要停用。

* 在(c)中激AEM活頁面需要選中(b)，只有在

   * 產品在 **線上** 產品頁的目錄版本。

   * 引用的產品在 **線上** 其他頁（例如市場活動頁）的目錄版本。

* 激活的產品頁需要訪問產品資料 **線上** 版本(d)。

* 發AEM布實例需要訪問用於檢索產品和個性化資料(d)的hybris。

### 架構 {#architecture}

#### 產品和變型的體系結構 {#architecture-of-product-and-variants}

一個產品可以有多種變化；例如，它可能因顏色和/或大小而異。 產品必須定義驅動變化的屬性；我們 *變型軸*。

但是，並非所有屬性都是變型軸。 變動也會影響其他物業；例如，價格可能取決於規模。 這些屬性不能由購物者選擇，因此不被視為變型軸。

每個產品和/或變型都由資源表示，因此將1:1映射到儲存庫節點。 這是一個推論，即特定產品和/或變型可以通過其路徑唯一地標識。

產品/變型資源並不總是保存實際產品資料。它可能是實際保存在另一個系統（如hybris）上的資料的表示形式。 例如，產品說明、定價等不儲存在AEM中，而是從電子商務引擎即時檢索。

任何產品資源都可以由 `Product API`。 產品API中的大多數調用都是特定於變體的（儘管變體可能從祖先繼承共用值），但也有一些調用列出了變體集( `getVariantAxes()`。 `getVariants()`等)。

>[!NOTE]
>
>實際上，變數軸由任何 `Product.getVariantAxes()` 返回：
>* hybris為hybris實施定義
>
>雖然產品（通常）可以有許多變型軸，但出廠預裝產品元件僅處理兩個：
>
>1. `size`
>
>1. 再加一個

>
>通過 `variationAxis` 產品引用的屬性(通常 `color` Geometrixx Outdoors)。

#### 產品參考和產品資料 {#product-references-and-product-data}

總的來說：

* 產品資料位於 `/etc`

* 和產品參考 `/content`。

產品變體和產品資料節點之間必須有1:1的映射。

產品引用還必須為所呈現的每個變體具有一個節點 — 但不要求顯示所有變體。 例如，如果產品有S、M、L變體，則產品資料可能是：

```shell
etc
|──commerce
|  |──products
|     |──shirt
|       |──shirt-s
|       |──shirt-m
|       |──shirt-l
```

儘管「大而高」目錄可能只有：

```shell
content
|──big-and-tall
|  |──shirt
|     |──shirt-l
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

   * 產品節點是 `nt:unstructured`。

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

   * 的 `CommerceSession` 執行添加/刪除/等。
   * 的 `CommerceSession` 還在購物車上執行各種計算。&quot;

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

   * 在hybris案中，hybris伺服器擁有該購物車。
   * 在通AEM用情況下， [ClientContext](/help/sites-administering/client-context.md)。

**個人化**

* 個性化應始終通過 [ClientContext](/help/sites-administering/client-context.md)。
* ClientContext `/version/` 建立Cart:

   * 應使用 `CommerceSession.addCartEntry()` 的雙曲餘切值。

* 以下說明了ClientContext車中的購物車資訊示例：

![chlimage_1-13](/help/sites-developing/assets/chlimage_1-13a.png)

#### 結帳體系結構 {#architecture-of-checkout}

**購物車和訂單資料**

的 `CommerceSession` 擁有三個元素：

1. 購物車內容
1. 定價
1. 訂單詳細資訊

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
   * 可以使用 `updateOrder(Map<String, Object> delta)`

>[!NOTE]
>
>您可以實現發運選擇器；例如：
>
>`yourProject/commerce/components/shippingpicker`:
>
>* 本質上，這可能是 `foundation/components/form/radio`但是回復了 `CommerceSession` 為：
>
>* 檢查方法是否可用
>* 添加定價資訊
>* 使購物者能夠在中更新訂單頁AEM（包括裝運方法的超集和描述它們的文本），同時仍具有顯示相關資訊的控制項 `CommerceSession` 的下界。


**付款處理**

* 的 `CommerceSession` 還擁有付款處理連接。

* 實施者需要將特定呼叫（添加到其選擇的付款處理服務）添加到 `CommerceSession` 執行。

**訂單履行**

* 的 `CommerceSession` 還擁有履行連接。
* 實施者需要將特定呼叫（添加到他們選擇的付款處理服務）添加到 `CommerceSession` 執行。

### 搜索定義 {#search-definition}

遵循標準服務API模型，電子商務項目提供了一組可由單個商務引擎實現的與搜索相關的API。

>[!NOTE]
>
>目前，只有hybris引擎實現現成的搜索API。
>
>但是，搜索API是通用的，可由每個CommerceService單獨實現。

電子商務項目包含預設搜索元件，位於：

`/libs/commerce/components/search`

![chlimage_1-14](/help/sites-developing/assets/chlimage_1-14a.png)

這利用搜索API查詢所選商業引擎(請參閱 [電子商務引擎選擇](#ecommerce-engine-selection)):

#### 搜索API {#search-api}

核心項目提供了幾個通用/幫助程式類：

1. `CommerceQuery`

   用於描述搜索查詢（包含有關查詢文本、當前頁、頁面大小、排序和所選小平面的資訊）。 所有實現搜索API的電子商務服務都將接收此類實例以執行其搜索。 A `CommerceQuery` 可以從請求對象( `HttpServletRequest`)。

1. `FacetParamHelper`

   是提供一種靜態方法的實用程式類 —  `toParams`  — 用於生成 `GET` 來自facets清單的參數字串和一個切換的值。 這在UI端非常有用，在UI端，您需要為每個方面的每個值顯示一個超連結，這樣當用戶按一下該超連結時，就會切換各個值（即，如果選擇了它，則會從查詢中刪除它，否則會添加）。 這將考慮處理多個/單值小平面、覆蓋值等的所有邏輯。

搜索API的入口點是 `CommerceService#search` 返回 `CommerceResult` 的雙曲餘切值。 查看 [API文檔](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) 的子菜單。

### 用戶整合 {#user-integration}

在各種電子商AEM務系統之間提供整合。 這要求在各種系統之間同步購物者的策略，AEM以便特定代碼只需知道，AEM反之亦然：

* 驗證

   AEM被推定為 *僅* Web前端，因此 *全部* 驗證。

* 赫布里斯賬戶

   為每AEM位購物者在hybris中建立相應（從屬）帳戶。 此帳戶的用戶名與用戶名相AEM同。 密碼隨機密碼被自動生成並儲存（加密）在AEM中。

#### 預先存在的用戶 {#pre-existing-users}

前AEM端可定位在現有的碎片實施之前。 還可以將液壓引擎添加到現有AEM設備。 為此，系統必須能夠妥善處理任一系統中的現有用戶：

* ->

   * 登錄到hybris時，如果用AEM戶尚不存在：

      * 使用密碼隨機密碼建立新的hybris用戶
      * 將hybris用戶名儲存在用戶的用戶目AEM錄中
   * 請參閱: `com.adobe.cq.commerce.hybris.impl.HybrisSessionImpl#login()`


* 赫布里斯 — AEM>

   * 登錄時，如果AEM系統識別用戶：

      * 嘗試使用提供的username/pwd登錄到hybris
      * 如果成功，則使用相AEM同密碼(特定AEM的鹽將導致特定的AEM哈希)在中建立新用戶
   * 在Sling中實現了上述算法 `AuthenticationInfoPostProcessor`

      * 請參閱: `com.adobe.cq.commerce.hybris.impl.user.LazyUserImporter.java`


### 自定義導入流程 {#customizing-the-import-process}

要在現有功能的基礎上構建自定義導入處理程式：

* 必須執行 `ImportHandler` 介面

* 可以擴展 `DefaultImportHandler`。

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

要讓導入程式識別您的自定義處理程式，它必須指定 `service.ranking`（二）價值大於0的；例如。

```java
@Component
@Service
@Property(name = "service.ranking", value = 100)
public class MyImportHandler extends DefaultImportHandler
{
...
}
```
