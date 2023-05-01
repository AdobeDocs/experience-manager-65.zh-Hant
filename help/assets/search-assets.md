---
title: 在中搜尋數位資產和影像 [!DNL Adobe Experience Manager]
description: 了解如何在 [!DNL Adobe Experience Manager] ，以及如何使用顯示在搜尋中的資產。
contentOwner: AG
mini-toc-levels: 1
feature: Search, Metadata
role: User
exl-id: 588433b2-564a-430f-9d04-480465ece2ad
source-git-commit: 9406dc74887d29e93461e1015a8f52fa7ee196f6
workflow-type: tm+mt
source-wordcount: '5613'
ht-degree: 6%

---

# 在中搜尋數位資產 [!DNL Adobe Experience Manager] {#search-assets-in-aem}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/search-assets.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/search-assets.html?lang=zh-Hant) |

[!DNL Adobe Experience Manager Assets] 提供強大的資產探索方法，可協助您達到更高的內容速度。 您的團隊可運用現成可用的功能和自訂方法，提供順暢的智慧型搜尋體驗，縮短上市時間。 搜尋資產是數位資產管理系統使用的核心，無論是供創意人員進一步使用、供業務使用者和行銷人員強大管理資產，還是由DAM管理員管理。 簡單、進階和自訂搜尋，您可透過 [!DNL Assets] 使用者介面或其他應用程式和介面，有助於完成這些使用案例。

[!DNL Experience Manager Assets] 支援下列使用案例，本文說明這些使用案例的使用方式、概念、設定、限制和疑難排解。

