---
title: 管理一般電子商務
seo-title: Administering generic eCommerce
description: AEM一般解決方案提供管理存放在存放庫中的商務資訊的方法。
seo-description: The AEM generic solution provides methods of managing the commerce information held within the repository.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '2910'
ht-degree: 1%

---

# 管理一般電子商務 {#administering-generic-ecommerce}

AEM通用解決方案提供管理存放在存放庫中的商務資訊的方法（與使用外部電子商務引擎相反）。 這包括：

* [產品](/help/commerce/cif-classic/administering/concepts.md#products)
* [產品的系列品種](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [目錄](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [促銷活動](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [憑單](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [訂購](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [代理頁](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>標準AEM安裝包含一般AEM(JCR)電子商務實作。
>
>這目前的用途為示範，或根據您的需求，做為自訂實作的基礎。

## 產品和產品變數 {#products-and-product-variations}

>[!NOTE]
>
>下列程式同時適用於產品和產品變異。

建立產品之前，您需要定義 [支架](/help/sites-authoring/scaffolding.md). 這會指定定義產品及其編輯方式所需的欄位。

每種不同的產品類型都需要架構。 適當的架構可透過下列任一方式與產品建立關聯：

* 路徑
* 產品可以參照支架

>[!NOTE]
>
>Geometrixx — 戶外商店只有一種產品類型（因此也只有一種架構）:
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Geometrixx — 戶外產品類型在上處於活動狀態：
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>您可以在任何位置建立新產品定義，而不需進行任何其他設定。

### 匯入產品 {#importing-products}

#### 匯入產品 — 觸控最佳化UI {#importing-products-touch-optimized-ui}

1. 導覽至 **產品** 主控台，透過 **商務**.
1. 使用 **產品** 主控台導覽至所需位置。
1. 使用 **匯入產品** 圖示以開啟精靈。

   ![chlimage_1-1](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 指定下列設定：

   * **匯入工具**

      特定 [商務提供商](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)，預設為 `Geometrixx`.

   * **來源**

      要導入的檔案；您可以使用瀏覽器來選取檔案。

   * **增量匯入**

      指出這是否為增量匯入（而非完整匯入）。
   >[!NOTE]
   >
   >增量匯入（sample geometrixx-outdoor匯入工具的）會在產品層級運作。
   >
   >可定義自訂匯入工具，以視需要運作。

1. 選擇 **下一個** 若要匯入產品，將會顯示所執行動作的記錄檔。

   >[!NOTE]
   >
   >產品將會匯入至目前位置，或相對於目前位置。

   >[!NOTE]
   >
   >重複使用 **下一個** 和 **返回** 會重複匯入產品定義。 但是，由於它們有相同的SKU，因此存放庫中現有的資訊只會遭到覆寫。

1. 選擇 **完成** 以關閉精靈。

#### 匯入產品 — 傳統UI {#importing-products-classic-ui}

1. 使用 **工具** 主控台會開啟 **商務** 檔案夾。
1. 按兩下以開啟 **產品匯入工具**:

   ![chlimage_1-22](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. 指定下列設定：

   * **存放區名稱**

      產品將進口至：

      `/etc/commerce/products/<*store name*>/`

   * **商務提供程式**

      匯入工具 [商務提供商](/help/commerce/cif-classic/administering/concepts.md#commerce-providers);預設Geometrixx。

   * **來源檔案**

      要導入的檔案的儲存庫中的位置。

   * **增量匯入**

      指出這是否為增量匯入（而非完整匯入）。

1. 按一下 **匯入產品**.

### 建立產品資訊 {#creating-product-information}

>[!NOTE]
>
>標準產品管理是基本的，因為Geometrixx — 戶外產品集保持基本。 複雜性取決於產品 [支架](/help/sites-authoring/scaffolding.md)，因此透過您自己的產品架構，便可進行更精密的編輯作業。

#### 建立產品資訊 — 觸控最佳化UI {#creating-product-information-touch-optimized-ui}

1. 使用 **產品** 主控台(透過 **商務**)導覽至所需位置。
1. 使用 **建立** 圖示來選取其中一個項目（視結構和位置而定）:

   * **建立產品**
   * **建立產品變異**

   ![chlimage_1-14](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 嚮導將開啟。 使用 **基本** 和 **產品標籤** ，輸入 [產品屬性](/help/commerce/cif-classic/administering/concepts.md#product-attributes) 用於新產品或產品變體。

   >[!NOTE]
   >
   >**標題** 和 **SKU** 是建立產品或變體所需的最低值。

1. 選擇 **建立** 以儲存資訊。

>[!NOTE]
>
>許多產品都以各種顏色和/或尺寸提供。 基本產品和相關產品變體的相關資訊均可從 **產品** 控制台。
>
>產品及其變體會儲存為樹狀結構，產品資訊位於頂端，下方會顯示變體（此結構由UI強制執行）。

### 編輯產品資訊 {#editing-product-information}

>[!NOTE]
>
>geometrixx-outdoors中的產品影像提供來源：
>
>`/etc/commerce/products/...`
>
>這表示依預設，會被 [dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html)，請視需要進行設定。

#### 編輯產品資訊 — 觸控最佳化UI {#editing-product-information-touch-optimized-ui}

1. 使用 **產品** 主控台(透過 **商務**)導覽至您的產品資訊。
1. 使用下列其中一項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選取 **檢視產品資料** 圖示：

   ![chlimage_1-3](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 此 [產品屬性](/help/commerce/cif-classic/administering/concepts.md#product-attributes) 即會顯示。 使用 **編輯** 和 **完成** 進行任何變更。

### 顯示產品參考 {#showing-product-references}

#### 顯示產品參考資料 — 觸控最佳化UI {#showing-product-references-touch-optimized-ui}

1. 使用 **產品** 主控台(透過 **商務**)導覽至您的產品資訊。
1. 使用圖示開啟「參考」的次要邊欄：

   ![chlimage_1-4](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. 選取您需要的產品 — 次要邊欄將會更新，以顯示可用的參考類型：

   ![chlimage_1-88](/help/sites-administering/assets/chlimage_1-88.png)

1. 按一下/點選參考類型（例如「產品頁面」）以展開清單。
1. 選取特定參考以顯示選項：

   * 導覽至產品頁面
   * 編輯產品頁面

   ![chlimage_1-89](/help/sites-administering/assets/chlimage_1-89.png)

### 搜尋產品 {#search-for-products}

1. 導覽至 **產品** 主控台，透過 **商務**.
1. 使用圖示開啟次要邊欄以供搜尋：

   ![](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. 您可搜尋產品有幾個面向。 搜索只能使用一個或多個刻面。 找到的產品將顯示：

   ![chlimage_1-90](/help/sites-administering/assets/chlimage_1-90.png)

1. 按一下/點選產品會開啟它。 您也可以發佈或檢視產品資料。

#### 延伸搜尋 {#extending-search}

您可以使用CRXDE Lite修改現有小面或新增小面：

1. 導航到:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. 例如，您可以修改產品搜尋頁面上顯示的大小。 按一下 `sizegroup` 節點。
1. 按一下 `items` 節點，然後按一下 `propertypredicate` 節點。
1. 您可以修改 `propertyValues`. 例如，您可以添加XS、XXL或移除大小。
1. 按一下 **全部儲存** 並導覽至產品搜尋頁面。 您的變更應會顯示。

### 多個資產 {#multiple-assets}

您可以在產品元件中新增多個資產，然後指定要出現在產品頁面上的資產。

>[!NOTE]
>
>所有與多個資產相關的作業都可使用觸控最佳化UI完成。

#### 新增多個資產 {#adding-multiple-assets}

1. 導覽至 **產品** 主控台，透過 **商務**.
1. 使用 **產品** 主控台，導覽至所需產品。

   >[!NOTE]
   >
   >您必須位於產品層級，而非變體層級。

1. 點選/按一下 **檢視產品資料** 表徵圖。
1. 點選/按一下「編輯」圖示。
1. 捲動至 **新增**.

   ![chlimage_1-91](/help/sites-administering/assets/chlimage_1-91.png)

1. 點選/按一下 **新增**. 隨即顯示新資產預留位置。
1. 點選/按一下**變更**會開啟一個對話方塊，讓您選擇資產。
1. 選取您要新增的資產。

   >[!NOTE]
   >
   >您可以選取的資產為 [資產](/help/assets/assets.md).

1. 點選/按一下「完成」圖示。

現在，您的產品元件中會儲存兩個資產。 您可以設定要在產品頁面上顯示哪個頁面。 這適用於類別系統。 首先，您需要將類別新增至個別資產：

1. 點選/按一下 **檢視產品資料**.
1. 輸入 **資產類別** 例如 `cat1` 和 `cat2`.

   >[!NOTE]
   >
   >您也可以使用類別的標籤。

1. 點選/按一下「完成」圖示。 你現在必須 [轉出](#rolling-out-a-catalog) 您的變更。

現在，您的資產在產品元件中已有類別。 您可以設定要在三個不同層級顯示的類別：

* [產品頁面](#product-page)
* [目錄](#catalog)
* [產品主控台](#products-console)

>[!NOTE]
>
>如果您未設定類別，則第一個資產會顯示在產品頁面上。

選擇要顯示的影像的機制如下：

1. 驗證是否為產品頁面設定了類別。
1. 否則，驗證是否為目錄設定了類別。
1. 若未設定，請確認是否已為產品控制台設定類別。

>[!NOTE]
>
>對於目錄層級和產品控制台層級，您必須轉出變更以套用修改，並在產品頁面上查看差異。

#### 產品頁面 {#product-page}

1. 導覽至您的產品頁面。
1. **編輯** 產品元件。
1. 輸入 **影像類別** 您選擇( `cat1` 例如)。
1. 點選/按一下 **完成**. 頁面會重新整理，且應顯示正確的資產。

#### 目錄  {#catalog}

1. 導覽至您的目錄。
1. 點選/按一下 **檢視屬性**.
1. 點選/按一下 **編輯**.
1. 點選/按一下 **資產** 標籤。
1. 輸入所需 **產品資產類別**.
1. 點選/按一下 **完成**.
1. [轉出](#rolling-out-a-catalog) 您的變更。

#### 產品主控台 {#products-console}

1. 使用 **產品** 主控台，導覽至所需的產品。
1. 點選/按一下 **檢視產品資料**.
1. 點選/按一下 **編輯**.
1. 輸入 **預設資產類別**.
1. 點選/按一下 **完成**.
1. [轉出](#rolling-out-a-catalog) 您的變更。

### 發佈/取消發佈產品資訊 {#publishing-unpublishing-product-information}

#### 發佈/取消發佈產品資訊 — 觸控最佳化UI {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>產品資訊通常會透過參考其頁面發佈。 例如，發佈參考產品Y的頁面X時，AEM會詢問您是否也要發佈產品Y。
>
>針對特殊情況，AEM也支援直接從產品資料發佈。

1. 使用 **產品** 主控台(透過 **商務**)導覽至您的產品資訊。
1. 使用下列其中一項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選取 **發佈** 或 **取消發佈** 圖示（視需要）。

   ![chlimage_1-6](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![chlimage_1-7](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   產品資訊將酌情發佈或取消發佈。

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration allows you to: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * leverage the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### 產品更新的事件處理常式 {#event-handler-for-product-updates}

有一個事件處理程式，它記錄在添加、修改或刪除產品頁面時以及添加、修改或刪除產品頁面時的事件。 有下列OSGi事件：

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

若 `PRODUCT_*` 事件，路徑會指向 `/etc/commerce/products`. 若 `PRODUCT_PAGE_*` 事件，路徑會指向 `cq:Page` 節點。

您可以在OSGI事件的Web主控台中查看這些事件( `/system/console/events`)，例如：

![](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>另請閱讀 [AEM中的事件處理](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/).

### 具有新增至購物車連結的影像 {#image-with-add-to-cart-links}

具有新增至購物車連結的影像元件可讓您透過在影像上建立與產品連結的熱點，快速將產品新增至購物車。

按一下熱點會開啟一個對話方塊，讓您選擇產品的大小和數量。

1. 導覽至您要新增元件的頁面。
1. 將元件拖放至頁面中。
1. 從 [資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. 您可以:

   * 按一下元件，然後按一下「編輯」圖示
   * 按兩下

1. 按一下全螢幕圖示。

   ![chlimage_1-92](/help/sites-administering/assets/chlimage_1-92.png)

1. 按一下「啟動對應」圖示。

   ![chlimage_1-93](/help/sites-administering/assets/chlimage_1-93.png)

1. 按一下其中一個形狀表徵圖。

   ![chlimage_1-21](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. 根據需要修改和移動形狀。
1. 按一下形狀。
1. 按一下瀏覽圖示會開啟 [資產選擇器](/help/assets/search-assets.md#assetpicker).

   >[!NOTE]
   >
   >或者，您可以直接輸入必須在產品層級（而非變型層級）的產品路徑。

   ![chlimage_1-94](/help/sites-administering/assets/chlimage_1-94.png)

1. 按兩下確認圖示，然後按一下退出全螢幕。
1. 按一下元件旁之頁面上的某處。 頁面應會重新整理，您應會在影像上看到下列符號：

   ![](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. 切換至 [預覽](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui) 模式。
1. 按一下+熱點。 將開啟一個對話框，您可以在其中選擇輸入的產品的大小和數量 **路徑**.

   ![chlimage_1-95](/help/sites-administering/assets/chlimage_1-95.png)

1. 輸入大小和數量。
1. 按一下「添加到購物車」按鈕。 對話框關閉。
1. 導覽至您的購物車。 產品應該在這裡。

#### 配置選項 {#configuration-options}

您可以設定按一下熱點時對話方塊的外觀：

1. 按一下元件，然後按一下設定圖示。

   ![chlimage_1-96](/help/sites-administering/assets/chlimage_1-96.png)

1. 向下捲動. 有 **新增至購物車** 標籤。

   ![chlimage_1-97](/help/sites-administering/assets/chlimage_1-97.png)

1. 按一下 **新增至購物車**. 您可以使用3個設定選項。

   ![chlimage_1-98](/help/sites-administering/assets/chlimage_1-98.png)

1. 按一下「完成」圖示。

## 目錄 {#catalogs}

### 產生目錄 {#generating-a-catalog}

#### 產生目錄 — 觸控最佳化UI {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>目錄會參考您的產品資料。

要生成目錄：

1. 開啟Sites主控台(例如 [http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content))。
1. 導覽至您要建立新頁面的位置。
1. 若要開啟選項清單，請使用 **建立** 圖示：

   ![建立圖示](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. 從清單中選取 **建立目錄**，則會開啟「建立目錄」精靈。

   ![chlimage_1-99](/help/sites-administering/assets/chlimage_1-99.png)

1. 導覽至所需的目錄Blueprint。
1. 點選/按一下 **選擇** 按鈕，然後點選/按一下所需的「目錄Blueprint」。
1. 點選/按一下 **下一個**.

   ![chlimage_1-100](/help/sites-administering/assets/chlimage_1-100.png)

1. 輸入 **標題** 和 **名稱**.
1. 點選/按一下 **建立** 按鈕。 目錄隨即建立，對話方塊隨即開啟。

   ![chlimage_1-101](/help/sites-administering/assets/chlimage_1-101.png)

1. 點選/按一下 **完成** 按鈕會將您帶回Sites主控台，讓您可在其中查看目錄。

   點選/按一下 **開啟目錄** 按鈕會開啟您的目錄(例如 `http://localhost:4502/editor.html/content/test-catalog.html`)。

#### 產生目錄 — 傳統UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>目錄會參考您的 [產品資料](#products-and-product-variants).

1. 使用 **網站** 主控台，導覽至 **目錄Blueprint**，然後是基礎目錄。

   例如：

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. 使用 **章節Blueprint** 範本。

   例如， `Swimwear`.

1. 開啟新 `Swimwear` 頁面，然後按一下 **編輯Blueprint** 開啟 **屬性** 對話框，可在此設定 **產品** 中。

   例如，開啟 **標籤/關鍵字** 欄位，依序選取「活動」、「從Geometrixx — 戶外區域游泳」。

1. 按一下 **確定** 儲存屬性；範例產品將顯示在 **產品選擇標準** 在Blueprint頁面上。
1. 按一下 **轉出變更……**，選取 **轉出頁面和所有子頁面**，然後按一下 **下一個** then **轉出**. 成功完成轉出後， **狀態** 指示器將顯示為綠色。
1. 您現在可以按一下 **關閉** 查新目錄部分；例如，在和底下：

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. 從Blueprint頁再次按一下 **編輯Blueprint** 和 **屬性** 對話框開啟 **產生的頁面** 標籤。 在「橫幅清單」欄位中，選取您要顯示的影像；例如， `summer.jpg`
1. 按一下 **確定** 儲存屬性；橫幅資訊會顯示在 **產品選擇標準** 在Blueprint頁面上。
1. 轉出這些新變更。

### 轉出目錄 {#rolling-out-a-catalog}

#### 轉出目錄 — 觸控最佳化UI {#rolling-out-a-catalog-touch-optimized-ui}

若要轉出目錄：

1. 導覽至 **目錄** 主控台，透過 **商務**.
1. 導覽至您要轉出的目錄。
1. 使用下列其中一項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選取 **轉出變更** 圖示：

   ![轉出](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. 在精靈中，視需要設定轉出，然後點選/按一下 **轉出變更**.
1. 對話方塊隨即開啟。 點選/按一下 **完成** 當處理完成時。

#### 轉出目錄 — 傳統UI {#rolling-out-a-catalog-classic-ui}

若要轉出目錄：

1. 導覽至您要轉出的目錄。 例如：

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. 按一下 **轉出變更……**
1. 視需要設定轉出。
1. 按一下 **轉出**.

### Blueprint匯入工具 {#blueprint-importer}

#### Blueprint匯入工具 — 觸控最佳化UI {#blueprint-importer-touch-optimized-ui}

1. 導覽至 **目錄** 主控台，透過 **商務**.
1. 導覽至您要匯入目錄Blueprint的位置。
1. 點選/按一下 **導入藍圖** 表徵圖。

   ![](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 在精靈中，視需要選取來源，然後點選/按一下 **下一個**.

   ![chlimage_1-340](/help/sites-administering/assets/chlimage_1-102.png)

1. 點選/按一下 **完成** 匯入完成後。

#### Blueprint匯入工具 — 傳統UI {#blueprint-importer-classic-ui}

1. 使用 **工具** 主控台，導覽至 **商務**.

   例如：

   `http://localhost:4502/miscadmin#/etc/commerce`

1. 開啟 **目錄Bluprint匯入工具**.
1. 視需要設定匯入。
1. 按一下 **導入目錄藍圖**.

## 促銷活動 {#promotions}

### 建立促銷活動 {#creating-a-promotion}

#### 建立促銷活動 — 傳統UI {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>下列範例處理直接在 [行銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)，這用於憑單。
>
>促銷活動也可以在 [體驗](/help/sites-authoring/personalization.md) 行銷活動內。
>
>如需詳細資訊，請參閱 [促銷活動和憑單](#promotions-and-vouchers).

1. 開啟 **網站** 製作例項的主控台。
1. 在左窗格中，選取您需要的 **行銷活動**.
1. 按一下 **新增**，請選取 **促銷活動** 範本，然後指定 **標題** (和 **名稱** （如有需要）。
1. 按一下&#x200B;**建立**。新的促銷活動頁面會顯示在右側窗格中。

1. 編輯 **屬性** 按下列其中一項：

   * 開啟頁面，然後按一下「編輯」按鈕以開啟「屬性」對話方塊
   * 在網站主控台中選取頁面，然後使用內容功能表（通常是滑鼠右鍵）來選取 **屬性……** 並開啟「屬性」對話框

   指定 **促銷活動類型**, **折扣類型**, **折扣值** 和任何其他欄位。

1. 按一下 **確定** 儲存。

1. 您現在可以啟動您的促銷活動，讓購物者在發佈執行個體上看到它。

## 憑單 {#vouchers}

### 建立憑單 {#creating-a-voucher}

#### 建立憑單 — 傳統UI {#creating-a-voucher-classic-ui}

1. 開啟 **網站** 製作例項的主控台。
1. 在左窗格中，選取您需要的 **行銷活動**.
1. 按一下 **新增**，請選取 **憑單** 範本，然後指定 **標題** (和 **名稱** （如有需要）。
1. 按一下&#x200B;**建立**。新憑單頁將顯示在右窗格中。

1. 按兩下以開啟新憑單頁面，然後按一下 **編輯** 以視需要設定資訊。
1. 按一下 **確定** 儲存。

1. 您現在可以啟動您的憑單，讓購物者可以在發佈執行個體的購物車中使用。

### 刪除憑單 {#removing-vouchers}

#### 刪除憑單 — 傳統UI {#removing-vouchers-classic-ui}

為使客戶無法使用憑單，您可以：

* 停用憑證 — 憑證將保留在製作環境中，以便您稍後重新啟用。
* 完全刪除。

這兩個動作都可從 **網站** 控制台。

### 修改憑單 {#modifying-vouchers}

#### 修改憑單 — 傳統UI {#modifying-vouchers-classic-ui}

要更改憑證或促銷的屬性，可以在 **網站** 主控台，按一下 **編輯**. 儲存後，您應該啟動它，以便將變更推送至發佈執行個體。

### 向購物車添加憑單 {#adding-vouchers-to-a-cart}

若要允許用戶向購物車添加憑單，您可以使用內置 **憑單** 元件（商務類別）。 您必須將此項目新增至與購物車顯示位置相同的頁面（但不是強制項目）。 憑單元件僅僅是一種表單，用戶可以在其中輸入憑單代碼，它是實際顯示已申請憑單及其折扣清單的購物車元件。

在示範網站(Geometrixx Outdoors — 英文)中，您可以在購物車頁面的實際購物車下方看到憑證表單。

## 訂購 {#orders}

>[!NOTE]
>
>應該記住，現成可用的AEM不具備與訂單相關的標準功能所需的操作，例如退回商品、更新訂單狀態、履行、生成裝箱單。 其主要用途為技術預覽。
>
>AEM中的一般訂單管理保持基本；精靈中可用的欄位取決於架構：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>如果您建立自訂的架構，則可儲存更多訂單資訊。

>[!NOTE]
>
>訂單控制台會公開供應商訂單資訊，這些資訊從未發佈。
>
>客戶訂單資訊保存在其主目錄中，並由其帳戶的訂單歷史記錄公開。 此資訊連同其他主目錄一起發佈。

### 建立訂單資訊 {#creating-order-information}

#### 建立訂單資訊 — 觸控最佳化UI {#creating-order-information-touch-optimized-ui}

1. 使用 **訂購** 主控台導覽至所需位置。
1. 使用 **建立** 圖示以選取 **建立順序**.

   ![](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 嚮導將開啟。 使用 **基本**, **內容**, **付款** 和 **履行** 頁簽 [關於新訂單的資訊](/help/commerce/cif-classic/administering/concepts.md#order-information).

1. 選擇 **建立** 以儲存資訊。

### 編輯訂單資訊 {#editing-order-information}

#### 編輯訂單資訊 — 觸控最佳化UI {#editing-order-information-touch-optimized-ui}

1. 使用 **訂購** 主控台導覽至順序。
1. 使用下列其中一項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選取 **檢視訂單資料** 圖示：

   ![](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 此 [訂購資訊](/help/commerce/cif-classic/administering/concepts.md#order-information) 即會顯示。 使用 **編輯** 和 **完成** 進行任何變更。

