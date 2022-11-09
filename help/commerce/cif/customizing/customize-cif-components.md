---
title: 自訂CIF核心元件
description: 了解如何自訂AEM CIF核心元件。 本教學課程說明如何安全地擴充CIF核心元件，以符合業務特定需求。 了解如何延伸GraphQL查詢，以傳回自訂屬性，並在CIF核心元件中顯示新屬性。
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
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '2592'
ht-degree: 1%

---

# 自訂AEM CIF核心元件 {#customize-cif-components}

此 [CIF Venia項目](https://github.com/adobe/aem-cif-guides-venia) 是使用的參考程式碼基底 [CIF核心元件](https://github.com/adobe/aem-core-cif-components). 在本教學課程中，您將進一步擴充 [Product Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) 元件以顯示Adobe Commerce的自訂屬性。 您也將進一步了解AEM與Adobe Commerce之間的GraphQL整合，以及CIF核心元件提供的擴充功能鈎點。

>[!TIP]
>
>使用 [AEM專案原型](https://github.com/adobe/aem-project-archetype) 開始您自己的商務實作時。

## 您要建置的

Venia品牌最近開始使用可持續材料製造一些產品，而企業想要展示 **生態友好** 徽章作為Product Teaser的一部分。 系統會在Adobe Commerce中建立新的自訂屬性，以指出產品是否使用 **生態友好** 材料。 然後，此自訂屬性將會新增為GraphQL查詢的一部分，並顯示在指定產品的產品預告上。

![Eco友好徽章最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 必備條件 {#prerequisites}

完成本教學課程需要本機開發環境。 這包括已設定並連線至Adobe Commerce執行個體的AEM執行個體。 檢閱 [使用AEM設定本機開發](../develop.md). 若要完整遵循本教學課程，您需要權限才能新增 [產品屬性](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) 在Adobe Commerce。

您還需要GraphQL IDE，例如 [GraphiQL](https://github.com/graphql/graphiql) 或是執行程式碼範例和教學課程的瀏覽器擴充功能。 如果您安裝瀏覽器擴充功能，請確定它能設定要求標題。 在Google Chrome上， [Altair GraphQL客戶端](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) 是可執行工作的擴充功能。

## 複製Venia專案 {#clone-venia-project}

我們將複製 [韋尼亞項目](https://github.com/adobe/aem-cif-guides-venia) 然後覆寫預設樣式。

>[!NOTE]
>
>**歡迎使用現有專案** (根據包含CIF的AEM專案原型)，並略過本節。

1. 執行下列git命令以複製專案：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 建立專案並部署至AEM的本機執行個體：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 新增必要的OSGi設定，將您的AEM例項連線至Adobe Commerce例項，或將設定新增至新建立的專案。

1. 此時，您應該擁有連接至Adobe Commerce執行個體之店面的有效版本。 導覽至 `US` > `Home` 頁面： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html).

   您應該會看到店面目前使用Venia主題。 展開店面的「主功能表」時，您應該會看到各種類別，指出與Adobe Commerce的連線正在運作。

   ![Venia主題配置的店面](../assets/customize-cif-components/venia-store-configured.png)

## 製作Product Teaser {#author-product-teaser}

本教學課程將擴充產品預告元件。 首先，將產品預告的新例項新增至首頁，以了解基線功能。

1. 導覽至 **首頁** (位於： [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. 插入新 **Product Teaser** 元件放入頁面上的主版面容器中。

   ![插入Product Teaser](../assets/customize-cif-components/product-teaser-add-component.png)

3. 展開「側面板」（如果尚未切換），並將資產尋找器下拉式清單切換為 **產品**. 這應該會顯示連線Adobe Commerce執行個體的可用產品清單。 選取產品和 **拖放** 在 **Product Teaser** 元件。

   ![拖放產品預告](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   >注意，您也可以使用對話方塊來設定元件(按一下 _扳手_ 圖示)。

4. 您現在應該會看到產品預告顯示。 產品名稱和產品價格是顯示的預設屬性。

   ![Product Teaser — 預設樣式](../assets/customize-cif-components/product-teaser-default-style.png)

## 在Adobe Commerce中新增自訂屬性 {#add-custom-attribute}

AEM中顯示的產品和產品資料會儲存在Adobe Commerce中。 接下來，為 **生態友好** 做為產品屬性集的一部分，請使用Adobe Commerce UI。

>[!TIP]
>
>已有自訂 **是/否** 屬性，作為產品屬性集的一部分？ 歡迎使用，並略過本節。

1. 登入Adobe Commerce執行個體。
1. 導覽至 **目錄** > **產品**.
1. 更新搜尋篩選器以尋找 **可設定產品** 在先前練習中新增至Teaser元件時使用。 在編輯模式中開啟產品。

   ![搜尋有效產品](../assets/customize-cif-components/search-valeria-product.png)

1. 在產品檢視中，按一下 **新增屬性** > **建立新屬性**.
1. 填寫 **新屬性** 表單中包含下列值（保留其他值的預設設定）

   | 欄位集 | 欄位標籤 | 值 |
   | ----------------------------- | ------------------ | ---------------- |
   | 屬性屬性 | 屬性標籤 | **生態友好** |
   | 屬性屬性 | 目錄輸入類型 | **是/否** |
   | 進階屬性 | 屬性代碼 | **eco_friendly** |

   ![新屬性表單](../assets/customize-cif-components/attribute-new-form.png)

   按一下 **儲存屬性** 完成時。

1. 捲動至產品底部，然後展開 **屬性** 標題。 您應該會看到新的 **生態友好** 欄位。 將切換開關切換為 **是**.

   ![切換為「是」](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **儲存** 產品的變更。

   >[!TIP]
   >
   >有關管理的更多詳細資訊 [可在Adobe Commerce使用手冊中找到產品屬性](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html).

1. 導覽至 **系統** > **工具** > **快取管理**. 由於資料結構已更新，因此我們需要使Adobe Commerce中的某些快取類型失效。
1. 勾選旁邊的方塊 **設定** 並提交快取類型 **重新整理**

   ![刷新配置快取類型](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   >有關的更多詳細資訊 [快取管理可在Adobe Commerce使用手冊中找到](https://docs.magento.com/user-guide/system/cache-management.html).

## 使用GraphQL IDE驗證屬性 {#use-graphql-ide}

跳入AEM程式碼前，請先探索 [Adobe Commerce GraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) 使用GraphQL IDE。 Adobe Commerce與AEM的整合主要是透過一系列GraphQL查詢完成。 了解和修改GraphQL查詢是擴充CIF核心元件的關鍵方式之一。

接下來，使用GraphQL IDE驗證 `eco_friendly` 屬性已新增至產品屬性集。 本教學課程中的螢幕擷取畫面使用 [Altair GraphQL客戶端](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja).

1. 開啟GraphQL IDE並輸入URL `http://<server>/graphql` 在IDE或擴展的URL欄中。
2. 新增下列項目 [產品查詢](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) where `YOUR_SKU` 是 **SKU** 上次練習中使用的產品：

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

3. 執行查詢，您應得到如下的回應：

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

   ![範例GraphQL回應](../assets/customize-cif-components/sample-graphql-query.png)

   請注意， **是** 是整數 **1**. 以Java編寫GraphQL查詢時，此功能會相當實用。

   >[!TIP]
   >
   >有關 [Adobe Commerce GraphQL位於此處](https://devdocs.magento.com/guides/v2.4/graphql/index.html).

## 更新Product Teaser的Sling模型 {#updating-sling-model-product-teaser}

接下來，我們將實作Sling模型，以擴充Product Teaser的商業邏輯。 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)，是註解導向的「POJO」（純舊Java對象），可實施元件所需的任何業務邏輯。 Sling模型與HTL指令碼搭配使用，是元件的一部分。 我們將遵循 [Sling模型的委派模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) 這樣我們就可以擴展現有產品預告模型的部分。

Sling模型以Java方式實作，可在 **核心** 生成項目的模組。

使用 [您選擇的IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#set-up-the-development-ide) 匯入Venia專案。 使用的螢幕擷取畫面來自 [Visual Studio代碼IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?#microsoft-visual-studio-code).

1. 在IDE中，導航 **核心** 模組至： `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`.

   ![核心位置IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` 是可擴充CIF的Java介面 [ProductTeaser](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) 介面。

   已新增新方法，命名為 `isShowBadge()` 以在產品被視為「新」時顯示徽章。

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

   這是我們將引入的一種新方法，用來封裝邏輯，以指出產品是否具有 `eco_friendly` 屬性設定為 **是** 或 **否**.

1. 接下來，檢查 `MyProductTeaserImpl.java` at `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`.

   此 [Sling模型的委派模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) allows `MyProductTeaserImpl` 參考 `ProductTeaser` 模型 `sling:resourceSuperType` 屬性：

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   對於我們不想覆寫或變更的所有方法，我們只需傳回 `ProductTeaser` 傳回。 例如：

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   這可將實施需要寫入的Java程式碼量降至最低。

1. AEM CIF核心元件提供的額外擴充點之一，是 `AbstractProductRetriever` 可存取特定產品屬性。 Inspect `initModel()` 方法：

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

   此 `@PostConstruct` annotation可確保Sling模型初始化後立即調用此方法。

   請注意，產品GraphQL查詢已使用 `extendProductQueryWith` 擷取其他 `created_at` 屬性。 此屬性稍後會作為 `isShowBadge()` 方法。

1. 更新GraphQL查詢以包括 `eco_friendly` 屬性：

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

   新增至 `extendProductQueryWith` 方法是確保模型其餘部分可使用其他產品屬性的強大方法。 它也會將執行的查詢數量降至最低。

   在上述程式碼中，`addCustomSimpleField` 用於擷取 `eco_friendly` 屬性。 這說明如何查詢屬於Adobe Commerce結構的任何自訂屬性。

   >[!NOTE]
   >
   >此 `createdAt()` 方法已作為 [產品介面](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java). 大部分常見的結構屬性都已實作，因此僅使用 `addCustomSimpleField` ，以真正自訂屬性。

1. 新增記錄器以協助偵錯Java程式碼：

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

   在上述方法中， `productRetriever` 用於擷取產品，而 `getAsInteger()` 方法來取得 `eco_friendly` 屬性。 根據我們先前執行的GraphQL查詢，我們知道當 `eco_friendly` 屬性設為「**是**&quot;實際上是整數 **1**.

   現在Sling模型已更新，需要更新元件標籤，才能實際顯示 **生態友好** 以Sling模型為基礎。

## 自訂Product Teaser的標籤 {#customize-markup-product-teaser}

AEM元件的常見擴充功能是修改元件產生的標籤。 這是透過覆寫 [HTL指令碼](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 元件用來呈現其標籤的資訊。 HTML範本語言(HTL)是一種精簡的範本語言，AEM元件可用來根據撰寫的內容動態轉譯標籤，以允許重複使用元件。 例如，產品預告可反複重複使用，以顯示不同的產品。

在此情況下，我們想在預告頂端呈現橫幅，以根據自訂屬性指出產品為「生態友好」。 的設計模式 [自定義標籤](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) 元件的標準實際上是所有AEM元件的標準，而不只是AEM CIF核心元件。

>[!NOTE]
>
>如果您使用CIF產品和類別選擇器（例如此產品預告）或CIF頁面元件來自訂元件，請務必納入必要項目 `cif.shell.picker` 元件對話方塊的clientlib 。 請參閱 [CIF產品和類別選擇器的使用](use-cif-pickers.md) 以取得詳細資訊。

1. 在IDE中，導航並展開 `ui.apps` 模組，然後展開資料夾階層以： `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` 檢查 `.content.xml` 檔案。

   ![Product Teaser ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   以上是專案中產品預告元件的元件定義。 請注意屬性 `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`. 這是建立 [代理元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html#create-proxy-components). 我們不必從AEM CIF核心元件複製並貼上所有產品預告HTL指令碼，而是可以使用 `sling:resourceSuperType` 繼承所有功能。

1. 開啟檔案 `productteaser.html`. 這是 `productteaser.html` 檔案 [CIF Product Teaser](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

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

   請注意， `MyProductTeaser` 已使用並指派給 `product` 變數。

1. 修改 `productteaser.html` 對 `isEcoFriendly` 先前練習中實作的方法：

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

   在HTL中呼叫Sling模型方法時，請 `get` 和 `is` 該方法的一部分被丟棄，第一字母被小寫。 So `isShowBadge()` com `.showBadge` 和 `isEcoFriendly` com `.ecoFriendly`. 根據傳回的布林值 `.isEcoFriendly()` 決定 `<span>Eco Friendly</span>` 的下界。

   有關 `data-sly-test` 其他 [您可在此處找到HTL區塊陳述式](https://experienceleague.adobe.com/docs/experience-manager-htl/content/specification.html).

1. 使用Maven技能，從命令列終端儲存變更並將更新部署至AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 開啟新的瀏覽器視窗，並導覽至AEM和 **OSGi主控台** > **狀態** > **Sling模型**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. 搜尋 `MyProductTeaserImpl` 您應該會看到如下的行：

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   這表示Sling模型已正確部署並對應至正確的元件。

1. 重新整理至 **韋尼亞首頁** at [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) 新增Product Teaser的位置。

   ![顯示「生態友好」消息](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   如果產品具有 `eco_friendly` 屬性設定為 **是**，您應該會在頁面上看到「生態友好」文字。 嘗試切換至不同的產品，以查看行為變更。

1. 下一步開啟AEM `error.log` 查看我們添加的log語句。 此 `error.log` 位於 `<AEM SDK Install Location>/crx-quickstart/logs/error.log`.

   搜尋AEM記錄檔，以查看Sling模型中新增的記錄陳述式：

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   >如果預告中使用的產品沒有 `eco_friendly` 屬性，作為屬性集的一部分。

## 為Eco友好徽章添加樣式 {#add-styles}

此時，何時顯示 **生態友好** 徽章正常運作，但純文字可能使用某些樣式。 接下來，在 `ui.frontend` 模組來完成實作。

1. 下載 [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) 檔案。 這將用作 **生態友好** 徽章。
1. 返回IDE並導航到 `ui.frontend` 檔案夾。
1. 新增 `eco_friendly.svg` 檔案 `ui.frontend/src/main/resources/images` 資料夾：

   ![新增生態友好SVG](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. 開啟檔案 `productteaser.scss` at `ui.frontend/src/main/styles/commerce/_productteaser.scss`.
1. 在 `.productteaser` 類別：

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
   >結帳 [樣式CIF核心元件](./style-cif-component.md) 如需前端工作流程的詳細資訊。

1. 使用Maven技能，從命令列終端儲存變更並將更新部署至AEM:

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 重新整理至 **韋尼亞首頁** at [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) 新增Product Teaser的位置。

   ![Eco友好徽章最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 恭喜 {#congratulations}

您剛自訂了第一個AEM CIF元件！ 下載 [已完成的解決方案檔案在此處](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip).

## 獎金挑戰 {#bonus-challenge}

檢閱 **新增** 已在Product Teaser中實作的徽章。 嘗試新增其他核取方塊，讓作者控制 **生態友好** 徽章。 您需要更新元件對話方塊，位於 `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`.

![新徽章實作挑戰](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## 其他資源 {#additional-resources}

- [AEM原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html)
- [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)
- [自訂AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [自訂核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
- [開始使用AEM Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)
- [CIF產品和類別選擇器的使用](use-cif-pickers.md)
