---
title: 自訂CIF核心元件
description: 瞭解如何自訂AEMCIF核心元件。 本教學課程涵蓋如何安全地擴充CIF核心元件，以符合商業特定需求。 瞭解如何擴充GraphQL查詢以傳回自訂屬性，並在CIF核心元件中顯示新屬性。
sub-product: 商務
topics: Development
version: cloud-service
doc-type: tutorial
activity: develop
audience: developer
feature: 商務整合框架
kt: 4279
thumbnail: customize-aem-cif-core-component.jpg
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '2549'
ht-degree: 1%

---

# 定制AEMCIF核心元件{#customize-cif-components}

[CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia)是使用[CIF核心元件](https://github.com/adobe/aem-core-cif-components)的參考代碼庫。 在本教學課程中，您將進一步擴充[Product Teaser](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser)元件，以顯示來自Magento的自訂屬性。 您還將進一步瞭解GraphQL在與Magento之AEM間的整合以及CIF核心元件提供的擴展掛接。

>[!TIP]
>
> 啟動您自己的商務實AEM施時，請使用[Project archetype](https://github.com/adobe/aem-project-archetype)。

## 您將建立的

Venia品牌最近開始使用可持續材料製造某些產品，而企業想要在產品摘要中顯示&#x200B;**Eco Friendly**&#x200B;徽章。 將在Magento中建立新的自定義屬性，以指示產品是否使用&#x200B;**Eco friendly**&#x200B;材料。 然後，此自訂屬性會新增為GraphQL查詢的一部分，並顯示在指定產品的產品摘要中。

![環保徽章最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 必備條件 {#prerequisites}

完成本教學課程時，需要有本機開發環境。 這包括已配置並連AEM接到Magento實例的運行實例。 檢視[設定使用](../develop.md)進行本機開發的AEM需求和步驟。 要完全遵循本教程，您需要將[屬性添加到Magento中的Product](https://docs.magento.com/user-guide/catalog/product-attributes-add.html)中的權限。

您還需要GraphQL IDE（例如[GraphiQL](https://github.com/graphql/graphiql)）或瀏覽器擴展來運行代碼示例和教程。 如果您安裝瀏覽器擴充功能，請確定它能夠設定請求標題。 在Google Chrome上，[Altair GraphQL Client](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)是可執行工作的擴充功能。

## 克隆Venia Project {#clone-venia-project}

我們將仿製[Venia Project](https://github.com/adobe/aem-cif-guides-venia)，然後覆寫預設樣式。

>[!NOTE]
>
> **您可以隨意使用現有專案** (根據包含CIF的AEM「專案原型」)，並略過本節。

1. 執行下列git命令以複製專案：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 將專案建立並部署至下列的本機例AEM項：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 添加必要的OSGi配置，將實AEM例連接到Magento實例，或將配置添加到新建的項目。

1. 此時，您應該擁有連接至Magento實例的店面的工作版本。 導覽至`US` > `Home`頁面，網址為：[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

   您應該會看到，店面目前使用的是Venia主題。 展開店面的「主功能表」時，您應該會看到各種類別，指出連線Magento正在運作。

   ![使用Venia Theme配置的店面](../assets/customize-cif-components/venia-store-configured.png)

## 製作產品摘要{#author-product-teaser}

本教學課程將擴充產品摘要元件。 首先，將「產品摘要」的新例項新增至首頁，以瞭解基準功能。

1. 導覽至網站的&#x200B;**首頁**:[http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. 將新的&#x200B;**產品摘要**&#x200B;元件插入頁面的主版面容器。

   ![插入產品摘要](../assets/customize-cif-components/product-teaser-add-component.png)

3. 展開「側面板」（如果尚未切換），並將資產搜尋器下拉式清單切換至「產品」****。 這應該會顯示連線Magento例項中可用產品的清單。 選擇產品並將&#x200B;**drag+drop**&#x200B;拖放到頁面上的&#x200B;**產品摘要**&#x200B;元件上。

   ![拖放產品摘要](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   > 請注意，您也可以使用對話方塊設定元件，以設定顯示的產品（按一下&#x200B;_wrench_&#x200B;圖示）。

4. 您現在應該會看到產品摘要正在顯示產品。 產品名稱和產品價格是顯示的預設屬性。

   ![產品摘要——預設樣式](../assets/customize-cif-components/product-teaser-default-style.png)

## 在Magento{#add-custom-attribute}中添加自定義屬性

顯示在中的產品和產品數AEM據儲存在Magento中。 接著，使用MagentoUI新增&#x200B;**Eco Friendly**&#x200B;屬性，作為產品屬性集的一部分。

>[!TIP]
>
> 已有自訂&#x200B;**是／否**&#x200B;屬性做為產品屬性集的一部分？ 您可隨意使用，並略過本節。

1. 登入您的Magento實例。
1. 導覽至&#x200B;**Catalog** > **Products**。
1. 更新搜尋篩選器，以尋找在上一練習中新增至Teaser元件時使用的&#x200B;**Configurable Product**。 在編輯模式中開啟產品。

   ![搜尋Valeria產品](../assets/customize-cif-components/search-valeria-product.png)

1. 在產品視圖中，按一下「添加屬性」>「建立新屬性」。********
1. 使用下列值填寫&#x200B;**新屬性**&#x200B;表單（保留其他值的預設設定）

   | 欄位集 | 欄位標籤 | 值 |
   | ----------------------------- | ------------------ | ---------------- |
   | 屬性屬性 | 屬性標籤 | **環保** |
   | 屬性屬性 | 目錄輸入類型 | **是／否** |
   | 進階屬性屬性 | 屬性代碼 | **eco_friendly** |

   ![新屬性表單](../assets/customize-cif-components/attribute-new-form.png)

   完成後，按一下「保存屬性」。****

1. 捲動至產品底部並展開&#x200B;**Attributes**&#x200B;標題。 您應看到新的&#x200B;**Eco Friendly**&#x200B;欄位。 將切換切換為&#x200B;**Yes**。

   ![切換為yes](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **保** 存對產品的更改。

   >[!TIP]
   >
   > 有關管理[產品屬性的詳細資訊，請參閱Magento使用手冊](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html)。

1. 導航至&#x200B;**System** > **Tools** > **Cache Management**。 由於對資料模式進行了更新，因此我們需要使Magento中的某些快取類型失效。
1. 選中&#x200B;**Configuration**&#x200B;旁邊的框，並提交&#x200B;**Refresh**&#x200B;的快取類型

   ![刷新配置快取類型](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   > 有關[快取管理的詳細資訊，請參閱Magento使用手冊](https://docs.magento.com/user-guide/system/cache-management.html)。

## 使用GraphQL IDE驗證屬性{#use-graphql-ide}

在跳至程AEM式碼之前，使用GraphQL IDE來探索[MagentoGraphQL](https://devdocs.magento.com/guides/v2.4/graphql/)非常實用。 與的Magento集AEM成主要通過一系列GraphQL查詢完成。 瞭解和修改GraphQL查詢是擴展CIF核心元件的關鍵方法之一。

接下來，使用GraphQL IDE驗證`eco_friendly`屬性是否已添加到產品屬性集。 本教學課程中的截屏使用[Altair GraphQL客戶端](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)。

1. 開啟GraphQL IDE，然後在IDE或副檔名的URL欄中輸入URL `http://<magento-server>/graphql`。
2. 新增下列[products query](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html)，其中`YOUR_SKU`是前一練習中使用之產品的&#x200B;**SKU**:

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

3. 執行查詢，您應得到如下響應：

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

   ![GraphQL響應示例](../assets/customize-cif-components/sample-graphql-query.png)

   請注意，**Yes**&#x200B;的值是&#x200B;**1**&#x200B;的整數。 當我們使用Java編寫GraphQL查詢時，這將非常有用。

   >[!TIP]
   >
   > 有關[Magento圖QL的更詳細文檔，請參閱](https://devdocs.magento.com/guides/v2.4/graphql/index.html)。

## 更新Product Teaser {#updating-sling-model-product-teaser}的Sling Model

接下來，我們將透過實作Sling Model來擴充Product Teaser的商業邏輯。 [Sling Models](https://sling.apache.org/documentation/bundles/models.html)，是註解導向的&quot;POJOs&quot;(Plain Old Java Objects)，可實作元件所需的任何商業邏輯。Sling Models會與HTL指令碼搭配使用，做為元件的一部分。 我們將遵循Sling Models](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models)的[委派模式，以便我們只延伸現有產品摘要模型的部分。

Sling Models是以Java實作，可在產生的專案的&#x200B;**core**&#x200B;模組中找到。

使用您選擇的[IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#set-up-the-development-ide)來導入Venia項目。 使用的截屏來自[Visual Studio代碼IDE](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html#microsoft-visual-studio-code)。

1. 在IDE中，導航&#x200B;**core**&#x200B;模組下方的以：`core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`。

   ![核心位置IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` 是可擴充CIF ProductTeaser介面的Java [](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) 介面。

   已新增名為`isShowBadge()`的新方法，如果產品被視為「新」，則會顯示徽章。

1. 將`isEcoFriendly()`新方法添加到介面：

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   我們將引入一種新方法來封裝邏輯，以指出產品的`eco_friendly`屬性是設為&#x200B;**Yes**&#x200B;或&#x200B;**No**。

1. 接下來，檢查`core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`處的`MyProductTeaserImpl.java`。

   Sling Models](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models)的[委派模式允許`MyProductTeaserImpl`透過`sling:resourceSuperType`屬性參考`ProductTeaser`模型：

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   對於我們不想覆寫或變更的所有方法，我們只要傳回`ProductTeaser`傳回的值即可。 例如：

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   這可將實作所需的Java程式碼量減到最小。

1. CIF核心元件提供的額外擴展點之AEM一是`AbstractProductRetriever` ，它提供對特定產品屬性的訪問。 Inspect`initModel()`方法：

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

   `@PostConstruct`註解可確保在Sling Model初始化時，就會立即呼叫此方法。

   請注意，產品GraphQL查詢已使用`extendProductQueryWith`方法進行擴展，以檢索其他`created_at`屬性。 此屬性稍後會用作`isShowBadge()`方法的一部分。

1. 更新GraphQL查詢，將`eco_friendly`屬性包含在部分查詢中：

   ```java
   //MyProductTeaserImpl.java
   
   private static final String ECO_FRIENDLY_ATTRIBUTE = "eco_friendly";
   
   @PostConstruct
   public void initModel() {
       productRetriever = productTeaser.getProductRetriever();
   
       if (productRetriever != null) {
           productRetriever.extendProductQueryWith(p ->
                productRetriever.extendProductQueryWith(p -> p
                   .createdAt()
                   .addCustomSimpleField(ECO_FRIENDLY_ATTRIBUTE)
               );
           );
       }
   }
   ```

   添加到`extendProductQueryWith`方法是確保模型其餘部分可以使用其他產品屬性的有力方法。 它還將執行的查詢數減到最小。

   在上述代碼中，`addCustomSimpleField`用於檢索`eco_friendly`屬性。 這說明了如何查詢屬於Magento架構的任何自定義屬性。

   >[!NOTE]
   >
   > `createdAt()`方法實際上已作為[產品介面](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)的一部分實施。 大多數常見的架構屬性都已實作，因此僅針對真正的自訂屬性使用`addCustomSimpleField`。

1. 新增記錄器以協助除錯Java程式碼：

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. 接下來，實施`isEcoFriendly()`方法：

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

   在上述方法中，`productRetriever`用於讀取產品，而`getAsInteger()`方法用於獲取`eco_friendly`屬性的值。 根據我們先前運行的GraphQL查詢，我們知道當`eco_friendly`屬性設定為&quot;**Yes**&quot;時的預期值實際上是&#x200B;**1**&#x200B;的整數。

   現在Sling Model已經更新，Component標籤需要更新，才能根據Sling Model實際顯示&#x200B;**Eco Friendly**&#x200B;的指標。

## 自定義產品摘要{#customize-markup-product-teaser}的標籤

元件的一個常AEM見擴展是修改元件生成的標籤。 這是透過覆寫元件用來呈現其標籤的[HTL指令碼](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html)來完成的。 HTML範本語言(HTL)是輕量型範本語言，元AEM件可用來根據編寫的內容動態轉換標籤，讓元件可重複使用。 例如，「產品摘要」可重複使用，以顯示不同的產品。

在我們的案例中，我們想要在摘要上方呈現橫幅，以指出產品是以自訂屬性為基礎的「Eco Friendly」（環保）。 [自訂元件標籤](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup)的設計模式實際上是所有元件的標準，而AEM不只是AEMCIF核心元件。

1. 在IDE中，導航並展開`ui.apps`模組，然後將資料夾層次展開為：`ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser`並檢查`.content.xml`檔案。

   ![產品摘要ui.apps](../assets/customize-cif-components/product-teaser-ui-apps-ide.png)

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="http://sling.apache.org/jcr/sling/1.0" xmlns:cq="http://www.day.com/jcr/cq/1.0" xmlns:jcr="http://www.jcp.org/jcr/1.0"
       jcr:description="Product Teaser Component"
       jcr:primaryType="cq:Component"
       jcr:title="Product Teaser"
       sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"
       componentGroup="Venia - Commerce"/>
   ```

   以上是我們專案中產品摘要元件的元件定義。 請注意`sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`屬性。 這是建立[Proxy元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/using.html#create-proxy-components)的示例。 與其從AEMCIF核心元件複製和貼上所有產品摘要HTL指令碼，我們可以使用`sling:resourceSuperType`繼承所有功能。

1. 開啟檔案`productteaser.html`。 這是[CIF產品摘要](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)中`productteaser.html`檔案的副本

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

   請注意，`MyProductTeaser`的Sling Model已使用並指派給`product`變數。

1. 修改`productteaser.html`以調用在上一練習中實現的`isEcoFriendly`方法：

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

   當在HTL中呼叫Sling Model方法時，方法的`get`和`is`部分會被捨棄，而第一個字母會被小寫。 因此，`isShowBadge()`變為`.showBadge`,`isEcoFriendly`變為`.ecoFriendly`。 根據從`.isEcoFriendly()`返回的布爾值確定是否顯示`<span>Eco Friendly</span>`。

   有關`data-sly-test`和其他[HTL塊語句的詳細資訊，請參閱](https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html#test)。

1. 從命令列終端儲存變更並部AEM署更新，以使用您的Maven技能：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 開啟新的瀏覽器視窗並導AEM覽至&#x200B;**OSGi主控台** > **Status** > **Sling Models**:[http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. 搜尋`MyProductTeaserImpl`，您應看到如下所示的行：

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   這表示Sling Model已正確部署並對應至正確的元件。

1. 重新整理至已新增產品摘要之[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)的&#x200B;**Venia首頁**。

   ![顯示Eco友好消息](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   如果產品的`eco_friendly`屬性設為&#x200B;**Yes**，您應該會在頁面上看到「Eco Friendly」文字。 嘗試切換至不同的產品，以檢視行為變更。

1. 接著開啟AEM`error.log`，查看我們新增的log陳述式。 `error.log`位於`<AEM SDK Install Location>/crx-quickstart/logs/error.log`。

   搜尋記AEM錄檔，以查看Sling Model中新增的log陳述式：

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   > 如果摘要中使用的產品沒有作為屬性集的一部分的`eco_friendly`屬性，您也會看到一些堆棧跟蹤。

## 新增Eco友好徽章的樣式{#add-styles}

此時，顯示&#x200B;**Eco Friendly**&#x200B;徽章的邏輯正在運作，但純文字檔案可能使用某些樣式。 接著，在`ui.frontend`模組中新增圖示和樣式以完成實作。

1. 下載[eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg)檔案。 這將用作&#x200B;**Eco Friendly**&#x200B;徽章。
1. 返回IDE並導航至`ui.frontend`資料夾。
1. 將`eco_friendly.svg`檔案添加到`ui.frontend/src/main/resources/images`資料夾：

   ![新增環保SVG](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. 在`ui.frontend/src/main/styles/commerce/_productteaser.scss`開啟檔案`productteaser.scss`。
1. 在`.productteaser`類別中新增下列Sass規則：

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
   > 有關前端工作流程的詳細資訊，請參閱[樣式CIF核心元件](./style-cif-component.md)。

1. 從命令列終端儲存變更並部AEM署更新，以使用您的Maven技能：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallPackage,cloud
   ```

1. 重新整理至已新增產品摘要之[http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)的&#x200B;**Venia首頁**。

   ![環保徽章最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 恭喜{#congratulations}

您剛自訂了第一個AEMCIF元件！ 在這裡下載[完成的解決方案檔案](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip)。

## 獎金競賽{#bonus-challenge}

檢視已在產品摘要中實作的&#x200B;**New**&#x200B;徽章的功能。 嘗試新增額外的核取方塊，讓作者控制何時應顯示&#x200B;**Eco Friendly**&#x200B;徽章。 您需要更新`ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`處的元件對話框。

![全新徽章實作挑戰](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## 其他資源 {#additional-resources}

- [原AEM型](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)
- [AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components)
- [自訂AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [自訂核心元件](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/customizing.html)
- [開始使用AEM Sites](https://docs.adobe.com/content/help/zh-Hant/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)
