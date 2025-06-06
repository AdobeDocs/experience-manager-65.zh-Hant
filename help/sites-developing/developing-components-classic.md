---
title: 開發Adobe Experience Manager元件（傳統UI）
description: 傳統UI會使用ExtJS建立提供元件外觀的Widget。 HTL不是Adobe Experience Manager (AEM)的建議指令碼語言。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
exl-id: 3f078139-73fd-4913-9d67-264fb2515f8a
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2340'
ht-degree: 1%

---

# 開發Adobe Experience Manager (AEM)元件（傳統UI）{#developing-aem-components-classic-ui}

傳統UI會使用ExtJS建立提供元件外觀的Widget。 由於這些Widget的性質，元件與傳統UI和[觸控式UI](/help/sites-developing/developing-components.md)的互動方式有一些差異。

>[!NOTE]
>
>元件開發的許多方面對於傳統UI和觸控式UI都是通用的，因此&#x200B;**您必須閱讀[AEM元件 — 基本知識](/help/sites-developing/components-basics.md)，然後再閱讀**，此頁面會說明傳統UI的具體功能。

>[!NOTE]
>
>雖然HTML範本語言(HTL)和JSP都可用於開發傳統UI的元件，此頁面說明了使用JSP進行的開發。 這完全是因為在傳統UI中使用JSP的歷史。
>
>HTL現在是AEM的建議指令碼語言。 請參閱[HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=zh-Hant)和[開發AEM元件](/help/sites-developing/developing-components.md)以比較方法。

## 結構 {#structure}

