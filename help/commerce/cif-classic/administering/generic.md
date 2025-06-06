---
title: 管理一般電子商務
description: AEM一般解決方案提供管理存放庫中持有的商業資訊的方法。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
source-git-commit: 10268f617b8a1bb22f1f131cfd88236e7d5beb47
workflow-type: tm+mt
source-wordcount: '2907'
ht-degree: 1%

---

# 管理一般電子商務 {#administering-generic-ecommerce}

Adobe Experience Manager (AEM)一般解決方案提供管理存放庫內所儲存之商務資訊的方法（與使用外部電子商務引擎相反）。 其中包括：

* [產品](/help/commerce/cif-classic/administering/concepts.md#products)
* [產品的系列品種](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [目錄](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [促銷活動](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [憑單](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [訂購](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [Proxy頁面](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>標準AEM安裝包含通用AEM (JCR)電子商務實作。
>
>其目的是為了示範，或作為根據您需求自訂實作的基本基礎。

## 產品和產品變數 {#products-and-product-variations}

>[!NOTE]
>
>下列程式同時適用於產品與產品變體。

在建立產品之前，請先定義[支架](/help/sites-authoring/scaffolding.md)。 這會指定您必須定義的欄位、產品及其編輯方式。

每個不同的產品型別都需要支架。 適當的支架可透過以下任一方式與產品相關聯：

* 路徑
* 產品可參考架構

>[!NOTE]
>
>Geometrixx-Outdoors商店有單一產品型別（因此是單一支架）：
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Geometrixx — 戶外活動產品型別啟用於：
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>您可在產品定義下的任何位置建立產品定義，而無需任何其他設定。

### 匯入產品 {#importing-products}

#### 匯入產品 — 觸控最佳化UI {#importing-products-touch-optimized-ui}

1. 透過&#x200B;**Commerce**&#x200B;導覽至&#x200B;**產品**&#x200B;主控台。
1. 使用&#x200B;**產品**&#x200B;主控台導覽至所需位置。
1. 使用&#x200B;**匯入產品**&#x200B;圖示開啟精靈。

   ![匯入產品圖示](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 指定下列設定：

   * **匯入工具**

     特定[商務提供者](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)的匯入工具，預設為`Geometrixx`。

   * **Source**

     您要匯入的檔案；您可以使用瀏覽器來選取檔案。

   * **增量匯入**

     指出是否為增量匯入（而非完全匯入）。

   >[!NOTE]
   >
   >增量匯入（範例geometrixx-outdoor匯入工具的）會在產品層級運作。
   >
   >您可以定義自訂的匯入工具來視需要操作。

1. 選取&#x200B;**下一步**&#x200B;以匯入產品，會顯示所採取動作的記錄。

   >[!NOTE]
   >
   >產品會匯入至目前位置或相對於目前位置。

   >[!NOTE]
   >
   >重複使用&#x200B;**Next**&#x200B;和&#x200B;**Back**&#x200B;重複匯入產品定義。 但是，由於它們的SKU相同，因此會覆寫存放庫中現有的資訊。

1. 選取&#x200B;**完成**&#x200B;以關閉精靈。

#### 匯入產品 — Classic UI {#importing-products-classic-ui}

1. 使用&#x200B;**工具**&#x200B;主控台開啟&#x200B;**Commerce**&#x200B;資料夾。
1. 按兩下以開啟&#x200B;**產品匯入工具**：

   ![產品匯入工具主控台](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. 指定下列設定：

   * **存放區名稱**

     產品會匯入至：

     `/etc/commerce/products/<*store name*>/`

   * **Commerce提供者**

     您的[商務提供者](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)的匯入工具；預設Geometrixx。

   * **Source檔案**

     您要匯入的檔案在存放庫中的位置。

   * **增量匯入**

     指出是否為增量匯入（而非完全匯入）。

1. 按一下&#x200B;**匯入產品**。

### 建立產品資訊 {#creating-product-information}

>[!NOTE]
>
>標準產品管理是基本的，因為Geometrixx-Outdoors產品組是基本的。 複雜性取決於產品[支架](/help/sites-authoring/scaffolding.md)，因此有了您自己的產品支架，就可以進行更複雜的編輯。

#### 建立產品資訊 — 觸控最佳化UI {#creating-product-information-touch-optimized-ui}

1. 使用&#x200B;**產品**&#x200B;主控台(透過&#x200B;**Commerce**)導覽至所需位置。
1. 使用「**建立**」圖示來選取（視結構和位置而定）：

   * **建立產品**
   * **建立產品變數**

   ![加號形狀建立圖示](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 精靈隨即開啟。 使用&#x200B;**基本**&#x200B;與&#x200B;**產品標籤**&#x200B;輸入新產品或產品變體的[產品屬性](/help/commerce/cif-classic/administering/concepts.md#product-attributes)。

   >[!NOTE]
   >
   >**Title**&#x200B;和&#x200B;**SKU**&#x200B;是建立產品或變體所需的最低值。

1. 選取&#x200B;**建立**&#x200B;以儲存資訊。

>[!NOTE]
>
>許多產品的色彩和/或尺寸範圍不一。 基本產品和相關產品系列的相關資訊均可從&#x200B;**產品**&#x200B;主控台進行管理。
>
>產品及其變體會以樹狀結構儲存，產品資訊位於頂端，變體位於下方（此結構由UI強制執行）。

### 編輯產品資訊 {#editing-product-information}

>[!NOTE]
>
>geometrixx-outdoors中的產品影像提供自：
>
>`/etc/commerce/products/...`
>
>這表示預設會被[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant)封鎖，因此請視需要設定。

#### 編輯產品資訊 — 觸控最佳化UI {#editing-product-information-touch-optimized-ui}

1. 使用&#x200B;**產品**&#x200B;主控台(透過&#x200B;**Commerce**)導覽至您的產品資訊。
1. 使用下列其中一項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選取&#x200B;**檢視產品資料**&#x200B;圖示：

   ![檢視產品資料圖示 — 資訊圖示](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 顯示[產品屬性](/help/commerce/cif-classic/administering/concepts.md#product-attributes)。 使用&#x200B;**編輯**&#x200B;和&#x200B;**完成**&#x200B;進行任何變更。

### 顯示產品引用 {#showing-product-references}

#### 顯示產品參考 — 觸控最佳化UI {#showing-product-references-touch-optimized-ui}

1. 使用&#x200B;**產品**&#x200B;主控台(透過&#x200B;**Commerce**)導覽至您的產品資訊。
1. 使用圖示開啟參照的次要邊欄：

   ![雙箭頭圖示](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. 選取您需要的產品 — 次要邊欄更新，顯示可用的參考型別：

   ![參考開啟的產品主控台](/help/sites-administering/assets/chlimage_1-88.png)

1. 按一下參照型別（例如「產品頁面」）以展開清單。
1. 選取特定參照，以便顯示選項：

   * 導覽至產品頁面
   * 編輯產品頁面

   ![產品主控台參考面板](/help/sites-administering/assets/chlimage_1-89.png)

### 搜尋產品 {#search-for-products}

1. 透過&#x200B;**Commerce**&#x200B;導覽至&#x200B;**產品**&#x200B;主控台。
1. 使用圖示開啟要搜尋的次要邊欄：

   ![放大鏡圖示](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. 有數個面向可供您搜尋產品。 搜尋時只能使用一或多個多面。 找到的產品會出現：

   ![產品主控台中的產品資料](/help/sites-administering/assets/chlimage_1-90.png)

1. 按一下/點選產品會開啟它。 您也可以發佈或檢視產品資料。

#### 延伸搜尋 {#extending-search}

您可以使用CRXDE Lite修改現有多面或新增多面：

1. 瀏覽到:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. 例如，您可以編輯出現在產品搜尋頁面上的大小。 按一下`sizegroup`節點。
1. 按一下`items`節點，然後按一下`propertypredicate`節點。
1. 您可以編輯`propertyValues`。 例如，您可以新增XS、XXL或移除大小。
1. 按一下「儲存全部」**&#x200B;**，並導覽至產品搜尋頁面。 您的變更將會顯示。

### 多個Assets {#multiple-assets}

您可以在產品元件中新增多個資產，然後指定您要顯示在產品頁面上的資產。

>[!NOTE]
>
>與多個資產相關的所有工作都透過觸控最佳化的UI完成。

#### 新增多個Assets {#adding-multiple-assets}

1. 透過&#x200B;**Commerce**&#x200B;導覽至&#x200B;**產品**&#x200B;主控台。
1. 使用&#x200B;**產品**&#x200B;主控台，導覽至所需的產品。

   >[!NOTE]
   >
   >您必須處於產品層級，而不是變體層級。

1. 選取&#x200B;**檢視產品資料**&#x200B;圖示，其中包含選取模式或快速動作。
1. 選取編輯圖示。
1. 捲動至&#x200B;**新增**。

   ![正在新增產品資料熒幕擷取畫面](/help/sites-administering/assets/chlimage_1-91.png)

1. 選取&#x200B;**新增**。 新的資產預留位置隨即出現。
1. 選取&#x200B;**變更**&#x200B;會開啟一個對話方塊，讓您選擇資產。
1. 選取您要新增的資產。

   >[!NOTE]
   >
   >您可選取的資產來自[Assets](/help/assets/assets.md)。

1. 選取完成圖示。

產品元件現在儲存兩個資產。 您可以設定哪個要顯示在產品頁面上。 這適用於類別系統。 首先，您必須將類別新增至個別資產：

1. 選取&#x200B;**檢視產品資料**。
1. 在資產下輸入&#x200B;**資產類別**，例如`cat1`和`cat2`。

   >[!NOTE]
   >
   >您也可以使用類別的標籤。

1. 選取完成圖示。 您現在必須[轉出](#rolling-out-a-catalog)您的變更。

現在，您在產品元件中的資產有一個類別。 您可以設定在三個不同層級顯示哪個類別：

* [產品頁面](#product-page)
* [目錄](#catalog)
* [產品主控台](#products-console)

>[!NOTE]
>
>如果您未設定類別，產品頁面上會顯示第一個資產。

選取要顯示影像的機制如下：

1. 驗證是否為產品頁面設定了類別。
1. 如果沒有，請確認是否為目錄設定了類別。
1. 如果沒有，請確認是否為產品主控台設定了類別。

>[!NOTE]
>
>對於目錄層級和產品主控台層級，您必須轉出變更以套用修改並在產品頁面上檢視差異。

#### 產品頁面 {#product-page}

1. 導覽至您的產品頁面。
1. **編輯**&#x200B;產品元件。
1. 輸入您選擇的&#x200B;**影像類別** （例如`cat1`）。
1. 選取&#x200B;**完成**。 頁面會重新整理，且應會顯示正確的資產。

#### 目錄  {#catalog}

1. 導覽至您的目錄。
1. 選取&#x200B;**檢視屬性**。
1. 選取&#x200B;**編輯**。
1. 選取「**資產**」標籤。
1. 輸入必要的&#x200B;**產品資產類別**。
1. 選取「**完成**」。
1. [轉出](#rolling-out-a-catalog)您的變更。

#### 產品主控台 {#products-console}

1. 使用&#x200B;**產品**&#x200B;主控台，導覽至所需的產品。
1. 選取&#x200B;**檢視產品資料**。
1. 選取&#x200B;**編輯**。
1. 輸入&#x200B;**預設資產類別**。
1. 選取「**完成**」。
1. [轉出](#rolling-out-a-catalog)您的變更。

### 發佈/取消發佈產品資訊 {#publishing-unpublishing-product-information}

#### 發佈/取消發佈產品資訊 — 觸控最佳化UI {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>通常產品資訊會透過參考它的頁面發佈。 例如，發佈參考產品Y的頁面X時，AEM會詢問您是否要發佈產品Y。
>
>對於特殊情況，AEM也支援直接從產品資料發佈。

1. 使用&#x200B;**產品**&#x200B;主控台(透過&#x200B;**Commerce**)導覽至您的產品資訊。
1. 使用下列其中一項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   視需要選取&#x200B;**Publish**&#x200B;或&#x200B;**取消發佈**&#x200B;圖示：

   ![世界圖示](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![具有十字元號的世界圖示 — 無符號](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   視需要發佈或取消發佈產品資訊。

<!-- Search&Promote is end of life as of September 1, 2022 ### Product Feed {#product-feed} -->

<!-- Search&Promote is end of life as of September 1, 2022 The Search&Promote integration lets you: -->

<!-- Search&Promote is end of life as of September 1, 2022 * use the eCommerce API, independently of the underlying repository structure and commerce platform. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Index Connector feature of Search&Promote to provide a product feed in XML format. -->
<!-- Search&Promote is end of life as of September 1, 2022 * use the Remote Control feature of Search&Promote to perform on-demand or scheduled requests of the product feed -->
<!-- Search&Promote is end of life as of September 1, 2022 * feed generation for different Search&Promote accounts, configured as cloud services configurations. -->

<!-- Search&Promote is end of life as of September 1, 2022 For more information, read [Product Feed](/help/sites-administering/product-feed.md). -->

### 產品更新的事件處理常式 {#event-handler-for-product-updates}

有一個「事件處理常式」，可在新增、編輯或刪除產品以及新增、編輯或刪除產品頁面時記錄事件。 有以下OSGi事件：

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

對於`PRODUCT_*`個事件，路徑指向`/etc/commerce/products`中的基礎產品。 對於`PRODUCT_PAGE_*`個事件，路徑指向`cq:Page`節點。

您可以在OSGI事件( `/system/console/events`)的Web主控台中檢視它們，例如：

![OSGI事件範例](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>另請閱讀AEM[&#128279;](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/)中的事件處理。

### 含有加入購物車連結的影像 {#image-with-add-to-cart-links}

包含加入購物車連結的影像元件可讓您在影像上建立與產品連結的熱點，快速將產品加入購物車。

按一下熱點會開啟對話方塊，讓您選擇產品的大小和數量。

1. 導覽至您要新增元件的頁面。
1. 將元件拖放到頁面中。
1. 從[資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser)拖放元件中的影像。
1. 您可以執行下列兩個動作中的一個:

   * 按一下元件，然後按一下編輯圖示
   * 進行緩慢連按兩下

1. 按一下全熒幕圖示。

   ![全熒幕圖示](/help/sites-administering/assets/chlimage_1-92.png)

1. 按一下「啟動地圖」圖示。

   ![啟動地圖圖示](/help/sites-administering/assets/chlimage_1-93.png)

1. 按一下其中一個形狀圖示。

   ![圖案圖示](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. 視需要修改和移動形狀。
1. 按一下形狀。
1. 按一下瀏覽圖示會開啟[資產選擇器](/help/assets/search-assets.md#assetpicker)。

   >[!NOTE]
   >
   >或者，您可以直接鍵入必須在產品層級而不是變體層級的產品路徑。

   ![輸入路徑](/help/sites-administering/assets/chlimage_1-94.png)

1. 按兩下確認圖示，然後按一下退出全熒幕。
1. 在頁面元件旁的某處按一下。 頁面應該會重新整理，且您應該會在影像上看到下列符號：

   ![加號](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. 切換至[預覽](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui)模式。
1. 按一下+熱點。 會開啟一個對話方塊，您可在其中選擇在&#x200B;**路徑**&#x200B;中輸入的產品大小與數量。

   ![產品範例： poncho](/help/sites-administering/assets/chlimage_1-95.png)

1. 輸入大小與數量。
1. 按一下加入購物車按鈕。 對話方塊關閉。
1. 導覽至您的購物車。 產品應在這裡。

#### 設定選項 {#configuration-options}

您可以設定當您按一下熱點時對話方塊的外觀：

1. 按一下元件，然後按一下設定圖示。

   ![設定圖示](/help/sites-administering/assets/chlimage_1-96.png)

1. 向下捲動。 有&#x200B;**加入購物車**&#x200B;標籤。

   ![加入購物車索引標籤](/help/sites-administering/assets/chlimage_1-97.png)

1. 按一下&#x200B;**加入購物車**。 有三個組態選項可供您使用。

   ![組態選項](/help/sites-administering/assets/chlimage_1-98.png)

1. 按一下「完成」圖示。

## 目錄 {#catalogs}

### 產生目錄 {#generating-a-catalog}

#### 產生目錄 — 觸控最佳化UI {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>目錄會參考您的產品資料。

若要產生目錄：

1. 開啟Sites主控台(例如，[http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content))。
1. 導覽至您要建立頁面的位置。
1. 若要開啟選項清單，請使用&#x200B;**建立**&#x200B;圖示：

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. 從清單中選取&#x200B;**建立目錄**。 「建立目錄」精靈隨即開啟。

   ![建立目錄精靈](/help/sites-administering/assets/chlimage_1-99.png)

1. 導覽至所需的目錄Blueprint。
1. 選取&#x200B;**選取**&#x200B;按鈕，然後按一下所需的目錄Blueprint。
1. 選取&#x200B;**「下一步」**。

   ![目錄屬性精靈](/help/sites-administering/assets/chlimage_1-100.png)

1. 輸入&#x200B;**標題**&#x200B;和&#x200B;**名稱**。
1. 選取&#x200B;**建立**&#x200B;按鈕。 目錄隨即建立，對話方塊隨即開啟。

   ![目錄已建立的對話方塊](/help/sites-administering/assets/chlimage_1-101.png)

1. 選取「**完成**」按鈕可讓您回到Sites主控台，在那裡可以檢視您的目錄。

   點選/按一下&#x200B;**開啟目錄**&#x200B;按鈕會開啟您的目錄（例如，`http://localhost:4502/editor.html/content/test-catalog.html`）。

#### 產生目錄 — Classic UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>目錄參考您的[產品資料](#products-and-product-variants)。

1. 使用&#x200B;**網站**&#x200B;主控台，導覽至您的&#x200B;**目錄Blueprint**，然後導覽基本目錄。

   例如：

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. 使用&#x200B;**區段Blueprint**&#x200B;範本建立頁面。

   例如，`Swimwear`。

1. 開啟新的`Swimwear`頁面，然後按一下&#x200B;**編輯Blueprint**。 **屬性**&#x200B;對話方塊開啟，您可以設定&#x200B;**產品**&#x200B;選項。

   例如，開啟&#x200B;**標籤/關鍵字**&#x200B;欄位以選取「活動」，然後從「Geometrixx — 戶外」區段選取「游泳」。

1. 按一下「確定」**&#x200B;**&#x200B;以儲存您的屬性；範例產品會顯示在Blueprint頁面的「**產品選取條件**」下。
1. 按一下&#x200B;**轉出變更……**，選取&#x200B;**轉出頁面與所有子頁面**，然後按一下&#x200B;**下一步**，再按一下&#x200B;**轉出**。 轉出成功完成後，**狀態**&#x200B;指標會顯示為綠色。
1. 您現在可以按一下&#x200B;**關閉**&#x200B;並檢查新目錄區段；例如，在和底下：

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. 再次從Blueprint頁面按一下&#x200B;**編輯Blueprint**，然後在&#x200B;**屬性**&#x200B;對話方塊中開啟&#x200B;**產生的頁面**&#x200B;標籤。 在「橫幅」清單欄位中，選取您要顯示的影像，例如`summer.jpg`
1. 按一下「確定」**&#x200B;**&#x200B;以儲存您的屬性；橫幅資訊會顯示在Blueprint頁面的&#x200B;**產品選取條件**&#x200B;下。
1. 轉出這些新變更。

### 轉出目錄 {#rolling-out-a-catalog}

#### 推出目錄 — 觸控最佳化UI {#rolling-out-a-catalog-touch-optimized-ui}

轉出目錄：

1. 透過&#x200B;**Commerce**&#x200B;瀏覽至&#x200B;**目錄**&#x200B;主控台。
1. 導覽至您要轉出的目錄。
1. 使用下列其中一項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選取&#x200B;**轉出變更**&#x200B;圖示：

   ![轉出](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. 在精靈中，視需要設定轉出，然後按一下&#x200B;**轉出變更**。
1. 對話方塊開啟。 處理程式完成時選取&#x200B;**完成**。

#### 轉出目錄 — Classic UI {#rolling-out-a-catalog-classic-ui}

轉出目錄：

1. 導覽至您要轉出的目錄。 例如：

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. 按一下&#x200B;**轉出變更……**
1. 視需要設定轉出。
1. 按一下&#x200B;**轉出**。

### Blueprint Importer {#blueprint-importer}

#### Blueprint Importer — 觸控最佳化的UI {#blueprint-importer-touch-optimized-ui}

1. 透過&#x200B;**Commerce**&#x200B;瀏覽至&#x200B;**目錄**&#x200B;主控台。
1. 導覽至您要匯入目錄Blueprint的位置。
1. 選取&#x200B;**匯入藍圖**&#x200B;圖示。

   ![匯入Blueprint圖示](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 在精靈中，視需要選取Source，然後按一下[下一步]。**&#x200B;**

   ![Blueprint精靈](/help/sites-administering/assets/chlimage_1-102.png)

1. 匯入完成時選取&#x200B;**完成**。

#### Blueprint Importer — 傳統UI {#blueprint-importer-classic-ui}

1. 使用&#x200B;**工具**&#x200B;主控台，導覽至&#x200B;**Commerce**。

   例如：

   `http://localhost:4502/miscadmin#/etc/commerce`

1. 開啟&#x200B;**目錄Blueprint匯入工具**。
1. 視需要設定匯入。
1. 按一下&#x200B;**匯入目錄Blueprint**。

## 促銷活動 {#promotions}

### 建立促銷活動 {#creating-a-promotion}

#### 建立促銷活動 — Classic UI {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>下列範例處理直接在[行銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)中持有的促銷活動，此促銷活動用於憑單。
>
>促銷活動內的[體驗](/help/sites-authoring/personalization.md)中也可以有促銷活動。
>
>如需詳細資訊，請參閱[促銷和憑單](#promotions-and-vouchers)。

1. 開啟作者執行個體的&#x200B;**網站**&#x200B;主控台。
1. 在左窗格中，選取您所需的&#x200B;**促銷活動**。
1. 按一下「新增&#x200B;**」，選取**&#x200B;促銷活動&#x200B;**範本，然後指定新憑單的**&#x200B;標題&#x200B;**（及必要時指定**&#x200B;名稱&#x200B;**）。**
1. 按一下「**建立**」。新的促銷活動頁面會顯示在右側窗格中。

1. 編輯&#x200B;**屬性**，方法如下：

   * 開啟頁面，然後按一下「編輯」按鈕以開啟「屬性」對話方塊
   * 在網站主控台中選取頁面，然後使用內容功能表（通常是滑鼠右鍵）選取&#x200B;**內容……**&#x200B;並開啟內容對話方塊

   指定&#x200B;**促銷活動型別**、**折扣型別**、**折扣值**&#x200B;以及任何其他必要的欄位。

1. 按一下&#x200B;**確定**&#x200B;以儲存。

1. 您現在可以啟動促銷活動，讓購物者可以在發佈例項上檢視。

## 憑單 {#vouchers}

### 建立憑單 {#creating-a-voucher}

#### 建立憑單 — 傳統UI {#creating-a-voucher-classic-ui}

1. 開啟作者執行個體的&#x200B;**網站**&#x200B;主控台。
1. 在左窗格中，選取您所需的&#x200B;**促銷活動**。
1. 按一下「新增&#x200B;**」，選取**&#x200B;憑單&#x200B;**範本，然後指定新憑單的**&#x200B;標題&#x200B;**（及必要時指定**&#x200B;名稱&#x200B;**）。**
1. 按一下「**建立**」。新的憑單頁面會顯示在右側窗格中。

1. 按兩下以開啟您的新憑單頁面，然後按一下[編輯] **&#x200B;**&#x200B;並視需要設定資訊。
1. 按一下&#x200B;**確定**&#x200B;以儲存。

1. 您現在可以啟用憑單，讓購物者可以在發佈執行個體的購物車中使用它。

### 移除憑單 {#removing-vouchers}

#### 移除憑單 — 傳統UI {#removing-vouchers-classic-ui}

若要讓憑單無法供客戶使用，您可以：

* 停用憑單 — 其仍可在作者環境中使用，以便您稍後重新啟用。
* 將其完全刪除。

這兩項動作都可以從&#x200B;**網站**&#x200B;主控台完成。

### 修改憑單 {#modifying-vouchers}

#### 修改憑單 — 傳統UI {#modifying-vouchers-classic-ui}

若要變更憑單或促銷活動的內容，您可以在&#x200B;**網站**&#x200B;主控台上連按兩下，然後按一下&#x200B;**編輯**。 儲存後，您應該啟動它，以便將變更推送至發佈執行個體。

### 新增憑單至購物車 {#adding-vouchers-to-a-cart}

若要讓使用者將憑單新增至購物車，您可以使用內建的&#x200B;**憑單**&#x200B;元件(Commerce類別)。 將此專案新增到顯示購物車的相同頁面（但這並非強制性）。 憑單元件只是使用者可在其中輸入憑單代碼的表單，它是實際顯示套用憑單清單及其折扣的購物車元件。

在示範網站(Geometrixx Outdoors文 — 英文)中，您可以在購物車頁面上實際購物車下方看到憑單表單。

## 訂購 {#orders}

>[!NOTE]
>
>請記得，現成可用的AEM沒有訂單相關標準功能所需的動作，例如退回商品、更新訂單狀態、執行履行、產生包裝單。 它主要是作為技術預覽。
>
>AEM中的通用Order Management一直是基本功能；精靈中的可用欄位取決於支架：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>如果您建立自訂架構，則可儲存更多訂單資訊。

>[!NOTE]
>
>訂單主控台會公開永遠不會發佈的廠商訂單資訊。
>
>客戶訂單資訊儲存在其主目錄中，並由其帳戶的「訂單歷史記錄」顯示。 此資訊會與其主目錄的其餘部分一起發佈。

### 建立訂單資訊 {#creating-order-information}

#### 建立訂單資訊 — 觸控最佳化UI {#creating-order-information-touch-optimized-ui}

1. 使用&#x200B;**訂單**&#x200B;主控台導覽至所需位置。
1. 使用&#x200B;**建立**&#x200B;圖示來選取&#x200B;**建立訂單**。

   ![加號形狀建立圖示](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 精靈隨即開啟。 使用&#x200B;**Basic**、**Content**、**Payment**&#x200B;及&#x200B;**Fulfillment**&#x200B;索引標籤，輸入有關新訂單[&#128279;](/help/commerce/cif-classic/administering/concepts.md#order-information)的資訊。

1. 選取&#x200B;**建立**&#x200B;以儲存資訊。

### 編輯訂單資訊 {#editing-order-information}

#### 編輯訂單資訊 — 觸控最佳化UI {#editing-order-information-touch-optimized-ui}

1. 使用&#x200B;**訂單**&#x200B;主控台導覽至訂單。
1. 使用下列其中一項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選取&#x200B;**檢視訂單資料**&#x200B;圖示：

   ![資訊圖示](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 顯示[訂單資訊](/help/commerce/cif-classic/administering/concepts.md#order-information)。 使用&#x200B;**編輯**&#x200B;和&#x200B;**完成**&#x200B;進行任何變更。

