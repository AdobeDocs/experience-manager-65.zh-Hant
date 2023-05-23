---
title: 自定義CIF核心元件
description: 瞭解如何自定義AEMCIF核心元件。 本教程介紹如何安全擴展CIF核心元件以滿足業務特定要求。 瞭解如何擴展GraphQL查詢以返回自定義屬性並在CIF核心元件中顯示新屬性。
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
ht-degree: 2%

---

# 自定義AEMCIF核心元件 {#customize-cif-components}

的 [CIF韋尼亞項目](https://github.com/adobe/aem-cif-guides-venia) 是用於使用的參考代碼庫 [CIF核心元件](https://github.com/adobe/aem-core-cif-components)。 在本教程中，您將進一步擴展 [產品預告](https://github.com/adobe/aem-core-cif-components/tree/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser) 元件以顯示來自Adobe Commerce的自定義屬性。 您還將瞭解GraphQL與AEMAdobe Commerce的整合以及CIF核心元件提供的擴展掛接。

>[!TIP]
>
>使用 [項AEM目原型](https://github.com/adobe/aem-project-archetype) 啟動您自己的商業實施。

## 您將構建的

維尼亞品牌最近開始使用可持續材料製造一些產品，該公司希望展示 **生態友好** 作為產品預告的一部分。 將在Adobe Commerce建立一個新的自定義屬性，以指示產品是否使用 **生態友好** 材料。 然後，此自定義屬性將作為GraphQL查詢的一部分添加，並顯示在指定產品的產品預告中。

![生態友好徽章最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 必備條件 {#prerequisites}

完成本教程需要本地開發環境。 這包括已配置並AEM連接到Adobe Commerce實例的運行實例。 查看 [建立地方開發AEM](../develop.md)。 要完全學習本教程，您需要權限才能添加 [產品的屬性](https://docs.magento.com/user-guide/catalog/product-attributes-add.html) 在Adobe Commerce。

您還需要GraphQLIDE，例如 [圖形QL](https://github.com/graphql/graphiql) 或瀏覽器擴展，以運行代碼示例和教程。 如果安裝瀏覽器擴展，請確保它能夠設定請求標頭。 在Google·克羅姆， [AltairGraphQL客戶](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja) 是能做這個工作的分機。

## 克隆Venia項目 {#clone-venia-project}

我們將克隆 [韋尼亞計畫](https://github.com/adobe/aem-cif-guides-venia) 然後覆蓋預設樣式。

>[!NOTE]
>
>**可以自由使用現有項目** (基於包含CIFAEM的項目原型)並跳過此部分。

1. 運行以下git命令以克隆項目：

   ```shell
   $ git clone git@github.com:adobe/aem-cif-guides-venia.git
   ```

1. 將項目構建並部署到以下的本地實AEM例：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 添加必要的OSGi配置，將實AEM例連接到Adobe Commerce實例或將配置添加到新建立的項目。

1. 此時，您應具有連接到Adobe Commerce實例的店面的工作版本。 導航到 `US` > `Home` 頁： [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html)。

   您應看到店面當前正在使用Venia主題。 展開店面的「主菜單」，您應看到各種類別，表明與Adobe Commerce的連接正在工作。

   ![配置Venia主題的店面](../assets/customize-cif-components/venia-store-configured.png)

## 編寫產品預告 {#author-product-teaser}

在本教程中，產品預告元件將進行擴展。 作為第一步，將「產品預告」的新實例添加到首頁以瞭解基線功能。

1. 導航到 **首頁** 地址欄： [http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)

2. 插入新 **產品預告** 元件到頁面上的主佈局容器中。

   ![插入產品預告](../assets/customize-cif-components/product-teaser-add-component.png)

3. 展開「側面板」（如果尚未切換），並將資產查找器下拉清單切換到 **產品**。 這應顯示連接的Adobe Commerce實例的可用產品清單。 選擇產品並 **拖放** 在 **產品預告** 元件。

   ![拖放產品預告](../assets/customize-cif-components/drag-drop-product-teaser.png)

   >[!NOTE]
   >
   >注意，也可通過使用對話框配置元件(按一下 _扳_ )的正平方根。

4. 現在，您應看到產品預告顯示的產品。 產品名稱和產品價格是顯示的預設屬性。

   ![產品預告 — 預設樣式](../assets/customize-cif-components/product-teaser-default-style.png)

## 在Adobe Commerce添加自定義屬性 {#add-custom-attribute}

所顯示的產品和產品數AEM據儲存在Adobe Commerce。 下一步，為 **生態友好** 作為使用Adobe CommerceUI設定的產品屬性的一部分。

>[!TIP]
>
>已有自定義 **是/否** 屬性作為產品屬性集的一部分？ 您可以隨意使用，並跳過此部分。

1. 登錄到您的Adobe Commerce實例。
1. 導航到 **目錄** > **產品**。
1. 更新搜索篩選器以查找 **可配置產品** 在上一練習中添加到「預激」元件時使用。 在編輯模式下開啟產品。

   ![搜索Valeria產品](../assets/customize-cif-components/search-valeria-product.png)

1. 在產品視圖中，按一下 **添加屬性** > **建立新屬性**。
1. 填寫 **新建屬性** 表單，其值如下（保留其他值的預設設定）

   | 欄位集 | 欄位標籤 | 值 |
   | ----------------------------- | ------------------ | ---------------- |
   | 屬性屬性 | 屬性標籤 | **生態友好** |
   | 屬性屬性 | 目錄輸入類型 | **是/否** |
   | 高級屬性屬性 | 屬性代碼 | **eco_friendly** |

   ![新建屬性窗體](../assets/customize-cif-components/attribute-new-form.png)

   按一下 **保存屬性** 的子菜單。

1. 滾動到產品底部並展開 **屬性** 的子菜單。 您應該看到新 **生態友好** 的子菜單。 切換到 **是**。

   ![切換為是](../assets/customize-cif-components/eco-friendly-toggle-yes.png)

   **保存** 產品的更改。

   >[!TIP]
   >
   >有關管理的詳細資訊 [產品屬性可在Adobe Commerce使用手冊中找到](https://docs.magento.com/user-guide/catalog/attribute-best-practices.html)。

1. 導航到 **系統** > **工具** > **快取管理**。 由於對資料架構進行了更新，因此我們需要使Adobe Commerce的某些快取類型失效。
1. 選中旁邊的框 **配置** 並提交快取類型 **刷新**

   ![刷新配置快取類型](../assets/customize-cif-components/refresh-configuration-cache-type.png)

   >[!TIP]
   >
   >有關 [可在《Adobe Commerce使用手冊》中找到快取管理](https://docs.magento.com/user-guide/system/cache-management.html)。

## 使用GraphQLIDE驗證屬性 {#use-graphql-ide}

在跳入代AEM碼之前，探索 [Adobe CommerceGraphQL](https://devdocs.magento.com/guides/v2.4/graphql/) 使用GraphQLIDE。 與Adobe Commerce的整AEM合主要通過一系列GraphQL查詢完成。 瞭解和修改GraphQL查詢是擴展CIF核心元件的關鍵方法之一。

接下來，使用GraphQLIDE驗證 `eco_friendly` 屬性已添加到產品屬性集。 本教程中的螢幕截圖使用 [AltairGraphQL客戶](https://chrome.google.com/webstore/detail/altair-graphql-client/flnheeellpciglgpaodhkhmapeljopja)。

1. 開啟GraphQLIDE並輸入URL `http://<server>/graphql` 的子菜單。
2. 添加以下內容 [產品查詢](https://devdocs.magento.com/guides/v2.4/graphql/queries/products.html) 何處 `YOUR_SKU` 是 **SKU** 上次練習中使用的產品：

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

   請注意， **是** 是整數 **1**。 當我們使用Java編寫GraphQL查詢時，這將非常有用。

   >[!TIP]
   >
   >更詳細的文檔關於 [Adobe Commerce·GraphQL在這裡](https://devdocs.magento.com/guides/v2.4/graphql/index.html)。

## 更新產品預告的吊具模型 {#updating-sling-model-product-teaser}

接下來，我們將通過實施Sling模型來擴展產品預告的業務邏輯。 [吊具模型](https://sling.apache.org/documentation/bundles/models.html)，是注釋驅動的「POJO」（普通舊Java對象），用於實現元件所需的任何業務邏輯。 Sling Models與HTL指令碼一起作為元件的一部分使用。 我們將跟蹤 [Sling模型的委託模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) 這樣我們就可以擴展現有產品預告模型的部分。

Sling模型以Java形式實現，可在 **核** 生成項目的模組。

使用 [您選擇的IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?lang=en#set-up-the-development-ide) 來修改標籤元素的屬性。 使用的螢幕截圖來自 [Visual Studio代碼IDE](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/development-tools.html?#microsoft-visual-studio-code)。

1. 在IDE中，在 **核** 模組： `core/src/main/java/com/venia/core/models/commerce/MyProductTeaser.java`。

   ![核心位置IDE](../assets/customize-cif-components/core-location-ide.png)

   `MyProductTeaser.java` 是擴展CIF的Java介面 [產品預告](https://github.com/adobe/aem-core-cif-components/blob/master/bundles/core/src/main/java/com/adobe/cq/commerce/core/components/models/productteaser/ProductTeaser.java) 。

   已添加名為 `isShowBadge()` 顯示徽章（如果產品被視為「新」）。

1. 添加新方法， `isEcoFriendly()` 到介面：

   ```java
   @ProviderType
   public interface MyProductTeaser extends ProductTeaser {
       // Extend the existing interface with the additional properties which you
       // want to expose to the HTL template.
       public Boolean isShowBadge();
   
       public Boolean isEcoFriendly();
   }
   ```

   這是我們將引入的一種新方法，用於封裝邏輯，以指示產品是否具有 `eco_friendly` 屬性集 **是** 或 **否**。

1. 接下來，檢查 `MyProductTeaserImpl.java` 在 `core/src/main/java/com/venia/core/models/commerce/MyProductTeaserImpl.java`。

   的 [Sling模型的委託模式](https://github.com/adobe/aem-core-wcm-components/wiki/Delegation-Pattern-for-Sling-Models) 允許 `MyProductTeaserImpl` 引用 `ProductTeaser` 通過 `sling:resourceSuperType` 屬性：

   ```java
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductTeaser productTeaser;
   ```

   對於我們不想覆蓋或更改的所有方法，我們只需返回 `ProductTeaser` 返回。 例如：

   ```java
   @Override
   public String getImage() {
       return productTeaser.getImage();
   }
   ```

   這將使實現所需寫入的Java代碼量減到最小。

1. CIF核心元件提供的額AEM外擴展點之一是 `AbstractProductRetriever` 提供對特定產品屬性的訪問。 Inspect `initModel()` 方法：

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

   的 `@PostConstruct` 注釋確保在初始化Sling模型後立即調用此方法。

   請注意，產品GraphQL查詢已使用 `extendProductQueryWith` 用於檢索附加內容的方法 `created_at` 屬性。 此屬性稍後用作 `isShowBadge()` 的雙曲餘切值。

1. 更新GraphQL查詢以包括 `eco_friendly` 部分查詢中的屬性：

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

   添加到 `extendProductQueryWith` 方法是確保模型其餘部分具有附加產品屬性的有效方法。 它還可以最大限度地減少執行的查詢數。

   在上述代碼中，`addCustomSimpleField` 用於檢索 `eco_friendly` 屬性。 這說明了如何查詢屬於Adobe Commerce架構的任何自定義屬性。

   >[!NOTE]
   >
   >的 `createdAt()` 方法實際上已作為 [產品介面](https://github.com/adobe/commerce-cif-magento-graphql/blob/master/src/main/java/com/adobe/cq/commerce/magento/graphql/ProductInterface.java)。 大多數常見的架構屬性已實現，因此僅使用 `addCustomSimpleField` 的子菜單。

1. 添加記錄器以幫助調試Java代碼：

   ```java
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   ...
   @Model(adaptables = SlingHttpServletRequest.class, adapters = MyProductTeaser.class, resourceType = MyProductTeaserImpl.RESOURCE_TYPE)
   public class MyProductTeaserImpl implements MyProductTeaser {
   
   private static final Logger LOGGER = LoggerFactory.getLogger(MyProductTeaserImpl.class);
   ```

1. 接下來，實施 `isEcoFriendly()` 方法：

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

   在以上方法中， `productRetriever` 用於獲取產品和 `getAsInteger()` 方法用於獲取 `eco_friendly` 屬性。 根據我們前面所做的GraphQL查詢，我們知道當 `eco_friendly` 屬性設定為「」**是**&quot;實際上是 **1**。

   現在已更新Sling模型，需要更新元件標籤，以實際顯示 **生態友好** 基於Sling模型。

## 自定義產品預告的標籤 {#customize-markup-product-teaser}

元件的一AEM個公共擴展是修改元件生成的標籤。 通過覆蓋 [HTL指令碼](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 元件用於呈現其標籤的標籤。 HTML模板語言(HTL)是一種輕量級模板語言AEM，元件使用它根據創作的內容動態呈現標籤，允許重新使用元件。 例如，產品預告可以反複使用，以顯示不同的產品。

在本例中，我們希望在預告的頂部渲染一個標題，以根據自定義屬性指示產品是「Eco Friendly」。 用於 [自定義標籤](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html#customizing-the-markup) 元件的標準實際上是所AEM有元件的標準，而不AEM僅是CIF核心元件。

>[!NOTE]
>
>如果您使用CIF產品和類別選擇器（如此產品預告器）或CIF頁面元件來定制元件，請確保包括所需的元件 `cif.shell.picker` 元件對話框的客戶端庫。 請參閱 [CIF產品和類別選取器的使用](use-cif-pickers.md) 的雙曲餘切值。

1. 在IDE中，導航並展開 `ui.apps` 將資料夾層次結構展開到： `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser` 檢查 `.content.xml` 的子菜單。

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

   上面是我們項目中「產品預告」元件的元件定義。 注意屬性 `sling:resourceSuperType="core/cif/components/commerce/productteaser/v1/productteaser"`。 這是建立 [代理元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/using.html#create-proxy-components)。 我們不能從CIF核心元件中複製和貼上所AEM有產品預告HTL指令碼，而是可以使用 `sling:resourceSuperType` 繼承所有功能。

1. 開啟檔案 `productteaser.html`。 這是 `productteaser.html` 檔案 [CIF產品預告](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/productteaser.html)

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

   注意， `MyProductTeaser` 被使用並分配給 `product` 變數。

1. 修改 `productteaser.html` 打電話給 `isEcoFriendly` 方法：

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

   在HTL中調用Sling模型方法時 `get` 和 `is` 該方法的一部分被丟棄並且第一字母被下寫。 所以 `isShowBadge()` 變成 `.showBadge` 和 `isEcoFriendly` 變成 `.ecoFriendly`。 基於從返回的布爾值 `.isEcoFriendly()` 確定 `<span>Eco Friendly</span>` 的上界。

   有關 `data-sly-test` 其他 [HTL塊語句可在此處找到](https://experienceleague.adobe.com/docs/experience-manager-htl/content/specification.html)。

1. 從命令行終端保存更改並AEM部署更新以使用Maven技能：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 開啟新瀏覽器窗口並導航AEM至 **OSGi控制台** > **狀態** > **吊具模型**: [http://localhost:4502/system/console/status-slingmodels](http://localhost:4502/system/console/status-slingmodels)

1. 搜索 `MyProductTeaserImpl` 您應看到如下行：

   ```plain
   com.venia.core.models.commerce.MyProductTeaserImpl - venia/components/commerce/productteaser
   ```

   這表示已正確部署Sling模型並將其映射到正確的元件。

1. 刷新到 **韋尼亞首頁** 在 [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) 已添加產品預告的位置。

   ![顯示Eco Friendly消息](../assets/customize-cif-components/eco-friendly-text-displayed.png)

   如果產品 `eco_friendly` 屬性集 **是**，您應在頁面上看到「Eco Friendly」文本。 嘗試切換到不同的產品以查看行為更改。

1. 下一步開啟AEM `error.log` 查看我們添加的日誌語句。 的 `error.log` 位於 `<AEM SDK Install Location>/crx-quickstart/logs/error.log`。

   搜索日AEM志以查看在Sling模型中添加的日誌語句：

   ```plain
   2020-08-28 12:57:03.114 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is Eco Friendly**
   ...
   2020-08-28 13:01:00.271 INFO [com.venia.core.models.commerce.MyProductTeaserImpl] *** Product is not Eco Friendly**
   ...
   ```

   >[!CAUTION]
   >
   >如果預告中使用的產品沒有 `eco_friendly` 屬性作為屬性集的一部分。

## 添加環保徽章的樣式 {#add-styles}

此時，何時顯示 **生態友好** 徽章起作用，但純文字檔案可能使用某些樣式。 下一步，將表徵圖和樣式添加到 `ui.frontend` 模組完成實現。

1. 下載 [eco_friendly.svg](../assets/customize-cif-components/eco_friendly.svg) 的子菜單。 這將用作 **生態友好** 徽章。
1. 返回到IDE並導航到 `ui.frontend` 的子菜單。
1. 添加 `eco_friendly.svg` 檔案 `ui.frontend/src/main/resources/images` 資料夾：

   ![添加了環保SVG](../assets/customize-cif-components/eco-friendly-svg-added.png)

1. 開啟檔案 `productteaser.scss` 在 `ui.frontend/src/main/styles/commerce/_productteaser.scss`。
1. 在 `.productteaser` 類：

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
   >簽出 [設計CIF核心元件的樣式](./style-cif-component.md) 的子菜單。

1. 從命令行終端保存更改並AEM部署更新以使用Maven技能：

   ```shell
   $ cd aem-cif-guides-venia/
   $ mvn clean install -PautoInstallSinglePackage,cloud
   ```

1. 刷新到 **韋尼亞首頁** 在 [http://localhost:4502/editor.html/content/venia/us/en.html](http://localhost:4502/editor.html/content/venia/us/en.html) 已添加產品預告的位置。

   ![生態友好徽章最終實施](../assets/customize-cif-components/final-product-teaser-eco-badge.png)

## 恭喜 {#congratulations}

您剛剛定製了第AEM一個CIF元件！ 下載 [已完成解決方案檔案](../assets/customize-cif-components/customize-cif-component-SOLUTION_FILES.zip)。

## 獎金挑戰 {#bonus-challenge}

查看 **新建** 已在產品預告中實施的徽章。 嘗試添加附加複選框，以便作者控制 **生態友好** 應顯示徽章。 您需要更新元件對話框，位於 `ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productteaser/_cq_dialog/.content.xml`。

![新的徽章實施挑戰](../assets/customize-cif-components/new-badge-implementation-challenge.png)

## 其他資源 {#additional-resources}

- [原AEM型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=zh-Hant)
- [AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components)
- [自定義AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components/wiki/Customizing-CIF-Core-Components)
- [自訂核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html)
- [AEM Sites入門](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)
- [CIF產品和類別選取器的使用](use-cif-pickers.md)
