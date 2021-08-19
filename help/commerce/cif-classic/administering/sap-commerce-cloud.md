---
title: SAPCommerce Cloud
seo-title: SAPCommerce Cloud
description: 了解如何將AEM與SAPCommerce Cloud搭配使用。
seo-description: 了解如何將AEM與SAPCommerce Cloud搭配使用。
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
source-git-commit: 61691c300322edcdee33b121ca400e4c89256e45
workflow-type: tm+mt
source-wordcount: '1726'
ht-degree: 1%

---

# SAPCommerce Cloud{#sap-commerce-cloud}

安裝後，您可以設定執行個體：

1. [設定Faceted Search for AnalyticsGeometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors)。
1. [設定目錄版本](#configure-the-catalog-version)。
1. [設定匯入結構](#configure-the-import-structure)。
1. [設定要載入的產品屬性](#configure-the-product-attributes-to-load)。
1. [匯入產品資料](#importing-the-product-data)。
1. [設定目錄匯入工具](#configure-the-catalog-importer)。
1. 使用[匯入工具將目錄](#catalog-import)匯入至AEM中的特定位置。

## 配置強制搜索Geometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>hybris 5.3.0.1和更新版本不需要此設定。

1. 在您的瀏覽器中，導覽至&#x200B;**hybris management console**，網址為：

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. 從側欄中，依序選擇&#x200B;**System**、**Facet search**、**Facet Search Config**。
1. **開啟** Editor ，以取 **得封裝目錄的範例解決器設定**。

1. 在&#x200B;**目錄版本**&#x200B;下，使用&#x200B;**新增目錄版本**&#x200B;將`outdoors-Staged`和`outdoors-Online`新增至清單。
1. **儲存設定。**
1. 開啟&#x200B;**SOLR項類型**&#x200B;以將&#x200B;**SOLR排序**&#x200B;添加到`ClothesVariantProduct`:

   * 關聯性（「關聯性」，分數）
   * name-asc(&quot;Name(ascending)&quot;, name)
   * name-desc(&quot;Name(descending)&quot;, name)
   * price-asc(&quot;price(ascending)&quot;, priceValue)
   * price-desc(&quot;Price(descending)&quot;, priceValue)

   >[!NOTE]
   >
   >使用上下文菜單（通常按一下右鍵）選擇`Create Solr sort`。
   >
   >針對Hybris 5.0.0，請開啟`Indexed Types`標籤，按兩下`ClothesVariantProduct`，然後開啟標籤`SOLR Sort`。

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. 在&#x200B;**索引類型**&#x200B;頁簽中，將&#x200B;**合成類型**&#x200B;設定為：

   `Product - Product`

1. 在&#x200B;**索引類型**&#x200B;頁簽中，為`full`調整&#x200B;**索引器查詢**:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. 在&#x200B;**索引類型**&#x200B;頁簽中，為`incremental`調整&#x200B;**索引器查詢**:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. 在&#x200B;**索引類型**&#x200B;標籤中，調整`category`面。 按兩下類別清單中的最後一個條目以開啟&#x200B;**索引屬性**&#x200B;頁簽：

   >[!NOTE]
   >
   >對於hybris 5.2，請根據下面的螢幕截圖，確定已選取「屬性」表格中的`Facet`屬性：

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. 開啟&#x200B;**Facet Settings**&#x200B;標籤並調整欄位值：

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **儲存變更。**
1. 再次從&#x200B;**SOLR項目類型**&#x200B;中，根據以下螢幕截圖調整`price`面。 與`category`一樣，按兩下`price`以開啟&#x200B;**索引屬性**&#x200B;標籤：

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. 開啟&#x200B;**Facet Settings**&#x200B;標籤並調整欄位值：

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **儲存變更。**
1. 開啟&#x200B;**System**,**Facet搜索**，然後開啟&#x200B;**索引器操作嚮導**。 啟動cronjob:

   * **索引器操作**:  `full`
   * **Sol配置**:  `Sample Solr Config for Clothes`

## 配置目錄版本 {#configure-the-catalog-version}

可以為OSGi服務配置導入的&#x200B;**目錄版本**(`hybris.catalog.version`):

**Day CQ Commerce Hybris設定**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**目** 錄版本通常設 `Online` 為 `Staged` 或（預設）。

>[!NOTE]
>
>使用AEM時，有數種方法可管理這類服務的組態設定；如需完整詳細資訊，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md) 。 另請參閱主控台，以取得可設定參數及其預設值的完整清單。

記錄輸出會針對已建立的頁面和元件提供意見反應，並報告可能的錯誤。

## 配置導入結構 {#configure-the-import-structure}

下列清單顯示預設建立的範例結構（資產、頁面和元件）:

```shell
+ /content/dam/path/to/images
  + 12345.jpg (dam:Asset)
    + ...
  + ...
+ /content/site/en
  - cq:commerceProvider = "hybris"
  - cq:hybrisBaseStore = "basestore"
  - cq:hybrisCatalogId = "catalog"
  + category1 (cq:Page)
    + jcr:content (cq:PageContent)
      - jcr:title = "Category 1"
    + category11 (cq:Page)
      + jcr:content (cq:PageContent)
        - jcr:title = "Category 1.1"
      + 12345 (cq:Page)
        + jcr:content (cq:PageContent)
          + par
            + product (nt:unstructured)
              - cq:hybrisProductId = "12345"
              - sling:resourceType = "commerce/components/product"
              + image (nt:unstructured)
                - sling:resourceType = "commerce/components/product/image"
                - fileReference = "/content/dam/path/to/images/12345.jpg"
              + 12345.1-S (nt:unstructured)
                - cq:hybrisProductId = "12345.1-S"
                - sling:resourceType = "commerce/components/product"
                + image (nt:unstructured)
                  - sling:resourceType = "commerce/components/product/image"
                  - fileReference = "/content/dam/path/to/images/12345.1-S.jpg"
              + ...
```

這種結構由實現`ImportHandler`介面的OSGi服務`DefaultImportHandler`建立。 實際匯入工具會呼叫匯入處理常式，以建立產品、產品變數、類別、資產等。

>[!NOTE]
>
>您可以實作自己的匯入處理常式](#configure-the-import-structure)自訂此程式。[

可為以下項配置導入時要生成的結構：

&quot;**Day CQ Commerce Hybris預設匯入處理常式**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`

使用AEM時，有數種方法可管理這類服務的組態設定；如需完整詳細資訊，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md) 。 另請參閱主控台，以取得可設定參數及其預設值的完整清單。

## 設定要載入的產品屬性 {#configure-the-product-attributes-to-load}

回應剖析器可設定為定義要為（變體）產品載入的屬性和屬性：

1. 配置OSGi捆綁包：

   **Day CQ商務Hybris預設回應剖析器**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   您可以在此處定義載入和對應所需的各種選項和屬性。

   >[!NOTE]
   >
   >使用AEM時，有數種方法可管理這類服務的組態設定；如需完整詳細資訊，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md) 。 另請參閱主控台，以取得可設定參數及其預設值的完整清單。

## 匯入產品資料 {#importing-the-product-data}

匯入產品資料的方式有許多種。 最初設定環境時，或在hybris資料中進行變更後，可匯入產品資料：

* [完整匯入](#full-import)
* [增量匯入](#incremental-import)
* [快速更新](#express-update)

從hybris匯入的實際產品資訊會存放在存放庫中：

`/etc/commerce/products`

下列屬性會指出與hybris的連結：

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>hybris實作(即`geometrixx-outdoors/en_US`)只會在`/etc/commerce`下儲存產品ID和其他基本資訊。
>
>每次請求產品相關資訊時，都會參考hybris伺服器。

### 完整匯入 {#full-import}

1. 如有需要，請使用CRXDE Lite刪除所有現有產品資料。

   1. 導航到保存產品資料的子樹：

      `/etc/commerce/products`

      例如：

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. 刪除保存產品資料的節點；例如`outdoors`。
   1. **「保** 存全部」以保留更改。

1. 在AEM中開啟hybris匯入工具：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 設定所需參數；例如：

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. 按一下&#x200B;**匯入目錄**&#x200B;以開始匯入。

   完成時，您可以驗證匯入的資料：

   ```
       /etc/commerce/products/outdoors
   ```

   你可以在CRXDE Lite中開啟這個；例如：

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### 增量匯入 {#incremental-import}

1. 查看AEM中相關產品的資訊，位於以下相應子樹中：

   `/etc/commerce/products`

   你可以在CRXDE Lite中開啟這個；例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. 在hybris中，更新有關相關產品的資訊。

1. 在AEM中開啟hybris匯入工具：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 選擇點按框&#x200B;**增量導入**。
1. 按一下&#x200B;**匯入目錄**&#x200B;以開始匯入。

   完成後，您可以驗證AEM中更新的資料：

   ```
       /etc/commerce/products
   ```


### 快速更新 {#express-update}

匯入程式可能需要很長的時間，因此，作為產品同步的擴充功能，您可以為手動觸發的快速更新選取目錄的特定區域。 這會使用匯出摘要與標準屬性設定。

1. 查看AEM中相關產品的資訊，位於以下相應子樹中：

   `/etc/commerce/products`

   你可以在CRXDE Lite中開啟這個；例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. 在hybris中，更新有關相關產品的資訊。

1. 在hybris中，將產品新增至Express Queue;例如：

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. 在AEM中開啟hybris匯入工具：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 選擇Clickbox **Express Update**。
1. 按一下&#x200B;**匯入目錄**&#x200B;以開始匯入。

   完成後，您可以驗證AEM中更新的資料：

   ```
       /etc/commerce/products
   ```

## 設定目錄匯入工具 {#configure-the-catalog-importer}

hybris目錄可使用批次匯入工具，將hybris目錄、類別和產品匯入至AEM。

匯入工具使用的參數可針對下列項目進行設定：

**Day CQ Commerce Hybris目錄匯入工具**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

使用AEM時，有數種方法可管理這類服務的組態設定；如需完整詳細資訊，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md) 。 另請參閱主控台，以取得可設定參數及其預設值的完整清單。

## 目錄匯入 {#catalog-import}

hybris套件隨附目錄匯入工具，用於設定初始頁面結構。

這可從下列位置取得：

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

必須提供下列資訊：

* **基**
本儲存以混合配置的基本儲存的標識符。

* ****
目錄要匯入的目錄識別碼。

* **根**
路徑應匯入目錄的路徑。

## 從目錄中移除產品 {#removing-a-product-from-the-catalog}

要從目錄中刪除一個或多個產品：

1. [設定OSGi serviceDay CQ ](/help/sites-deploying/configuring-osgi.md) **Commerce Hybris Catalog Importer的**;另請參閱 [設定目錄匯入工具](#configure-the-catalog-importer)。

   啟用下列屬性：

   * **啟用產品移除**
   * **啟用產品資產移除**

   >[!NOTE]
   >
   >使用AEM時，有數種方法可管理這類服務的組態設定；如需完整詳細資訊，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md) 。 另請參閱主控台，以取得可設定參數及其預設值的完整清單。

1. 通過執行兩個增量更新來初始化導入程式（請參閱[目錄導入](#catalog-import)）:

   * 第一次執行會產生一組變更的產品 — 顯示在記錄清單中。
   * 第二次不應更新任何產品。

   >[!NOTE]
   >
   >第一個匯入是初始化產品資訊。 第二個匯入會驗證一切皆正常運作，而且產品集已就緒。

1. 檢查包含您要移除之產品的類別頁面。 產品詳細資訊應該會顯示。

   例如，以下類別顯示Cajamara產品的詳細資訊：

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. 在Hybris主控台中移除產品。 使用選項&#x200B;**更改批准狀態**&#x200B;將狀態設定為`unapproved`。 產品將從即時摘要中移除。

   例如：

   * 開啟頁面[http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * 選擇目錄`Outdoors Staged`
   * 搜尋 `Cajamara`
   * 選擇此產品並將批准狀態更改為`unapproved`

1. 執行另一增量更新（請參閱[目錄導入](#catalog-import)）。 記錄檔會列出已刪除的產品。
1. [](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) 統計適當的目錄。產品和產品頁面將從AEM中移除。

   例如：

   * 開啟:

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * 轉出`Hybris Base`目錄
   * 開啟:

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * `Cajamara`產品將從`Bike`類別中移除

1. 要重新註冊產品，請執行以下操作：

   1. 在hybris中，將核准狀態設回&#x200B;**approved**
   1. 在AEM中：

      1. 執行增量更新
      1. 再次轉出適當的目錄
      1. 刷新相應的類別頁

## 將訂單歷史記錄特徵新增至用戶端內容 {#add-order-history-trait-to-the-client-context}

要將訂單歷史記錄添加到[客戶端上下文](/help/sites-developing/client-context.md)中，請執行以下操作：

1. 開啟[客戶端上下文設計頁面](/help/sites-administering/client-context.md)，方法如下：

   * 開啟要編輯的頁面，然後使用&#x200B;**Ctrl-Alt-c**(windows)或&#x200B;**control-option-c**(Mac)開啟客戶端上下文。 使用客戶端上下文左上角的鉛筆表徵圖&#x200B;**開啟ClientContext設計頁**。
   * 直接導覽至[http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [將訂 **單歷** ](/help/sites-administering/client-context.md#adding-a-property-component) 史元件新增至 **用**&#x200B;戶端內容的購物車元件。
1. 您可以確認用戶端內容顯示訂單歷史記錄的詳細資訊。 例如：

   1. 開啟[客戶端上下文](/help/sites-administering/client-context.md)。
   1. 將項目新增至購物車。
   1. 完成結帳。
   1. 檢查客戶端上下文。
   1. 新增其他項目至購物車。
   1. 導覽至結帳頁面：

      * 客戶端上下文顯示訂單歷史記錄的摘要。
      * 畫面會顯示「您是回頭的客戶」訊息。

   >[!NOTE]
   >
   >消息的實現方式為：
   >
   >* 導覽至[http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  促銷活動包含一個體驗。
   >
   >* 按一下區段([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
      >
      >
   * 區段是使用&#x200B;**順序歷史記錄屬性**&#x200B;特徵建立。

