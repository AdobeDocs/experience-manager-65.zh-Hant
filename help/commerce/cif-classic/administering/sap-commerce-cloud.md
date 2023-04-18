---
title: 將AEM與SAPCommerce Cloud
description: 了解如何將AEM與SAPCommerce Cloud搭配使用。
uuid: cee1a781-fcba-461e-a0a4-c561a1dbcbf3
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: c342f789-2ff7-4802-99c7-c3699218fe47
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 2%

---

# SAPCommerce Cloud{#sap-commerce-cloud}

安裝後，您可以設定執行個體：

1. [配置強制搜索Geometrixx Outdoors](#configure-the-facetted-search-for-geometrixx-outdoors).
1. [配置目錄版本](#configure-the-catalog-version).
1. [配置導入結構](#configure-the-import-structure).
1. [設定要載入的產品屬性](#configure-the-product-attributes-to-load).
1. [匯入產品資料](#importing-the-product-data).
1. [設定目錄匯入工具](#configure-the-catalog-importer).
1. 使用 [匯入工具以匯入目錄](#catalog-import) 進入AEM中的特定位置。

## 配置強制搜索Geometrixx Outdoors {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>hybris 5.3.0.1和更新版本不需要此設定。

1. 在您的瀏覽器中，導覽至 **hybris management console** at:

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. 從側欄中，選取 **系統**，然後 **Facet搜尋**，然後 **Facet搜尋設定**.
1. **開啟編輯器** 針對 **服裝目錄的Solr配置示例**.

1. 在 **目錄版本** use **新增目錄版本** 新增 `outdoors-Staged` 和 `outdoors-Online` 到清單中。
1. **儲存設定。**
1. 開啟 **SOLR物料類型** 新增 **SOLR排序** to `ClothesVariantProduct`:

   * 關聯性（「關聯性」，分數）
   * name-asc(&quot;Name(ascending)&quot;, name)
   * name-desc(&quot;Name(descending)&quot;, name)
   * price-asc(&quot;price(ascending)&quot;, priceValue)
   * price-desc(&quot;Price(descending)&quot;, priceValue)

   >[!NOTE]
   >
   >使用上下文菜單（通常按一下右鍵）來選擇 `Create Solr sort`.
   >
   >針對Hybris 5.0.0，請開啟 `Indexed Types` 按兩下 `ClothesVariantProduct`，然後是索引標籤 `SOLR Sort`.

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. 在 **索引類型** 標籤設定 **合成類型** 至：

   `Product - Product`

1. 在 **索引類型** 標籤調整 **索引器查詢** for `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. 在 **索引類型** 標籤調整 **索引器查詢** for `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. 在 **索引類型** 標籤調整 `category` 刻面。 按兩下類別清單中的最後一個項目以開啟 **索引屬性** 標籤：

   >[!NOTE]
   >
   >針對hybris 5.2，請確定 `Facet` 屬性表中的屬性是根據下面的螢幕截圖選擇的：

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. 開啟 **Facet設定** 標籤並調整欄位值：

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **儲存變更。**
1. 再次從 **SOLR物料類型**，調整 `price` 會根據下列螢幕擷取畫面顯示。 與 `category`，按兩下 `price` 開啟 **索引屬性** 標籤：

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. 開啟 **Facet設定** 標籤並調整欄位值：

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **儲存變更。**
1. 開啟 **系統**, **Facet搜尋**，然後 **索引器操作嚮導**. 啟動cronjob:

   * **索引器操作**: `full`
   * **Solr配置**: `Sample Solr Config for Clothes`

## 配置目錄版本 {#configure-the-catalog-version}

此 **目錄版本** ( `hybris.catalog.version`)，則可針對OSGi服務進行設定：

**Day CQ Commerce Hybris設定**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**目錄版本** 通常設為 `Online` 或 `Staged` （預設）。

>[!NOTE]
>
>使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。 另請參閱主控台，以取得可設定參數及其預設值的完整清單。

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

此結構由OSGi服務建立 `DefaultImportHandler` 實施 `ImportHandler` 介面。 實際匯入工具會呼叫匯入處理常式，以建立產品、產品變數、類別、資產等。

>[!NOTE]
>
>您可以 [通過實施自己的導入處理程式來自定義此過程](#configure-the-import-structure).

可為以下項配置導入時要生成的結構：

&quot;**Day CQ商務Hybris預設匯入處理常式**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。 另請參閱主控台，以取得可設定參數及其預設值的完整清單。

## 設定要載入的產品屬性 {#configure-the-product-attributes-to-load}

回應剖析器可設定為定義要為（變體）產品載入的屬性和屬性：

1. 配置OSGi捆綁包：

   **Day CQ商務Hybris預設回應剖析器**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   您可以在此處定義載入和對應所需的各種選項和屬性。

   >[!NOTE]
   >
   >使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。 另請參閱主控台，以取得可設定參數及其預設值的完整清單。

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
>hybris實作(即 `geometrixx-outdoors/en_US`)只會儲存產品ID和下方的其他基本資訊 `/etc/commerce`.
>
>每次請求產品相關資訊時，都會參考hybris伺服器。

### 完整匯入 {#full-import}

1. 如有需要，請使用CRXDE Lite刪除所有現有產品資料。

   1. 導航到保存產品資料的子樹：

      `/etc/commerce/products`

      例如：

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. 刪除保存產品資料的節點；例如， `outdoors`.
   1. **全部儲存** 以保留變更。

1. 在AEM中開啟hybris匯入工具：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 設定所需參數；例如：

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. 按一下 **匯入目錄** 以開始匯入。

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

1. 選取點按方塊 **增量導入**.
1. 按一下 **匯入目錄** 以開始匯入。

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

1. 選取點按方塊 **快速更新**.
1. 按一下 **匯入目錄** 以開始匯入。

   完成後，您可以驗證AEM中更新的資料：

   ```
       /etc/commerce/products
   ```

## 設定目錄匯入工具 {#configure-the-catalog-importer}

hybris目錄可使用批次匯入工具將hybris目錄、類別和產品匯入至AEM。

匯入工具使用的參數可針對下列項目進行設定：

**Day CQ Commerce Hybris目錄匯入工具**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。 另請參閱主控台，以取得可設定參數及其預設值的完整清單。

## 目錄匯入 {#catalog-import}

hybris套件隨附目錄匯入工具，用於設定初始頁面結構。

這可從下列位置取得：

`http://localhost:4502/etc/importers/hybris.html`

![ecommerceimportconsole](/help/sites-administering/assets/ecommerceimportconsole.png)

必須提供下列資訊：

* **基本儲存**
以Hybris配置的基礎儲存的標識符。

* **目錄**
要匯入的目錄識別碼。

* **根路徑**
應匯入目錄的路徑。

## 從目錄中移除產品 {#removing-a-product-from-the-catalog}

要從目錄中刪除一個或多個產品：

1. [為OSGi服務配置](/help/sites-deploying/configuring-osgi.md) **Day CQ Commerce Hybris目錄匯入工具**;另請參閱 [設定目錄匯入工具](#configure-the-catalog-importer).

   啟用下列屬性：

   * **啟用產品移除**
   * **啟用產品資產移除**

   >[!NOTE]
   >
   >使用AEM時，有數種方法可管理這類服務的組態設定；請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 以取得完整詳細資訊。 另請參閱主控台，以取得可設定參數及其預設值的完整清單。

1. 執行兩個增量更新以初始化匯入工具(請參閱 [目錄匯入](#catalog-import)):

   * 第一次執行會產生一組變更的產品 — 顯示在記錄清單中。
   * 第二次不應更新任何產品。

   >[!NOTE]
   >
   >第一個匯入是初始化產品資訊。 第二個匯入會驗證一切皆正常運作，而且產品集已就緒。

1. 檢查包含您要移除之產品的類別頁面。 產品詳細資訊應該會顯示。

   例如，以下類別顯示Cajamara產品的詳細資訊：

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. 在Hybris主控台中移除產品。 使用選項 **更改批准狀態** 將狀態設定為 `unapproved`. 產品將從即時摘要中移除。

   例如：

   * 開啟頁面 [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * 選擇目錄 `Outdoors Staged`
   * 搜尋 `Cajamara`
   * 選擇此產品，並將批准狀態更改為 `unapproved`

1. 執行其他增量更新(請參閱 [目錄匯入](#catalog-import))。 記錄檔會列出已刪除的產品。
1. [轉出](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) 適當的目錄。 產品和產品頁面將從AEM中移除。

   例如：

   * 開啟:

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * 轉出 `Hybris Base` 目錄
   * 開啟:

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * 此 `Cajamara` 產品將從 `Bike` 類別

1. 要重新註冊產品，請執行以下操作：

   1. 在hybris中，將核准狀態設回 **核准**
   1. 在AEM中：

      1. 執行增量更新
      1. 再次轉出適當的目錄
      1. 刷新相應的類別頁

## 將訂單歷史記錄特徵新增至用戶端內容 {#add-order-history-trait-to-the-client-context}

若要將訂單歷史記錄新增至 [用戶上下文](/help/sites-developing/client-context.md):

1. 開啟 [客戶端上下文設計頁面](/help/sites-administering/client-context.md)，方法為：

   * 開啟要編輯的頁面，然後使用 **Ctrl-Alt-c** (windows)或 **control-option-c** (Mac)。 使用用戶端內容左上角的鉛筆圖示，即可 **開啟ClientContext設計頁面**.
   * 直接導覽至 [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [新增 **訂單歷史記錄** 元件](/help/sites-administering/client-context.md#adding-a-property-component) 到 **購物車**&#x200B;客戶端上下文的t元件。
1. 您可以確認用戶端內容顯示訂單歷史記錄的詳細資訊。 例如：

   1. 開啟 [用戶上下文](/help/sites-administering/client-context.md).
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
   >* 導覽至 [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  促銷活動包含一個體驗。
   >
   >* 按一下區段([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
   >
   >* 區段是使用 **訂單歷史記錄屬性** 特徵。

