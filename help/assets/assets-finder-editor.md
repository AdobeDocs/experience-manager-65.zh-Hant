---
title: 建立及設定資產編輯器頁面
description: 了解如何建立自訂資產編輯器頁面及同時編輯多個資產。
contentOwner: AG
role: User, Admin
feature: Developer Tools,Asset Management
exl-id: 53e310a9-c511-447a-91bd-8c5b2760dc03
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '2125'
ht-degree: 1%

---

# 建立及設定資產編輯器頁面 {#creating-and-configuring-asset-editor-pages}

本檔案說明下列項目：

* 建立自訂資產編輯器頁面的原因。
* 如何建立和自訂資產編輯器頁面（WCM頁面），可讓您檢視和編輯中繼資料，以及對資產執行動作。
* 如何同時編輯多個資產。

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 default samples. -->

>[!NOTE]
>
>「資產共用」可作為開放原始碼參考實作。 請參閱 [資產共用公域](https://adobe-marketing-cloud.github.io/asset-share-commons/). 未正式支援。

## 為何要建立和設定資產編輯器頁面？ {#why-create-and-configure-asset-editor-pages}

數位資產管理正在越來越多的案例中使用。 從面向專業培訓用戶（例如攝影師或分類學家）的小用戶群的小型解決方案，轉向更大、更多樣化的用戶群（例如業務用戶、WCM作者、記者等）時，功能強大的用戶介面 [!DNL Adobe Experience Manager Assets] 對於專業用戶，可能提供太多資訊，而利益相關方開始請求特定的用戶介面或應用程式，以訪問與他們相關的數字資產。

這些以資產為中心的應用程式可以是內部網路中的簡單照片集，員工可以從貿易展訪問上傳照片，或在面向公眾的網站中上傳新聞中心。 以資產為中心的應用程式也可以擴展到完整的解決方案，包括購物車、結帳和驗證流程。

建立以資產為中心的應用程式在很大程度上成為一種配置過程，它不需要編碼，只需了解用戶組及其需要，以及所使用元資料的知識。 以資產為中心的應用程式 [!DNL Assets] 可擴充：只要編碼工作量適中，便可建立可重複使用的元件，以便搜尋、檢視和修改資產。

以資產為中心的應用程式， [!DNL Experience Manager] 包含資產編輯器頁面，可用來取得特定資產的詳細檢視。 如果存取資產的使用者具有必要權限，資產編輯器頁面也允許編輯中繼資料。

<!--
## Create and configure an Asset Share page {#creating-and-configuring-an-asset-share-page}

You customize the DAM Finder functionality and create pages that have all the functionality you require, which are called Asset Share pages. To create a new Asset Share page, you add the page using the Geometrixx Asset Share template and then you customize the actions users can perform on that page, determine how viewers see the assets, and decide how users can build their queries.

Here are some use cases for creating a customized Asset Share page:

* Press Center for Journalists.
* Image Search Engine for internal business users.
* Image Database for website users.
* Media Tagging Interface for metadata editors.

### Create an Asset Share page {#creating-an-asset-share-page}

To create a new Asset Share page, you can either create it when you are working on web sites or from the digital asset manager.

>[!NOTE]
>
>By default, when you create an Asset Share page from **New** in the digital asset manager, an Asset viewer and Asset editor are automatically created for you.

To create an new Asset Share page in the **Websites** console:

1. In the **Websites** tab, navigate to the place where you want to create an asset share page and click **New**.

1. Select the **Asset Share** page and click **Create**. The new page is created and the asset share page is listed in the **Websites** tab.

![dam8](assets/dam8.png)

The basic page created using the Geometrixx DAM Asset Share template looks as follows:

![screen_shot_2012-04-18at115456am](assets/screen_shot_2012-04-18at115456am.png)

To customize your Asset Share page, you use elements from the sidekick and you also edit query builder properties. The page **Geometrixx Press Center** is a customized version of a page based on this template:

![screen_shot_2012-04-19at123048pm](assets/screen_shot_2012-04-19at123048pm.png)

To create a new asset share page via the digital asset manager:

1. In the digital asset manager, in **New**, select **New Asset Share**.
1. In the **Title**, enter the name of the asset share page. If desired, enter a name for the URL.

   ![screen_shot_2012-04-19at23626pm](assets/screen_shot_2012-04-19at23626pm.png)

1. Double-click the asset share page to open it and configure the page.

   ![screen_shot_2012-04-19at24114pm](assets/screen_shot_2012-04-19at24114pm.png)

   By default, when you create an Asset Share page from **New**, an Asset viewer and Asset editor are automatically created for you.

#### Customize actions {#customizing-actions}

You can determine what actions users can perform on selected digital assets from a selection of predefined actions.

To add actions to the Asset Share page:

1. In the Asset Share page that you want to customize, click **Actions** in the sidekick.

The following actions are available:

 | Action | Description |
 |---|---|
 | [!UICONTROL Delete Action] | Users can delete the selected assets. |
 | [!UICONTROL Download Action] | Lets users download selected assets to their computers. |
 | [!UICONTROL Lightbox Action] | Saves assets to a "lightbox"   where you can perform other actions on them. This comes in handy when working   with assets across multiple pages. The lightbox can also be used as a   shopping cart for assets. |
 | [!UICONTROL Move Action] | Users can move the asset to another   location |
 | [!UICONTROL Tags Action] | Lets users add tags to selected assets |
 | [!UICONTROL View Asset Action] | Opens the asset in the Asset editor for   user manipulation. |

1. Drag the appropriate action to the **Actions** area on the page. Doing so creates a button that is used to execute that action.

![chlimage_1-159](assets/chlimage_1-387.png)

#### Determine how search results are presented {#determining-how-search-results-are-presented}

You determine how results are displayed from a predefined list of lenses.

To change how search results are viewed:

1. In the Asset Share page that you want to customize, click Search.

![chlimage_1](assets/assetshare3.png)

1. Drag the appropriate lens to the top center of the page. In the Press Center, the lenses are already available. Users press the appropriate lens icon to display search results as desired.

The following lenses are available:

| Lens | Description |
|---|---|
| **[!UICONTROL List Lens]** |Presents the assets in a list fashion with details. |
| **[!UICONTROL Mosaic Lens]** |Presents assets in a mosaic fashion. |

#### Mosaic Lens {#mosaic-lens}

![chlimage_1-160](assets/chlimage_1-388.png)

#### List Lens {#list-lens}

![chlimage_1-161](assets/chlimage_1-389.png)

#### Customize the Query Builder {#customizing-the-query-builder}

The query builder lets you enter search terms and create content for the Asset Share page. When you edit the query builder, you also get to determine how many search results are displayed per page, which asset editor opens when you double-click an asset, the path the query searches, and customizes nodetypes.

To customize the query builder:

1. In the Asset Share page that you want to customize, click **Edit** in the Query Builder. By default, the **General** tab opens.
1. Select the number of results per page, the path of the asset editor (if you have a customized asset editor) and the Actions title.

![screen_shot_2012-04-23at15055pm](assets/screen_shot_2012-04-23at15055pm.png)

1. Click the **Paths** tab. Enter a path or multiple paths that the search will run. These paths are overwritten if the user uses the Paths predicate.

![screen_shot_2012-04-23at15150pm](assets/screen_shot_2012-04-23at15150pm.png)

1. Enter another node type, if desired.

1. In the **Query Builder URL** field, you can override or wrap the query builder and enter the new servlet URLs with the existing query builder component. In the **Feed URL** field, you can override the Feed URL as well.

![screen_shot_2012-04-23at15313pm](assets/screen_shot_2012-04-23at15313pm.png)

1. In the **Text** field, enter the text you want to appear for results and page numbers of results. Click **OK** when finished making changes.

![screen_shot_2012-04-23at15300pm](assets/screen_shot_2012-04-23at15300pm.png)

#### Add predicates {#adding-predicates}

Experience Manager Assets includes a number of predicates that you can add to the Asset Share page. These let your users further narrow searches. In some cases, they may override a query builder parameter (for example, the Path parameter).

To add predicates:

1. In the Asset Share page that you want to customize, click **Search**.

![assetshare3](assets/assetshare3.png)

1. Drag the appropriate predicates to the Asset Share page underneath the query builder. Doing so creates the appropriate fields.

![assetshare4](assets/assetshare4.png)

The following predicates are available:

| Predicate | Description |
|---|---|
| **[!UICONTROL Date Predicate]** |Lets users search for assets that were modified before and after certain dates. |
| **[!UICONTROL Options Predicate]** |The site owner can specify a property to search for (as in the property predicate, for example cq:tags) and a content tree to populate the options from (for example the tag tree). Doing so generates a list of options where the users can select the values (tags) that the selected property (tag property) should have. This predicate lets you build list controls like the list of tags, file types, image orientations, and so on. It is great for a fixed set of options. |
| **[!UICONTROL Path Predicate]** |Lets users define the path and subfolders, if desired. |
| **[!UICONTROL Property Predicate]** |The site owner specifies a property to search for, e.g. tiff:ImageLength and the user can then enter a value, e.g. 800. This returns all images that are 800 pixels high. Useful predicate if your property can have arbitrary values. |

For more information, see the [predicate Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/eval/package-summary.html).

1. To configure the predicate further, double-click it. For example, when you open the Path Predicate, you need to assign the root path.

![screen_shot_2012-04-23at15640pm](assets/screen_shot_2012-04-23at15640pm.png)
-->

## 建立和設定資產編輯器頁面 {#creating-and-configuring-an-asset-editor-page}

您可以自訂資產編輯器，以決定使用者如何檢視及編輯數位資產。 若要這麼做，您需建立新的資產編輯器頁面，然後自訂使用者可在該頁面上執行的檢視和動作。

>[!NOTE]
>
>如果您想要將自訂欄位新增至DAM資產編輯器，請新增 `cq:Widget` 節點到 `/apps/dam/content/asseteditors.`

### 建立資產編輯器頁面 {#creating-the-asset-editor-page}

建立「資產編輯器」頁面時，最佳作法是在「資產共用」頁面正下方建立頁面。

若要建立資產編輯器頁面：

1. 在 **[!UICONTROL 網站]** 標籤，導覽至您要建立資產編輯器頁面的位置，然後按一下 **新增**.
1. 選擇 **Geometrixx資產編輯器** 按一下 **建立**. 新頁面隨即建立，且頁面會列於 **網站** 標籤。

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

使用Geometrixx資產編輯器範本建立的基本頁面外觀如下：

![assetshare5](assets/assetshare5.png)

若要自訂資產編輯器頁面，請使用sidekick中的元素。 從 **Geometrixx新聞中心** 是根據此範本的自訂頁面版本：

![assetshare6](assets/assetshare6.png)

#### 設定從「資產共用」頁面開啟的資產編輯器 {#setting-which-asset-editor-opens-from-an-asset-share-page}

建立自訂的「資產編輯器」頁面後，您必須確定當您連按兩下自訂「資產共用」所建立的資產時，會在自訂的「編輯器」頁面中開啟資產。

若要設定「資產編輯器」頁面：

1. 在「資產共用」頁面中，按一下 **編輯** 查詢產生器旁邊。

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. 按一下 **一般** 頁簽。

1. 在 **資產編輯器路徑** 欄位中，輸入您要讓「資產共用」頁面在中開啟資產的資產編輯器路徑，然後按一下 **確定**.

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### 新增資產編輯器元件 {#adding-asset-editor-components}

您可以將元件新增至頁面，借此決定資產編輯器的功能。

若要新增資產編輯器元件：

1. 在您要自訂的資產編輯器頁面中，選取 **資產編輯器** 在側踢中。 隨即顯示所有可用的資產編輯器元件。

>[!NOTE]
>
>您可以自訂的項目取決於可用的元件。 要啟用元件，請轉至「設計」模式並選擇需要啟用的元件。

1. 將元件從sidekick拖曳至資產編輯器，並在元件對話方塊中進行任何修改。 這些元件在下表中進行了描述，並在後面的詳細說明中進行了描述。

>[!NOTE]
>
>設計資產編輯器頁面時，您會建立唯讀或可編輯的元件。 使用者知道，如果鉛筆的影像出現在該元件中，便可編輯欄位。 依預設，大部分元件都設為唯讀。

| Component | 說明 |
|---|---|
| **[!UICONTROL 中繼資料表單] 和 [!UICONTROL 中繼資料文字欄位]** | 可讓您新增其他中繼資料至資產，並對該資產執行動作（例如提交）。 |
| **[!UICONTROL 子資產]** | 可讓您自訂子資產。 |
| **標記** | 讓使用者選取標籤並新增至資產。 |
| **[!UICONTROL 縮圖]** | 顯示資產的縮圖、其檔案名稱，並讓您新增替代文字。 您也可以在此處新增資產編輯器動作。 |
| **[!UICONTROL 標題]** | 顯示可自訂的資產標題。 |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### 中繼資料表單和文字欄位 — 設定檢視中繼資料元件 {#metadata-form-and-text-field-configuring-the-view-metadata-component}

「中繼資料表單」是包含開始和結束動作的表單。 在中間，輸入 **文字** 欄位。 請參閱 [Forms](/help/sites-authoring/default-components-foundation.md#form-component) 以取得使用表單的詳細資訊。

1. 按一下 **編輯** 在表單的「開始」區域中。 您可以視需要輸入方塊標題。 依預設，方塊標題為 **中繼資料**. 如果要生成用於驗證的java-script客戶端代碼，請選中「客戶端驗證」複選框。

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. 按一下 **編輯** 在表單的「結束」區域。 例如，您可能想要建立 **[!UICONTROL 提交]** 選項，讓使用者提交其中繼資料變更。 您可以選擇新增 **重設** 將中繼資料重設為原始狀態的選項。

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. 介於 **表單開始** 和 **表單結尾**，將「中繼資料文字欄位」拖曳至表單。 使用者將中繼資料填入這些文字欄位中，以便提交或完成其他動作。

1. 按兩下欄位名稱，例如 **標題** 開啟中繼資料欄位並進行變更。 在 **一般** 的 **編輯元件** 視窗中，您可以定義命名空間和欄位標籤以及類型，例如 `dc:title`.

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

請參閱 [自訂和擴充資產](/help/assets/extending-assets.md) 有關修改元資料表單中可用命名空間的資訊。

1. 按一下 **限制** 標籤。 您可以在此選取欄位是否為必要欄位，並視需要新增任何限制。

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. 按一下 **顯示** 標籤。 您可以在此為中繼資料欄位輸入新的列寬和數目。 選取 **欄位為只讀** 核取方塊可讓使用者編輯中繼資料。

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

以下是包含各種欄位的中繼資料表單的範例：

![中繼資料](assets/chlimage_1-390.png)

然後，在「資產編輯器」頁面上，使用者可以在中繼資料欄位中輸入值（如果可編輯），並執行結束動作（例如提交變更）。

#### 子資產 {#sub-assets}

您可以在「子資產」元件檢視並選取子資產。 您可以決定下方顯示的名稱 [主要資產](/help/assets/assets.md#what-are-digital-assets) 和子資產。

連按兩下「子資產」元件以開啟子資產對話方塊，您可以在其中變更主要資產和任何子資產的標題。 預設值會顯示在對應欄位下方。

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

以下是填入的子資產元件的範例：

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

例如，如果您選取子資產，請注意元件如何顯示適當頁面，而Box標題會從「子資產」變更為「同層級」。

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### 標記 {#tags}

「標籤」元件是供使用者指派現有標籤至資產的元件，有助於日後進行組織與擷取。 您可將此元件設為唯讀，因此使用者無法新增標籤，而只能檢視標籤。

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

連按兩下「標籤」元件以開啟「標籤」對話方塊，您可以視需要從「標籤」變更標題，也可以在其中選取已分配的命名空間。 若要讓此欄位可編輯，請清除 **[!UICONTROL 隱藏編輯]** 框。 依預設，標籤是可編輯的。

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

如果使用者可以編輯標籤，則可從「標籤」下拉式選單中選取標籤，以按一下鉛筆來新增標籤。

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

以下是填入的「標籤」元件：

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### 縮圖 {#thumbnail}

縮圖元件是資產顯示所選縮圖的位置（對於許多格式，會自動擷取縮圖）。 此外，元件會顯示檔案名稱，以及 [可修改的動作](/help/assets/assets-finder-editor.md#adding-asset-editor-actions).

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

按兩下縮圖元件以開啟縮圖對話方塊，您可在其中變更alt文字。 預設情況下，縮圖alt文本預設為 **按一下以下載** 資產。

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

以下是填入的縮圖元件的範例：

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### 標題 {#title}

標題元件會顯示資產的標題和說明。

依預設，此選件為唯讀模式，因此使用者無法編輯。 若要讓其可編輯，請連按兩下元件並清除 **隱藏編輯按鈕** 核取方塊。 此外，請輸入多個資產的標題。

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

如果可以編輯「標題」，您可以按一下「鉛筆」開啟 **資產屬性** 窗口。 此外，您可以選取日期和時間，以開啟或關閉資產。

編輯 [!UICONTROL 標題]，則使用者可以變更 **標題**, **說明**，然後輸入 **開啟** 和 **關閉時間** 開啟或關閉資產。

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

以下是填入的標題元件的範例：

![chlimage_1-164](assets/chlimage_1-392.png)

#### 新增資產編輯器動作 {#adding-asset-editor-actions}

您可以從一系列預先定義的動作中，決定使用者可以對選取的數位資產執行哪些動作。

若要將動作新增至資產編輯器頁面：

1. 在您要自訂的資產編輯器頁面中，按一下 **資產編輯器** 在側踢中。

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

可使用下列動作：

| 動作 | 說明 |
|---|---|
| [!UICONTROL 下載] | 讓使用者將選取的資產下載至其電腦。 |
| [!UICONTROL 編輯] | 讓使用者編輯影像（互動式編輯） |
| [!UICONTROL Lightbox] | 將資產儲存至「燈箱」，您可在其中執行其他動作。 跨多個頁面使用資產時，此功能相當實用。 |
| [!UICONTROL 鎖定] | 讓使用者鎖定資產。 預設不會啟用此功能，且必須在元件清單中啟用。 |
| [!UICONTROL 引用] | 按一下這個按鈕，即可顯示使用資產的頁面。 |
| [!UICONTROL 版本設定] | 可讓您建立和還原資產的版本。 |

1. 將適當的動作拖曳至 **動作** 區域。 它會建立一個選項，用來執行拖曳至頁面上的動作。

![chlimage_1-165](assets/chlimage_1-393.png)

## 使用資產編輯器頁面多次編輯資產 {#multi-editing-assets-with-the-asset-editor-page}

使用 [!DNL Experience Manager Assets] 您可以一次變更數個資產。 選取資產後，您可以同時變更其：

* 標記
* 中繼資料

若要使用資產編輯器頁面多次編輯資產：

1. 開啟Geometrixx **新聞中心** 頁面：
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. 選取資產：

   * 在Windows上： `Ctrl + click` 每個資產。
   * 在Mac上： `Cmd + click` 每個資產。

   若要選取資產範圍：按一下第一個資產，然後 `Shift + click` 最後一個資產。

1. 按一下 **編輯中繼資料** 在 **動作** 欄位（頁面的左側）。
1. Geometrixx **新聞中心資產編輯器** 頁面會在新索引標籤中開啟。 資產的中繼資料顯示如下：

   * 標籤不會套用至所有資產，但只會套用至少數資產，而會以斜體顯示。
   * 套用至所有資產的標籤會以一般字型顯示。
   * 標籤以外的中繼資料：只有在所有選取的資產皆相同時，才會顯示欄位的值。

1. 按一下 **下載** 若要下載包含資產原始轉譯的ZIP檔案。
1. 按一下 **標籤** 欄位。

   * 不會套用至所有資產，但只會套用至少數資產的標籤，其背景會是灰色。
   * 套用至所有資產的標籤會有白色背景。

   您可以：

   * 按一下 `x` 移除所有資產的標籤。
   * 按一下 `+` 將標籤新增至所有資產。
   * 按一下 **箭頭** 並選取標籤，以新增標籤至所有資產。

   按一下 **確定** 將更改寫入窗體。 旁邊的盒子 **標籤** 欄位會自動勾選。

1. 編輯說明欄位。 例如，將其設為：

   `This is a common description`

   編輯欄位時，其值會在提交表單時覆寫所選資產的現有值。

   注意：編輯欄位時，會自動核取欄位旁的方塊。

1. 按一下 **更新中繼資料** 提交表單並儲存所有資產的變更。

   注意：僅修改已檢查的元資料。
