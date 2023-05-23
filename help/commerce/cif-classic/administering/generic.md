---
title: 管理通用電子商務
seo-title: Administering generic eCommerce
description: 該通AEM用解決方案提供了管理儲存在儲存庫中的商業資訊的方法。
seo-description: The AEM generic solution provides methods of managing the commerce information held within the repository.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '2910'
ht-degree: 2%

---

# 管理通用電子商務 {#administering-generic-ecommerce}

該通AEM用解決方案提供了管理儲存庫中保存的商業資訊（而不是使用外部電子商務引擎）的方法。 這包括：

* [產品](/help/commerce/cif-classic/administering/concepts.md#products)
* [產品的系列品種](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [目錄](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [促銷活動](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [憑單](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [訂購](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [代理頁](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>標準安AEM裝包括通AEM用(JCR)電子商務實現。
>
>目前，這是為了演示目的，或根據您的要求作為自定義實施的基本基礎。

## 產品和產品變體 {#products-and-product-variations}

>[!NOTE]
>
>以下過程適用於「產品」和「產品變體」。

在建立產品之前，您需要定義 [支架](/help/sites-authoring/scaffolding.md)。 這指定了定義產品以及編輯產品的方式所需的欄位。

每種不同的產品類型都需要支架。 適當的支架通過以下任一方式與產品相關聯：

* 路徑
* 產品可以參照腳手架

>[!NOTE]
>
>Geometrixx — 室外商店有一種單一的產品類型（因此也有一種支架）:
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Geometrixx — 室外產品類型在以下位置處於活動狀態：
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>您可以在新產品定義的任何位置建立新產品定義，而無需任何附加設定。

### 導入產品 {#importing-products}

#### 導入產品 — 觸摸優化UI {#importing-products-touch-optimized-ui}

1. 導航到 **產品** 控制台，通過 **商業**。
1. 使用 **產品** 控制台導航到所需位置。
1. 使用 **導入產品** 表徵圖開啟嚮導。

   ![chlimage_1-1](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 指定下列設定：

   * **匯入工具**

      具體的進口商 [商務提供商](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)，預設 `Geometrixx`。

   * **來源**

      要導入的檔案；可以使用瀏覽器來選擇檔案。

   * **增量匯入**

      指示這是否是增量導入（而不是完全導入）。
   >[!NOTE]
   >
   >增量導入（樣例幾何 — 室外導入程式）在產品級操作。
   >
   >可根據需要定義自定義導入程式以運行。

1. 選擇 **下一個** 要導入產品，將顯示所執行操作的日誌。

   >[!NOTE]
   >
   >產品將導入到當前位置或相對於當前位置。

   >[!NOTE]
   >
   >重複使用 **下一個** 和 **後退** 將重複導入產品定義。 但是，由於它們具有相同的SKU，因此儲存庫中現有的資訊將被覆蓋。

1. 選擇 **完成** 按鈕。

#### 導入產品 — 經典UI {#importing-products-classic-ui}

1. 使用 **工具** 控制台開啟 **商業** 的子菜單。
1. 按兩下以開啟 **產品導入程式**:

   ![chlimage_1-22](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. 指定下列設定：

   * **存放區名稱**

      產品將導入到：

      `/etc/commerce/products/<*store name*>/`

   * **商務提供程式**

      你的進口商 [商務提供商](/help/commerce/cif-classic/administering/concepts.md#commerce-providers);預設Geometrixx。

   * **來源檔案**

      要導入的檔案的儲存庫中的位置。

   * **增量匯入**

      指示這是否是增量導入（而不是完全導入）。

1. 按一下 **導入產品**。

### 建立產品資訊 {#creating-product-information}

>[!NOTE]
>
>標準產品管理是基本的，因為Geometrixx — 室外產品集一直保持基本。 複雜性基於產品 [腳](/help/sites-authoring/scaffolding.md)因此，借助您自己的產品腳手架，可以實現更複雜的編輯。

#### 建立產品資訊 — 觸控優化的UI {#creating-product-information-touch-optimized-ui}

1. 使用 **產品** 控制台(通過 **商業**)導航到所需位置。
1. 使用 **建立** 表徵圖，以選擇以下任一選項（取決於結構和位置）:

   * **建立產品**
   * **建立產品變體**

   ![chlimage_1-14](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 嚮導將開啟。 使用 **基本** 和 **產品頁籤** 的 [產品屬性](/help/commerce/cif-classic/administering/concepts.md#product-attributes) 或產品變型。

   >[!NOTE]
   >
   >**標題** 和 **SKU** 是建立產品或變型所需的最小值。

1. 選擇 **建立** 的子菜單。

>[!NOTE]
>
>許多產品都以各種顏色和/或尺寸提供。 有關基本產品和相關產品變型的資訊都可以從 **產品** 控制台。
>
>產品及其變型以樹形結構儲存，產品資訊位於頂部，下面有變型（此結構由UI強制實施）。

### 編輯產品資訊 {#editing-product-information}

>[!NOTE]
>
>Geometrixx-outdoors中的產品影像提供自：
>
>`/etc/commerce/products/...`
>
>這意味著，預設情況下，它們被 [調度](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html)，因此根據需要進行配置。

#### 編輯產品資訊 — 觸控優化的UI {#editing-product-information-touch-optimized-ui}

1. 使用 **產品** 控制台(通過 **商業**)導航到您的產品資訊。
1. 使用以下任一項：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選擇 **查看產品資料** 表徵圖：

   ![chlimage_1-3](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 的 [產品屬性](/help/commerce/cif-classic/administering/concepts.md#product-attributes) 的下界。 使用 **編輯** 和 **完成** 進行任何更改。

### 顯示產品參考 {#showing-product-references}

#### 顯示產品參考 — 觸控優化的用戶介面 {#showing-product-references-touch-optimized-ui}

1. 使用 **產品** 控制台(通過 **商業**)導航到您的產品資訊。
1. 使用表徵圖開啟「參照」(References)的輔助滑軌：

   ![chlimage_1-4](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. 選擇所需產品 — 輔助導軌將更新以顯示可用的參考類型：

   ![chlimage_1-88](/help/sites-administering/assets/chlimage_1-88.png)

1. 按一下/點按參考類型（如「產品頁」）以展開清單。
1. 選擇特定參照以顯示選項：

   * 導覽至產品頁面
   * 編輯產品頁面

   ![chlimage_1-89](/help/sites-administering/assets/chlimage_1-89.png)

### 搜索產品 {#search-for-products}

1. 導航到 **產品** 控制台，通過 **商業**。
1. 使用表徵圖開啟輔助導軌以進行搜索：

   ![](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. 有幾個方面可供您搜索產品。 只能使用一個或多個小平面進行搜索。 將顯示找到的產品：

   ![chlimage_1-90](/help/sites-administering/assets/chlimage_1-90.png)

1. 按一下/輕擊產品可開啟產品。 您還可以發佈或查看產品資料。

#### 擴展搜索 {#extending-search}

可以使用CRXDE Lite修改現有小平面或添加新小平面：

1. 瀏覽到:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. 例如，您可以修改將出現在產品搜索頁面上的大小。 按一下 `sizegroup` 的下界。
1. 按一下 `items` 節點，然後按一下 `propertypredicate` 的下界。
1. 可以修改 `propertyValues`。 例如，可以添加XS、XXL或刪除大小。
1. 按一下 **全部保存** 並導航到產品搜索頁。 應顯示您所做的更改。

### 多資產 {#multiple-assets}

您可以在產品元件中添加多個資產，然後指定將出現在產品頁面上的資產。

>[!NOTE]
>
>與多個資產相關的所有操作都使用Touch優化的UI完成。

#### 添加多個資產 {#adding-multiple-assets}

1. 導航到 **產品** 控制台，通過 **商業**。
1. 使用 **產品** 控制台，導航至所需產品。

   >[!NOTE]
   >
   >你必須在產品級別，而不是變型級別。

1. 點擊/按一下 **查看產品資料** 表徵圖。
1. 點擊/按一下「編輯」表徵圖。
1. 滾動到 **添加**。

   ![chlimage_1-91](/help/sites-administering/assets/chlimage_1-91.png)

1. 點擊/按一下 **添加**。 此時將出現新的資產佔位符。
1. 點擊/按一下**更改**開啟一個對話框，您可以選擇資產。
1. 選擇要添加的資產。

   >[!NOTE]
   >
   >可以選擇的資產來自 [資產](/help/assets/assets.md)。

1. 點擊/按一下「完成」表徵圖。

兩個資產現在儲存在您的產品元件中。 您可以配置在產品頁上顯示哪個。 這適用於類別系統。 首先，您需要向單個資產添加一個類別：

1. 點擊/按一下 **查看產品資料**。
1. 鍵入 **資產類別** 例如 `cat1` 和 `cat2`。

   >[!NOTE]
   >
   >也可以對類別使用標籤。

1. 點擊/按一下「完成」表徵圖。 你現在必須 [推廣](#rolling-out-a-catalog) 您的更改。

現在，您在產品元件中的資產具有類別。 您可以配置在三個不同級別顯示的類別：

* [產品頁面](#product-page)
* [目錄](#catalog)
* [產品控制台](#products-console)

>[!NOTE]
>
>如果未設定類別，則第一個資產將顯示在產品頁面上。

選擇要顯示的影像的機制如下：

1. 驗證是否為「產品」頁設定了類別。
1. 否則，驗證是否為目錄設定了類別。
1. 否則，驗證是否為產品控制台設定了類別。

>[!NOTE]
>
>對於目錄級別和產品控制台級別，您必須先部署更改，然後應用修改並在產品頁面上查看差異。

#### 產品頁面 {#product-page}

1. 導航到您的產品頁。
1. **編輯** 產品元件。
1. 鍵入 **影像類別** 您選擇了( `cat1` 例如)。
1. 點擊/按一下 **完成**。 頁面將刷新，應顯示正確的資產。

#### 目錄  {#catalog}

1. 導航到目錄。
1. 點擊/按一下 **查看屬性**。
1. 點擊/按一下 **編輯**。
1. 點擊/按一下 **資產** 頁籤。
1. 鍵入所需 **產品資產類別**。
1. 點擊/按一下 **完成**。
1. [推廣](#rolling-out-a-catalog) 您的更改。

#### 產品控制台 {#products-console}

1. 使用 **產品** 控制台，導航至所需的產品。
1. 點擊/按一下 **查看產品資料**。
1. 點擊/按一下 **編輯**。
1. 鍵入 **預設資產類別**。
1. 點擊/按一下 **完成**。
1. [推廣](#rolling-out-a-catalog) 您的更改。

### 發佈/取消發佈產品資訊 {#publishing-unpublishing-product-information}

#### 發佈/取消發佈產品資訊 — 觸控優化用戶介面 {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>產品資訊通常通過引用它的頁面發佈。 例如，在發佈引用產品Y的頁面X時，AEM會詢問您是否也要發佈產品Y。
>
>對於特殊情況，AEM還支援直接從產品資料發佈。

1. 使用 **產品** 控制台(通過 **商業**)導航到您的產品資訊。
1. 使用以下任一項：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選擇 **發佈** 或 **取消發佈** 表徵圖（如需要）:

   ![chlimage-1-6](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![chlimage-1-7](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   產品資訊將根據需要發佈或取消發佈。

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration allows you to: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### 產品更新的事件處理程式 {#event-handler-for-product-updates}

有一個事件處理程式，它在添加、修改或刪除產品以及添加、修改或刪除產品頁面時記錄事件。 有以下OSGi事件：

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

對於 `PRODUCT_*` 事件，路徑指向 `/etc/commerce/products`。 對於 `PRODUCT_PAGE_*` 事件，路徑指向 `cq:Page` 的下界。

您可以在Web控制台中的OSGI事件中查看它們( `/system/console/events`)，例如：

![](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>另請閱讀 [事件處AEM理](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/)。

### 具有添加到購物車連結的影像 {#image-with-add-to-cart-links}

使用「添加到購物車連結的影像」元件，您可以通過在影像上建立與產品連結的熱點來快速將產品添加到購物車。

按一下熱點將開啟一個對話框，您可以選擇產品的大小和數量。

1. 導航到要添加元件的頁面。
1. 在頁面中拖放元件。
1. 從 [資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser)。
1. 您可以執行下列兩個動作中的一個:

   * 按一下元件，然後按一下「編輯」表徵圖
   * 慢點按兩下

1. 按一下全屏表徵圖。

   ![chlimage_1-92](/help/sites-administering/assets/chlimage_1-92.png)

1. 按一下「啟動映射」表徵圖。

   ![chlimage_1-93](/help/sites-administering/assets/chlimage_1-93.png)

1. 按一下其中一個形狀表徵圖。

   ![chlimage_1-21](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. 根據需要修改和移動形狀。
1. 按一下形狀。
1. 按一下瀏覽表徵圖可開啟 [資產選取器](/help/assets/search-assets.md#assetpicker)。

   >[!NOTE]
   >
   >或者，可以直接鍵入必須位於產品級別而不是變型級別的產品路徑。

   ![chlimage_1-94](/help/sites-administering/assets/chlimage_1-94.png)

1. 按一下兩次確認表徵圖，然後按一下退出全屏。
1. 按一下該元件旁邊的頁面上的某個位置。 頁面應刷新，您應在影像上看到以下符號：

   ![](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. 切換到 [預覽](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) 的子菜單。
1. 按一下+熱點。 將開啟一個對話框，您可以在其中選擇在中輸入的產品的大小和數量 **路徑**。

   ![chlimage_1-95](/help/sites-administering/assets/chlimage_1-95.png)

1. 輸入大小和數量。
1. 按一下「Add to cart（添加到購物車）」按鈕。 對話框關閉。
1. 導航到您的購物車。 產品應該在這裡。

#### 配置選項 {#configuration-options}

您可以配置按一下熱點時對話框的外觀：

1. 按一下元件，然後按一下「配置」表徵圖。

   ![chlimage_1-96](/help/sites-administering/assets/chlimage_1-96.png)

1. 向下捲動. 有 **添加到購物車** 頁籤。

   ![chlimage_1-97](/help/sites-administering/assets/chlimage_1-97.png)

1. 按一下 **添加到購物車**。 可以使用3個配置選項。

   ![chlimage_1-98](/help/sites-administering/assets/chlimage_1-98.png)

1. 按一下「完成」(Done)表徵圖。

## 目錄 {#catalogs}

### 生成目錄 {#generating-a-catalog}

#### 生成目錄 — 觸控優化的UI {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>目錄將引用您的產品資料。

要生成目錄，請執行以下操作：

1. 開啟「站點」控制台(例如， [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content))。
1. 導航到要建立新頁面的位置。
1. 要開啟選項清單，請使用 **建立** 表徵圖：

   ![建立表徵圖](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. 從清單中選擇 **建立目錄**，將開啟「建立目錄」嚮導。

   ![chlimage_1-99](/help/sites-administering/assets/chlimage_1-99.png)

1. 導航到所需的目錄藍圖。
1. 點擊/按一下 **選擇** 按鈕，然後按一下/按一下所需的目錄藍圖。
1. 點擊/按一下 **下一個**。

   ![chlimage_1-100](/help/sites-administering/assets/chlimage_1-100.png)

1. 鍵入 **標題** 和 **名稱**。
1. 點擊/按一下 **建立** 按鈕 將建立目錄並開啟一個對話框。

   ![chlimage_1-101](/help/sites-administering/assets/chlimage_1-101.png)

1. 點擊/按一下 **完成** 按鈕將返回到「站點」控制台，在該控制台中，您將能夠查看目錄。

   點擊/按一下 **開啟目錄** 按鈕開啟目錄(例如 `http://localhost:4502/editor.html/content/test-catalog.html`)。

#### 生成目錄 — 經典UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>目錄將引用 [產品資料](#products-and-product-variants)。

1. 使用 **網站** 控制台，導航至 **目錄藍圖**，然後是基目錄。

   例如：

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. 使用 **節藍圖** 的下界。

   比如說， `Swimwear`。

1. 開啟新 `Swimwear` ，然後按一下 **編輯藍圖** 開啟 **屬性** 對話框，您可以在其中設定 **產品** 的子菜單。

   例如，開啟 **標籤/關鍵字** 欄位以選擇「活動」，然後從「Geometrixx — 室外」部分選擇「游泳」。

1. 按一下 **確定** 保存您的財產；示例產品將顯示在 **產品選擇標準** 在藍圖頁面。
1. 按一下 **推廣更改……**&#x200B;選中 **展示頁和所有子頁**，然後按一下 **下一個** 然後 **推廣**。 成功完成部署後， **狀態** 指示器將顯示為綠色。
1. 您現在可以按一下 **關閉** 查新目錄部分；例如，on和on:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. 再次從「藍圖」頁面按一下 **編輯藍圖** 在 **屬性** 對話框開啟 **生成的頁** 頁籤。 在「橫幅廣告」清單欄位中，選擇要顯示的影像；比如說， `summer.jpg`
1. 按一下 **確定** 保存您的財產；標題資訊將顯示在 **產品選擇標準** 在藍圖頁面。
1. 推廣這些新更改。

### 展開目錄 {#rolling-out-a-catalog}

#### 推出目錄 — 觸控優化的UI {#rolling-out-a-catalog-touch-optimized-ui}

要部署目錄，請執行以下操作：

1. 導航到 **目錄** 控制台，通過 **商業**。
1. 導航到要推廣的目錄。
1. 使用以下任一項：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選擇 **推廣更改** 表徵圖：

   ![轉出](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. 在嚮導中，根據需要設定展示，然後點擊/按一下 **推廣更改**。
1. 將開啟一個對話框。 點擊/按一下 **完成** 的子菜單。

#### 正在推出目錄 — 經典UI {#rolling-out-a-catalog-classic-ui}

要部署目錄，請執行以下操作：

1. 導航到要推廣的目錄。 例如：

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. 按一下 **推廣更改……**
1. 根據需要設定部署。
1. 按一下 **推廣**。

### 藍圖導入程式 {#blueprint-importer}

#### 藍圖導入程式 — 觸控優化的UI {#blueprint-importer-touch-optimized-ui}

1. 導航到 **目錄** 控制台，通過 **商業**。
1. 導航到要導入目錄藍圖的位置。
1. 點擊/按一下 **導入藍圖** 表徵圖

   ![](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 在嚮導中，根據需要選擇「源」，然後點擊/按一下 **下一個**。

   ![chlimage_1-340](/help/sites-administering/assets/chlimage_1-102.png)

1. 點擊/按一下 **完成** 完成導入後。

#### 藍圖導入程式 — 經典UI {#blueprint-importer-classic-ui}

1. 使用 **工具** 控制台，導航至 **商業**。

   例如：

   `http://localhost:4502/miscadmin#/etc/commerce`

1. 開啟 **目錄藍印導入程式**。
1. 根據需要設定導入。
1. 按一下 **導入目錄藍圖**。

## 促銷活動 {#promotions}

### 建立促銷 {#creating-a-promotion}

#### 建立升級 — 經典用戶介面 {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>以下示例處理直接在 [活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)，這用於憑證。
>
>促銷也可以在 [體驗](/help/sites-authoring/personalization.md) 在競選中。
>
>有關詳細資訊，請參閱 [促銷和憑單](#promotions-and-vouchers)。

1. 開啟 **網站** 作者實例的控制台。
1. 在左窗格中，選擇所需 **活動**。
1. 按一下 **新建**，選擇 **升級** 模板，然後指定 **標題** (和 **名稱** )。
1. 按一下&#x200B;**建立**。新的升級頁面將顯示在右窗格中。

1. 編輯 **屬性** 按以下任一：

   * 開啟頁面，然後按一下「編輯」按鈕以開啟「屬性」對話框
   * 在「網站」控制台中選擇頁面，然後使用上下文菜單（通常是滑鼠右鍵）選擇 **屬性……** 開啟「屬性」對話框

   指定 **升級類型**。 **折扣類型**。 **折扣值** 和其他任何需要的欄位。

1. 按一下 **確定** 來保存。

1. 您現在可以激活促銷，以便購物者在發佈實例上看到它。

## 憑單 {#vouchers}

### 建立憑證 {#creating-a-voucher}

#### 建立憑單 — 傳統用戶介面 {#creating-a-voucher-classic-ui}

1. 開啟 **網站** 作者實例的控制台。
1. 在左窗格中，選擇所需 **活動**。
1. 按一下 **新建**，選擇 **憑證** 模板，然後指定 **標題** (和 **名稱** )。
1. 按一下&#x200B;**建立**。新憑證頁將顯示在右窗格中。

1. 按兩下開啟新的憑單頁，然後按一下 **編輯** 以根據需要配置資訊。
1. 按一下 **確定** 來保存。

1. 現在，您可以激活您的憑單，以便購物者可以在發佈實例上的購物車中使用它。

### 刪除憑單 {#removing-vouchers}

#### 刪除憑單 — 經典UI {#removing-vouchers-classic-ui}

為使憑證不可供客戶使用，您可以執行以下任一操作：

* 停用憑單 — 憑單將在作者環境中保持可用，以便您可以稍後重新激活它。
* 完全刪除它。

可以通過 **網站** 控制台。

### 修改憑證 {#modifying-vouchers}

#### 修改憑單 — 經典UI {#modifying-vouchers-classic-ui}

要更改憑證或促銷的屬性，可在 **網站** 按一下 **編輯**。 保存後，應激活它，以便將更改推送到發佈實例。

### 將憑單添加到購物車 {#adding-vouchers-to-a-cart}

要允許用戶將憑單添加到購物車中，可以使用 **憑證** 元件（Commerce類別）。 您需要將此內容添加到顯示購物車的同一頁（但不是強制）。 憑單元件只是用戶可以輸入憑單代碼的表單，實際顯示已應用憑單及其折扣清單的購物車元件。

在演示站點(Geometrixx Outdoors — 英語)中，您可以在購物車頁面的實際購物車下查看憑單。

## 訂購 {#orders}

>[!NOTE]
>
>應該記住，現成產品不AEM具備與訂單相關的標準功能所需的操作，例如退貨、更新訂單狀態、完成、生成裝箱單。 它主要是作為技術預覽。
>
>中的通用訂單管AEM理保持基本；嚮導中可用的欄位取決於指令碼框：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>如果建立了自定義的支架，則可以儲存更多訂單資訊。

>[!NOTE]
>
>訂單控制台公開供應商訂單資訊，這些資訊從未發佈。
>
>客戶訂單資訊保存在其主目錄中，並由其帳戶的訂單歷史記錄公開。 此資訊與其他主目錄一起發佈。

### 建立訂單資訊 {#creating-order-information}

#### 建立訂單資訊 — 觸控優化用戶介面 {#creating-order-information-touch-optimized-ui}

1. 使用 **訂單** 控制台導航到所需位置。
1. 使用 **建立** 表徵圖 **建立訂單**。

   ![](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 嚮導將開啟。 使用 **基本**。 **內容**。 **付款** 和 **履行** 頁籤 [有關新訂單的資訊](/help/commerce/cif-classic/administering/concepts.md#order-information)。

1. 選擇 **建立** 的子菜單。

### 編輯訂單資訊 {#editing-order-information}

#### 編輯訂單資訊 — 觸控優化用戶介面 {#editing-order-information-touch-optimized-ui}

1. 使用 **訂單** 控制台導航至訂單。
1. 使用以下任一項：

   * [快速操作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選擇 **查看訂單資料** 表徵圖：

   ![](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 的 [訂單資訊](/help/commerce/cif-classic/administering/concepts.md#order-information) 的下界。 使用 **編輯** 和 **完成** 進行任何更改。

