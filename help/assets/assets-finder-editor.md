---
title: 「建立和配置資產編輯器」頁
description: 瞭解如何建立自訂資產編輯器頁面並同時編輯多個資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '2120'
ht-degree: 1%

---


# 「建立和配置資產編輯器」頁 {#creating-and-configuring-asset-editor-pages}

本檔案說明下列內容：

* 建立自訂資產編輯器頁面的原因。
* 如何建立和自訂資產編輯器頁面，這些頁面是WCM頁面，可讓您檢視和編輯中繼資料，以及對資產執行動作。
* 如何同時編輯多個資產。

<!-- TBD: Add UICONTROL tags. Need PM review. Flatten the structure a bit. Re-write to remove Geometrixx mentions and to adhere to 6.5 default samples. -->

>[!NOTE]
>
>「資產共用」可做為開放原始碼參考實作。 請參 [閱資產共用共用](https://adobe-marketing-cloud.github.io/asset-share-commons/)。 未正式支援。

## 為何要建立和設定資產編輯器頁面？ {#why-create-and-configure-asset-editor-pages}

數位資產管理正被越來越多的案例所使用。 當專業使用者從專業訓練使用者的小型解決方案（例如攝影師或分類學者）移轉至更大且更多樣化的使用者群組（例如商業使用者、WCM作者、記者等）時，專業使用者的強大使用者介面可提供太多資訊，而利益相關者會開始要求特定使用者介面或應用程式存取與他們相關的數位資產。 [!DNL Adobe Experience Manager Assets]

這些以資產為中心的應用程式可以是內部網路中簡單的像片收藏館，員工可從商業展覽或公開網站的新聞中心上傳像片。 以資產為中心的應用程式也可以延伸至完整的解決方案，包括購物車、結帳和驗證程式。

建立以資產為中心的應用程式，在很大程度上會變成不需撰寫程式碼的設定程式，只需瞭解使用者群組及其需求，以及所使用中繼資料的知識即可。 使用建立的資產導向應用程式可 [!DNL Assets] 擴充： 使用適中的編碼工作，可重複使用的元件來搜尋、檢視和修改資產。

中以資產為中心的應 [!DNL Experience Manager] 用程式包含「資產編輯器」頁面，可用來取得特定資產的詳細檢視。 資產編輯器頁面也允許編輯元資料，前提是訪問資產的用戶具有必要的權限。

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

## 「建立和配置資產編輯器」頁 {#creating-and-configuring-an-asset-editor-page}

您可自訂資產編輯器，以決定使用者如何檢視和編輯數位資產。 若要這麼做，請建立新的「資產編輯器」頁面，然後自訂使用者可在該頁面上執行的檢視和動作。

>[!NOTE]
>
>如果要將自訂欄位新增至DAM資產編輯器，請新增節 `cq:Widget` 點至 `/apps/dam/content/asseteditors.`

### 「建立資產編輯器」頁 {#creating-the-asset-editor-page}

建立「資產編輯器」頁面時，最佳做法是直接在「資產共用」頁面下方建立頁面。

要建立「資產編輯器」頁，請執行以下操作：

1. 在「網 **[!UICONTROL 站]** 」標籤中，導覽至您要建立資產編輯器頁面的位置，然後按一下「新 **增」**。
1. 選取「 **Geometrixx Asset Editor」(Geometrixx資產編輯器** )，然後按 **一下「建立**」。 新頁面隨即建立，頁面會列在「網站」 **標籤** 中。

![screen_shot_2012-04-23at15858pm](assets/screen_shot_2012-04-23at15858pm.png)

使用Geometrixx Asset Editor範本建立的基本頁面外觀如下：

![assetshare5](assets/assetshare5.png)

若要自訂資產編輯器頁面，請使用sidekick中的元素。 從 **** Geometrixx Press Center存取的「資產編輯器」頁面是以此範本為基礎的頁面自訂版本：

![assetshare6](assets/assetshare6.png)

#### 將「資產編輯器」設為從「資產共用」頁面開啟 {#setting-which-asset-editor-opens-from-an-asset-share-page}

建立自訂的「資產編輯器」頁面後，您必須確定，當您連按兩下所建立之自訂「資產共用」資產時，會在自訂的「編輯器」頁面中開啟資產。

要設定「資產編輯器」頁：

1. 在「資產共用」頁面中，按一下「 **查詢產生器** 」旁的「編輯」。

![screen_shot_2012-04-23at20123pm](assets/screen_shot_2012-04-23at20123pm.png)

1. 如果尚未選 **擇** 「常規」頁籤，請按一下該頁籤。

1. 在「資 **產編輯器的路徑」欄位中** ，輸入您要讓「資產共用」頁面在中開啟資產的資產編輯器的路徑，然後按一下「確 **定」**。

![screen_shot_2012-04-23at21653pm](assets/screen_shot_2012-04-23at21653pm.png)

#### 新增資產編輯器元件 {#adding-asset-editor-components}

您可以借由將元件新增至頁面，來決定資產編輯器的功能。

要添加資產編輯器元件：

1. 在您要自訂的「資產編輯器」頁面中，選取側 **點中的「資產編輯器** 」。 將顯示所有可用的資產編輯器元件。

>[!NOTE]
>
>您可自訂的項目取決於可用的元件。 若要啟用元件，請移至「設計」模式，並選取您需要啟用的元件。

1. 將元件從側腳拖曳至資產編輯器，並在元件對話方塊中進行任何修改。 下表對這些元件進行了說明，並在後面的詳細說明中進行了說明。

>[!NOTE]
>
>在設計資產編輯器頁面時，您可以建立唯讀或可編輯的元件。 使用者知道，如果鉛筆的影像出現在該元件中，就可以編輯欄位。 依預設，大部分元件都會設為唯讀。

| 元件 | 說明 |
|---|---|
| **[!UICONTROL 中繼資料表單]和中繼資[!UICONTROL 料文字欄位]** | 可讓您新增其他中繼資料至資產，並對該資產執行動作，例如提交。 |
| **[!UICONTROL 子資產]** | 可讓您自訂子資產。 |
| **標記** | 可讓使用者選取並新增標籤至資產。 |
| **[!UICONTROL 縮圖]** | 顯示資產的縮圖及其檔案名稱，並讓您新增替代文字。 您也可以在此處新增資產編輯器動作。 |
| **[!UICONTROL 標題]** | 顯示可自訂的資產標題。 |

![screen_shot_2012-04-23at22743pm](assets/screen_shot_2012-04-23at22743pm.png)

#### 中繼資料表單與文字欄位——設定檢視中繼資料元件 {#metadata-form-and-text-field-configuring-the-view-metadata-component}

中繼資料表單是包含開始和結束動作的表單。 在中間輸入「文 **本** 」欄位。 如需使 [用表單的詳細資訊](/help/sites-authoring/default-components-foundation.md#form-component) ，請參閱表單。

1. 按一下表單「開始」區 **域中的** 「編輯」，建立開始動作。 您可以視需要輸入「方塊」標題。 依預設，「方塊」標題為「中繼 **資料」**。 如果要生成用於驗證的java-script客戶端代碼，請選中「客戶端驗證」複選框。

![screen_shot_2012-04-23at22911pm](assets/screen_shot_2012-04-23at22911pm.png)

1. 通過按一下表單的「結 **束** 」區域中的「編輯」(Edit)建立「結束」(End)操作。 例如，您可能想要建立「提交」 **按鈕** ，讓使用者提交其中繼資料變更。 或者，您可以新增「重設 **」按鈕** ，將中繼資料重設為其原始狀態。

![screen_shot_2012-04-23at23138pm](assets/screen_shot_2012-04-23at23138pm.png)

1. 在「表單開 **始** 」和「表 **單結束」之間**，將中繼資料文字欄位拖曳至表單。 使用者將中繼資料填入這些文字欄位，以提交或完成其他動作。

1. 連按兩下欄位名稱，例如 **Title** ，以開啟中繼資料欄位並進行變更。 在「編 **輯元件** 」窗口的「常規」頁籤中，定義命名空間和欄位標籤以及類型，例如 ****`dc:title`。

![screen_shot_2012-04-23at23305pm](assets/screen_shot_2012-04-23at23305pm.png)

如需 [](/help/assets/extending-assets.md) 修改中繼資料表單中可用名稱空間的相關資訊，請參閱自訂和擴充資產。

1. 按一下「約 **束** 」(Constraints)頁籤。 您可以在此處選擇欄位是否為必需欄位，並根據需要添加任何約束。

![screen_shot_2012-04-23at23435pm](assets/screen_shot_2012-04-23at23435pm.png)

1. 按一下「顯 **示** 」標籤。 在這裡，您可以為中繼資料欄位輸入新的寬度和行數。 選取「 **欄位為唯讀** 」核取方塊，讓使用者編輯中繼資料。

![screen_shot_2012-04-23at23446pm](assets/screen_shot_2012-04-23at23446pm.png)

以下是包含各種欄位的中繼資料表單範例：

![中繼資料](assets/chlimage_1-390.png)

然後，在「資產編輯器」頁面上，使用者可以在中繼資料欄位中輸入值（如果可編輯），並執行結束動作（例如提交變更）。

#### 子資產 {#sub-assets}

子資產元件是您可以檢視及選取子資產的位置。 您可以決定主要資產和子 [資產下](/help/assets/assets.md#what-are-digital-assets) ，顯示哪些名稱。

連按兩下「子資產」元件以開啟子資產對話方塊，您可在其中變更主要資產和任何子資產的標題。 預設值會顯示在對應欄位下方。

![screen_shot_2012-04-23at23907pm](assets/screen_shot_2012-04-23at23907pm.png)

以下是已填入子資產元件的範例：

![screen_shot_2012-04-23at24442pm](assets/screen_shot_2012-04-23at24442pm.png)

例如，如果您選取子資產，請注意元件如何顯示適當的頁面，而「方塊」標題會從「子資產」變更為「同級」。

![screen_shot_2012-04-23at24552pm](assets/screen_shot_2012-04-23at24552pm.png)

#### 標記 {#tags}

「標籤」元件是使用者可指派現有標籤至資產的元件，可協助日後組織與擷取。 您可將此元件設為唯讀，因此使用者無法新增標籤，但只能檢視標籤。

![screen_shot_2012-04-23at25031pm](assets/screen_shot_2012-04-23at25031pm.png)

連按兩下「標籤」元件以開啟「標籤」對話方塊，您可在其中視需要從「標籤」中變更標題，以及選取已分配的名稱空間。 若要讓此欄位可編輯，請清除「 **[!UICONTROL 隱藏編輯]** 」核取方塊。 依預設，標籤是可編輯的。

![screen_shot_2012-04-23at24731pm](assets/screen_shot_2012-04-23at24731pm.png)

如果使用者可以編輯標籤，則可以從「標籤」下拉式選單中選取標籤，按一下鉛筆以新增標籤。

![screen_shot_2012-04-23at25150pm](assets/screen_shot_2012-04-23at25150pm.png)

以下是已填入的「標籤」元件：

![screen_shot_2012-04-23at25244pm](assets/screen_shot_2012-04-23at25244pm.png)

#### 縮圖 {#thumbnail}

Thumbnail元件是資產顯示所選縮圖的位置（對於許多格式，會自動擷取縮圖）。 此外，元件會顯示檔案名稱，以 [及您可修改的動作](/help/assets/assets-finder-editor.md#adding-asset-editor-actions)。

![screen_shot_2012-04-23at25452pm](assets/screen_shot_2012-04-23at25452pm.png)

連按兩下縮圖元件，以開啟縮圖對話方塊，您可在其中變更alt文字。 依預設，縮圖alt文字預設為「按 **一下以下載資產** 」。

![screen_shot_2012-04-23at25604pm](assets/screen_shot_2012-04-23at25604pm.png)

以下是已填入的Thumbnail元件的範例：

![screen_shot_2012-04-23at34815pm](assets/screen_shot_2012-04-23at34815pm.png)

#### 標題 {#title}

「標題」元件會顯示資產的標題和說明。

依預設，它處於唯讀模式，因此使用者無法編輯它。 若要讓它可編輯，請連按兩下元件並清除「隱藏編 **輯按鈕** 」核取方塊。 此外，請輸入多個資產的標題。

![screen_shot_2012-04-23at35100pm](assets/screen_shot_2012-04-23at35100pm.png)

如果可以編輯「標題」，您可以按一下「鉛筆」開啟「資產屬性」視窗，以新增標題 **和說明** 。 此外，您也可以選擇日期和時間來開啟或關閉資產。

在編輯標題時 [!UICONTROL ，用戶可以更改]Title **、On**、 **Description**、Enter Times和Off Times以 ******** 關閉資產並關閉。

![screen_shot_2012-04-23at35241pm](assets/screen_shot_2012-04-23at35241pm.png)

以下是已填入Title元件的範例：

![chlimage_1-164](assets/chlimage_1-392.png)

#### 新增資產編輯器動作 {#adding-asset-editor-actions}

您可以從一系列預先定義的動作中，決定使用者可對選取的數位資產執行哪些動作。

要向「資產編輯器」頁添加操作，請執行以下操作：

1. 在您要自訂的「資產編輯器」頁面中，按一下側 **點中的「資產編輯器** 」。

![screen_shot_2012-04-23at35515pm](assets/screen_shot_2012-04-23at35515pm.png)

可執行下列動作：

| 動作 | 說明 |
|---|---|
| [!UICONTROL 下載] | 可讓使用者將選取的資產下載至其電腦。 |
| [!UICONTROL 編輯] | 讓使用者編輯影像（互動式編輯） |
| [!UICONTROL 燈箱] | 將資產儲存至「燈箱」，您可在其中執行其他動作。 在跨多個頁面處理資產時，此功能十分有用。 |
| [!UICONTROL 鎖定] | 可讓使用者鎖定資產。 此功能預設未啟用，必須在元件清單中啟用。 |
| [!UICONTROL 引用] | 按一下此按鈕，以顯示資產使用的頁面。 |
| [!UICONTROL 版本設定] | 可讓您建立和還原資產的版本。 |

1. 將適當的動作拖曳至頁 **面上** 「動作」區域。 這樣會建立用於執行該動作的按鈕。

![chlimage_1-165](assets/chlimage_1-393.png)

## 使用「資產編輯器」頁面進行多重編輯資產 {#multi-editing-assets-with-the-asset-editor-page}

您 [!DNL Experience Manager Assets] 可以一次變更數個資產。 在擁有選取的資產後，您可以同時變更其：

* 標記
* 中繼資料

若要使用「資產編輯器」頁面多重編輯資產：

1. 開啟Geometrixx **Press Center頁** :
   `https://localhost:4502/content/geometrixx/en/company/press.html`

1. 選取資產：

   * 在Windows上： `Ctrl + click` 每個資產。
   * 在Mac上： `Cmd + click` 每個資產。

   若要選取資產範圍： 按一下第一個資產，然 `Shift + click` 後按一下最後一個資產。

1. 按一 **下「動作****** 」欄位（頁面左側）中的「編輯中繼資料」。
1. 「Geometrixx **Press Center Asset Editor** 」（Geometrixx按中心資產編輯器）頁面會在新標籤中開啟。 資產的中繼資料顯示如下：

   * 標籤（不適用於所有資產，但僅適用於少數資產）會以斜體顯示。
   * 套用至所有資產的標籤會以一般字型顯示。
   * 除標籤以外的中繼資料： 只有在所有選取資產的欄位值相同時，才會顯示欄位值。

1. 按一 **下「下載** 」以下載包含資產原始轉譯的ZIP檔案。
1. 按一下「標籤」欄位旁的「編輯 **標籤** 」選項。

   * 標籤不會套用至所有資產，但只會套用至少數資產具有灰色背景。
   * 套用至所有資產的標籤具有白色背景。

   您可以：

   * 按一 `x` 下可移除所有資產的標籤。
   * 按一 `+` 下以新增標籤至所有資產。
   * 按一 **下箭頭** ，並選取標籤，以新增標籤至所有資產。

   按一下 **確定** ，將更改寫入表單。 「標籤」欄位旁 **的方塊** ，會自動勾選。

1. 編輯「說明」欄位。 例如，將其設定為：

   `This is a common description`

   編輯欄位時，其值會在提交表單時覆寫所選資產的現有值。

   注意： 編輯欄位時，會自動勾選欄位旁的方塊。

1. 按一 **下「更新中繼資料** 」以提交表單並儲存所有資產的變更。

   注意： 僅會修改已勾選的中繼資料。
