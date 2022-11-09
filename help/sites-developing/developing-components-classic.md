---
title: 開發AEM元件（傳統UI）
seo-title: Developing AEM Components (Classic UI)
description: 傳統UI使用ExtJS來建立小工具集，以提供元件的外觀和風格。 HTL不是建議使用的AEM指令碼語言。
seo-description: The classic UI uses ExtJS to create widgets that provide the look-and-feel of the components. HTL is not the recommended scripting language for AEM.
uuid: ed53d7c6-5996-4892-81a4-4ac30df85f04
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: c68f724f-f9b3-4018-8d3a-1680c53d73f8
legacypath: /content/docs/en/aem/6-2/develop/components/components-classic
exl-id: 3f078139-73fd-4913-9d67-264fb2515f8a
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 1%

---

# 開發AEM元件（傳統UI）{#developing-aem-components-classic-ui}

傳統UI使用ExtJS來建立小工具集，以提供元件的外觀和風格。 由於這些Widget的性質，元件與傳統UI和 [觸控式UI](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>傳統UI和觸控式UI都有許多元件開發的常見方面，因此 **你必須讀 [AEM元件 — 基本概念](/help/sites-developing/components-basics.md) befor** 使用此頁面，說明傳統UI的詳細資訊。

>[!NOTE]
>
>雖然HTML範本語言(HTL)和JSP都可用來開發傳統UI的元件，但本頁說明如何使用JSP進行開發。 這完全是因為傳統UI中使用JSP的記錄。
>
>HTL現在是AEM建議的指令碼語言。 請參閱 [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) 和 [開發AEM元件](/help/sites-developing/developing-components.md) 來比較方法。

## 結構 {#structure}

頁面會說明元件的基本結構 [AEM元件 — 基本概念](/help/sites-developing/components-basics.md#structure)，可同時套用觸控式和傳統UI。 即使您不需要在新元件中使用觸控式UI的設定，在繼承現有元件時也應注意這些設定。

## JSP指令碼 {#jsp-scripts}

JSP指令碼或Servlet可用於呈現元件。 根據Sling的請求處理規則，預設指令碼的名稱為：

`<*componentname*>.jsp`

## global.jsp {#global-jsp}

JSP指令碼檔案 `global.jsp` 用於提供對特定對象（即訪問內容）的快速訪問，以訪問用於呈現元件的任何JSP指令碼檔案。

因此 `global.jsp` 應包含在每個元件呈現JSP指令碼中，其中提供了一個或多個對象 `global.jsp` 中所有規則的URL區段。

預設值的位置 `global.jsp` 為：

`/libs/foundation/global.jsp`

>[!NOTE]
>
>路徑 `/libs/wcm/global.jsp`,CQ 5.3版及舊版已使用，現已淘汰。

### global.jsp、已使用API和Taglibs的函式 {#function-of-global-jsp-used-apis-and-taglibs}

以下列出預設提供的最重要對象 `global.jsp`:

摘要:

* `<cq:defineObjects />`

   * `slingRequest`  — 包裝的請求物件( `SlingHttpServletRequest`)。
   * `slingResponse`  — 包裝的回應物件( `SlingHttpServletResponse`)。
   * `resource` - Sling資源物件( `slingRequest.getResource();`)。
   * `resourceResolver` - Sling資源解析器物件( `slingRequest.getResoucreResolver();`)。
   * `currentNode`  — 要求的已解析JCR節點。
   * `log`  — 預設記錄器()。
   * `sling` - Sling指令碼協助程式。
   * `properties`  — 已定址資源的屬性( `resource.adaptTo(ValueMap.class);`)。
   * `pageProperties`  — 已定址資源的頁面屬性。
   * `pageManager`  — 存取AEM內容頁面的頁面管理器( `resourceResolver.adaptTo(PageManager.class);`)。
   * `component`  — 目前AEM元件的元件物件。
   * `designer`  — 用於檢索設計資訊的設計器對象( `resourceResolver.adaptTo(Designer.class);`)。
   * `currentDesign`  — 設計已定址的資源。
   * `currentStyle`  — 已定址資源的樣式。

### 存取內容 {#accessing-content}

存取AEM WCM中的內容有三種方法：

* 透過 `global.jsp`:

   屬性對象是ValueMap的實例(請參閱 [Sling API](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ValueMap.html))，並包含目前資源的所有屬性。

   範例： `String pageTitle = properties.get("jcr:title", "no title");` 用於頁面元件的呈現指令碼中。

   範例： `String paragraphTitle = properties.get("jcr:title", "no title");` 用於標準段落元件的呈現指令碼。

* 透過 `currentPage` 導入的對象 `global.jsp`:

   此 `currentPage` 物件是頁面的例項(請參閱 [AEM API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.mhtml))。 頁面類別提供一些存取內容的方法。

   範例: `String pageTitle = currentPage.getTitle();`

* 透過 `currentNode` 導入的對象 `global.jsp`:

   此 `currentNode` 物件是節點的例項(請參閱 [JCR API](https://jackrabbit.apache.org/api/2.16/org/apache/jackrabbit/standalone/cli/core/CurrentNode.html))。 節點的屬性可由 `getProperty()` 方法。

   範例: `String pageTitle = currentNode.getProperty("jcr:title");`

## JSP標籤庫 {#jsp-tag-libraries}

CQ和Sling標籤程式庫可讓您存取特定函式，以用於範本和元件的JSP指令碼。

如需詳細資訊，請參閱本檔案 [標籤程式庫](/help/sites-developing/taglib.md).

## 使用用戶端HTML程式庫 {#using-client-side-html-libraries}

現代網站嚴重依賴由複雜JavaScript和CSS程式碼驅動的用戶端處理。 組織並最佳化此程式碼的服務可能是個複雜的問題。

為協助處理此問題，AEM提供 **用戶端程式庫資料夾**，可讓您將用戶端代碼儲存在存放庫中、將其組織為類別，並定義將每類代碼提供給用戶端的時間和方式。 然後，用戶端程式庫系統會負責在您的最終網頁中產生正確的連結，以載入正確的程式碼。

請參閱檔案 [使用用戶端HTML程式庫](/help/sites-developing/clientlibs.md) 以取得更多資訊。

## 對話方塊 {#dialog}

您的元件需要對話方塊，供作者新增及設定內容。

請參閱 [AEM元件 — 基本概念](/help/sites-developing/components-basics.md#dialogs) 以取得詳細資訊。

## 設定編輯行為 {#configuring-the-edit-behavior}

您可以設定元件的編輯行為。 這包括可用於元件的動作、就地編輯器的特性以及與元件上的事件相關的監聽器等屬性。 觸控式和傳統UI都會使用此設定，雖然有某些特定差異。

此 [配置元件的編輯行為](/help/sites-developing/components-basics.md#edit-behavior) 新增 `cq:editConfig` 類型節點 `cq:EditConfig` 元件節點下(類型 `cq:Component`)和新增特定屬性和子節點。

## 使用和擴充ExtJS Widget {#using-and-extending-extjs-widgets}

請參閱 [使用和擴充ExtJS Widget](/help/sites-developing/widgets.md) 以取得更多詳細資訊。

## 對ExtJS Widget使用xtype {#using-xtypes-for-extjs-widgets}

請參閱 [使用xtype](/help/sites-developing/xtypes.md) 以取得更多詳細資訊。

## 開發新元件 {#developing-new-components}

本節說明如何建立自己的元件並將其添加到段落系統中。

快速入門的方法是複製現有元件，然後進行您想要的變更。

如需如何開發元件的範例，請參閱 [擴充文字和影像元件 — 範例。](#extending-the-text-and-image-component-an-example)

### 開發新元件（調整現有元件） {#develop-a-new-component-adapt-existing-component}

若要根據現有元件為AEM開發新元件，您可以複製元件，為新元件建立javascript檔案，並將其儲存在AEM可存取的位置(另請參閱 [自訂元件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)):

1. 使用CRXDE Lite，在中建立新元件資料夾：

   / `apps/<myProject>/components/<myComponent>`

   重新建立lib中的節點結構，然後複製現有元件的定義，如Text元件。 例如，要自定義文本元件副本：

   * 從 `/libs/foundation/components/text`
   * 至 `/apps/myProject/components/text`

1. 修改 `jcr:title` 以反映其新名稱。
1. 開啟新元件資料夾，並進行您需要的變更。 同時，刪除資料夾中任何無關的資訊。

   您可以進行下列變更：

   * 在對話方塊中新增欄位

      * `cq:dialog`  — 觸控式UI的對話方塊
      * `dialog`  — 傳統UI的對話方塊
   * 更換 `.jsp` 檔案（在新元件後命名）
   * 或完全重新處理整個元件（如果您想要）

   例如，如果您取用標準文字元件的復本，可以新增其他欄位至對話方塊，然後更新 `.jsp` 來處理那裡的輸入。

   >[!NOTE]
   >
   >以下元件：
   >
   >* 觸控式UI使用 [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html) 元件
   >* 傳統UI使用 [ExtJS Widget](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html)


   >[!NOTE]
   >
   >針對傳統UI定義的對話方塊會在觸控式UI中運作。
   >
   >為觸控式UI定義的對話方塊不會在傳統UI中運作。
   >
   >視您的例項和製作環境而定，您可能會想要為元件定義這兩種對話方塊類型。

1. 下列節點之一應存在並正確初始化，新元件才會出現：

   * `cq:dialog`  — 觸控式UI的對話方塊
   * `dialog`  — 傳統UI的對話方塊
   * `cq:editConfig`  — 元件在編輯環境中的行為（例如拖放）
   * `design_dialog`  — 設計模式的對話框（僅限傳統UI）

1. 通過以下方法之一激活段落系統中的新元件：

   * 使用CRXDE Lite來新增值 `<path-to-component>` (例如， `/apps/geometrixx/components/myComponent`)到節點的屬性元件 `/etc/designs/geometrixx/jcr:content/contentpage/par`
   * 遵循 [向段落系統添加新元件](#adding-a-new-component-to-the-paragraph-system-design-mode)

1. 在AEM WCM中，開啟您網站的頁面，並插入您剛建立的類型的新段落，以確保元件正常運作。

>[!NOTE]
>
>若要查看頁面載入的計時統計資料，您可以使用Ctrl-Shift-U — 搭配 `?debugClientLibs=true` 在URL中設定。

### 向段落系統添加新元件（設計模式） {#adding-a-new-component-to-the-paragraph-system-design-mode}

開發元件後，可將其添加到段落系統中，以便作者在編輯頁面時選擇和使用元件。

1. 在使用段落系統的創作環境中訪問頁面 `<contentPath>/Test.html`.
1. 通過以下任一方式切換到「設計」模式：

   * 新增 `?wcmmode=design` 到URL結尾再次存取，例如：

      `<contextPath>/ Test.html?wcmmode=design`

   * 按一下Sidekick中的設計

   您現在處於設計模式，可以編輯段落系統。

1. 按一下「編輯」。

   將顯示屬於段落系統的元件清單。 也會列出您的新元件。

   元件可以啟動（或停用），以決定在編輯頁面時提供給作者的元件。

1. 啟動元件，然後回到一般編輯模式，確認元件可供使用。

### 擴充文字和影像元件 — 範例 {#extending-the-text-and-image-component-an-example}

本節提供有關如何使用可配置的影像放置特徵擴展廣泛使用的文本和影像標準元件的示例。

文字和影像元件的擴充功能可讓編輯器使用元件的所有現有功能，另加一個選項可指定影像的放置位置：

* 在文字的左側（目前行為和新預設值）
* 在右邊

擴展此元件後，可通過元件的對話框配置影像放置。

本練習將說明下列技術：

* 複製現有元件節點並修改其元資料
* 修改元件的對話方塊，包括父對話方塊中小工具的繼承
* 修改元件的指令碼以實作新功能

>[!NOTE]
>
>此範例針對傳統UI。

>[!NOTE]
>
>此範例以Geometrixx範例內容為基礎，此範例內容已由We.Retail取代，不再隨AEM提供。 請參閱檔案 [We.Retail參考實作](/help/sites-developing/we-retail.md#we-retail-geometrixx) 以了解如何下載和安裝Geometrixx。

#### 擴充現有文字時間元件 {#extending-the-existing-textimage-component}

若要建立新元件，我們會以標準文字時間元件為基礎，並加以修改。 我們將新元件儲存在GeometrixxAEM WCM範例應用程式中。

1. 複製標準文字時間元件 `/libs/foundation/components/textimage` 放入Geometrixx元件資料夾， `/apps/geometrixx/components`，使用textimage作為目標節點名稱。 （導覽至元件，按一下滑鼠右鍵並選取「複製」 ，然後瀏覽至目標目錄，即可複製元件。）

   ![chlimage_1-59](assets/chlimage_1-59a.png)

1. 若要讓此範例簡單明瞭，請導覽至您複製的元件，並刪除新文字時間節點的所有子節點，但下列子節點除外：

   * 對話框定義： `textimage/dialog`
   * 元件指令碼： `textimage/textimage.jsp`
   * 編輯設定節點（允許拖放資產）: `textimage/cq:editConfig`

   >[!NOTE]
   >
   >對話方塊定義取決於UI:
   >
   >* 觸控式UI: `textimage/cq:dialog`
   >* 傳統 UI: `textimage/dialog`


1. 編輯元件中繼資料：

   * 元件名稱

      * 設定 `jcr:description` to `Text Image Component (Extended)`
      * 設定 `jcr:title` to `Text Image (Extended)`
   * 群組，其中元件列在sidekick中（維持原狀）

      * 離開 `componentGroup` 設為 `General`
   * 新元件的父元件（標準文字時間元件）

      * 設定 `sling:resourceSuperType` to `foundation/components/textimage`

   在此步驟後，元件節點如下所示：

   ![chlimage_1-60](assets/chlimage_1-60a.png)

1. 變更 `sling:resourceType` 影像的編輯配置節點的屬性(屬性： `textimage/cq:editConfig/cq:dropTargets/image/parameters/sling:resourceType`) `geometrixx/components/textimage.`

   如此一來，當影像拖放到頁面上的元件時， `sling:resourceType` extended textimage元件的屬性設為： `geometrixx/components/textimage.`

1. 修改元件的對話方塊以包含新選項。 新元件繼承與原始元件相同的對話框部分。 我們所做的唯一補充是 **進階** 標籤，添加 **影像位置** 下拉清單，帶選項 **Left** 和 **右**:

   * 保留 `textimage/dialog`屬性未變更。

   注意方式 `textimage/dialog/items` 有四個子節點tab1到tab4，代表textimage對話框的四個頁簽。

   * 前兩個標籤（tab1和tab2）:

      * 將xtype變更為cqinclude（從標準元件繼承）。
      * 使用值新增路徑屬性 `/libs/foundation/components/textimage/dialog/items/tab1.infinity.json`和 `/libs/foundation/components/textimage/dialog/items/tab2.infinity.json`，分別為。
      * 移除所有其他屬性或子節點。
   * 對於tab3:

      * 保留屬性和子節點，不變更
      * 新增欄位定義至 `tab3/items`，類型的節點位置 `cq:Widget`
      * 為新 `tab3/items/position`節點：

         * `name`: `./imagePosition`
         * `xtype`: `selection`
         * `fieldLabel`: `Image Position`
         * `type`: `select`
      * 新增子節點 `position/options` 類型 `cq:WidgetCollection` 表示影像放置的兩個選擇，並在其下建立兩個節點，即o1和o2類型 `nt:unstructured`.
      * 針對節點 `position/options/o1` 設定屬性： `text` to `Left` 和 `value` to `left.`
      * 針對節點 `position/options/o2` 設定屬性： `text` to `Right` 和 `value` to `right`.
   * 刪除頁簽4。

   影像位置會以 `imagePosition`代表節點的屬性 `textimage` 段落。 執行這些步驟後，元件對話方塊如下所示：

   ![chlimage_1-61](assets/chlimage_1-61a.png)

1. 擴充元件指令碼， `textimage.jsp`，並額外處理新參數：

   ```xml
   Image image = new Image(resource, "image");
   
   if (image.hasContent() || WCMMode.fromRequest(request) == WCMMode.EDIT) {
        image.loadStyleData(currentStyle);
   ```

   我們將取代強調的程式碼片段 *%>&lt;div class=&quot;image&quot;>&lt;%* 新程式碼產生此標籤的自訂樣式。

   ```xml
   // todo: add new CSS class for the 'right image' instead of using
   // the style attribute
   String style="";
        if (properties.get("imagePosition", "left").equals("right")) {
             style = "style=\"float:right\"";
        }
        %><div <%= style %> class="image"><%
   ```

1. 將元件儲存至存放庫。 元件已準備好測試。

#### 檢查新元件 {#checking-the-new-component}

開發元件後，可將其添加到段落系統中，使作者能夠在編輯頁面時選擇和使用元件。 這些步驟可讓您測試元件。

1. 以英文/公司等Geometrixx開啟頁面。
1. 按一下Sidekick中的「設計」，切換至設計模式。
1. 通過按一下頁面中間的段落系統上的「編輯」(Edit)來編輯段落系統設計。 將顯示可放置在段落系統中的元件清單，其中應包括新開發的元件「文本影像（擴展）」。 通過選擇段落系統並按一下「確定」來激活它。
1. 切換回編輯模式。
1. 將「文本影像（擴展）」段落添加到段落系統，初始化帶有示例內容的文本和影像。 儲存變更。
1. 開啟文本和影像段落的對話框，並將「高級」頁簽上的「影像位置」更改為「右」 ，然後按一下「確定」以保存更改。
1. 該段落的右側顯示了影像。
1. 元件現已可供使用。

元件會將其內容儲存在「公司」頁面的段落中。

### 停用影像元件的上傳功能 {#disable-upload-capability-of-the-image-component}

若要停用此功能，我們會以標準影像元件為基礎並加以修改。 我們將新元件儲存在Geometrixx示例應用程式中。

1. 從複製標準影像元件 `/libs/foundation/components/image` 放入Geometrixx元件資料夾， `/apps/geometrixx/components`，使用影像作為目標節點名稱。

   ![chlimage_1-62](assets/chlimage_1-62a.png)

1. 編輯元件中繼資料：

   * 設定 **jcr:title** to `Image (Extended)`

1. 導覽至 `/apps/geometrixx/components/image/dialog/items/image`。
1. 新增屬性:

   * **名稱**: `allowUpload`
   * **類型**: `String`
   * **值**: `false`

   ![chlimage_1-63](assets/chlimage_1-63a.png)

1. 按一下 **全部儲存**. 元件已準備好測試。
1. 以英文/公司等Geometrixx開啟頁面。
1. 切換到設計模式並激活映像（擴展）。
1. 切換回編輯模式，並將其添加到段落系統。 在下一張圖片中，您可以看到原始影像元件與您剛剛建立的影像元件之間的差異。

   原始影像元件：

   ![chlimage_1-64](assets/chlimage_1-64a.png)

   您的新影像元件：

   ![chlimage_1-65](assets/chlimage_1-65a.png)

1. 元件現已可供使用。
