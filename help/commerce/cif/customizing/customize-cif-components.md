---
title: 自訂CIF核心元件
description: 瞭解如何自訂Adobe Experience Manager CIF核心元件。 本教學課程涵蓋如何安全地擴充CIF核心元件，以符合特定企業的需求。 瞭解如何延伸GraphQL查詢以傳回自訂屬性，並在CIF核心元件中顯示新屬性。
sub-product: Commerce
topics: Development
version: Cloud Service
doc-type: tutorial
activity: develop
audience: developer
feature: Commerce Integration Framework
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
exl-id: 8933942e-be49-49d3-bf0a-7225257e2803
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '2567'
ht-degree: 2%

---

# 自訂Adobe Experience Manager CIF核心元件 {#customize-cif-components}

此 [CIF Venia專案](https://github.com/adobe/aem-cif-guides-venia) 是用於的參考程式碼基底 [CIF核心元件](https://github.com/adobe/aem-core-cif-components). 在本教學課程中，您將進一步延伸 [產品Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) 元件以顯示來自Adobe Commerce的自訂屬性。 您也將深入瞭解Adobe Experience Manager (AEM)與Adobe Commerce之間的GraphQL整合，以及CIF核心元件提供的擴充功能勾點。

>[!TIP]
>
>使用 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 當您開始自己的commerce實作時。

## 您將建置的內容

Venia品牌最近開始使用永續性材料來製造某些產品，而企業想要展示 **環保型** 徽章，產品Teaser的一部分。 在Adobe Commerce中建立新的自訂屬性，以指出產品是否使用 **環保型** 材質。 此自訂屬性會新增為GraphQL查詢的一部分，並顯示在指定產品的產品Teaser上。

![Eco Friendly Badge最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 先決條件 {#prerequisites}

本機開發環境是完成本教學課程的必要條件。 這包括已設定並連線至Adobe Commerce執行個體的AEM執行個體。 檢閱的需求和步驟 [使用AEM設定本機開發](../develop.md). 若要完全按照本教學課程操作，您需要許可權才能新增 [產品的屬性](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) 在Adobe Commerce中。

您還需要GraphQL IDE，例如 [GraphiQL](https://github.com/graphql/graphiql) 或瀏覽器擴充功能來執行程式碼範例和教學課程。 如果您安裝瀏覽器擴充功能，請確定它可設定請求標頭。 在Google Chrome上， [Altair GraphQL使用者端](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) 是可執行此工作的擴充功能。

## 原地複製Venia專案 {#clone-venia-project}

您將複製 [Venia專案](https://github.com/adobe/aem-cif-guides-venia) 然後覆寫預設樣式。

>[!NOTE]
>
>**您可以隨意使用現有的專案** (根據包含CIF的AEM專案原型)並略過本節。

1. 執行下列git命令以複製專案：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 建立專案並將其部署到AEM的本機執行個體：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 新增必要的OSGi設定以將您的AEM執行個體連線到Adobe Commerce執行個體，或將設定新增到新建立的專案。

1. 此時，您應該有已連線至Adobe Commerce執行個體的有效店面版本。 導覽至 `US` > `Home` 頁面位置： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   您應該會看到店面目前使用Venia佈景主題。 展開店面的「主要」功能表，應該會看到各種類別，表示與Adobe Commerce的連線正常運作。

   ![使用Venia佈景主題設定的店面](../assets/customize-cif-components/venia-store-configured.png)

## 編寫產品Teaser {#author-product-teaser}

產品Teaser元件在本教學課程中皆已擴充。 首先，將產品Teaser的執行個體新增到首頁以瞭解基準功能。

1. 導覽至 **首頁** 網站的： [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. 插入新專案 **產品Teaser** 元件放入頁面上的主版面容器中。

   ![插入產品Teaser](../assets/customize-cif-components/product-teaser-add-component.png)

3. 展開「側面板」（如果尚未切換），然後將「資產尋找器」下拉式清單切換至 **產品**. 這應該會顯示已連線之Adobe Commerce執行個體的可用產品清單。 選取產品並 **拖放** 它登入 **產品Teaser** 元件時。

   ![拖放產品Teaser](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   >注意，您也可以使用對話方塊(按一下 _扳手_ 圖示)。

4. 您現在應該會看到產品Teaser顯示的產品。 產品的「名稱」和產品的「價格」是顯示的預設屬性。

   ![產品Teaser — 預設樣式](../assets/customize-cif-components/product-teaser-default-style.png)

## 在Adobe Commerce中新增自訂屬性 {#add-custom-attribute}

AEM中顯示的產品和產品資料儲存在Adobe Commerce中。 接著，新增屬性 **環保型** 做為使用Adobe Commerce UI設定的產品屬性的一部分。

>[!TIP]
>
>已有自訂 **是/否** 屬性是否屬於產品屬性集？ 歡迎您隨時使用，並略過本節。

1. 登入您的Adobe Commerce執行個體。
1. 瀏覽至 **目錄** > **產品**.
1. 更新搜尋篩選器以尋找 **可設定的產品** 用於上一個練習中新增至Teaser元件時。 在編輯模式中開啟產品。

   ![搜尋Valeria產品](../assets/customize-cif-components/search-valeria-product.png)

1. 在產品檢視中，按一下 **新增屬性** > **建立新屬性**.
1. 填寫 **新增屬性** 表單的預設值（保留其他值的預設設定）

   | 欄位集 | 欄位標籤 | 值 |
   | ----------------------------- | ------------------ | ---------------- |
   | 屬性屬性 | 屬性標籤 | **環保型** |
   | 屬性屬性 | 目錄輸入型別 | **是/否** |
   | 進階屬性特性 | 屬性代碼 | **eco_friendly** |

   ![新增屬性表單](../assets/customize-cif-components/attribute-new-form.png)

   按一下 **儲存屬性** 完成後。

1. 捲動至產品底部並展開 **屬性** 標題。 您應該會看到新的 **環保型** 欄位。 切換至 **是**.

   ![切換切換為是](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **儲存** 產品的變更。

   >[!TIP]
   >
   >有關管理的更多詳細資料 [您可以在Adobe Commerce使用手冊中找到產品屬性](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html).

1. 瀏覽至 **系統** > **工具** > **快取管理**. 由於資料結構已更新，因此您必須使Adobe Commerce中的部分快取型別失效。
1. 勾選「 」旁的方塊 **設定** 並提交快取型別 **重新整理**

   ![重新整理組態快取型別](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   >更多關於以下內容的詳細資訊： [快取管理可在Adobe Commerce使用手冊中找到](https://docs.magento.com/user-guide/system/cache-management.html).

## 使用GraphQL IDE驗證屬性 {#use-graphql-ide}

在跳入AEM程式碼之前，探索 [Adobe Commerce GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) 使用GraphQL IDE。 Adobe Commerce與AEM的整合主要是透過一系列GraphQL查詢來完成。 瞭解並修改GraphQL查詢是擴充CIF核心元件的重要方式之一。

接下來，使用GraphQL IDE來驗證 `eco_friendly` 屬性已新增至產品屬性集。 本教學課程中的熒幕擷取畫面使用 [Altair GraphQL使用者端](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. 開啟GraphQL IDE並輸入URL `http://<server>/graphql` 在IDE或擴充功能的URL列中。
2. 新增下列專案 [產品查詢](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) 位置 `YOUR_SKU` 是 **SKU** 上一個練習使用的產品：

   ```json
     {
       products(
       filter: { sku: { eq: "YOUR_SKU" } }
       ) {
           items {
           name
           sku
           eco_friendly
           }
       }
   }
   ```

3. 執行查詢，您應該會收到如下的回應：

   ```json
   {
     "data": {
       "products": {
         "items": [
           {
             "name": "Valeria Two-Layer Tank",
             "sku": "VT11",
             "eco_friendly": 1
           }
         ]
       }
     }
   }
   ```

   ![GraphQL回應範例](../assets/customize-cif-components/sample-graphql-query.png)

的值 **是** 為的整數 **1**. 當您使用Java™撰寫GraphQL查詢時，這會很有用。

>[!TIP]
>
>更多有關以下內容的詳細檔案： [您可以在此處找到Adobe Commerce GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## 更新產品Teaser的Sling模型 {#updating-sling-model-product-teaser}

接下來，您將實作Sling模型以擴充產品Teaser的商業邏輯。 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)是註解導向的「POJO」(純舊Java™物件)，可實作元件所需的任何商業邏輯。 Sling模型會搭配HTL指令碼使用作為元件的一部分。 您將遵循 [Sling模型的委派模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) 以便您能延伸現有「產品Teaser」模型的零件。

Sling模型會實作為Java™，且可在以下網址找到： **核心** 所產生專案的模組。

使用 [您選擇的IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#set-up-the-development-ide) 匯入Venia專案。 使用的熒幕擷取畫面來自 [Visual Studio Code IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?#microsoft-visual-studio-code).

1. 在IDE中，瀏覽至 **核心** 模組至： `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![核心位置IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` 是擴充CIF的Java™介面 [產品預告](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) 介面。

   已新增名為的新方法 `isShowBadge()` 以在產品視為「新」時顯示徽章。

1. 新增方法， `isEcoFriendly()` 至介面：

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

這是封裝邏輯的新方法，可指出產品是否具有 `eco_friendly` 屬性設定為 **是** 或 **否**.

1. 接下來，檢查 `MyProductTeaserImpl.java` 在 `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   此 [Sling模型的委派模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) 允許 `MyProductTeaserImpl` 以參照 `ProductTeaser` 模型透過 `sling:resourceSuperType` 屬性：

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   對於未覆寫或變更的所有方法，您可以傳回 `ProductTeaser` 會傳回。 例如：

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   這會讓實作必須寫入的Java™程式碼減到最少。

1. AEM CIF核心元件提供的額外擴充功能點之一是 `AbstractProductRetriever` 可讓您存取特定產品屬性。 Inspect `initModel()` 方法：

   ```java
   import javax.annotation.PostConstruct;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
       ...
       private AbstractProductRetriever productRetriever;
   
       /* add this method to intialize the proudctRetriever */
       @PostConstruct
       public void initModel() {
           productRetriever = productTeaser.getProductRetriever();
   
           if (productRetriever != null) {
               productRetriever.extendProductQueryWith(p -> p.createdAt());
           }
   
       }
   ...
   ```

   此 `@PostConstruct` 註解可確保在Sling模型初始化時呼叫此方法。

   請注意，產品GraphQL查詢已使用 `extendProductQueryWith` 擷取其他專案的方法 `created_at` 屬性。 此屬性稍後會用作 `isShowBadge()` 方法。

1. 更新GraphQL查詢以包含 `eco_friendly` 部分查詢中的屬性：

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p -> p
               .createdAt()
               .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
           );
       }
   }
   ```

   將新增至 `extendProductQueryWith` 方法是一種強大的方式，可確保模型的其餘部分都可以使用其他產品屬性。 它也會將執行的查詢數減到最少。

   在上述程式碼中，`addCustomSimpleField` 用於擷取 `eco_friendly` 屬性。 這說明了如何查詢屬於Adobe Commerce結構描述的任何自訂屬性。

   >[!NOTE]
   >
   >此 `createdAt()` 方法已實作為 [產品介面](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java). 大部分常見的結構描述屬性均已實作，因此僅使用 `addCustomSimpleField` 以取得真正自訂的屬性。

1. 新增記錄器以協助偵錯Java™程式碼：

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. 接下來，實作 `isEcoFriendly()` 方法：

   ```java
   @Override
   public Boolean isEcoFriendly() {
   
       Integer ecoFriendlyValue;
       try {
           ecoFriendlyValue = productRetriever.fetchProduct().getAsInteger(ECO_FRIENDLY_ATTRIBUTE);
           if(ecoFriendlyValue != null && ecoFriendlyValue.equals(Integer.valueOf(1))) {
               LOGGER.info("*** Product is Eco Friendly**");
               return true;
           }
       } catch (SchemaViolationError e) {
           LOGGER.error("Error retrieving eco friendly attribute");
       }
       LOGGER.info("*** Product is not Eco Friendly**");
       return false;
   }
   ```

   在上述方法中， `productRetriever` 用於擷取產品和 `getAsInteger()` 方法用來取得 `eco_friendly` 屬性。 根據您先前執行的GraphQL查詢，您知道當 `eco_friendly` 屬性已設定為&quot;**是**&quot;實際上是整數， **1**.

   現在Sling模型已更新，需要更新元件標籤以實際顯示指標 **環保型** 根據Sling模型。

## 自訂產品Teaser的標籤 {#customize-markup-product-teaser}

AEM元件的常見擴充功能是修改元件產生的標籤。 覆寫 [HTL指令碼](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 元件用來呈現其標籤的專案。 HTML範本語言(HTL)是一種輕量型的範本語言，AEM元件會使用它來根據編寫的內容動態呈現標籤，並允許元件重複使用。 例如，產品Teaser可以重複使用以顯示不同的產品。

在此案例中，您想要在Teaser上方呈現橫幅，以根據自訂屬性指出產品是「環保的」。 的設計模式 [自訂標籤](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) 實際上元件是所有AEM元件的標準，而不僅僅是AEM CIF核心元件。

>[!NOTE]
>
>如果您使用CIF產品和類別選擇器(例如此產品Teaser或CIF頁面元件)來自訂元件，請務必包含必要的 `cif.shell.picker` 元件對話方塊的clientlib。 另請參閱 [CIF產品和類別選擇器的使用情況](use-cif-pickers.md) 以取得詳細資訊。

1. 在IDE中，瀏覽並展開 `ui.apps` 模組，並將資料夾階層展開至： `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` 並檢查 `.content.xml` 檔案。

   ![產品預告ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   此專案中產品Teaser元件的元件定義位於上面。 注意屬性 `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. 此為建立 [Proxy元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html#create-proxy-components). AEM CIF您可以使用 `sling:resourceSuperType` 以繼承所有功能。

1. 開啟檔案 `productteaser.html`. 這是 `productteaser.html` 來自的檔案 [CIF產品Teaser](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

   ```html
   <!--/* productteaser.html */-->
   <sly
     data-sly-use.product="com.venia.core.models.commerce.MyProductTeaser"
     data-sly-use.templates="core/wcm/components/commons/v1/templates.html"
     data-sly-use.actionsTpl="actions.html"
     data-sly-test.isConfigured="${properties.selection}"
     data-sly-test.hasProduct="${product.url}"
   ></sly>
   ```

   請注意，的Sling模型 `MyProductTeaser` 已使用並指派給 `product` 變數中。

1. 修改 `productteaser.html` 以呼叫 `isEcoFriendly` 上一個練習實作的方法：

   ```html
   ...
   <div
     data-sly-test="${isConfigured && hasProduct}"
     class="item__root"
     data-cmp-is="productteaser"
     data-virtual="${product.virtualProduct}"
   >
     <div data-sly-test="${product.showBadge}" class="item__badge">
       <span>${properties.text || 'New'}</span>
     </div>
     <!--/* Insert call to Eco Friendly here */-->
     <div data-sly-test="${product.ecoFriendly}" class="item__eco">
       <span>Eco Friendly</span>
     </div>
     ...
   </div>
   ```

   在HTL中呼叫Sling模型方法時 `get` 和 `is` 方法的部分會被捨棄，第一個字母會變為小寫。 所以 `isShowBadge()` 變為 `.showBadge` 和 `isEcoFriendly` 變為 `.ecoFriendly`. 根據傳回的布林值 `.isEcoFriendly()` 判斷此專案是否 `<span>Eco Friendly</span>` 隨即顯示。

   更多關於 `data-sly-test` 和其他 [您可以在此處找到HTL區塊陳述式](https://experienceleague.adobe.com/docs/experience-manager-htl/content/specification.html).

1. 從命令列終端機，使用Maven技能儲存變更並將更新部署到AEM：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 開啟新的瀏覽器視窗，並導覽至AEM與 **OSGi控制檯** > **狀態** > **Sling模型**： [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. 搜尋 `MyProductTeaserImpl` 而且您應該會看到類似以下的一行：

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   這表示Sling模型已正確部署並對應至正確的元件。

1. 重新整理至 **Venia首頁** 在 [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) 新增產品Teaser的位置。

   ![顯示環保訊息](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   如果產品具有 `eco_friendly` 屬性設定為 **是**，您應該會在頁面上看到「生態友好」文字。 請嘗試切換至不同的產品，以檢視行為變更。

1. 接著，開啟AEM `error.log` 檢視新增的記錄陳述式。 此 `error.log` 位於 `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   搜尋AEM記錄檔以檢視已在Sling模型中新增的記錄檔陳述式：

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   >如果Teaser中使用的產品沒有 `eco_friendly` 屬性作為其屬性集的一部分。

## 新增環保徽章的樣式 {#add-styles}

此時，顯示「 」的時機邏輯 **環保型** 徽章正在運作，但純文字可以使用某些樣式。 接著，將圖示和樣式新增至 `ui.frontend` 完成實作的模組。

1. 下載 [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) 檔案。 此專案用作 **環保型** 徽章。
1. 返回IDE並瀏覽至 `ui.frontend` 資料夾。
1. 新增 `eco_friendly.svg` 檔案到 `ui.frontend/src/main/resources/images` 資料夾：

   ![新增環保型SVG](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. 開啟檔案 `productteaser.scss` 在 `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. 將下列Sass規則新增至 `.productteaser` 類別：

   ```scss
   .productteaser {
       ...
       .item__eco {
           width: 60px;
           height: 60px;
           left: 0px;
           overflow: hidden;
           position: absolute;
           padding: 5px;
   
       span {
           display: block;
           position: absolute;
           width: 45px;
           height: 45px;
           text-indent: -9999px;
           background: no-repeat center center url('../resources/images/eco_friendly.svg');
           }
       }
   ...
   }
   ```

   >[!NOTE]
   >
   >簽出 [設定CIF核心元件的樣式](./style-cif-component.md) 以取得有關前端工作流程的更多詳細資訊。

1. 從命令列終端機，使用Maven技能儲存變更並將更新部署到AEM：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 重新整理至 **Venia首頁** 在 [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) 新增產品Teaser的位置。

   ![Eco Friendly Badge最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 恭喜 {#congratulations}

您已自訂您的第一個AEM CIF元件！ 下載 [在這裡完成解決方案檔案](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## 額外挑戰 {#bonus-challenge}

檢閱的功能 **新增** 已在產品Teaser中實施的徽章。 嘗試新增額外的核取方塊讓作者控制 **環保型** 應顯示徽章。 您必須更新元件對話方塊： `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![新徽章實作挑戰](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## 其他資源 {#additional-resources}

- [AEM原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
- [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components)
- [自訂AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)
- [自訂核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
- [AEM Sites快速入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)
- [CIF產品和類別選擇器的使用情況](use-cif-pickers.md)