元件基本結構涵蓋在[AEM Components - The Basics](/help/sites-developing/components-basics.md#structure)頁面，此頁面同時套用觸控式Eanbeld和傳統UI。 即使您不需要在新元件中使用觸控式UI的設定，從現有元件繼承時瞭解這些設定也會有所幫助。

## JSP指令碼 {#jsp-scripts}

JSP指令碼或Servlet可用於呈現元件。 根據Sling的請求處理規則，預設指令碼的名稱為：

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

JSP指令碼檔案`global.jsp`可用來讓特定物件（亦即存取內容）快速存取任何用來呈現元件的JSP指令碼檔案。

因此，每個元件轉譯JSP指令碼中都應包含`global.jsp`，其中使用了`global.jsp`中提供的一或多個物件。

預設`global.jsp`的位置為：

`/libs/foundation/global.jsp`

>[!NOTE]
>
>CQ 5.3及舊版所使用的路徑`/libs/wcm/global.jsp`現已過時。

### global.jsp、used API和Taglibs的功能 {#function-of-global-jsp-used-apis-and-taglibs}

以下列出預設`global.jsp`中提供的最重要物件：

摘要:

* `<cq:defineObjects />`

   * `slingRequest` — 包裝的要求物件( `SlingHttpServletRequest`)。
   * `slingResponse` — 包裝的回應物件( `SlingHttpServletResponse`)。
   * `resource` - Sling資源物件( `slingRequest.getResource();`)。
   * `resourceResolver` - Sling資源解析程式物件( `slingRequest.getResoucreResolver();`)。
   * `currentNode` — 要求的已解析JCR節點。
   * `log` — 預設記錄器()。
   * `sling` - Sling指令碼協助程式。
   * `properties` — 已定址資源( `resource.adaptTo(ValueMap.class);`)的屬性。
   * `pageProperties` — 已定址資源的頁面屬性。
   * `pageManager` — 存取AEM內容頁面的頁面管理員( `resourceResolver.adaptTo(PageManager.class);`)。
   * `component` — 目前AEM元件的元件物件。
   * `designer` — 用於擷取設計資訊的Designer物件( `resourceResolver.adaptTo(Designer.class);`)。
   * `currentDesign` — 已定址資源的設計。
   * `currentStyle` — 已定址資源的樣式。

### 存取內容 {#accessing-content}

存取AEM WCM中的內容有三種方法：

* 透過`global.jsp`中引入的屬性物件：

  屬性物件是ValueMap的執行個體（請參閱[Sling API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html)），並包含目前資源的所有屬性。

  範例： `String pageTitle = properties.get("jcr:title", "no title");`用於頁面元件的轉譯指令碼。

  範例： `String paragraphTitle = properties.get("jcr:title", "no title");`用於標準段落元件的轉譯指令碼。

* 透過`global.jsp`中引入的`currentPage`物件：

  `currentPage`物件是頁面的執行個體(請參閱[AEM API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html))。 Page類別提供一些存取內容的方法。

  範例： `String pageTitle = currentPage.getTitle();`

* 透過`global.jsp`中引入的`currentNode`物件：

  `currentNode`物件是節點的執行個體（請參閱[JCR API](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html)）。 `getProperty()`方法可存取節點的屬性。

  範例： `String pageTitle = currentNode.getProperty("jcr:title");`

## JSP標籤庫 {#jsp-tag-libraries}

CQ和Sling標籤庫可讓您存取特定函式，以便在範本和元件的JSP指令碼中使用。

如需詳細資訊，請參閱檔案[標籤庫](/help/sites-developing/taglib.md)。

## 使用使用者端HTML程式庫 {#using-client-side-html-libraries}

現代網站非常依賴由複雜的JavaScript和CSS程式碼驅動的使用者端處理。 組織和最佳化此程式碼的伺服可能是一個複雜的問題。

為協助處理此問題，AEM提供&#x200B;**使用者端程式庫資料夾**，可讓您將使用者端程式碼儲存在存放庫中、將其組織成類別並定義每個類別程式碼何時及如何提供給使用者端。 然後，使用者端程式庫系統會負責在最終網頁中產生正確的連結，以載入正確的程式碼。

如需詳細資訊，請參閱檔案[使用使用者端HTML庫](/help/sites-developing/clientlibs.md)。

## 對話方塊 {#dialog}

您的元件需要一個對話方塊供作者新增和設定內容。

如需詳細資訊，請參閱[AEM元件 — 基本知識](/help/sites-developing/components-basics.md#dialogs)。

## 設定編輯行為 {#configuring-the-edit-behavior}

您可以設定元件的編輯行為。 這包括元件可用的動作、就地編輯器的特性，以及與元件事件相關的接聽程式等屬性。 此設定對觸控式與傳統UI而言都是通用的，不過會有某些特定差異。

在元件節點（型別為`cq:Component`）下方新增型別為`cq:EditConfig`的`cq:editConfig`節點，以及新增特定屬性和子節點，以設定元件的[編輯行為](/help/sites-developing/components-basics.md#edit-behavior)。

## 使用和擴充ExtJS Widget {#using-and-extending-extjs-widgets}

如需詳細資訊，請參閱[使用和擴充ExtJS Widget](/help/sites-developing/widgets.md)。

## 對ExtJS Widget使用xtype {#using-xtypes-for-extjs-widgets}

如需詳細資訊，請參閱[使用xtypes](/help/sites-developing/xtypes.md)。

## 開發新元件 {#developing-new-components}

本節說明如何建立您自己的元件，並將其新增至段落系統。

快速入門方法是複製現有元件，然後進行您想要的變更。

有關如何開發元件的範例，詳情請參閱[擴充文字和影像元件 — 範例。](#extending-the-text-and-image-component-an-example)

### 開發新元件（調整現有元件） {#develop-a-new-component-adapt-existing-component}

若要根據現有元件為AEM開發新元件，您可以複製元件、為新元件建立JavaScript檔案，並將其儲存在AEM可存取的位置（另請參閱[自訂元件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)）：

1. 使用CRXDE Lite，在下方建立元件資料夾：

   / `apps/<myProject>/components/<myComponent>`

   像在程式庫中一樣重新建立節點結構，然後複製現有元件（例如文字元件）的定義。 例如，若要自訂文字元件複製：

   * 從 `/libs/foundation/components/text`
   * 至`/apps/myProject/components/text`

1. 修改`jcr:title`以反映其新名稱。
1. 開啟新的元件資料夾，並進行您需要的變更。 此外，請刪除資料夾中任何無關的資訊。

   您可以進行下列變更：

   * 在對話方塊中新增欄位

      * `cq:dialog` — 觸控式UI的對話方塊
      * `dialog` — 傳統UI的對話方塊

   * 取代`.jsp`檔案（以新元件命名）
   * 或完全重工整個元件（若您需要）

   例如，如果您取得標準文字元件的復本，您可以將額外的欄位新增至對話方塊，然後更新`.jsp`以處理在那裡輸入的內容。

   >[!NOTE]
   >
   >的元件：
   >
   >* 觸控式UI使用[Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)元件
   >* 傳統UI使用[ExtJS Widget](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

   >[!NOTE]
   >
   >為傳統UI定義的對話方塊會在觸控式UI中運作。
   >
   >針對觸控式UI定義的對話方塊無法在傳統UI中運作。
   >
   >根據您的執行個體和作者環境，您可能會想要為元件定義這兩種型別的對話方塊。

1. 下列節點之一應存在且已正確初始化，新元件才能顯示：

   * `cq:dialog` — 觸控式UI的對話方塊
   * `dialog` — 傳統UI的對話方塊
   * `cq:editConfig` — 元件在編輯環境中的行為（例如拖放）
   * `design_dialog` — 設計模式的對話方塊（僅限傳統UI）

1. 透過下列任一方式在您的段落系統中啟動新元件：

   * 使用CRXDE Lite將值`<path-to-component>` （例如`/apps/geometrixx/components/myComponent`）新增至節點`/etc/designs/geometrixx/jcr:content/contentpage/par`的屬性元件
   * 遵循[將新元件加入段落系統](#adding-a-new-component-to-the-paragraph-system-design-mode)中的指示

1. 在AEM WCM中，開啟網站中的頁面並插入您建立型別的段落，以確保元件正常運作。

>[!NOTE]
>
>若要檢視頁面載入的時間統計資料，您可以使用Ctrl-Shift-U — 在URL中設定`?debugClientLibs=true`。

### 將新元件加入段落系統（設計模式） {#adding-a-new-component-to-the-paragraph-system-design-mode}

開發元件後，您將其新增至段落系統，讓作者在編輯頁面時可選取並使用元件。

1. 存取您編寫環境中使用段落系統的頁面，例如`<contentPath>/Test.html`。
1. 透過以下任一方式切換到設計模式：

   * 將`?wcmmode=design`新增至URL結尾並重新存取，例如：

     `<contextPath>/ Test.html?wcmmode=design`

   * 按一下Sidekick中的「設計」

   您現在處於設計模式，可以編輯段落系統。

1. 按一下「編輯」。

   隨即顯示屬於段落系統的元件清單。 也會列出您的新元件。

   可以啟動（或停用）元件以決定在編輯頁面時提供給作者的元件。

1. 啟動元件，然後返回正常編輯模式以確認其可供使用。

### 擴充文字和影像元件 — 範例 {#extending-the-text-and-image-component-an-example}

本節提供如何使用可設定的影像放置功能來擴充廣泛使用的文字和影像標準元件的範例。

文字和影像元件的擴充功能可讓編輯器使用元件的所有現有功能，另外還有一個額外選項可指定影像的位置：

* 在文字的左側（目前行為與新的預設值）
* 而在右側

延伸此元件後，可透過元件的對話方塊配置影像位置。

本練習將說明下列技巧：

* 複製現有元件節點並修改其中繼資料
* 修改元件的對話方塊，包括從父對話方塊繼承Widget
* 修改元件的指令碼以實作新功能

>[!NOTE]
>
>此範例目標是傳統UI。

>[!NOTE]
>
>此範例是根據AEM不再隨附的Geometrixx範例內容，已由We.Retail取代。 如需如何下載和安裝Geometrixx，請參閱檔案[We.Retail參考實作](/help/sites-developing/we-retail.md#we-retail-geometrixx)。

#### 擴充現有的文字元件 {#extending-the-existing-textimage-component}

若要建立元件，可使用標準文字元件作為基礎並加以修改。 您可以將新元件儲存在GeometrixxAEM WCM範例應用程式中。

1. 將標準文字檔元件從`/libs/foundation/components/textimage`複製到Geometrixx元件資料夾`/apps/geometrixx/components`，使用文字檔作為目標節點名稱。 （瀏覽至元件、以滑鼠右鍵按一下並選取「複製」，然後瀏覽至目標目錄，以複製元件。）

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. 若要讓此範例維持簡單，請導覽至您複製的元件，並刪除新文位元組點的所有子節點，以下子節點除外：

   * 對話方塊定義： `textimage/dialog`
   * 元件指令碼： `textimage/textimage.jsp`
   * 編輯設定節點（允許拖放資產）： `textimage/cq:editConfig`

   >[!NOTE]
   >
   >對話方塊定義取決於UI：
   >
   >* 觸控式UI： `textimage/cq:dialog`
   >* 傳統UI： `textimage/dialog`

1. 編輯元件中繼資料：

   * 元件名稱

      * 將`jcr:description`設為`Text Image Component (Extended)`
      * 將`jcr:title`設為`Text Image (Extended)`

   * 群組，其中元件列在Sidekick中（維持原狀）

      * 保留`componentGroup`設定為`General`

   * 新元件的父元件（標準文字元件）

      * 將`sling:resourceSuperType`設為`foundation/components/textimage`

   在此步驟後，元件節點看起來像這樣：

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. 將影像的編輯設定節點（屬性： `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`）的`sling:resourceType`屬性變更為`geometrixx/components/textimage.`

   如此一來，當影像放到頁面上的元件時，擴充文字時間元件的`sling:resourceType`屬性會設為： `geometrixx/components/textimage.`

1. 修改元件的對話方塊以包含新選項。 新元件會繼承對話方塊中與原始元件相同的零件。 您僅需新增下列選項，即可擴充&#x200B;**進階**&#x200B;索引標籤，新增&#x200B;**影像位置**&#x200B;下拉式清單： **左**&#x200B;和&#x200B;**右**：

   * 保留`textimage/dialog`屬性不變。

   請注意`textimage/dialog/items`有四個子節點（tab1到tab4），代表文字文字對話方塊的四個索引標籤。

   * 在前兩個標籤（tab1和tab2）中：

      * 將xtype變更為cqinclude （繼承自標準元件）。
      * 分別使用值`/libs/foundation/components/textimage/dialog/items/tab1.infinity.json`和`/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`新增路徑屬性。
      * 移除所有其他屬性或子節點。

   * 針對索引標籤3：

      * 保留屬性和子節點而不變更
      * 新增欄位定義至`tab3/items`，節點位置為`cq:Widget`
      * 為新`tab3/items/position`節點設定下列屬性（型別為String）：

         * `name`: `./imagePosition`
         * `xtype`: `selection`
         * `fieldLabel`: `Image Position`
         * `type`: `select`

      * 新增型別`cq:WidgetCollection`的子節點`position/options`以代表兩個影像放置選項，並在其下建立兩個節點，即`nt:unstructured`型別的o1和o2。
      * 針對節點`position/options/o1`，將屬性： `text`設定為`Left`，`value`設定為`left.`
      * 針對節點`position/options/o2`，將屬性： `text`設定為`Right`，`value`設定為`right`。

   * 刪除Tab4。

   影像位置會作為代表`textimage`段落之節點的`imagePosition`屬性保留在內容中。 執行這些步驟後，元件對話方塊看起來會像這樣：

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. 使用新引數的額外處理來擴充元件指令碼`textimage.jsp`：

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   您即將用產生此標籤的自訂樣式的新程式碼取代強調的程式碼片段&#x200B;*%>&lt;div class=&quot;image&quot;>&lt;%*。

   ```xml
   // todo: add new CSS class for the 'right image' instead of using
   // the style attribute
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) {
             style = "style=\"float:right\"";
        }
        %><div <%= style %> class="image"><%
   ```

1. 將元件儲存至存放庫。 元件已準備好進行測試。

#### 檢查新元件 {#checking-the-new-component}

開發元件後，您可以將其新增至段落系統，讓作者在編輯頁面時可選取並使用元件。 這些步驟可讓您測試元件。

1. 以Geometrixx（例如英文/公司）開啟頁面。
1. 按一下Sidekick中的「設計」以切換至設計模式。
1. 按一下頁面中間段落系統上的「編輯」，編輯段落系統設計。 隨即顯示元件清單，這些元件可放置在段落系統中，清單中應包含您新開發的元件「文字影像（延伸）」 。 選取它並按一下確定，為段落系統啟動它。
1. 切換回編輯模式。
1. 將文字影像（延伸）段落新增至段落系統，以範例內容初始化文字和影像。 儲存變更。
1. 開啟文字和影像段落的對話方塊，並將「進階」標籤上的「影像位置」變更為「右側」，然後按一下「確定」以儲存變更。
1. 段落會以影像在右側呈現。
1. 元件現在已可供使用。

元件會將其內容儲存在公司頁面上的段落中。

### 停用影像元件的上傳功能 {#disable-upload-capability-of-the-image-component}

若要停用此功能，請使用標準影像元件作為基礎並加以修改。 您可以將新元件儲存在Geometrixx範例應用程式中。

1. 將標準影像元件從`/libs/foundation/components/image`複製到Geometrixx元件資料夾`/apps/geometrixx/components`，使用影像作為目標節點名稱。

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. 編輯元件中繼資料：

   * 將&#x200B;**jcr：title**&#x200B;設為`Image (Extended)`

1. 導覽至 `/apps/geometrixx/components/image/dialog/items/image`。
1. 新增屬性：

   * **名稱**：`allowUpload`
   * **類型**：`String`
   * **值**：`false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. 按一下&#x200B;**全部儲存**。 元件已準備好進行測試。
1. 以Geometrixx（例如英文/公司）開啟頁面。
1. 切換到設計模式並啟動影像（延伸）。
1. 切換回編輯模式，並將其新增至段落系統。 在下一張圖片中，您可以看到原始影像元件與您建立的影像元件之間的差異。

   原始影像元件：

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   您的新影像元件：

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. 元件現在已可供使用。