| 搜尋資產 | 配置和管理搜索功能 | 使用搜索結果 |
|---|---|---|
| [基本搜尋](#searchbasics) | [搜索索引](#searchindex) | [排序結果](#sort) |
| [了解搜尋UI](#searchui) | [視覺或相似性搜尋](#configvisualsearch) | [檢查資產的屬性和中繼資料](#checkinfo) |
| [搜尋建議](#searchsuggestions) | [必填中繼資料](#mandatorymetadata) | [下載](#download) |
| [了解搜尋結果和行為](#searchbehavior) | [修改搜尋刻面](#searchfacets) | [大量中繼資料更新](#metadataupdates) |
| [搜尋排名和提升](#searchrank) | [文字擷取](#extracttextupload) | [智慧型集合](#collections) |
| [高級搜索：篩選和搜尋範圍](#scope) | [自訂述詞](#custompredicates) | [了解並疑難排解非預期的結果](#unexpected-results) |
| [從其他解決方案和應用程式中搜尋](#search-assets-other-surfaces):<ul><li>[Adobe Asset Link](#aal)</li><li>[Brand Portal](#brand-portal)</li><li>[Experience Manager案頭應用程式](#desktop-app)</li><li>[Adobe Stock影像](#adobe-stock)</li><li>[Dynamic Media資產](#dynamic-media)</li></ul> |  |  |
| [資產選擇器](#asset-picker) |  |  |
| [限制](#limitations) 和 [提示](#tips) |  |  |
| [插圖範例](#samples) |  |  |

使用頂端的Omnisearch欄位搜尋數位資產 [!DNL Experience Manager] 網頁介面。 前往 **[!UICONTROL 資產]** > **[!UICONTROL 檔案]** in [!DNL Experience Manager]，按一下 ![search_icon](assets/do-not-localize/search_icon.png) 在頂端列中輸入搜尋關鍵字，然後選取 `Return`. 或者，使用關鍵字快速鍵 `/` （正斜線）以開啟「Omnisearch」欄位。 `Location:Assets` 已預先選取，以將搜尋限制在DAM資產。 [!DNL Experience Manager] 在您開始輸入搜尋關鍵字時提供建議。

使用 **[!UICONTROL 篩選器]** 面板來搜尋資產、資料夾、標籤和中繼資料。 您可以根據各種選項（述詞）來篩選搜尋結果，例如檔案類型、檔案大小、上次修改日期、資產狀態、前瞻分析資料和Adobe Stock授權。 您可以自訂「篩選器」面板，並使用 [搜尋面向](/help/assets/search-facets.md). 此 [!UICONTROL 檔案類型] 篩選 [!UICONTROL 篩選器] 面板具有混合狀態複選框。 因此，除非您選取所有巢狀謂語（或格式），否則會部分勾選第一級核取方塊。

[!DNL Experience Manager] 搜尋功能支援搜尋集合，以及搜尋集合內的資產。 請參閱 [搜尋集合](/help/assets/manage-collections.md).

## 了解搜尋介面 {#searchui}

請熟悉搜尋介面和可用動作。

![了解Experience Manager Assets搜尋結果介面](assets/aem_search_results.png)

*圖：了解 [!DNL Experience Manager Assets] 搜尋結果介面。*

**答：** 將搜尋儲存為智慧型集合。 **B.** 篩選或述詞以縮小搜尋結果。 **C.** 顯示檔案、資料夾或兩者。 **D.** 按一下「篩選器」以開啟或關閉左側邊欄。**E.** 搜尋位置為 DAM。**F.** Omnisearch欄位及使用者提供的搜尋關鍵字。 **G.** 選擇載入的搜索結果。 **H.** 顯示的搜索結果總數。 **我。** 關閉搜索。 **J.** 在卡片檢視和清單檢視之間切換。

### 動態搜尋Facet {#dynamicfacets}

您可以使用動態更新的搜尋Facet中預期搜尋結果數量，從搜尋結果頁面更快地找到所需資產。 預期的資產數量會在套用搜尋篩選前更新。 查看篩選條件的預期計數，有助於您快速且有效地導覽搜尋結果。

![查看資產的約略數量，而不篩選搜尋Facet中的搜尋結果。](assets/asset_search_results_in_facets_filters.png)

*圖：查看資產的約略數量，而不篩選搜尋Facet中的搜尋結果。*

## 了解搜尋結果和行為 {#searchbehavior}

### 基本搜尋詞和結果 {#searchbasics}

您可以從OmniSearch欄位執行關鍵字搜尋。 關鍵字搜尋不區分大小寫，且是全文搜尋（涵蓋熱門中繼資料欄位）。 若使用了多個關鍵字， `AND` 是關鍵字之間的預設運算子。

結果會依關聯性排序，從最接近的相符項目開始。 對於多個關鍵字，更相關的結果是在其中繼資料中包含兩個詞語的資產。 在中繼資料中，顯示為智慧標籤的關鍵字的排名高於顯示在其他中繼資料欄位中的關鍵字。 [!DNL Experience Manager] 可賦予特定搜尋詞更高的權重。 此外， [提升排名](#searchrank) 特定搜尋詞的幾個目標資產。

為了快速找到相關資產，豐富的介面提供篩選、排序和選取機制。 您可以根據多個條件篩選結果，並查看針對各種篩選條件搜尋的資產數量。 或者，您也可以變更Omnisearch欄位中的查詢，以重新執行搜尋。 當您變更搜尋詞或篩選器時，其他篩選器會保留套用以保留搜尋的內容。

當結果為多個資產時， [!DNL Experience Manager] 在卡片檢視中顯示前100個，在清單檢視中顯示前200個。 當使用者捲動時，會載入更多資產。 這是為了改善效能。 觀看 [顯示的資產數](https://www.youtube.com/watch?v=LcrGPDLDf4o).

有時候，您可能會在搜尋結果中看到一些非預期的資產。 如需詳細資訊，請參閱 [意外結果](#unexpected-results).

[!DNL Experience Manager] 可以搜索許多檔案格式，而且可以自定義搜索篩選器以滿足您的業務要求。 請連絡您的管理員，了解哪些搜尋選項可供您的DAM存放庫使用，以及您的帳戶有哪些限制。

### 使用和不使用增強的智慧標籤產生的結果 {#withsmarttags}

依預設， [!DNL Experience Manager] search將搜索詞與AND子句組合。 例如，請考慮搜尋關鍵字「女性」跑步。 依預設，中繼資料中只有同時包含女性和執行中關鍵字的資產會顯示在搜尋結果中。 與關鍵字搭配使用特殊字元（句號、底線或破折號）時，會保留相同的行為。 下列搜尋查詢會傳回相同的結果：

* `woman running`
* `woman.running`
* `woman-running`

但查詢 `woman -running` 傳回資產不傳回 `running` 元資料中。
使用智慧標籤會新增 `OR` 子句，將任何搜索詞作為應用的智慧標籤查找。 標籤有 `woman` 或 `running` 使用智慧標籤也會出現在這類搜尋查詢中。 搜索結果是，

* 具有 `woman` 和 `running` 中繼資料中的關鍵字（預設行為）。

* 使用任一關鍵字（智慧標籤行為）標示的資產智慧。

### 在您輸入時搜尋建議 {#searchsuggestions}

當您開始輸入關鍵字時， [!DNL Experience Manager] 建議可能的搜尋關鍵字或片語。 建議是以現有資產的中繼資料為基礎。 [!DNL Experience Manager] 索引所有元資料欄位，以協助搜尋。 為了提供搜尋建議，系統會使用下列幾個中繼資料欄位的值。 若要提供搜尋建議，請考慮使用適當的關鍵字填入下列欄位：

* 資產標籤。 (將 `jcr:content/metadata/cq:tags`)
* 資產標題。 (將 `jcr:content/metadata/dc:title`)
* 資產說明。 (將 `jcr:content/metadata/dc:description`)
* JCR存放庫中的標題。 值可能會對應至資產標題。 (將 `jcr:content/jcr:title`)
* JCR存放庫中的說明。 值可能會對應至資產說明。 (將 `jcr:content/jcr:description`)

若要接收多個搜尋關鍵字的建議，請繼續輸入所有關鍵字，而不要為單一關鍵字選取任何建議。

![輸入多個關鍵字以檢視符合所有關鍵字的建議](assets/search_suggestionsmanykeywords.gif)

*圖：輸入多個關鍵字以檢視符合所有關鍵字的建議。*

### 搜尋排名和提升 {#searchrank}

會先顯示符合中繼資料欄位中所有搜尋詞的搜尋結果，接著顯示符合智慧標籤中任何搜尋詞的搜尋結果。 在上述範例中，搜尋結果的顯示約略順序為：

1. 匹配的 `woman running` 在各種中繼資料欄位中。
1. 匹配的 `woman running` 在智慧標籤中。
1. 匹配的 `woman` 或 `running` 在智慧標籤中。

您可以改善特定資產的關鍵字相關性，以協助根據關鍵字提升搜尋。 換句話說，當您根據這些關鍵字進行搜尋時，您促銷特定關鍵字的影像會顯示在搜尋結果頂端。

1. 從 [!DNL Assets] 使用者介面，開啟資產的屬性頁面。 按一下 **[!UICONTROL 進階]** 按一下 **[!UICONTROL 新增]** 在 **[!UICONTROL Elevate搜索關鍵字]**.
1. 在 **[!UICONTROL Search Promote]** 框中，指定要增加影像搜索的關鍵字，然後按一下 **[!UICONTROL 新增]**. 您可以以相同方式指定多個關鍵字。
1. 按一下&#x200B;**[!UICONTROL 「儲存並關閉」]**。您為此關鍵字促銷的資產會顯示在最上層搜尋結果中。

您可以提升目標關鍵字搜尋結果中某些資產的排名，借此善加運用。 請參閱下方的範例影片。 如需詳細資訊，請參閱 [搜尋 [!DNL Experience Manager]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html).

>[!VIDEO](https://video.tv.adobe.com/v/16766/?quality=6)

*影片：了解搜尋結果的排名方式，以及如何影響排名。*

## 進階搜尋 {#scope}

[!DNL Experience Manager] 提供套用至所搜尋資產的各種方法，例如篩選器，可協助您更快找到所需資產。 以下說明一些常用的方法。 部分 [插圖範例](#samples) 共用。

**搜索檔案或資料夾**:在搜索結果中，可以查看檔案、資料夾或兩者。 從 **[!UICONTROL 篩選器]** ，您可以選取適當的選項。 請參閱 [搜尋介面](#searchui).

**在資料夾中搜尋資產**:您可以將搜尋限制在特定資料夾。 在 **[!UICONTROL 篩選器]** 面板，添加資料夾的路徑。 一次只能選取一個資料夾。

![在「篩選器」面板中新增資料夾路徑，將搜尋結果限制為資料夾](assets/search_folder_select.gif)

*圖：在「篩選器」面板中新增資料夾路徑，將搜尋結果限制為資料夾。*

### 尋找類似的影像 {#visualsearch}

若要尋找視覺上類似使用者選取之影像的影像，請從影像的卡片檢視或工具列按一下「尋找類似 **** 」選項。[!DNL Experience Manager]會顯示來自DAM儲存庫的智慧型標籤影像，這些影像類似於使用者選取的影像。瞭解 [如何設定相似性搜尋](#configvisualsearch)。

![使用卡片檢視中的選項尋找類似的影像](assets/search_find_similar.png)

*圖：使用卡片檢視中的選項尋找類似的影像。*

### Adobe Stock影像 {#adobe-stock}

從 [!DNL Experience Manager] 用戶介面，用戶可搜索 [Adobe Stock資產](/help/assets/aem-assets-adobe-stock.md) 及授權所需資產。 新增 `Location: Adobe Stock` 的下界。 您也可以使用「篩選器」面板來尋找所有授權或未授權的資產，或使用Adobe Stock檔案號搜尋特定資產。

### Dynamic Media資產 {#dmassets}

您可以從&#x200B;**[!UICONTROL 「篩選器」]**&#x200B;面板中選取&#x200B;**[!UICONTROL 「動態媒體」]**>**[!UICONTROL 「集合」]**，以篩選動態媒體影像。這樣可以篩選並顯示影像集、旋轉木馬、混合媒體集和迴轉集等資產。

### 使用元資料欄位中的特定值進行GQL搜索 {#gql-search}

您可以根據中繼資料欄位的確切值（例如標題、說明和建立者）來搜尋數位資產。 GQL全文搜索功能只會擷取其中繼資料值與您的搜索查詢完全相符的資產。 屬性的名稱（建立者、標題等）和值區分大小寫。

| 中繼資料欄位 | Facet值和使用狀況 |
|---|---|
| 標題 | 標題：John |
| 建立者 | 建立者：約翰 |
| 位置 | 位置：不適用 |
| 說明 | 說明：&quot;範例影像&quot; |
| 建立者工具 | 建立工具：&quot;Adobe Photoshop&quot; |
| 版權擁有者 | 版權人：&quot;Adobe Systems&quot; |
| 參與者 | 貢獻者：John |
| 使用條款 | 使用條款：「保留CopyRights」 |
| 建立日期 | 已建立：YYYY-MM-DDTHH |
| 到期日 | 過期時間： YYYY-MM-DDTHH |
| 準時 | ontime:YYYY-MM-DDTHH |
| 關閉時間 | offtime:YYYY-MM-DDTHH |
| 時間範圍（過期日期時間、offtime） | facet欄位：下界……上界限 |
| 路徑 | /content/dam/&lt;folder name=&quot;&quot;> |
| PDF 標題 | pdftitle:&quot;Adobe檔案&quot; |
| 主旨 | 主題：「培訓」 |
| 標記 | 標籤：&quot;Location And Travel&quot; |
| 類型 | 類型：&quot;image\png&quot; |
| 影像寬度 | width:lowerbound..上界限 |
| 影像高度 | height:lowerbound..上界限 |
| 人員 | person:John |

屬性 `path`, `limit`, `size`，和 `orderby` 無法結合使用 `OR` 運算子與任何其他屬性。

<!-- TBD: Where are the limit, size, orderby properties defined?
-->

使用者產生屬性的關鍵字是其屬性編輯器中的欄位標籤（以小寫顯示），並移除空格。

以下是複雜查詢的搜尋格式的一些範例：

* 若要顯示具有多個Facet欄位的所有資產(例如：title=John Doe and creator tool = Adobe Photoshop): `title:"John Doe" creatortool:Adobe*`
* 若要在Facet值不是單一字詞而是句子時顯示所有資產(例如：title=Scott Reynolds): `title:"Scott Reynolds"`
* 若要顯示具有單一屬性多個值的資產(例如：title=Scott Reynolds或John Doe): `title:"Scott Reynolds" OR "John Doe"`
* 若要顯示屬性值以特定字串開頭的資產(例如：標題是斯科特·雷諾茲): `title:Scott*`
* 若要顯示屬性值結尾為特定字串的資產(例如：標題是斯科特·雷諾茲): `title:*Reynolds`
* 若要顯示包含特定字串之屬性值的資產(例如：標題=巴塞爾會議室): `title:*Meeting*`
* 若要顯示包含特定字串且具有特定屬性值的資產(例如：在標題=John Doe的資產中搜尋字串Adobe): `*Adobe* title:"John Doe"`

## 從其他 [!DNL Experience Manager] 產品或介面 {#search-assets-other-surfaces}

[!DNL Adobe Experience Manager] 將DAM存放庫連線至其他各種 [!DNL Experience Manager] 提供更快速存取數位資產及簡化創意工作流程的解決方案。 任何資產探索都會從瀏覽或搜尋開始。 在不同的曲面和解決方案中，搜索行為基本保持不變。 有些搜尋方法會隨著目標對象、使用案例和使用者介面而改變， [!DNL Experience Manager] 解決方案。 以下連結會記錄個別解決方案的特定方法。 本文記錄了普遍適用的提示和行為。

### 從「Adobe資產連結」面板搜尋數位資產 {#aal}

創意Adobe專業人員現在可以透過Asset Link存取儲存在 [!DNL Experience Manager Assets]，而不需離開支援的Adobe Creative Cloud應用程式。 創意人員可使用 [!DNL Adobe Creative Cloud] 應用程式： [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]，和 [!DNL Adobe InDesign]. 資產連結也可讓使用者以視覺上類似的結果搜尋。 視覺搜尋顯示結果由Adobe Sensei的機器學習演算法提供技術支援，並協助使用者尋找審美上類似的影像。 請參閱 [搜尋和瀏覽資產](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink) 使用Adobe資產連結。

### 在中搜尋數位資產 [!DNL Experience Manager] 案頭應用程式 {#desktop-app}

創意專業人員可使用案頭應用程式， [!DNL Experience Manager Assets] 可輕鬆搜尋，並可在其本機案頭(Win或Mac)上使用。 創意人員可以在Mac Finder或Windows Explorer中輕鬆顯示所需資產、在案頭應用程式中開啟並在本機變更 — 變更會儲存回 [!DNL Experience Manager] 在儲存庫中建立新版本。 應用程式支援使用一個或多個關鍵字進行基本搜索， `*` 和 `?` 萬用字元和 `AND` 運算元。 請參閱 [瀏覽、搜尋和預覽資產](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#browse-search-preview-assets) 在案頭應用程式中。

### 在中搜尋數位資產 [!DNL Brand Portal] {#brand-portal}

業務線使用者和行銷人員使用Brand Portal，以有效且安全的方式與其延伸的內部團隊、合作夥伴和經銷商共用已核准的數位資產。 請參閱 [在Brand Portal上搜尋資產](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/search-capabilities/brand-portal-searching.html).

### 搜尋 [!DNL Adobe Stock] 影像 {#adobe-stock1}

從 [!DNL Experience Manager] 使用者介面，使用者可以搜尋Adobe Stock資產，並授權所需的資產。 新增 `Location: Adobe Stock` 在Omnisearch欄位中。 您也可以使用 **[!UICONTROL 篩選器]** 面板，尋找所有授權或未授權的資產，或使用Adobe Stock檔案號搜尋特定資產。 請參閱 [管理 [!DNL Adobe Stock] 影像 [!DNL Experience Manager]](/help/assets/aem-assets-adobe-stock.md#usemanage).

### 搜尋 [!DNL Dynamic Media] 資產 {#dynamic-media}

您可以從&#x200B;**[!UICONTROL 「篩選器」]**&#x200B;面板中選取&#x200B;**[!UICONTROL 「動態媒體」]**>**[!UICONTROL 「集合」]**，以篩選動態媒體影像。這樣可以篩選並顯示影像集、旋轉木馬、混合媒體集和迴轉集等資產。在製作網頁時，作者可在內容尋找工具中搜尋集合。集合的篩選器可從快顯功能表中取得。

### 編寫網頁時，在「內容尋找器」中搜尋數位資產 {#content-finder}

作者可以使用「內容尋找器」來搜尋DAM存放庫中的相關資產，以及在其建立的網頁中使用資產。 作者也可以使用連線資產功能來搜尋遠端上可用的資產 [!DNL Experience Manager] 部署。 然後，作者就可以在本機的網頁中使用這些資產 [!DNL Experience Manager] 部署。 請參閱 [使用遠端資產](/help/assets/use-assets-across-connected-assets-instances.md#use-remote-assets).

### 搜尋集合 {#collections}

[!DNL Experience Manager] 搜尋功能支援搜尋集合，以及搜尋集合內的資產。 請參閱 [搜尋集合](/help/assets/manage-collections.md).

## 資產選擇器 {#asset-picker}

>[!NOTE]
>
>已呼叫資產選擇器 [資產選擇器](https://helpx.adobe.com/experience-manager/6-2/assets/using/asset-picker.html) 在舊版 [!DNL Adobe Experience Manager].

資產選擇器可讓您以特殊方式搜尋、篩選及瀏覽DAM資產。 資產選擇器位於 `https://[aem_server]:[port]/aem/assetpicker.html`. 您可以使用資產選取器來擷取所選資產的中繼資料。 您可以使用支援的請求參數來啟動它，例如資產類型（影像、視訊、文字）和選取模式（單選或多選）。 這些參數會設定特定搜尋例項的資產選取器內容，並在整個選取項目中保持不變。

資產選擇器使用HTML5 `Window.postMessage` 訊息，將所選資產的資料傳送給收件者。 它只能在瀏覽模式下運作，且只能搭配Omnisearch結果頁面運作。

在URL中傳遞下列要求參數，以在特定內容中啟動資產選取器：

| 名稱 | 值 | 範例 | 用途 |
|---|---|---|---|
| 資源尾碼(B) | 在URL中作為資源尾碼的資料夾路徑： [https://localhost:4502/aem/assetpicker.html/&lt;folder_path>](https://localhost:4502/aem/assetpicker.html) | 若要啟動已選取特定資料夾的資產選取器，例如在資料夾中 `/content/dam/we-retail/en/activities` 選取，則URL應為： `https://localhost:4502/aem/assetpicker.html/content/dam/we-retail/en/activities?assettype=images` | 如果在啟動資產選取器時需要選取特定資料夾，請以資源尾碼的形式傳遞。 |
| `mode` | 單一，多個 | <ul><li>`https://localhost:4502/aem/assetpicker.html?mode=single`</li><li>`https://localhost:4502/aem/assetpicker.html?mode=multiple`</li></ul> | 在多個模式中，您可以使用資產選擇器同時選取數個資產。 |
| `dialog` | true,false | [https://localhost:4502/aem/assetpicker.html?dialog=true](https://localhost:4502/aem/assetpicker.html?dialog=true) | 使用這些參數，以Granite對話方塊的形式開啟資產選取器。 只有當您透過Granite路徑欄位啟動資產選取器，並將其設定為pickerSrc URL時，才適用此選項。 |
| `root` | &lt;folder_path> | `https://localhost:4502/aem/assetpicker.html?assettype=images&root=/content/dam/we-retail/en/activities` | 使用此選項可指定資產選擇器的根資料夾。 在此情況下，資產選擇器可讓您僅選取根資料夾下的子資產（直接/間接）。 |
| `viewmode` | 搜尋 |  | 若要在搜尋模式中啟動資產選取器，請使用 `assettype` 和 `mimetype` 參數。 |
| `assettype` | 影像、檔案、多媒體、檔案。 | <ul><li>`https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=images`</li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=documents` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=multimedia` </li><li> `https://localhost:4502/aem/assetpicker.html?viewmode=search&assettype=archives` </li></ul> | 使用選項，根據提供的值來篩選資產類型。 |
| `mimetype` | MIME類型(`/jcr:content/metadata/dc:format`)（也支援萬用字元）。 | <ul><li>`https://localhost:4502/aem/assetpicker.html?mimetype=image/png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*png`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation`</li><li>`https://localhost:4502/aem/assetpicker.html?mimetype=*presentation&mimetype=*png`</li></ul> | 使用它以根據MIME類型篩選資產。 |

若要存取資產選擇器介面，請前往 `https://[aem_server]:[port]/aem/assetpicker`. 導覽至所需的資料夾，然後選取一或多個資產。 或者，您也可以從Omnisearch方塊搜尋所需的資產，視需要套用篩選，然後選取它。

![在資產選擇器中瀏覽並選取資產](assets/assetpicker.png)

*圖：瀏覽並在資產選擇器中選取資產。*

## 限制 {#limitations}

中的搜尋功能 [!DNL Experience Manager Assets] 有下列限制：

* 請勿在搜尋查詢中輸入前導空格，否則搜尋無法運作。
* [!DNL Experience Manager] 在您從搜尋結果中選取資產的屬性，然後取消搜尋後，可繼續顯示搜尋詞。 <!-- (CQ-4273540) -->
* 搜索資料夾或檔案和資料夾時，無法對任何參數排序搜索結果。
* 如果您選取 `Return` 不用在Omnisearch列里輸入， [!DNL Experience Manager] 返回僅檔案而不是資料夾的清單。 如果您不使用關鍵字而專門搜索資料夾， [!DNL Experience Manager] 不會傳回任何結果。
* 您可以對資料夾執行全文搜索。 指定搜尋詞以讓搜尋運作。

視覺搜尋或相似性搜尋有下列限制：

* 視覺化搜尋在大型存放庫中的效果最佳。 雖然獲得良好結果所需的影像數量並非最少，但與一些影像的匹配質量不如來自大型儲存庫的匹配質量好。
* 不能更改模型或列車 [!DNL Experience Manager] 尋找類似的影像。 例如，新增或移除智慧標籤至一些資產並不會變更模型。 會從視覺上類似的搜尋結果中排除資產。

在下列情況下，搜尋功能可能會有效能限制：

* 與顯示搜尋結果的清單檢視相比，卡片檢視的載入時間更快。

## 搜尋提示 {#tips}

* 在監控資產的審閱狀態時，請使用適當的選項查找已批准的資產或等待批准的資產。
* 使用前瞻分析述詞，根據從各種創意應用程式取得的使用統計資料來搜尋支援的資產。 使用量資料會依資產出現類別的使用量分數、曝光數、點按和媒體管道分組。
* 使用 **[!UICONTROL 全選]** 核取方塊以選取搜尋的資產。 [!DNL Experience Manager] 最初在卡片檢視中顯示100個資產，在清單檢視中顯示200個資產。 當您捲動搜尋結果時，會載入更多資產。 您可以選取比載入資產更多的資產。 選取的資產計數會顯示在搜尋結果頁面的右上角。 您可以對選取項目執行操作，例如下載選取的資產、大量更新選取資產的中繼資料屬性，或將選取的資產新增至集合。 當選取的資產數量超過顯示數量時，會對所有選取的資產套用動作，或對話方塊顯示套用的資產數量。 若要對未載入的資產套用動作，請確定已明確選取所有資產。
* 若要搜尋不包含必要中繼資料的資產，請參閱 [必填中繼資料](#mandatorymetadata).
* 搜尋會使用所有中繼資料欄位。 一般搜尋（例如搜尋12）通常會傳回許多結果。 為獲得更好的結果，請使用雙引號（非單引號），或確保數字與單詞連續，不帶特殊字元(例如 `shoe12`)。
* 全文搜尋支援運算子，例如 `-` 和 `^`. 若要將這些字母作為字串文本進行搜索，請以雙引號將搜索表達式括住。 例如，使用 `"Notebook - Beauty"` 而非 `Notebook - Beauty`.
* 如果搜索結果太多，請限制 [搜索範圍](#scope) 選取要的資產。 當您想到如何更妥善地尋找所需資產（例如特定檔案類型、特定位置、特定中繼資料等）時，效果最佳。

* **標籤**:標籤可協助您對可以更有效率地瀏覽和搜尋的資產進行分類。 標籤有助於將適當的分類法傳播給其他使用者和工作流程。 [!DNL Experience Manager] 提供使用Adobe Sensei的人工智慧服務來自動標籤資產的方法，讓您更能透過使用方式和訓練來標籤資產。 當您搜尋資產時，如果帳戶已啟用功能，系統會加入智慧標籤。 可與內建的搜尋功能搭配使用。 請參閱 [搜尋行為](#searchbehavior). 要優化搜索結果的顯示順序，您可以 [提升搜尋排名](#searchrank) 中指定的資產。

* **索引**:搜尋結果中只會傳回已索引的中繼資料和資產。 為獲得更好的覆蓋範圍和效能，請確保建立正確的索引並遵循最佳做法。 請參閱 [索引](#searchindex).

* 若要從搜尋結果中排除特定資產，請使用 `excludedPath` 屬性。

## 說明搜尋的一些範例 {#samples}

請在關鍵字周圍使用雙引號，以尋找包含使用者指定之確切順序之確切字句的資產。

![含引號和不含引號的搜尋行為](assets/search_with_quotes.gif)

*圖：有引號和沒有引號的搜尋行為。*

**使用星號通配符搜索**:要擴大搜索範圍，請在搜索詞之前或之後使用星號來匹配任意數量的字元。 例如，搜尋沒有星號的執行不會傳回包含字詞任何變異（包括在中繼資料中）的資產。 星號可代替任意數量的字元。 例如，

* `run` 傳回完全執行關鍵字的資產
* `run*` 傳回資產 `running`, `run`, `runaway`等。
* `*run` 傳回資產 `outrun`, `rerun`等。
* `*run*` 傳回所有可能的組合。

![以範例說明在資產搜尋中使用星號萬用字元的方式](assets/search_with_asterisk_run.gif)

*圖：以範例說明在資產搜尋中使用星號萬用字元的方式。*

**使用問號通配符搜索**:要擴大搜索範圍，請使用一個或多個「？」 字元數來比對字元數。 例如，在下圖中，

* `run???` 查詢與任何資產不符。

* `run????` 查詢與單詞匹配 `running` 後面四個字元 `run`.

* `??run` 查詢與單詞匹配 `rerun` 前面兩個字元 `run`.

![以範例說明在資產搜尋中使用問號萬用字元的方式](assets/search_with_questionmark_run.gif)

*圖：以範例說明在資產搜尋中使用問號萬用字元的方式。*

**排除關鍵字**:使用破折號來搜尋不含關鍵字的資產。 例如， `running -shoe` 查詢返回包含的資產 `running`，但不是 `shoe`. 同樣， `camp -night` 查詢返回包含的資產 `camp` 但 `night`. 查詢 `camp-night` 傳回同時包含兩者的資產 `camp` 和 `night`.

![使用破折號來搜尋不含已排除關鍵字的資產](assets/search_dash_exclude_keyword.gif)

*圖：使用破折號來搜尋不含已排除關鍵字的資產。*

## 與搜索功能相關的配置和管理任務 {#configadmin}

### 搜索索引配置 {#searchindex}

資產探索仰賴DAM內容的索引，包括中繼資料。 更快、更準確的資產發現依賴於優化的索引和適當的配置。 請參閱 [搜尋索引](/help/assets/performance-tuning-guidelines.md#search-indexes), [oak查詢和索引](/help/sites-deploying/queries-and-indexing.md)，和 [最佳實務](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

若要從搜尋結果中排除特定資產，請使用 `excludedPath` 屬性。

### 視覺或相似性搜尋 {#configvisualsearch}

視覺搜尋使用智慧標籤。 設定智慧標籤功能後，請遵循下列步驟。

1. 在 [!DNL Experience Manager] CRXDE，在 `/oak:index/lucene` 節點，添加以下屬性和值並保存更改。

   * `costPerEntry` 類型屬性 `Double` 值 `10`.
   * `costPerExecution` 類型屬性 `Double` 值 `2`.
   * `refresh` 類型屬性 `Boolean` 值 `true`.

   此配置允許從相應索引中進行搜索。

1. 要在CRXDE中建立Lucene索引，請訪問 `/oak:index/damAssetLucene/indexRules/dam:Asset/properties`，建立節點名為 `imageFeatures` 類型 `nt-unstructured`. 在 `imageFeatures` 節點，

   * 新增 `name` 類型屬性 `String` 值 `jcr:content/metadata/imageFeatures/haystack0`.
   * 新增 `nodeScopeIndex` 類型屬性 `Boolean` 值 `true`.
   * 新增 `propertyIndex` 類型屬性 `Boolean` 值 `true`.
   * 新增 `useInSimilarity` 類型屬性 `Boolean` 值 `true`.

   儲存變更。

1. 存取 `/oak:index/damAssetLucene/indexRules/dam:Asset/properties/predictedTags` 新增 `similarityTags` 類型屬性 `Boolean` 值 `true`.
1. 將智慧標籤套用至 [!DNL Experience Manager] 存放庫。 請參閱 [如何配置智慧標籤](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/configuring/tagging.html#configuring).
1. 在CRXDE中，在 `/oak-index/damAssetLucene` 節點，設定 `reindex` 屬性 `true`. 儲存變更。
1. （選用）如果您已自訂搜尋表單，請複製 `/libs/settings/dam/search/facets/assets/jcr%3Acontent/items/similaritysearch` 節點到 `/conf/global/settings/dam/search/facets/assets/jcr:content/items`. 儲存變更。

如需相關資訊，請參閱 [了解Experience Manager中的智慧標籤](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/metadata/image-smart-tags.html) 和 [如何管理智慧標籤](/help/assets/enhanced-smart-tags.md).

>[!CAUTION]
>
>如果Lucene索引已用完 [!DNL Adobe Experience Manager]，則根據智慧標籤的搜尋將無法如預期運作。

### 必填中繼資料 {#mandatorymetadata}

業務使用者、管理員或DAM圖書館員可將某些中繼資料定義為必要中繼資料，這是業務流程運作所必須的。 由於各種原因，某些資產可能會遺失此中繼資料，例如大量移轉的舊版資產或資產。 系統會根據索引中繼資料屬性，偵測並報告遺失或無效的中繼資料資產。 若要設定，請參閱 [必填中繼資料](/help/assets/metadata-schemas.md#define-mandatory-metadata).

### 修改搜尋刻面 {#searchfacets}

為了提高發現速度， [!DNL Experience Manager Assets] 提供可用來篩選搜尋結果的搜尋Facet。 依預設，「篩選器」面板包含一些標準Facet。 管理員可以自訂「篩選」面板，使用內建的述詞來修改預設Facet。 [!DNL Experience Manager] 提供內建述詞的完整集合，以及可自訂Facet的編輯器。 請參閱 [搜尋面向](/help/assets/search-facets.md).

### 上傳資產時擷取文字 {#extracttextupload}

您可以設定 [!DNL Experience Manager] 在使用者上傳資產時(例如PSD或PDF檔案)，從資產中擷取文字。 [!DNL Experience Manager] 索引擷取的文字，並協助使用者根據擷取的文字來搜尋這些資產。 請參閱 [上傳資產](/help/assets/manage-assets.md#uploading-assets).

如果文字擷取對您的部署而言耗用大量資源，請考慮 [禁用文本提取](https://helpx.adobe.com/experience-manager/kb/Disable-binary-text-extraction-to-optimize-Lucene-indexing-AEM.html).

### 篩選搜尋結果的自訂述詞 {#custompredicates}

述詞可用來建立Facet。 管理員可以使用預先設定的述詞來自訂「篩選器」面板中的搜尋刻面。 這些述詞可使用覆蓋來自訂。 請參閱 [建立自訂述詞](/help/assets/searchx.md).

您可以根據下列一或多個屬性來搜尋數位資產。 套用至其中某些屬性的篩選器預設可用，而其他某些篩選器則可自訂建立以套用至其他屬性。

| 搜尋欄位 | 搜索屬性值 |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------|
| MIME 類型 | 影像、檔案、多媒體、封存或其他。 |
| 上次修改時間 | 小時、日、周、月或年。 |
| 檔案大小 | 小、中或大。 |
| 發佈狀態 | 已發佈或未發佈。 |
| 批准狀態 | 已核准或已拒絕。 |
| 方向 | 水準、垂直或方形。 |
| 樣式 | 顏色或黑白。 |
| 視訊高度 | 指定為最小值和最大值。 值只會儲存在視訊轉譯的中繼資料中。 |
| 視訊寬度 | 指定為最小值和最大值。 值只會儲存在視訊轉譯的中繼資料中。 |
| 視訊格式 | DVI、Flash、MPEG4、MPEG、OGG Theora、QuickTime、Windows Media。 值會儲存在來源視訊和任何轉譯的中繼資料中。 |
| 視訊轉碼器 | x264。 值只會儲存在視訊轉譯的中繼資料中。 |
| 視訊位元速率 | 指定為最小值和最大值。 值只會儲存在視訊轉譯的中繼資料中。 |
| 音訊轉碼器 | Libvorbis,Lame MP3,AAC編碼。 值只會儲存在視訊轉譯的中繼資料中。 |
| 音訊位元速率 | 指定為最小值和最大值。 值只會儲存在視訊轉譯的中繼資料中。 |

## 使用資產搜尋結果 {#aftersearch}

您可以對搜尋的資產執行下列動作 [!DNL Experience Manager]:

* 檢視中繼資料屬性和其他資訊。
* 下載一或多個資產。
* 使用案頭動作在案頭應用程式中開啟這些資產。
* 建立智慧型集合。

### 對搜索結果排序 {#sort}

排序搜尋結果以更快找到所需資產。 您可以在清單檢視中排序搜尋結果，且僅限於選取 **[[!UICONTROL 檔案]](#searchui)** 從 **[!UICONTROL 篩選器]** 中。 [!DNL Assets]使用伺服器端排序功能，快速排序資料夾或搜尋查詢結果中的所有資產 (無論多少)。伺服器端排序比用戶端排序提供更快速且更精確的結果。

在清單檢視中，您可以排序搜尋結果，就像排序任何資料夾中的資產一樣。 排序適用於這些列 — 名稱、標題、狀態、Dimension、大小、評分、使用情況、建立的日期、修改的日期、發佈的日期、工作流和簽出。

如需排序功能的限制，請參閱 [限制](#limitations).

### 檢查資產的詳細資訊 {#checkinfo}

您可以從搜尋結果頁面檢查所搜尋資產的詳細資訊。

若要查看資產的所有中繼資料，請選取資產並按一下 **[!UICONTROL 屬性]** 的上界。

若要檢查資產或資產版本記錄的註解，請按一下資產以開啟大型預覽。在左側導軌中開啟時間軸，並選取「 **[!UICONTROL 注釋]** 」或「 **[!UICONTROL 版本」]**。您也可以依時間順序將時間軸活動 (例如注釋或版本) 排序。

![對搜索資產的時間軸條目進行排序](assets/sort_timeline_search_results.gif)

*圖：排序搜尋資產的時間軸項目。*

### 下載搜尋的資產 {#download}

您可以像從資料夾下載一般資產一樣，下載搜尋的資產及其轉譯。 從搜尋結果中選取一或多個資產，然後按一下 **[!UICONTROL 下載]** 的上界。

### 大量更新元資料屬性 {#metadataupdates}

您可以大量更新多個資產的通用中繼資料欄位。 從搜尋結果中選取一或多個資產。 按一下 **[!UICONTROL 屬性]** 從工具列，並視需要更新中繼資料。 按一下 **[!UICONTROL 儲存並關閉]** 時才能使用。 更新欄位中先前存在的中繼資料會遭到覆寫。

若為單一資料夾或集合中可用的資產，可更輕鬆 [大量更新中繼資料](/help/assets/metadata.md) 不使用搜尋功能。 對於可跨資料夾使用或符合通用條件的資產，透過搜尋大量更新中繼資料會更快。

### 智慧型集合 {#smart-collections}

集合是一組有序的資產，可包含來自不同位置的資產，因為集合僅包含這些資產的參考。 集合分為下列兩種類型：

* 資產、資料夾和其他集合的靜態參考清單。
* 根據搜尋條件填入集合中資產的動態清單（智慧型集合）。

您可以根據搜尋准則建立智慧型系列。從「濾鏡 **[!UICONTROL 器]** 」面板中，選 **[!UICONTROL 擇「檔案]** 」並單 **[!UICONTROL 擊「保存智慧集」]**。請參閱 [管理系列](/help/assets/manage-collections.md)。

## 意外的搜索結果和問題 {#unexpected-results}

| 錯誤、問題、症狀 | 可能的原因 | 可能的問題修正或了解 |
|---|---|---|
| 搜尋遺失中繼資料的資產時，結果不正確。 | 搜尋遺失必要中繼資料的資產時， [!DNL Experience Manager] 可能會顯示某些資產具有有效的中繼資料。 結果基於索引元資料屬性。 | 更新中繼資料後，必須重新索引以反映資產中繼資料的正確狀態。 請參閱 [必填中繼資料](metadata-schemas.md#define-mandatory-metadata). |
| 搜索結果太多。 | 廣泛搜尋參數。 | 請考慮限制 [搜索範圍](#scope). 使用智慧標籤可能會提供比預期更多的搜尋結果。 請參閱 [智慧標籤的搜尋行為](#withsmarttags). |
| 無關或部分相關的搜索結果。 | 搜尋行為會隨著智慧標籤而變更。 | 了解 [智慧標籤後的搜尋變更](#withsmarttags). |
| 沒有資產的自動完成建議。 | 新上傳的資產尚未建立索引。 當您開始在Omnisearch列中輸入搜尋關鍵字時，中繼資料不會立即作為建議使用。 | [!DNL Experience Manager] 會等到逾時期間到期（預設為一小時），才執行背景工作，為所有新上傳或更新的資產建立中繼資料索引，然後將中繼資料新增至建議清單。 |
| 沒有搜尋結果. | <ul><li>符合查詢的資產不存在。 </li><li> 搜尋查詢前新增空白字元。 </li><li> 不支援的元資料欄位包含您搜索的關鍵字。</li><li> 在資產的離職期間進行搜尋。 </li></ul> | <ul><li>使用不同的關鍵字進行搜尋。 或者，使用智慧標籤或相似性搜尋來改善搜尋結果。 </li><li>[已知限制](#limitations).</li><li>搜尋時不會考慮所有中繼資料欄位。 請參閱 [範圍](#scope).</li><li>稍後搜尋或修改所需資產的準時和非時間。</li></ul> |
| 搜尋篩選器或述詞無法使用。 | <ul><li>未配置搜索篩選器。</li><li>無法供您登入。</li><li>（不太可能）您使用的部署上沒有自訂搜尋選項。</li></ul> | <ul><li>請與管理員聯繫，以檢查搜索自定義項是否可用。</li><li>請聯絡管理員，以檢查您的帳戶是否具有使用自訂的權限/權限。</li><li>請聯絡管理員，並檢查 [!DNL Assets] 正在使用的部署。</li></ul> |
| 搜尋視覺上類似的影像時，缺少預期的影像。 | <ul><li>影像無法在 [!DNL Experience Manager].</li><li>影像未編列索引。 通常是在最近上傳時。</li><li>影像沒有智慧標籤。</li></ul> | <ul><li>將影像新增至 [!DNL Assets].</li><li>請與管理員聯繫，以重新索引儲存庫。 同時，請確定您使用的是適當的索引。</li><li>請連絡您的管理員以智慧標籤相關資產。</li></ul> |
| 搜尋視覺上類似的影像時，會顯示不相關的影像。 | 視覺搜尋行為。 | [!DNL Experience Manager] 盡可能顯示多個潛在相關資產。 相關度較低的影像（如果有）會新增至結果，但搜尋排名會較低。 當您向下捲動搜尋結果時，相符項目的品質和所搜尋資產的相關性會降低。 |
| 選取搜尋結果並對其執行作業時，系統不會對所有搜尋的資產執行作業。 | 此 [!UICONTROL 全選] 選項只會在卡片檢視中選取前100個搜尋結果，在清單檢視中選取前200個搜尋結果。 |  |

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 搜尋實作指南](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/search-tutorial-develop.html)
>* [進階設定可提升搜尋結果](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)
>* [配置智慧翻譯搜索](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/translation/smart-translation-search-technical-video-setup.html)

