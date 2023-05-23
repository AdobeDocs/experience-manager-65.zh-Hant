---
title: 與AEMSAPCommerce Cloud一起使用
description: 瞭解如何與AEMSAPCommerce Cloud一起使用。
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

安裝後，您可以配置實例：

1. [配置面向Geometrixx Outdoors的強制搜索](#configure-the-facetted-search-for-geometrixx-outdoors)。
1. [配置目錄版本](#configure-the-catalog-version)。
1. [配置導入結構](#configure-the-import-structure)。
1. [配置要載入的產品屬性](#configure-the-product-attributes-to-load)。
1. [導入產品資料](#importing-the-product-data)。
1. [配置目錄導入程式](#configure-the-catalog-importer)。
1. 使用 [導入程式](#catalog-import) 進入特定位AEM置。

## 配置面向Geometrixx Outdoors的強制搜索 {#configure-the-facetted-search-for-geometrixx-outdoors}

>[!NOTE]
>
>這不是Hybris5.3.0.1和以後的需要。

1. 在瀏覽器中，導航到 **hybris管理控制台** 地址：

   [http://localhost:9001/hmc/hybris](http://localhost:9001/hmc/hybris)

1. 從提要欄中，選擇 **系統**，則 **小平面搜索**，則 **方面搜索配置**。
1. **開啟編輯器** 為 **用於封裝目錄的Solr配置示例**。

1. 下 **目錄版本** 使用 **添加目錄版本** 添加 `outdoors-Staged` 和 `outdoors-Online` 清單中。
1. **儲存設定。**
1. 開啟 **SOLR物料類型** 添加 **SOLR排序** 至 `ClothesVariantProduct`:

   * 相關性（「相關性」，分數）
   * name-asc(&quot;名稱（升序）&quot;，名稱)
   * name-desc(&quot;名稱（降序）&quot;, name)
   * price-asc(「price(ascing)」， priceValue)
   * price-desc(&quot;Price(descending)&quot;, priceValue)

   >[!NOTE]
   >
   >使用上下文菜單（通常按一下右鍵）選擇 `Create Solr sort`。
   >
   >希布里5.0.0開門 `Indexed Types` 頁籤，按兩下 `ClothesVariantProduct`，則 `SOLR Sort`。

   ![chlimage_1-36](/help/sites-administering/assets/chlimage_1-36a.png)

1. 在 **索引類型** 頁籤 **合成的類型** 至：

   `Product - Product`

1. 在 **索引類型** 調整 **索引器查詢** 為 `full`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}})
   ```

1. 在 **索引類型** 調整 **索引器查詢** 為 `incremental`:

   ```shell
   SELECT {pk} FROM {Product} WHERE {pk} NOT IN ({{SELECT {baseProductpk} FROM {variantproduct}}}) AND {modifiedtime} <= ?lastIndexTime
   ```

1. 在 **索引類型** 調整 `category` 方面。 按兩下類別清單中的最後一個條目以開啟 **索引屬性** 頁籤：

   >[!NOTE]
   >
   >5.2號碎片，確保 `Facet` 「屬性」(Properties)表格中的屬性將根據以下螢幕快照進行選擇：

   ![chlimage_1-37](/help/sites-administering/assets/chlimage_1-37a.png) ![chlimage_1-38](/help/sites-administering/assets/chlimage_1-38a.png)

1. 開啟 **方面設定** 頁籤並調整欄位值：

   ![chlimage_1-39](/help/sites-administering/assets/chlimage_1-39a.png)

1. **儲存變更。**
1. 從 **SOLR物料類型**，調整 `price` 根據以下螢幕截圖顯示。 與 `category`，按兩下 `price` 開啟 **索引屬性** 頁籤：

   ![chlimage_1-40](/help/sites-administering/assets/chlimage_1-40a.png)

1. 開啟 **方面設定** 頁籤並調整欄位值：

   ![chlimage_1-41](/help/sites-administering/assets/chlimage_1-41a.png)

1. **儲存變更。**
1. 開啟 **系統**。 **小平面搜索**，則 **索引器操作嚮導**。 啟動cronjob:

   * **索引器操作**: `full`
   * **Solr配置**: `Sample Solr Config for Clothes`

## 配置目錄版本 {#configure-the-catalog-version}

的 **目錄版本** ( `hybris.catalog.version`)，可以為OSGi服務配置：

**Day CQ Commerce Hybris配置**
( `com.adobe.cq.commerce.hybris.common.DefaultHybrisConfigurationService`)

**目錄版本** 通常設定為 `Online` 或 `Staged` （預設）。

>[!NOTE]
>
>使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的雙曲餘切值。 另請參見控制台，瞭解可配置參數及其預設值的完整清單。

日誌輸出提供對建立的頁面和元件的反饋，並報告潛在錯誤。

## 配置導入結構 {#configure-the-import-structure}

以下清單顯示預設建立的示例結構（資產、頁面和元件）:

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

這種結構由OSGi服務建立 `DefaultImportHandler` 實現 `ImportHandler` 。 實際導入程式調用導入處理程式以建立產品、產品變體、類別、資產等。

>[!NOTE]
>
>你可以 [通過實現自己的導入處理程式自定義此過程](#configure-the-import-structure)。

導入時要生成的結構可配置為：

&quot;**Day CQ Commerce Hybris預設導入處理程式**
`(com.adobe.cq.commerce.hybris.importer.DefaultImportHandler`)

使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的雙曲餘切值。 另請參見控制台，瞭解可配置參數及其預設值的完整清單。

## 配置要載入的產品屬性 {#configure-the-product-attributes-to-load}

響應分析器可配置為定義要為（變型）產品載入的屬性和屬性：

1. 配置OSGi捆綁包：

   **Day CQ Commerce Hybris預設響應分析器**
(`com.adobe.cq.commerce.hybris.impl.importer.DefaultResponseParser`)

   在此，您可以定義載入和映射所需的各種選項和屬性。

   >[!NOTE]
   >
   >使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的雙曲餘切值。 另請參見控制台，瞭解可配置參數及其預設值的完整清單。

## 導入產品資料 {#importing-the-product-data}

有多種方法可導入產品資料。 在初始設定環境時或在對混合資料進行更改後，可以導入產品資料：

* [完全導入](#full-import)
* [增量匯入](#incremental-import)
* [快速更新](#express-update)

從碎片中導入的實際產品資訊保存在儲存庫中，位於：

`/etc/commerce/products`

以下屬性指示與hybris的連結：

* `commerceProvider`
* `cq:hybrisCatalogId`
* `cq:hybrisProductID`

>[!NOTE]
>
>Hybris的實施(即 `geometrixx-outdoors/en_US`)僅將產品ID和其他基本資訊儲存在 `/etc/commerce`。
>
>每次請求關於產品的資訊時都引用該混合伺服器。

### 完全導入 {#full-import}

1. 如果需要，請使用CRXDE Lite刪除所有現有產品資料。

   1. 導航到保存產品資料的子樹：

      `/etc/commerce/products`

      例如：

      [`http://localhost:4502/crx/de/index.jsp#/etc/commerce/products`](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

   1. 刪除保存產品資料的節點；比如說， `outdoors`。
   1. **全部保存** 來堅持改變。

1. 在以下位置開啟碎石進口AEM商：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 配置所需參數；例如：

   ![chlimage_1-42](/help/sites-administering/assets/chlimage_1-42a.png)

1. 按一下 **導入目錄** 的子菜單。

   完成後，您可以驗證導入的資料：

   ```
       /etc/commerce/products/outdoors
   ```

   你可以用CRXDE Lite開啟它。例如：

   `[http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)`

### 增量匯入 {#incremental-import}

1. 在以下相應子樹AEM中檢查相關產品中保存的資訊：

   `/etc/commerce/products`

   你可以用CRXDE Lite開啟它。例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. 在hybris中，更新有關相關產品的資訊。

1. 在以下位置開啟碎石進口AEM商：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 選擇按一下框 **增量導入**。
1. 按一下 **導入目錄** 的子菜單。

   完成後，可以驗證在以下位置更新的AEM資料：

   ```
       /etc/commerce/products
   ```


### 快速更新 {#express-update}

導入過程可能需要很長時間，因此作為產品同步的擴展，您可以選擇目錄的特定區域以進行手動觸發的快速更新。 此操作將導出源與標準屬性配置一起使用。

1. 在以下相應子樹AEM中檢查相關產品中保存的資訊：

   `/etc/commerce/products`

   你可以用CRXDE Lite開啟它。例如：

   [http://localhost:4502/crx/de/index.jsp#/etc/commerce/products](http://localhost:4502/crx/de/index.jsp#/etc/commerce/products)

1. 在hybris中，更新有關相關產品的資訊。

1. 在Hybris中，將產品添加到Express隊列；例如：

   ![chlimage_1-43](/help/sites-administering/assets/chlimage_1-43a.png)

1. 在以下位置開啟碎石進口AEM商：

   `/etc/importers/hybris.html`

   例如：

   [http://localhost:4502/etc/importers/hybris.html](http://localhost:4502/etc/importers/hybris.html)

1. 選擇按一下框 **快速更新**。
1. 按一下 **導入目錄** 的子菜單。

   完成後，可以驗證在以下位置更新的AEM資料：

   ```
       /etc/commerce/products
   ```

## 配置目錄導入程式 {#configure-the-catalog-importer}

可以使用批量導入器將碎AEM物目錄、類別和產品導入到碎物目錄中。

導入程式使用的參數可配置為：

**Day CQ Commerce Hybris目錄導入程式**
( `com.adobe.cq.commerce.hybris.impl.importer.DefaultHybrisImporter`)

使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的雙曲餘切值。 另請參見控制台，瞭解可配置參數及其預設值的完整清單。

## 目錄導入 {#catalog-import}

Hybris包附帶了一個目錄導入程式，用於設定初始頁面結構。

可從以下網站獲得：

`http://localhost:4502/etc/importers/hybris.html`

![cemomerce導入控制台](/help/sites-administering/assets/ecommerceimportconsole.png)

必須提供以下資訊：

* **基本儲存**
以混合形式配置的基本儲存的標識符。

* **目錄**
要導入的目錄的標識符。

* **根路徑**
應將目錄導入的路徑。

## 從目錄中刪除產品 {#removing-a-product-from-the-catalog}

要從目錄中刪除一個或多個產品：

1. [為OSGi服務配置](/help/sites-deploying/configuring-osgi.md) **Day CQ Commerce Hybris目錄導入程式**;參見 [配置目錄導入程式](#configure-the-catalog-importer)。

   激活以下屬性：

   * **啟用產品刪除**
   * **啟用產品資產刪除**

   >[!NOTE]
   >
   >使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的雙曲餘切值。 另請參見控制台，瞭解可配置參數及其預設值的完整清單。

1. 通過執行兩個增量更新來初始化導入程式(請參見 [目錄導入](#catalog-import)):

   * 第一次運行的結果是一組更改的產品 — 在日誌清單中指明。
   * 第二次不應更新任何產品。

   >[!NOTE]
   >
   >第一個導入是初始化產品資訊。 第二次導入驗證所有工作都已就緒，且產品集已就緒。

1. 檢查包含要刪除的產品的類別頁。 產品詳細資訊應可見。

   例如，以下類別顯示Cajamara產品的詳細資訊：

   [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

1. 在Hybris控制台中刪除產品。 使用選項 **更改審批狀態** 將狀態設定為 `unapproved`。 產品將從即時進紙中刪除。

   例如：

   * 開啟頁面 [http://localhost:9001/productcockpit](http://localhost:9001/productcockpit)
   * 選擇目錄 `Outdoors Staged`
   * 搜尋 `Cajamara`
   * 選擇此產品並將審批狀態更改為 `unapproved`

1. 執行其他增量更新(請參閱 [目錄導入](#catalog-import))。 日誌將列出已刪除的產品。
1. [推廣](/help/commerce/cif-classic/administering/generic.md#rolling-out-a-catalog) 相應的目錄。 產品和產品頁面將從內部刪除AEM。

   例如：

   * 開啟:

      [http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris](http://localhost:4502/aem/catalogs.html/content/catalogs/geometrixx-outdoors-hybris)

   * 推廣 `Hybris Base` 目錄
   * 開啟:

      [http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html](http://localhost:4502/editor.html/content/geometrixx-outdoors/en_US/equipment/biking.html)

   * 的 `Cajamara` 產品將從 `Bike` 類別

1. 要重新聲明產品，請執行以下操作：

   1. 在hybris中，將批准狀態設定回 **批准**
   1. 在AEM:

      1. 執行增量更新
      1. 再次部署適當的目錄
      1. 刷新相應類別頁

## 將訂單歷史記錄特性添加到客戶端上下文 {#add-order-history-trait-to-the-client-context}

將訂單歷史記錄添加到 [客戶端上下文](/help/sites-developing/client-context.md):

1. 開啟 [客戶端上下文設計頁](/help/sites-administering/client-context.md)，按以下任一：

   * 開啟要編輯的頁面，然後使用 **Ctrl-Alt-c** （窗口）或 **控制選項 — c** (Mac) 使用客戶端上下文左上角的鉛筆表徵圖 **開啟ClientContext設計頁**。
   * 直接導航到 [http://localhost:4502/etc/clientcontext/default/content.html](http://localhost:4502/etc/clientcontext/default/content.html)

1. [添加 **訂單歷史記錄** 元件](/help/sites-administering/client-context.md#adding-a-property-component) 到 **購物車** t客戶端上下文的元件。
1. 您可以確認客戶端上下文顯示了訂單歷史記錄的詳細資訊。 例如：

   1. 開啟 [客戶端上下文](/help/sites-administering/client-context.md)。
   1. 將物料添加到購物車。
   1. 完成簽出。
   1. 檢查客戶端上下文。
   1. 向購物車中添加其他物料。
   1. 導航到簽出頁：

      * 客戶端上下文顯示訂單歷史記錄的摘要。
      * 將顯示「您是退回客戶」消息。

   >[!NOTE]
   >
   >消息通過以下方式實現：
   >
   >* 導航到 [http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html](http://localhost:4502/content/campaigns/geometrixx-outdoors/hybris-returning-customer.html)
   >
   >  這次活動只有一次經歷。
   >
   >* 按一下段([http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html](http://localhost:4502/etc/segmentation/geometrixx-outdoors/returning-customer.html))
   >
   >* 該段使用 **訂單歷史記錄屬性** 特質。

