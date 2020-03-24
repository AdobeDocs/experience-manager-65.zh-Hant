---
title: 在AEM中搜尋數位資產和影像
description: 瞭解如何使用「篩選」面板在AEM中尋找所需資產，以及如何使用顯示在搜尋中的資產。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: d29c86108fc4d856eefd9530f699d400445f2843

---


# 在AEM中搜尋資產 {#search-assets-in-aem}

Adobe Experience Manager(AEM)Assets提供強穩的資產發現方法，協助您提高內容速度。 您的團隊使用現成可用的功能和自訂方法，提供順暢、智慧的搜尋體驗，縮短上市時間。 搜尋資產是數位資產管理系統的核心使用，不論是供創意人員進一步使用、由商業使用者和行銷人員強穩管理資產，或由DAM管理員管理。 您可透過AEM Assets使用者介面或其他應用程式和介面執行簡單、進階和自訂的搜尋，以協助您完成這些使用案例。

AEM支援下列使用案例，而本文則說明這些使用案例的使用、概念、設定、限制和疑難排解。

| 搜尋資產 | 配置和管理 | 使用搜尋結果 |
|---|---|---|
| [基本搜尋](#searchbasics) | [搜尋索引](#searchindex) | [排序結果](#sort) |
| [瞭解搜尋UI](#searchui) | [視覺化或相似性搜尋](#configvisualsearch) | [檢查資產的屬性和中繼資料](#checkinfo) |
| [搜尋建議](#searchsuggestions) | [必備中繼資料](#mandatorymetadata) | [下載](#download) |
| [瞭解搜尋結果和行為](#searchbehavior) | [修改搜尋刻面](#searchfacets) | [大量中繼資料更新](#metadataupdates) |
| [搜尋排名與提升](#searchrank) | [文字擷取](#extracttextupload) | [智慧型系列](#collections) |
| [進階搜尋：篩選和搜尋範圍](#scope) | [自訂謂語](#custompredicates) | [瞭解意外結果和疑難排解](#troubleshoot-unexpected-search-results-and-issues) |
| [從其他解決方案和應用程式搜尋](#beyondomnisearch):<ul><li>[Adobe Asset Link](#aal)</li><li>[品牌入口網站](#brandportal)</li><li>[AEM案頭應用程式](#desktopapp)</li><li>[Adobe Stock影像](#adobestock)</li><li>[動態媒體資產](#dynamicmedia)</li></ul> |  |  |
| [資產選擇器／選擇器](#assetselector) |  |  |
| [限制](#limitations) 和提 [示](#tips) |  |  |
| [圖示範例](#samples) |  |  |

使用AEM網頁介面頂端的Omnisearch欄位來搜尋資產。 前往「 **[!UICONTROL Assets]** > **** Files in AEM」（資產> AEM中的檔案），按一下頂端列中的搜尋圖示，輸入搜尋關鍵字，然後按回車鍵。 或者，使用關鍵字快速鍵/（正斜線）來開啟Omnisearch欄位。 位置：資產已預先選取，以限制搜尋DAM資產。 AEM會在您開始輸入搜尋關鍵字時提供建議。

使用「篩 **[!UICONTROL 選器]** 」面板，根據各種選項（謂語）篩選搜尋結果，以縮小搜尋範圍，例如檔案類型、檔案大小、上次修改日期、資產狀態、前瞻分析資料和Adobe Stock授權。 您的管理員可以自訂「篩選」面板，並使用搜尋Facet新增或移除搜尋謂語。 「篩 [!UICONTROL 選器] 」面板中的「檔案類型  」篩選器具有混合狀態核取方塊。 因此，除非選擇所有嵌套的謂語（或格式），否則第一級複選框將被部分選中。

AEM搜尋功能支援搜尋系列並搜尋系列中的資產。 請參閱 [搜尋系列](/help/assets/managing-collections-touch-ui.md)。

## 瞭解搜尋介面 {#searchui}

熟悉搜尋介面和可用動作。

![瞭解Assets搜尋結果介面的部分](assets/aem_search_results.png)

*圖：瞭解Assets搜尋結果介面的部分*

**A.** 將搜尋儲存為智慧型集合。**B.** 用來縮減搜尋結果的篩選器 (述詞)。**C.** 在搜索結果中顯示檔案和 (或) 資料夾。**D.** 按一下「篩選器」以開啟或關閉左側邊欄。**E.** 搜尋位置為 DAM。**F.** Omnisearch欄位，包含使用者提供的搜尋關鍵字。 **G.** 複選框以選擇所有搜索結果。 **H.** 顯示的搜尋結果總數。 **我。** 關閉搜 **索J。** 在卡片檢視和清單檢視之間切換。

### 動態搜尋Facet {#dynamicfacets}

您可以使用搜尋Facet中動態更新的預期搜尋結果數目，更快地從搜尋結果頁面發現所需資產。 預期的資產數目會在套用搜尋篩選之前更新。 查看篩選的預期計數有助於您快速且有效地瀏覽搜尋結果。 如需詳細資訊，請參閱「 [在AEM中搜尋資產」](search-assets.md)。

![在搜尋Facet中檢視資產的概約數目，而不篩選搜尋結果。](assets/asset_search_results_in_facets_filters.png)

*圖：在搜尋刻面中檢視資產的概約數目，而不篩選搜尋結果*

## 瞭解搜尋結果和行為 {#searchbehavior}

### 基本搜尋詞和結果 {#searchbasics}

您可以從OmniSearch欄位執行關鍵字搜尋。 關鍵字搜尋不區分大小寫，而且是全文搜尋（跨常用中繼資料欄位）。 如果搜尋了多個關鍵字，則關鍵字之間的預設運算子是預設搜 `AND` 尋，而是在資產 `OR` 智慧標籤時。

結果會依相關性排序，從最接近的相符項目開始。 對於多個關鍵字，更相關的結果是在其中繼資料中包含兩個詞語的資產。 在中繼資料中，顯示為智慧標籤的關鍵字比顯示在其他中繼資料欄位中的關鍵字的排名更高。 AEM可讓特定搜尋詞賦予較高的權重。 此外，您也可以提 [升特定搜尋詞](#searchrank) ，數個目標資產的排名。

為快速找到相關資產，豐富式介面提供篩選、排序和選擇機制。 您可以根據多個條件來篩選結果，並查看搜尋的資產數目，以找出各種篩選條件。 或者，您也可以在Omnisearch欄位中變更查詢，以重新執行搜尋。 當您變更搜尋詞或篩選器時，其他篩選器仍會套用，以保留您搜尋的上下文。

當結果是許多資產時，AEM會在卡片檢視中顯示前100個，在清單檢視中顯示200個。 當使用者捲動時，會載入更多資產。 這是為了改善效能。

>[!VIDEO](https://www.youtube.com/watch?v=LcrGPDLDf4o)

有時候，您會在搜尋結果中看到一些非預期的資產。 如需詳細資訊，請查看未 [預期的結果](#troubleshoot-unexpected-search-results-and-issues)。

AEM可搜尋許多檔案格式，而且可自訂搜尋篩選器以符合您的業務需求。 請連絡您的管理員，瞭解您的DAM儲存庫有哪些搜尋選項，以及您的帳戶有哪些限制。

### 有無增強的智慧型標籤結果 {#withsmarttags}

依預設，AEM搜尋會將搜尋詞與AND子句結合。 例如，請考慮搜尋正在執行的關鍵字女性。 預設情況下，只有中繼資料中同時包含女性和執行關鍵字的資產才會出現在搜尋結果中。 當特殊字元（句號、底線或破折號）與關鍵字搭配使用時，會保留相同的行為。 下列搜尋查詢會傳回相同的結果：

* `woman running`
* `woman.running`
* `woman-running`

不過，查詢會傳 `woman -running` 回資產，但未 `running` 加入中繼資料。
使用智慧型標籤會新增一 `OR` 個額外的子句，以尋找任何搜尋詞作為套用的智慧型標籤。 使用智慧型標籤標 `woman` 記或 `running` 使用智慧型標籤的資產也會出現在此類搜尋查詢中。 所以搜索結果是，

* 中繼資料中 `woman` 包含 `running` 關鍵字的資產（預設行為）。

* 使用任一關鍵字（智慧標籤行為）標籤智慧資產。

### 在您輸入時搜尋建議 {#searchsuggestions}

當您開始輸入關鍵字時，AEM會建議可能的搜尋關鍵字或片語。 建議是以現有資產的中繼資料為基礎。 AEM為所有中繼資料欄位建立索引，以協助搜尋。 為提供搜尋建議，系統會使用下列數個中繼資料欄位的值。 若要提供搜尋建議，請考慮將適當的關鍵字填入下列欄位：

* 資產標籤。 (映射至 `jcr:content/metadata/cq:tags`)
* 資產標題。 (映射至 `jcr:content/metadata/dc:title`)
* 資產說明。 (映射至 `jcr:content/metadata/dc:description`)
* JCR資料庫中的標題。 值可能會對應至資產標題。 (映射至 `jcr:content/jcr:title`)
* JCR儲存庫中的說明。 值可能會對應至資產說明。 (映射至 `jcr:content/jcr:description`)

若要收到多個搜尋關鍵字的建議，請繼續輸入所有關鍵字，而不要為單一關鍵字選取任何建議。

![輸入多個關鍵字以檢視符合所有關鍵字的建議](assets/search_suggestionsmanykeywords.gif)

*圖：輸入多個關鍵字以檢視符合所有關鍵字的建議*

### 搜尋排名與提升 {#searchrank}

會先顯示符合中繼資料欄位中所有搜尋詞的搜尋結果，接著顯示符合智慧標籤中任何搜尋詞的搜尋結果。 在上述範例中，搜尋結果的顯示近似順序為：

1. 在各個中 `woman running` 繼資料欄位中的相符項目。
1. 智慧型標 `woman running` 簽中的相符項目。
1. 智慧標 `woman` 簽中 `running` 的或的比對。

您可以改善特定資產的關鍵字關聯性，以協助根據關鍵字提高搜尋效率。 換言之，當您根據這些關鍵字進行搜尋時，您促銷特定關鍵字的影像會出現在搜尋結果的頂端。

1. 從「資產」使用者介面，開啟資產的屬性頁面。按一 **[!UICONTROL 下「進階]** 」，然後按一下/點選「 **[!UICONTROL Elevate for search keywords]** 」下 **[!UICONTROL 方的「新增」]**。
1. 在「搜 **[!UICONTROL 尋促銷]** 」方塊中，指定您要大幅提升影像搜尋的關鍵字，然後按一下／點選「新增」 ****。 您可以以相同的方式指定多個關鍵字。
1. 按一下／點選「 **[!UICONTROL 儲存並關閉]**」。 您為此關鍵字促銷的資產會出現在熱門搜尋結果中。

您可以透過提升目標關鍵字搜尋結果中某些資產的排名，來利用此功能。 請參閱以下範例影片。 如需詳細資訊，請參 [閱「AEM中的搜尋」](https://helpx.adobe.com/experience-manager/kt/assets/using/search-feature-video-use.html)。

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*瞭解搜尋結果的排名方式，以及排名的影響。*

## Advanced search {#scope}

AEM提供各種方法，例如套用至已搜尋資產的篩選器，以協助您更快找到所需的資產。 以下說明一些常用的方法。 以下 [共用一些](#samples) 圖示範例。

**搜索檔案或資料夾**:在搜索結果中，查看檔案、資料夾或兩者。 從「篩 **[!UICONTROL 選器]** 」面板中，您可以選取適當的選項。 請參閱 [搜尋介面](#searchui)。

**在資料夾中搜尋資產**:您可以將搜尋限制在特定資料夾。 在「篩 **[!UICONTROL 選器]** 」面板中，新增資料夾的路徑。 一次只能選擇一個資料夾。

![在「篩選器」面板中新增檔案夾路徑，將搜尋結果限制在檔案夾中](assets/search_folder_select.gif)

*圖：在「篩選器」面板中新增檔案夾路徑，將搜尋結果限制在檔案夾中*

### 尋找類似的影像 {#visualsearch}

若要尋找視覺上類似使用者選取之影像的影像，請從影像的卡片檢視或工具列按一下「尋找類似 **** 」選項。AEM會顯示來自DAM儲存庫的智慧型標籤影像，這些影像類似於使用者選取的影像。瞭解 [如何設定相似性搜尋](#configvisualsearch)。

![使用卡片檢視中的選項尋找類似的影像](assets/search_find_similar.png)

*圖：使用卡片檢視中的選項尋找類似的影像*

### Adobe Stock影像 {#adobestock}

在AEM使用者介面中，使用者可以搜尋 [Adobe Stock資產](/help/assets/aem-assets-adobe-stock.md) ，並授權所需的資產。 新增 `Location: Adobe Stock` 至Omnisearch列。 您也可以使用「篩選」面板來尋找所有授權或未授權的資產，或使用Adobe Stock檔案號碼搜尋特定資產。

### 動態媒體資產 {#dmassets}

您可以從&#x200B;**[!UICONTROL 「篩選器」]**&#x200B;面板中選取&#x200B;**[!UICONTROL 「動態媒體」>「集合」]**，以篩選動態媒體影像。這樣可以篩選並顯示影像集、旋轉木馬、混合媒體集和迴轉集等資產。

### 在中繼資料欄位中使用特定值進行搜尋 {#gqlsearch}

您可以根據特定中繼資料欄位的精確值來搜尋資產，例如標題、說明和作者。 GQL全文搜索功能僅提取那些元資料值與搜索查詢完全匹配的資產。 屬性的名稱（例如作者、標題等）和值會區分大小寫。

| 中繼資料欄位 | Facet值與使用 |
|---|---|
| 標題 | 標題：John |
| 產生器 | 建立者：John |
| 位置 | 位置： NA |
| 說明 | 說明：「範例影像」 |
| 製作工具 | 創作工具：「Adobe Photoshop CC 2015」 |
| 版權擁有者 | copyrightowner:「Adobe Systems」 |
| 參與者 | 投稿人：John |
| 使用條款 | 使用條款：「保留CopyRights」 |
| 建立日期 | 已建立：YYYY-MM-DDTHH |
| 到期日 | 過期：YYYY-MM-DDTHH |
| 準時 | ontime:YYYY-MM-DDTHH |
| 關閉時間 | offtime:YYYY-MM-DDTHH |
| 時間範圍（過期的dateontime,offtime） | facet欄位：下限……上界 |
| 路徑 | /content/dam/&lt;資料夾名稱> |
| PDF 標題 | pdftitle:「Adobe檔案」 |
| 主旨 | 主旨：「訓練」 |
| 標記 | 標籤：「位置與旅行」 |
| 類型 | 類型：&quot;image\png&quot; |
| 影像寬度 | width:lowberbound..上界 |
| 影像高度 | 高度：下限。上界 |
| 人員 | 人：John |

屬性路徑、限制、大小和orderby不能與任何其他屬性一起使用ORed。

使用者產生屬性的關鍵字是屬性編輯器中的小寫欄位標籤，並移除空格。

以下是複雜查詢的搜尋格式範例：

* 若要顯示具有多個刻面欄位的所有資產(例如：title=John Doe and creator tool = Adobe Photoshop): `tiltle:"John Doe" creatortool : Adobe*`
* 若要在Facet值不是單字而是句子時顯示所有資產(例如：title=Scott Reynolds): `title:"Scott Reynolds"`
* 若要顯示具有單一屬性多個值的資產(例如：title=Scott Reynolds或John Doe): `title:"Scott Reynolds" OR "John Doe"`
* 若要顯示屬性值以特定字串開頭的資產(例如：標題是Scott Reynolds): `title:Scott*`
* 若要顯示屬性值以特定字串結尾的資產(例如：標題是Scott Reynolds): `title:*Reynolds`
* 若要顯示包含特定字串的屬性值的資產(例如：標題=巴塞爾會議室): `title:*Meeting*`
* 若要顯示包含特定字串且具有特定屬性值的資產(例如：在具有title=John Doe的資產中搜尋字串Adobe): `*Adobe* title:"John Doe"`

## 從其他AEM產品或介面搜尋資產 {#beyondomnisearch}

Adobe Experience Manager(AEM)將DAM存放庫與各種其他AEM解決方案連結，讓您更快速地存取數位資產，並簡化創意工作流程。 任何資產搜尋都從瀏覽或搜尋開始。 在不同的曲面和解決方案上，搜索行為基本保持不變。 有些搜尋方法會隨著目標對象、使用案例和使用者介面而變更，而且AEM解決方案的使用者介面會有所不同。 以下連結說明個別解決方案的特定方法。 本文將說明普遍適用的提示和行為。

### 從Adobe Asset Link面板搜尋資產 {#aal}

使用Adobe Asset Link，創意專業人員現在可以存取儲存在AEM Assets中的內容，而不需離開支援的Adobe Creative Cloud應用程式。 創意人員可使用Creative Cloud應用程式中的應用程式內面板，順暢地瀏覽、搜尋、結帳和結帳資產：Photoshop、Illustrator和InDesign。 資產連結也可讓使用者搜尋視覺上類似的結果。 視覺化搜尋顯示結果由Adobe Sensei的機器學習演算法提供支援，並協助使用者尋找美學上類似的影像。 請參 [閱使用Adobe資產連結](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) ，搜尋及瀏覽資產。

### 在AEM案頭應用程式中搜尋資產 {#desktopapp}

創意專業人員使用案頭應用程式，讓AEM Assets可輕鬆搜尋，並可在其本機案頭（Win或Mac）上使用。 創意人員可以輕鬆地在Mac Finder或Windows檔案總管中顯示所需資產、在案頭應用程式中開啟並在本機變更——這些變更會以儲存庫中建立的新版本儲存回AEM。 應用程式支援使用一或多個關鍵字*和？的基本搜尋 萬用字元和AND運算子。 請參閱 [在案頭應用程式中瀏覽](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 、搜尋和預覽資產。

### Search assets in Brand Portal {#brandportal}

業務線使用者和行銷人員使用品牌入口網站，以有效且安全的方式與延伸的內部團隊、合作夥伴和經銷商共用經過核准的數位資產。 See [search assets on Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### 搜尋Adobe Stock影像 {#adobestock-1}

在AEM使用者介面中，使用者可以搜尋Adobe Stock資產並授權所需的資產。 在Omnisearch `Location: Adobe Stock` 欄位中新增。 您也可以使用「篩 **[!UICONTROL 選器]** 」面板來尋找所有授權或未授權的資產，或使用Adobe Stock檔案號碼搜尋特定資產。 請參 [閱「在AEM中管理Adobe Stock影像」](/help/assets/aem-assets-adobe-stock.md#usemanage)。

### 搜尋動態媒體資產 {#dynamicmedia}

您可以從&#x200B;**[!UICONTROL 「篩選器」]**&#x200B;面板中選取&#x200B;**[!UICONTROL 「動態媒體」]**>**[!UICONTROL 「集合」]**，以篩選動態媒體影像。這樣可以篩選並顯示影像集、旋轉木馬、混合媒體集和迴轉集等資產。在製作網頁時，作者可在內容尋找工具中搜尋集合。集合的篩選器可從快顯功能表中取得。

### 在製作網頁時，在Content Finder中搜尋資產 {#contentfinder}

作者可以使用Content Finder搜尋DAM儲存庫中的相關資產，並使用他們建立的網頁中的資產。 作者也可以使用「已連線的資產」功能來搜尋可在遠端AEM部署中使用的資產。 然後，作者可以在本機AEM部署的網頁中使用這些資產。 請參 [閱使用遠端資產](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets)。

### 搜尋系列 {#collections}

AEM搜尋功能支援搜尋系列並搜尋系列中的資產。 請參閱 [搜尋系列](/help/assets/managing-collections-touch-ui.md)。

## Asset selector {#assetselector}

資產選擇器可讓您以特殊方式搜尋、篩選及瀏覽DAM資產。 資產選擇器可在取得 `https://[aem-server]:[port]/aem/assetpicker.html`。 您可以使用資產選擇器擷取所選資產的中繼資料。 您可以使用支援的請求參數來啟動它，例如資產類型（影像、視訊、文字）和選擇模式（單選或多選）。 這些參數會為特定搜尋例項設定資產選取器的上下文，並在整個選取範圍內保持不變。

資產選擇器使用HTML5 Window.postMessage訊息，將所選資產的資料傳送給收件者。 資產選擇器是以Granite的基礎選擇器辭彙為基礎。 依預設，資產選擇器會在「瀏覽」模式中運作。

您可以在URL中傳遞下列請求參數，以在特定內容中啟動資產選擇器：

| 名稱 | 值 | 範例 | 目的 |
|---|---|---|---|
| 資源尾碼(B) | 資料夾路徑作為URL中的資源尾碼：[https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 若要啟動已選取特定檔案夾的資產選擇器，例如已選取 `/content/dam/we-retail/en/activities` 檔案夾，URL應為： [https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images](https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images) | 如果在啟動資產選擇器時需要選取特定資料夾，請將其作為資源尾碼傳遞。 |
| 模式 | 單一，多重 | <ul><li>[https://localhost:4502/aem/assetpicker.html?mode=single](https://localhost:4502/aem/assetpicker.html?mode=single)</li><li>[https://localhost:4502/aem/assetpicker.html?mode=multiple](https://localhost:4502/aem/assetpicker.html?mode=multiple)</li></ul> | 在多個模式中，您可以使用資產選擇器同時選取多個資產。 |
| mimetype | 資產的mimetype(s`/jcr:content/metadata/dc:format`)（也支援萬用字元） | <ul><li>[https://localhost:4502/aem/assetpicker.html?mimetype=image/png](https://localhost:4502/aem/assetpicker.html?mimetype=image/png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*png)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation)</li><li>[https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&amp;mimetype=*png](https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png)</li></ul> | 使用它以MIME類型篩選資產 |
| 對話方塊 | true, false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用這些參數將資產選擇器開啟為「花崗岩」對話方塊。 只有當您透過Granite路徑欄位啟動資產選擇器，並將其設定為pickerSrc URL時，此選項才適用。 |
| assettype(S) | 影像、檔案、多媒體、封存 | <ul><li>[https://localhost:4502/aem/assetpicker.html?assettype=images](https://localhost:4502/aem/assetpicker.html?assettype=images)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=documents](https://localhost:4502/aem/assetpicker.html?assettype=documents)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=multimedia](https://localhost:4502/aem/assetpicker.html?assettype=multimedia)</li><li>[https://localhost:4502/aem/assetpicker.html?assettype=archives](https://localhost:4502/aem/assetpicker.html?assettype=archives)</li></ul> | 使用這個選項可根據傳遞的值來篩選資產類型。 |
| 根 | &lt;folder_path> | [https://localhost:4502/aem/assetpicker.html?assettype=images&amp;root=/content/dam/we-retail/en/activities](https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities) | 使用此選項可指定資產選擇器的根資料夾。 在這種情況下，資產選擇器可讓您只選取根資料夾下的子資產（直接／間接）。 |

若要存取資產選擇器介面，請前往 `https://[aem_server]:[port]/aem/assetpicker`。 導覽至所要的檔案夾，並選取一或多個資產。 或者，從Omnisearch方塊中搜尋所要的資產、視需要套用篩選，然後選取它。

![在資產選擇器中瀏覽並選取資產](assets/assetpicker.png)

*圖：在資產選擇器中瀏覽並選取資產*

## 限制 {#limitations}

AEM Assets中的搜尋功能有下列限制：

* 請勿在搜索查詢中輸入前導空格，否則搜索無效。
* 在您從搜尋結果中選取資產的屬性，然後取消搜尋後，AEM可能會繼續顯示搜尋詞。 <!-- (CQ-4273540) -->
* 搜索資料夾或檔案和資料夾時，不能對任何參數對搜索結果進行排序。
* 如果您按下傳回鍵，而未在Omnisearch列中輸入任何內容，AEM會傳回僅包含檔案而非檔案夾的清單。 如果您在未使用關鍵字的情況下特別搜尋資料夾，AEM不會傳回任何結果。
* 使用「 [!UICONTROL 全選] 」核取方塊，您只能在卡片檢視中選取前100個搜尋的資產，在清單檢視中選取前200個搜尋的資產。 如果您在使用者介面中捲動並載入更多資產，您可以使用「全選」選 [!UICONTROL 項選取更多] 。

視覺搜尋或相似性搜尋有下列限制：

* 視覺化搜尋最適合大型儲存庫。 雖然沒有最佳結果所需的影像數量下限，但少數影像的比對品質可能不如大型儲存庫中的比對品質好。
* 您無法變更模型或訓練AEM以尋找類似的影像。 例如，新增或移除智慧標籤至少數資產並不會變更模型。 資產確實會從視覺上類似的搜尋結果中排除。

搜尋功能在下列情況下可能會有效能限制：

* 與清單檢視相比，卡片檢視的載入時間更快，可顯示搜尋結果。

## 搜尋秘訣 {#tips}

* 監控資產的審閱狀態時，請使用適當的選項來尋找已核准的資產或待核准的資產。
* 使用「前瞻分析」述詞，根據從各種Creative應用程式取得的資產使用統計資料來搜尋支援的資產。 使用資料會分組在資產顯示類別的「使用分數」、「印象」、「點按」和「媒體」渠道下。
* 使用「全 **[!UICONTROL 選]** 」核取方塊選取搜尋的資產。 它會在卡片檢視中選取前100個資產，在清單檢視中選取前200個資產。 您可以對選取範圍進行操作，例如下載選取的資產、大量更新選取資產的中繼資料屬性，或將選取的資產新增至系列。
* 若要搜尋不含必要中繼資料的資產，請參閱必 [要中繼資料](#mandatorymetadata)。
* 搜尋使用所有中繼資料欄位。 一般搜尋（例如搜尋12）通常會傳回許多結果。 為獲得更佳結果，請使用雙引號（非單引號），或確保數字與沒有特殊字元的單字相鄰(例如 *shoe12*)。
* 全文搜尋支援運算子，例如-、^等。 要將這些字母作為字串文本搜索，請用雙引號將搜索表達式括起來。 例如，使用「筆記型電腦——美容」而非「筆記型電腦——美容」。
* 如果搜尋結果太多，請將 [搜尋範圍限制](#scope) 為所要資產的零值。 當您對如何更好地尋找所需資產（例如特定檔案類型、特定位置、特定中繼資料等）有一些概念時，效果最佳。

* **標籤**:標籤可協助您將可以更有效率地瀏覽和搜尋的資產分類。 標籤有助於將適當的分類傳播給其他用戶和工作流。 AEM提供使用Adobe Sensei人工智慧服務自動標籤資產的方法，這些服務可讓您在使用和訓練資產時不斷取得進步。 當您搜尋資產時，如果您的帳戶已啟用功能，智慧標籤會加入。 它可與AEM的內建搜尋功能搭配使用。 請參閱 [搜尋行為](#searchbehavior)。 若要最佳化搜尋結果的顯示順序，您可以提 [高少數選取資產的搜尋](#searchrank) 排名。

* **索引**:搜尋結果中只會傳回已建立索引的中繼資料和資產。 為了獲得更好的覆蓋面和效能，請確保正確編製索引並遵循最佳做法。 請參 [閱索引](#searchindex)。

## 一些範例說明搜尋 {#samples}

在關鍵字周圍使用雙引號，以尋找包含使用者指定之確切順序之確切片語的資產。

![使用引號和不使用引號的搜尋行為](assets/search_with_quotes.gif)

*圖：使用引號和不使用引號的搜尋行為*

**使用星號通配符進行搜索**:若要擴大搜尋範圍，請在搜尋字詞前後使用星號，以比對任意數目的字元。 例如，搜尋沒有星號的執行並不會傳回包含字詞變異的資產（包括在中繼資料中）。 星號可取代任意數字元。 例如，

* `run` 返回正確執行關鍵字的資產
* `run*` 傳回資產，包括執行、執行、逃跑等。
* `*run` 傳回Outrun、重新執行等。
* `*run*` 傳回所有可能的組合。

![以範例說明在資產搜尋中使用星號萬用字元](assets/search_with_asterisk_run.gif)

*圖：以範例說明在資產搜尋中使用星號萬用字元*

**使用問號萬用字元搜尋**:若要擴大搜尋範圍，請使用一或多個「?」 字元來比對字元數目。 例如，在下圖中，

* `run???` 查詢不符合任何資產。

* `run????` query與後4個字 `running` 元的字詞相符 `run`。

* `??run` query與之前包含兩 `rerun` 個字元的單字相符 `run`。

![使用範例說明在資產搜尋中使用問號萬用字元](assets/search_with_questionmark_run.gif)

*圖：使用範例說明在資產搜尋中使用問號萬用字元*

**排除關鍵字**:使用破折號來搜尋不含關鍵字的資產。 例如，查 `running -shoe` 詢會傳回包含但 `running`不包含的資產 `shoe`。 同樣地， `camp -night` 查詢會傳回包含但不包含 `camp` 的資產 `night`。 請注意， `camp-night` 查詢會傳回同時包含和的 `camp` 資產 `night`。

![使用破折號來搜尋不含已排除關鍵字的資產](assets/search_dash_exclude_keyword.gif)

*圖：使用破折號來搜尋不含已排除關鍵字的資產*

## 與搜索功能相關的配置和管理任務 {#configadmin}

### 搜索索引配置 {#searchindex}

資產發現需要建立DAM內容的索引，包括中繼資料。 更快速且精確的資產發現有賴於最佳化索引和適當的組態。 請參 [閱搜尋索引](/help/assets/performance-tuning-guidelines.md#search-indexes)、 [oak查詢和索引](/help/sites-deploying/queries-and-indexing.md)，以及 [最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md)。

### 視覺化或相似性搜尋 {#configvisualsearch}

視覺搜尋使用智慧型標籤，並需要AEM 6.5.2.0或更新版本。 在設定智慧型標籤功能後，請遵循下列步驟。

1. 在AEM CRXDE的節點中， `/oak:index/lucene` 新增下列屬性和值並儲存變更。

   * `costPerEntry` 屬性( `Double` 含值) `10`。

   * `costPerExecution` 屬性( `Double` 含值) `2`。

   * `refresh` 屬性( `Boolean` 含值) `true`。
   此配置允許從適當的索引中進行搜索。

1. 要建立Lucene索引，請在CRXDE中， `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`建立名為type `imageFeatures` 的節點 `nt-unstructured`。 在節 `imageFeatures` 點中，

   * 新增 `name` 具有值 `String` 的類型屬性 `jcr:content/metadata/imageFeatures/haystack0`。

   * 新 `nodeScopeIndex` 增值 `Boolean` 為的類型屬性 `true`。

   * 新 `propertyIndex` 增值 `Boolean` 為的類型屬性 `true`。

   * 新增 `useInSimilarity` 具有值 `Boolean` 的類型屬性 `true`。
   儲存變更。

1. 存取 `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` 並新 `similarityTags` 增具 `Boolean` 有值的type屬性 `true`。
1. 將智慧型標籤套用至AEM儲存庫中的資產。 瞭解 [如何設定智慧標籤](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/smart-tags-technical-video-setup.html)。
1. 在CRXDE的節 `/oak-index/damAssetLucene` 點中，將屬 `reindex` 性設定為 `true`。 儲存變更。
1. （可選）如果您有自訂的搜尋表單，請將節 `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` 點複製到 `/conf/global/settings/dam/search/facets/assets/jcr:content/items`。 儲存所有變更。

如需相關資訊，請參 [閱瞭解AEM中的智慧標籤](https://helpx.adobe.com/experience-manager/kt/assets/using/smart-tags-feature-video-understand.html) , [以及如何管理智慧標籤](/help/assets/managing-smart-tags.md)。

### 必備中繼資料 {#mandatorymetadata}

企業使用者、管理員或DAM圖書管理員可將部分中繼資料定義為必要的中繼資料，這是商業程式運作的必備中繼資料。 由於各種原因，某些資產可能會遺失此中繼資料，例如大量移轉的舊資產或資產。 會根據索引的中繼資料屬性，偵測並報告遺失或無效中繼資料的資產。 若要設定，請參閱必 [要的中繼資料](/help/assets/metadata-schemas.md#define-mandatory-metadata)。

### 修改搜尋刻面 {#searchfacets}

為了改善搜尋速度，AEM Assets提供搜尋Facet，您可使用這些Facet來篩選搜尋結果。 依預設，「濾鏡」面板包含一些標準刻面。 管理員可以自訂「篩選」面板，使用內建的謂語修改預設刻面。 AEM提供一組完善的內建謂語和編輯器，以自訂Facet。 請參 [閱搜尋Facet](/help/assets/search-facets.md)。

### 上傳資產時擷取文字 {#extracttextupload}

您可以設定AEM，在使用者上傳資產（例如PSD或PDF檔案）時，從資產擷取文字。 AEM為擷取的文字建立索引，並協助使用者根據擷取的文字來搜尋這些資產。 請參閱 [上傳資產](/help/assets/managing-assets-touch-ui.md#uploading-assets)。

### 自訂謂語以篩選搜尋結果 {#custompredicates}

謂語用於建立刻面。 管理員可以使用預先設定的謂詞，自訂「篩選器」面板中的搜尋刻面。 這些謂語可以使用覆蓋自訂。 請參閱 [建立自訂謂語](/help/assets/searchx.md)。

您可以根據下列一或多個屬性來搜尋數位資產。 依預設，套用在某些屬性上的篩選器是可用的，而某些其他篩選器則可以自訂建立，以套用在其他屬性上。

| 搜尋欄位 | 搜尋屬性值 |
|---|---|
| MIME類型 | 影像、檔案、多媒體、封存或其他。 |
| 上次修改時間 | 小時、日、周、月或年。 |
| 檔案大小 | 小型、中型或大型。 |
| 發佈狀態 | 已發佈或未發佈。 |
| 批准狀態 | 已核准或已拒絕。 |
| 方向 | 水準、垂直或正方形。 |
| 樣式 | 顏色或黑白。 |
| 視訊高度 | 指定為最小值和最大值。 值僅儲存在視訊轉譯的中繼資料中。 |
| 視訊寬度 | 指定為最小值和最大值。 值僅儲存在視訊轉譯的中繼資料中。 |
| 視訊格式 | DVI、Flash、MPEG4、MPEG、OGG Theora、QuickTime、Windows Media。 值會儲存在來源視訊的中繼資料和任何轉譯中。 |
| 視訊轉碼器 | x264。 值僅儲存在視訊轉譯的中繼資料中。 |
| 視訊位元速率 | 指定為最小值和最大值。 值僅儲存在視訊轉譯的中繼資料中。 |
| 音訊轉碼器 | Libvorbis、Lame MP3、AAC編碼。 值僅儲存在視訊轉譯的中繼資料中。 |
| 音訊位元速率 | 指定為最小值和最大值。 值僅儲存在視訊轉譯的中繼資料中。 |

## 使用資產搜尋結果 {#aftersearch}

在您看到一些符合標準的搜尋資產後，您可以執行下列典型工作，或對這些搜尋結果執行下列動作：

* 檢視中繼資料屬性和其他資訊。
* 下載一或多個資產。
* 使用「案頭動作」在案頭應用程式中開啟這些資產。
* 建立智慧型系列。

### 對搜索結果排序 {#sort}

排序搜尋結果有助於您更快找到所需資產。排序搜索結果在清單視圖中工作，且僅當從「篩選器」面板 **[!UICONTROL [中選擇「檔案](#searchui)]**」時**[!UICONTROL &#x200B;工作&#x200B;]**。AEM Assets使用伺服器端排序功能，快速排序資料夾或搜尋查詢結果中的所有資產 (無論多少)。伺服器端排序比用戶端排序提供更快速且更精確的結果。

在清單檢視中，您可以像排序任何資料夾中的資產一樣，對搜尋結果進行排序。 排序功能適用於這些欄——名稱、標題、狀態、維度、大小、評分、使用狀況、（日期）建立、（日期）修改、（日期）發佈、工作流程和檢出。

有關排序功能的限制，請參見 [限制](#limitations)。

### 檢查資產的詳細資訊 {#checkinfo}

您可以從搜尋結果頁面檢查搜尋資產的詳細資訊。

若要查看資產的所有中繼資料，請選取資產，然後從工具 **[!UICONTROL 列按一]** 下屬性。

若要檢查資產或資產版本記錄的註解，請按一下資產以開啟大型預覽。在左側導軌中開啟時間軸，並選取「 **[!UICONTROL 注釋]** 」或「 **[!UICONTROL 版本」]**。您也可以依時間順序將時間軸活動 (例如注釋或版本) 排序。

![排序搜尋資產的時間軸項目](assets/sort_timeline_search_results.gif)

*圖：排序搜尋資產的時間軸項目*

### 下載搜尋的資產 {#download}

您可以從資料夾下載搜尋的資產及其轉譯，就像下載一般資產一樣。 從搜尋結果中選取一或多個資產，然後按一下工 **[!UICONTROL 具列中]** 的「下載」。

### 大量更新中繼資料屬性 {#metadataupdates}

您可大量更新多個資產的常用中繼資料欄位。 從搜尋結果中，選取一或多個資產。 按一 **[!UICONTROL 下工具列]** 中的「屬性」，並視需要更新中繼資料。 完成 **[!UICONTROL 時，按一下「儲存]** 」並關閉。 會覆寫更新欄位中先前存在的中繼資料。

對於單一資料夾或系列中可用的資產，不需要使用搜尋功能，就 [能更輕鬆地大量更新中繼](/help/assets/managing-multiple-assets.md) 資料。 對於跨資料夾可用或符合一般准則的資產，透過搜尋大量更新中繼資料會更快速。

### 智慧型系列 {#collections-1}

系列是一組有序的資產，可包含不同位置的資產，因為系列僅包含這些資產的參考。 系列有下列兩種類型：

* 資產、檔案夾和其他系列的靜態參考清單。
* 動態清單（智慧型系列），會根據搜尋准則填入系列中的資產。

您可以根據搜尋准則建立智慧型系列。從「濾鏡 **[!UICONTROL 器]** 」面板中，選 **[!UICONTROL 擇「檔案]** 」並單 **[!UICONTROL 擊「保存智慧集」]**。請參閱 [管理系列](/help/assets/managing-collections-touch-ui.md)。

## 疑難排解未預期的搜尋結果和問題 {#troubleshoot-unexpected-search-results-and-issues}

| 錯誤、問題、症狀 | 可能的原因 | 可能修正或瞭解問題 |
|---|---|---|
| 搜尋遺失中繼資料的資產時，結果不正確 | 當搜尋遺失必要中繼資料的資產時，AEM可能會顯示某些具有有效中繼資料的資產。 結果基於索引元資料屬性。 | 更新中繼資料後，需要重新建立索引，以反映資產中繼資料的正確狀態。 請參 [閱必要中繼資料](metadata-schemas.md#define-mandatory-metadata)。 |
| 搜尋結果過多 | 廣泛的搜尋參數。 | 考慮限制 [搜索範圍](#scope)。 使用智慧型標籤可能會提供比預期更多的搜尋結果。 請參 [閱使用智慧標籤的搜尋行為](#withsmarttags)。 |
| 不相關或部分相關的搜尋結果 | 使用智慧標籤來變更搜尋行為。 | 瞭解 [智慧標籤後搜尋的變更](#withsmarttags)。 |
| 無資產自動完成建議 | 新上傳的資產尚未建立索引。 當您開始在Omnisearch列中輸入搜尋關鍵字時，中繼資料無法立即當做建議使用。 | AEM Assets會等到逾時期間（預設為一小時）到期後，再執行背景工作，為所有新上傳或更新的資產建立中繼資料索引，然後將中繼資料新增至建議清單。 |
| 沒有搜尋結果 | <ul><li>沒有與查詢相符的資產。</li><li>您在搜尋查詢前新增了空白字元。</li><li>不支援的中繼資料欄位包含您搜尋的關鍵字。</li><li>會為資產設定啟動和關閉時間，而搜尋是在資產關閉時間進行。</li></ul> | <ul><li>使用不同關鍵字進行搜尋。 或者，使用（智慧型）標籤來改善搜尋結果。</li><li>這是已知 [的限制](#limitations)。</li><li>並非所有中繼資料欄位都會被視為搜尋。 請參 [閱範圍](#scope)。</li><li>稍後搜尋或修改所需資產的開啟和關閉時間。</li></ul> |
| Search filter/ predicate is not available | <ul><li>搜尋篩選器未設定。</li><li>登入時無法使用。</li><li>（不太可能）您使用的部署不會自訂搜尋選項。</li></ul> | <ul><li>請連絡管理員以檢查搜尋自訂是否可用。</li><li>請連絡管理員以檢查您的帳戶是否具有使用自訂的權限。</li><li>聯絡管理員，並檢查您所使用之AEM Assets部署的可用自訂項目。</li></ul> |
| 在搜尋視覺上類似的影像時，會遺失預期的影像 | <ul><li>AEM中無法使用影像。</li><li>未對影像編製索引。 通常是在最近上傳時。</li><li>影像未標籤智慧型。</li></ul> | <ul><li>將影像新增至AEM Assets。</li><li>請與管理員聯繫以重新為儲存庫編製索引。 此外，請確定您使用的是適當的索引。</li><li>請洽詢您的管理員，以智慧標籤相關資產。</li></ul> |
| 當搜尋視覺上類似的影像時，會顯示不相關的影像 | 視覺搜尋行為。 | AEM會顯示盡可能多的潛在相關資產。 較不相關的影像（如果有）會新增至結果，但搜尋排名較低。 當您向下捲動搜尋結果時，相符項目的品質和搜尋資產的相關性會降低。 |
| 在選取並操作搜尋結果時，所有搜尋的資產都不會在 | 「全 [!UICONTROL 選] 」選項僅在卡片檢視中選取前100個搜尋結果，在清單檢視中選取前200個搜尋結果。 |  |

>[!MORELIKETHIS]
>
>* [AEM搜尋實作指南](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [多值和標籤搜尋謂語的進階設定](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/metadata/search-feature-video-use.html)
>* [配置智慧翻譯搜索](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

