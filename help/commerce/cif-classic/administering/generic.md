---
title: 管理一般電子商務
seo-title: 管理一般電子商務
description: 通用AEM解決方案提供了管理儲存在儲存庫中的商務資訊的方法。
seo-description: 通用AEM解決方案提供了管理儲存在儲存庫中的商務資訊的方法。
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
docset: aem65
exl-id: c29f6213-1df6-45af-91c8-14b255276d82
translation-type: tm+mt
source-git-commit: 1cef6f87fa66fd78d439c23e6ac907f9531b8fd6
workflow-type: tm+mt
source-wordcount: '3009'
ht-degree: 1%

---

# 管理一般電子商務{#administering-generic-ecommerce}

該通AEM用解決方案提供了管理存放在儲存庫中的商務資訊的方法（而不是使用外部電子商務引擎）。 這包括：

* [產品](/help/commerce/cif-classic/administering/concepts.md#products)
* [產品的系列品種](/help/commerce/cif-classic/administering/concepts.md#product-variants)
* [目錄](/help/commerce/cif-classic/administering/concepts.md#catalogs)
* [促銷活動](/help/commerce/cif-classic/administering/concepts.md#promotions)
* [憑單](/help/commerce/cif-classic/administering/concepts.md#vouchers)
* [訂購](/help/commerce/cif-classic/administering/concepts.md#shopping-cart-and-orders)
* [代理頁](/help/commerce/cif-classic/administering/concepts.md#proxy-pages)

>[!NOTE]
>
>標準安AEM裝包含通用AEM(JCR)電子商務實作。
>
>這目前僅供展示之用，或根據您的需求做為自訂實作的基礎。

## 產品和產品變化{#products-and-product-variations}

>[!NOTE]
>
>下列程式適用於產品和產品變數。

在建立產品之前，您需要定義[Scaffold](/help/sites-authoring/scaffolding.md)。 這可指定您定義產品及編輯方式所需的欄位。

每種不同的產品類型都需要一個支架。 適當的支架通過以下任一方法與產品相關聯：

* 路徑
* 產品可以參照腳手架

>[!NOTE]
>
>Geometrixx-戶外商店有單一產品類型（因此也有單一支架）:
>
>`/etc/scaffolding/geometrixx-outdoors`
>
>Geometrixx-戶外產品類型在上處於活動狀態：
>
>`/etc/commerce/products/geometrixx-outdoors`
>
>您可以在任何位置建立新的產品定義，而不需進行任何其他設定。

### 導入產品{#importing-products}

#### 匯入產品——最佳化觸控式UI {#importing-products-touch-optimized-ui}

1. 通過&#x200B;**Commerce**&#x200B;瀏覽至&#x200B;**Products**&#x200B;控制台。
1. 使用&#x200B;**Products**&#x200B;控制台導航到所需位置。
1. 使用&#x200B;**匯入產品**&#x200B;圖示來開啟精靈。

   ![chlimage_1-1](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 指定下列設定：

   * **匯入工具**

      特定[商務提供者](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)的匯入工具，預設為`Geometrixx`。

   * **來源**

      要導入的檔案；您可以使用瀏覽器來選擇檔案。

   * **增量匯入**

      指出這是否為增量匯入（而非完全匯入）。
   >[!NOTE]
   >
   >遞增匯入（範例geometrixx-outdoor匯入工具的）會在產品層級運作。
   >
   >可以定義自訂的匯入工具，以視需要運作。

1. 選擇&#x200B;**Next**&#x200B;以導入產品，將顯示所執行操作的日誌。

   >[!NOTE]
   >
   >產品將匯入或相對於目前位置。

   >[!NOTE]
   >
   >重複使用&#x200B;**Next**&#x200B;和&#x200B;**Back**&#x200B;將重複導入產品定義。 但是，由於它們具有相同的SKU，因此僅會覆寫儲存庫中現有的資訊。

1. 選擇&#x200B;**Done**&#x200B;關閉嚮導。

#### 導入產品- Classic UI {#importing-products-classic-ui}

1. 使用&#x200B;**Tools**&#x200B;控制台開啟&#x200B;**Commerce**&#x200B;資料夾。
1. 連按兩下以開啟&#x200B;**Product Importer**:

   ![chlimage_1-22](/help/sites-administering/assets/chlimage_1-22.jpeg)

1. 指定下列設定：

   * **存放區名稱**

      產品將匯入至：

      `/etc/commerce/products/<*store name*>/`

   * **商務提供程式**

      [commerce provider](/help/commerce/cif-classic/administering/concepts.md#commerce-providers)的匯入工具；預設Geometrixx。

   * **來源檔案**

      要導入的檔案的儲存庫中的位置。

   * **增量匯入**

      指出這是否為增量匯入（而非完全匯入）。

1. 按一下「匯入產品」。****

### 建立產品資訊{#creating-product-information}

>[!NOTE]
>
>標準產品管理是基本的，因為Geometrixx-戶外產品集一直保持基本。 複雜度是以產品[支架](/help/sites-authoring/scaffolding.md)為基礎，因此使用您自己的產品支架，就可進行更精密的編輯。

#### 建立產品資訊——最佳化觸控式UI {#creating-product-information-touch-optimized-ui}

1. 使用&#x200B;**Products**&#x200B;控制台（通過&#x200B;**Commerce**）導航到所需位置。
1. 使用&#x200B;**Create**&#x200B;圖示來選擇其中一個（視結構和位置而定）:

   * **建立產品**
   * **建立產品變數**

   ![chlimage_1-14](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 嚮導將開啟。 使用&#x200B;**Basic**&#x200B;和&#x200B;**產品標籤**&#x200B;輸入新產品或產品變型的[產品屬性](/help/commerce/cif-classic/administering/concepts.md#product-attributes)。

   >[!NOTE]
   >
   >**標** 題和 **** SKU是建立產品或變型所需的最低值。

1. 選擇&#x200B;**建立**&#x200B;以保存資訊。

>[!NOTE]
>
>許多產品都提供多種顏色和／或尺寸。 有關基本產品和相關產品變型的資訊可從&#x200B;**產品**&#x200B;控制台進行管理。
>
>產品及其變數會儲存為樹狀結構，產品資訊位於頂端，其下會有變數（此結構由UI強制執行）。

### 編輯產品資訊{#editing-product-information}

>[!NOTE]
>
>Geometrixx-outdoors中的產品影像可從以下網址取得：
>
>`/etc/commerce/products/...`
>
>這表示預設情況下，它們被[dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html)阻止，因此請根據需要進行配置。

#### 編輯產品資訊——最佳化觸控式UI {#editing-product-information-touch-optimized-ui}

1. 使用&#x200B;**Products**&#x200B;控制台（透過&#x200B;**Commerce**）瀏覽至您的產品資訊。
1. 使用下列任一項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選擇&#x200B;**查看產品資料**&#x200B;表徵圖：

   ![chlimage_1-3](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 將顯示[產品屬性](/help/commerce/cif-classic/administering/concepts.md#product-attributes)。 使用&#x200B;**Edit**&#x200B;和&#x200B;**Done**&#x200B;進行任何變更。

### 顯示產品參考{#showing-product-references}

#### 顯示產品參考——最佳化觸控式UI {#showing-product-references-touch-optimized-ui}

1. 使用&#x200B;**Products**&#x200B;控制台（透過&#x200B;**Commerce**）瀏覽至您的產品資訊。
1. 使用圖示開啟「參照」的次導軌：

   ![chlimage_1-4](/help/sites-administering/do-not-localize/chlimage_1-16.png)

1. 選擇所需產品——輔助導軌將更新以顯示可用的參考類型：

   ![chlimage_1-88](/help/sites-administering/assets/chlimage_1-88.png)

1. 按一下／點選參考類型（例如「產品頁面」）以展開清單。
1. 選擇特定參考以顯示選項：

   * 導覽至產品頁面
   * 編輯產品頁面

   ![chlimage_1-89](/help/sites-administering/assets/chlimage_1-89.png)

### 搜尋產品{#search-for-products}

1. 通過&#x200B;**Commerce**&#x200B;瀏覽至&#x200B;**Products**&#x200B;控制台。
1. 使用圖示開啟「搜尋」的次要邊欄：

   ![](/help/sites-administering/do-not-localize/chlimage_1-17.png)

1. 您可使用數個Facet來搜尋產品。 搜索只能使用一個或多個刻面。 找到的產品將顯示：

   ![chlimage_1-90](/help/sites-administering/assets/chlimage_1-90.png)

1. 按一下／點選產品會開啟產品。 您也可以發佈或檢視產品資料。

#### 擴展搜索{#extending-search}

您可以使用CRXDE Lite來修改現有Facet或新增Facet:

1. 導航到:

   `http://localhost:4502/crx/de/index.jsp#/libs/commerce/gui/content/products/aside/items/search/items/searchpanel/facets`

1. 例如，您可以修改產品搜尋頁面上將顯示的大小。 按一下`sizegroup`節點。
1. 按一下`items`節點，然後按一下`propertypredicate`節點。
1. 您可以修改`propertyValues`。 例如，您可以新增XS、XXL或移除大小。
1. 按一下「全部儲存」，並導覽至產品搜尋頁面。 ****&#x200B;您的變更應該會出現。

### 多個資產{#multiple-assets}

您可以在產品元件中新增多個資產，然後指定將顯示在產品頁面上的資產。

>[!NOTE]
>
>所有與多個資產相關的工作都可透過觸控最佳化UI完成。

#### 新增多個資產{#adding-multiple-assets}

1. 通過&#x200B;**Commerce**&#x200B;瀏覽至&#x200B;**Products**&#x200B;控制台。
1. 使用&#x200B;**Products**&#x200B;控制台，導覽至所需產品。

   >[!NOTE]
   >
   >你必須在產品層級，而不是在變型層級。

1. 點選／按一下「檢視產品資料」圖示（含選擇模式或快速動作）。****
1. 點選／按一下「編輯」圖示。
1. 捲動至&#x200B;**Add**。

   ![chlimage_1-91](/help/sites-administering/assets/chlimage_1-91.png)

1. 點選／按一下「**新增**」。 隨即出現新資產預留位置。
1. 點選／按一下**變更**會開啟一個對話方塊，讓您選擇資產。
1. 選取您要新增的資產。

   >[!NOTE]
   >
   >您可以選擇的資產為[Assets](/help/assets/assets.md)。

1. 點選／按一下「完成」圖示。

兩個資產現在會儲存在您的產品元件中。 您可以設定產品頁面上會顯示哪一個。 這適用於類別系統。 首先，您需要將類別新增至個別資產：

1. 點選／按一下「檢視產品資料」。****
1. 在資產下方鍵入&#x200B;**資產類別**，例如`cat1`和`cat2`。

   >[!NOTE]
   >
   >您也可以使用類別的標籤。

1. 點選／按一下「完成」圖示。 您現在必須[轉出](#rolling-out-a-catalog)您的變更。

現在，您的資產在產品元件中有一個類別。 您可以設定在三個不同層級顯示的類別：

* [產品頁面](#product-page)
* [目錄](#catalog)
* [產品主控台](#products-console)

>[!NOTE]
>
>如果您未設定類別，第一個資產會顯示在產品頁面上。

選擇要顯示的影像的機制如下：

1. 驗證是否為「產品頁」設定了類別。
1. 如果沒有，請驗證是否為目錄設定了類別。
1. 否則，驗證是否為產品控制台設定了類別。

>[!NOTE]
>
>對於目錄層級和產品主控台層級，您必須首先展開變更，才能套用修改並在產品頁面上查看差異。

#### 產品頁面 {#product-page}

1. 導覽至您的產品頁面。
1. **編** 輯產品元件。
1. 鍵入您選擇的&#x200B;**影像類別**（例如`cat1`）。
1. 點選／按一下&#x200B;**Done**。 頁面會重新整理，並應顯示正確的資產。

#### 目錄  {#catalog}

1. 導覽至您的目錄。
1. 點選／按一下「檢視屬性」。****
1. 點選／按一下&#x200B;**編輯**。
1. 點選／按一下&#x200B;**Assets**&#x200B;標籤。
1. 鍵入所需的&#x200B;**產品資產類別**。
1. 點選／按一下&#x200B;**Done**。
1. [統](#rolling-out-a-catalog) 計變更。

#### 產品控制台{#products-console}

1. 使用&#x200B;**Products**&#x200B;控制台，導覽至所需的產品。
1. 點選／按一下「檢視產品資料」。****
1. 點選／按一下&#x200B;**編輯**。
1. 鍵入&#x200B;**預設資產類別**。
1. 點選／按一下&#x200B;**Done**。
1. [統](#rolling-out-a-catalog) 計變更。

### 發佈／取消發佈產品資訊{#publishing-unpublishing-product-information}

#### 發佈／取消發佈產品資訊——觸控最佳化UI {#publishing-unpublishing-product-information-touch-optimized-ui}

>[!NOTE]
>
>通常，產品資訊會透過參考其頁面發佈。 例如，在發佈參照產品Y的頁面XAEM時，會詢問您是否也要發佈產品Y。
>
>在特殊情況下，AEM也支援直接從產品資料發佈。

1. 使用&#x200B;**Products**&#x200B;控制台（透過&#x200B;**Commerce**）瀏覽至您的產品資訊。
1. 使用下列任一項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   根據需要選擇&#x200B;**Publish**&#x200B;或&#x200B;**Unpublish**&#x200B;表徵圖：

   ![chlimage_1-6](/help/sites-administering/do-not-localize/chlimage_1-18.png) ![chlimage_1-7](/help/sites-administering/do-not-localize/chlimage_1-19.png)

   產品資訊會視需要發佈或取消發佈。

### 產品摘要{#product-feed}

Search&amp;Promote整合可讓您：

* 使用eCommerce API，獨立於基礎資料庫結構和商務平台。
* 運用Search&amp;Promote的「索引連接器」功能，以XML格式提供產品摘要。
* 運用Search&amp;Promote的「遠端控制」功能，執行產品饋送的隨選或排程要求
* 不同Search&amp;Promote帳戶的動態消息產生，設定為雲端服務設定。

如需詳細資訊，請閱讀[產品摘要](/help/sites-administering/product-feed.md)。

### 產品更新的事件處理常式{#event-handler-for-product-updates}

事件處理常式會在新增、修改或刪除產品時，以及新增、修改或刪除產品頁面時記錄事件。 有下列OSGi事件：

* `com/adobe/cq/commerce/pim/PRODUCT_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_DELETED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_ADDED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_MODIFIED`
* `com/adobe/cq/commerce/pim/PRODUCT_PAGE_DELETED`

對於`PRODUCT_*`事件，路徑指向`/etc/commerce/products`中的基本產品。 對於`PRODUCT_PAGE_*`事件，路徑指向`cq:Page`節點。

您可在Web Console的OSGI事件(`/system/console/events`)中查看這些事件，例如：

![](/help/sites-administering/do-not-localize/chlimage_1-20.png)

>[!NOTE]
>
>另請閱讀[](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/)中的AEM事件處理。[](https://blogs.adobe.com/experiencedelivers/experience-management/event_handling_incq/)

### 加入購物車連結的影像{#image-with-add-to-cart-links}

「包含新增至購物車連結的影像」元件可讓您在影像上建立與產品連結的熱點，以快速將產品新增至購物車。

按一下熱點將開啟一個對話框，可讓您選擇產品的大小和數量。

1. 導覽至您要新增元件的頁面。
1. 將元件拖放至頁面中。
1. 從[assets瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser)拖放元件中的影像。
1. 您可以:

   * 按一下元件，然後按一下「編輯」圖示
   * 按兩下滑鼠鍵，

1. 按一下全螢幕圖示。

   ![chlimage_1-92](/help/sites-administering/assets/chlimage_1-92.png)

1. 按一下「啟動地圖」圖示。

   ![chlimage_1-93](/help/sites-administering/assets/chlimage_1-93.png)

1. 按一下其中一個形狀圖示。

   ![chlimage_1-21](/help/sites-administering/do-not-localize/chlimage_1-21.png)

1. 根據需要修改和移動形狀。
1. 按一下形狀。
1. 按一下瀏覽圖示會開啟[資產選擇器](/help/assets/search-assets.md#assetpicker)。

   >[!NOTE]
   >
   >或者，您可以直接鍵入必須在產品層級而不是變型層級的產品路徑。

   ![chlimage_1-94](/help/sites-administering/assets/chlimage_1-94.png)

1. 按兩下確認圖示，然後按一下退出全螢幕。
1. 按一下元件旁頁面的某處。 頁面應會重新整理，您應會在影像上看到下列符號：

   ![](/help/sites-administering/do-not-localize/chlimage_1-22.png)

1. 切換至[preview](/help/sites-authoring/editing-content.md#previewingpagestouchoptimizedui)模式。
1. 按一下+熱點。 此時將開啟一個對話框，您可以在其中選擇在&#x200B;**Path**&#x200B;中輸入的產品的大小和數量。

   ![chlimage_1-95](/help/sites-administering/assets/chlimage_1-95.png)

1. 輸入大小和數量。
1. 按一下「新增至購物車」按鈕。 對話框關閉。
1. 導覽至您的購物車。 產品應該在這裡。

#### 配置選項{#configuration-options}

您可以配置按一下熱點時對話框的外觀：

1. 按一下元件，然後按一下設定圖示。

   ![chlimage_1-96](/help/sites-administering/assets/chlimage_1-96.png)

1. 向下捲動. 有一個&#x200B;**「添加到購物車」標籤。**

   ![chlimage_1-97](/help/sites-administering/assets/chlimage_1-97.png)

1. 按一下「新增至購物車」。 ****&#x200B;您可以使用3個配置選項。

   ![chlimage_1-98](/help/sites-administering/assets/chlimage_1-98.png)

1. 按一下「完成」圖示。

## 目錄{#catalogs}

### 生成目錄{#generating-a-catalog}

#### 產生目錄——最佳化觸控式UI {#generating-a-catalog-touch-optimized-ui}

>[!NOTE]
>
>目錄將參照您的產品資料。

要生成目錄，請執行以下操作：

1. 開啟網站主控台(例如[http://localhost:4502/sites.html/content](http://localhost:4502/sites.html/content))。
1. 導覽至您要建立新頁面的位置。
1. 要開啟選項清單，請使用&#x200B;**建立**&#x200B;表徵圖：

   ![create-icon](/help/sites-administering/do-not-localize/chlimage_1-23.png)

1. 從清單中選擇&#x200B;**建立目錄**，將開啟建立目錄嚮導。

   ![chlimage_1-99](/help/sites-administering/assets/chlimage_1-99.png)

1. 導覽至所需的目錄藍圖。
1. 點選／按一下&#x200B;**「選擇**」按鈕，點選／按一下所需的目錄藍圖。
1. 點選／按一下&#x200B;**Next**。

   ![chlimage_1-100](/help/sites-administering/assets/chlimage_1-100.png)

1. 鍵入&#x200B;**Title**&#x200B;和&#x200B;**Name**。
1. 點選／按一下&#x200B;**Create**&#x200B;按鈕。 目錄即會建立，並開啟對話方塊。

   ![chlimage_1-101](/help/sites-administering/assets/chlimage_1-101.png)

1. 點選／按一下&#x200B;**Done**&#x200B;按鈕會回到Sites主控台，您將可在此檢視目錄。

   點選／按一下&#x200B;**開啟目錄**&#x200B;按鈕可開啟您的目錄（例如`http://localhost:4502/editor.html/content/test-catalog.html`）。

#### 生成目錄- Classic UI {#generating-a-catalog-classic-ui}

>[!NOTE]
>
>目錄將引用您的[產品資料](#products-and-product-variants)。

1. 使用&#x200B;**Websites**&#x200B;控制台，導覽至&#x200B;**Catalog Blueprint**，然後導覽至Base Catalog。

   例如：

   `http://localhost:4502/siteadmin#/content/catalogs/geometrixx-outdoors/base-catalog`

1. 使用&#x200B;**Section Blueprint**&#x200B;範本建立新頁面。

   例如，`Swimwear`。

1. 開啟新的`Swimwear`頁面，然後按一下「編輯Blueprint **」以開啟「屬性****」對話方塊，您可在其中設定「產品****」選項。**

   例如，開啟&#x200B;**Tags/Keywords**&#x200B;欄位以選取「活動」，然後從「Geometrixx-戶外」區段中選取「游泳」。

1. 按一下&#x200B;**OK**&#x200B;保存屬性；範例產品將顯示在Blueprint頁面的&#x200B;**產品選擇標準**&#x200B;下。
1. 按一下&#x200B;**轉出更改……**，選擇&#x200B;**轉出頁面和所有子頁面**，然後按一下&#x200B;**Next**，然後按一下&#x200B;**Lovolt**。 成功完成轉出後，**Status**&#x200B;指示器將顯示為綠色。
1. 您現在可以按一下&#x200B;**Close**&#x200B;並檢查新目錄區段；例如，on和under:

   `http://localhost:4502/cf#/content/geometrixx-outdoors/en/swimwear.html`

1. 在藍圖頁面中，再次按一下&#x200B;**編輯Blueprint**，並在&#x200B;**屬性**&#x200B;對話框中開啟&#x200B;**生成的頁面**&#x200B;頁籤。 在「橫幅」清單欄位中，選取您要顯示的影像；例如，`summer.jpg`
1. 按一下&#x200B;**OK**&#x200B;保存屬性；橫幅資訊會顯示在Blueprint頁面的&#x200B;**產品選擇准則**&#x200B;下。
1. 推出這些新變更。

### 推出目錄{#rolling-out-a-catalog}

#### 推出目錄——最佳化觸控式UI {#rolling-out-a-catalog-touch-optimized-ui}

若要推出目錄：

1. 透過&#x200B;**Commerce**&#x200B;導覽至&#x200B;**Catalogs**&#x200B;主控台。
1. 導覽至您要推出的目錄。
1. 使用下列任一項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選擇&#x200B;**轉出更改**&#x200B;表徵圖：

   ![轉出](/help/sites-administering/do-not-localize/chlimage_1-24.png)

1. 在精靈中，視需要設定轉出，然後點選／按一下「轉出變更」**。**
1. 對話方塊隨即開啟。 當程式完成時，點選／按一下「完成&#x200B;****」。

#### 推出目錄- Classic UI {#rolling-out-a-catalog-classic-ui}

若要推出目錄：

1. 導覽至您要推出的目錄。 例如：

   `http://localhost:4502/cf#/content/catalogs/geometrixx-outdoors/base-catalog.html`

1. 按一下&#x200B;**轉出更改……**
1. 視需要設定轉出。
1. 按一下&#x200B;**Rovolt**。

### Blueprint Importer {#blueprint-importer}

#### Blueprint匯入工具——觸控最佳化UI {#blueprint-importer-touch-optimized-ui}

1. 透過&#x200B;**Commerce**&#x200B;導覽至&#x200B;**Catalogs**&#x200B;主控台。
1. 導覽至您要匯入目錄藍圖的位置。
1. 點選／按一下「匯入Blueprints **」圖示。**

   ![](/help/sites-administering/do-not-localize/chlimage_1-13.png)

1. 在嚮導中，根據需要選擇源並點選／按一下&#x200B;**Next**。

   ![chlimage_1-340](/help/sites-administering/assets/chlimage_1-102.png)

1. 匯入完成後點選／按一下「完成&#x200B;****」。

#### Blueprint Importer - Classic UI {#blueprint-importer-classic-ui}

1. 使用&#x200B;**Tools**&#x200B;控制台，導航至&#x200B;**Commerce**。

   例如：

   `http://localhost:4502/miscadmin#/etc/commerce`

1. 開啟&#x200B;**Catalog Bluprint Importer**。
1. 視需要設定匯入。
1. 按一下「**導入目錄藍圖**」。

## 促銷活動 {#promotions}

### 建立促銷{#creating-a-promotion}

#### 建立促銷- Classic UI {#creating-a-promotion-classic-ui}

>[!NOTE]
>
>下列範例處理直接在[促銷活動](/help/sites-classic-ui-authoring/classic-personalization-campaigns.md)中舉行的促銷活動，此促銷活動用於憑證。
>
>促銷活動也可以位於促銷活動的[experience](/help/sites-authoring/personalization.md)中。
>
>如需詳細資訊，請參閱[促銷和優惠券](#promotions-and-vouchers)。

1. 開啟您作者例項的&#x200B;**Websites**&#x200B;主控台。
1. 在左窗格中，選擇您所需的&#x200B;**促銷活動**。
1. 按一下「新增」**，選取「促銷」**&#x200B;範本，然後為新優惠券指定&#x200B;**「標題」**（如有需要，請指定&#x200B;**名稱**）。****
1. 按一下&#x200B;**建立**。新促銷頁面將顯示在右窗格中。

1. 編輯&#x200B;**Properties**，方法為：

   * 開啟頁面，然後按一下「編輯」按鈕以開啟「屬性」對話框
   * 在網站主控台中選取頁面，然後使用內容選單（通常是滑鼠右鍵）來選取「屬性……」**並開啟屬性對話方塊**

   根據需要指定&#x200B;**促銷類型**、**折扣類型**、**折扣值**&#x200B;和任何其他欄位。

1. 按一下&#x200B;**確定**&#x200B;保存。

1. 您現在可以啟動促銷，讓購物者在發佈例項中看到促銷。

## 憑單 {#vouchers}

### 建立優惠券{#creating-a-voucher}

#### 建立優惠券- Classic UI {#creating-a-voucher-classic-ui}

1. 開啟您作者例項的&#x200B;**Websites**&#x200B;主控台。
1. 在左窗格中，選擇您所需的&#x200B;**促銷活動**。
1. 按一下「新增」**「優惠券」範本，然後為新優惠券指定** Title **（如有需要，請指定** Name **）。******
1. 按一下&#x200B;**建立**。新的優惠券頁面會顯示在右側窗格中。

1. 按兩下以開啟新的優惠券頁面，然後按一下&#x200B;**編輯**&#x200B;以視需要設定資訊。
1. 按一下&#x200B;**確定**&#x200B;保存。

1. 您現在可以啟動優惠券，讓購物者可以在發佈實例的購物車中使用優惠券。

### 刪除憑單{#removing-vouchers}

#### 刪除憑單- Classic UI {#removing-vouchers-classic-ui}

為了讓客戶無法使用優惠券，您可以：

* 停用優惠券——優惠券將保留在作者環境中，以便您稍後重新啟用。
* 完全刪除。

這兩種動作都可從&#x200B;**Websites**&#x200B;主控台進行。

### 修改憑單{#modifying-vouchers}

#### 修改憑單——傳統UI {#modifying-vouchers-classic-ui}

若要變更優惠券或促銷的屬性，您可以在&#x200B;**網站**&#x200B;主控台上連按兩下優惠券或促銷的屬性，然後按一下&#x200B;**編輯**。 儲存後，您應啟用變更，以便將變更推送至發佈例項。

### 將憑單新增至購物車{#adding-vouchers-to-a-cart}

若要允許使用者將憑證新增至購物車，您可以使用內建的&#x200B;**憑證**&#x200B;元件（商務類別）。 您必須將此項目新增至顯示購物車的相同頁面（但非必要）。 憑單元件只是用戶可以輸入憑單代碼的表單，而購物車元件實際上顯示了已申請的憑單及其折扣清單。

在示範網站(Geometrixx Outdoors-英文)中，您可以在購物車頁面的實際購物車下看到優惠券表格。

## 訂購 {#orders}

>[!NOTE]
>
>應記住，現成可用的功能不AEM需要執行與訂單相關的標準功能，例如退貨、更新訂單狀態、完成、產生裝箱單。 主要是以技術預覽為目的。
>
>中的通用訂單管AEM理一直保持基本；嚮導中可用的欄位取決於腳手架：
>`/etc/scaffolding/geometrixx-outdoors/order/jcr:content/cq:dialog`
>
>如果您建立自訂的Scaffold，則可儲存更多訂單資訊。

>[!NOTE]
>
>訂單主控台會公開供應商訂單資訊，這些資訊從未發佈。
>
>客戶訂單資訊會保存在其首頁目錄中，並透過其帳戶的訂單記錄公開。 這些資訊會連同其他首頁目錄一起發佈。

### 建立訂單資訊{#creating-order-information}

#### 建立訂單資訊——觸控最佳化UI {#creating-order-information-touch-optimized-ui}

1. 使用&#x200B;**Orders**&#x200B;控制台導航到所需位置。
1. 使用&#x200B;**Create**&#x200B;表徵圖選擇&#x200B;**Create Order**。

   ![](/help/sites-administering/do-not-localize/chlimage_1-14.png)

1. 嚮導將開啟。 使用&#x200B;**Basic**、**Content**、**Payment**&#x200B;和&#x200B;**Fulfillment**&#x200B;標籤輸入有關新訂單[的資訊。](/help/commerce/cif-classic/administering/concepts.md#order-information)

1. 選擇&#x200B;**建立**&#x200B;以保存資訊。

### 編輯訂單資訊{#editing-order-information}

#### 編輯訂單資訊——觸控最佳化UI {#editing-order-information-touch-optimized-ui}

1. 使用&#x200B;**Orders**&#x200B;控制台導航至訂單。
1. 使用下列任一項：

   * [快速動作](/help/sites-authoring/basic-handling.md#quick-actions)
   * [選擇模式](/help/sites-authoring/basic-handling.md#navigating-and-selection-mode)

   選擇&#x200B;**查看訂單資料**&#x200B;表徵圖：

   ![](/help/sites-administering/do-not-localize/chlimage_1-15.png)

1. 將顯示[順序資訊](/help/commerce/cif-classic/administering/concepts.md#order-information)。 使用&#x200B;**Edit**&#x200B;和&#x200B;**Done**&#x200B;進行任何變更。

