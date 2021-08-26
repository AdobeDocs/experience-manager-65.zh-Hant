---
title: '[!DNL Experience Manager] 6.5 service pack發行說明'
description: ' [!DNL Adobe Experience Manager] 6.5 service pack 10的發行說明'
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '3652'
ht-degree: 1%

---

# [!DNL Adobe Experience Manager] 6.5 service pack發行說明 {#aem-service-pack-release-notes}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.10.0 |
| 類型 | Service Pack發行 |
| 日期 | 2021 年 8 月 26 日 |
| 下載URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip) |

## [!DNL Adobe Experience Manager] 6.5.10.0中包含的內容 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.10.0包含自2019年4月發行6.5版以來所發行的新功能、客戶要求的重要增強功能，以及效能、穩定性和安全性等改善項目。Service Pack安裝在[!DNL Adobe Experience Manager] 6.5上。

[!DNL Adobe Experience Manager] 6.5.10.0中推出的主要功能和增強功能為：

* **增強 [!DNL Content Fragment] 模型和編輯器**:您現在可以使用巢狀模型，為結構化內容建立複雜和自訂 [!DNL Content Fragment] 的模型。內容結構被模組化為基本元素，這些基本元素被建模為子片段。 較高層級片段會參考這些子片段。 更多資料類型增強功能（例如進階驗證規則）進一步增強了[!DNL Content Fragments]內容模型的彈性。 [!DNL Experience Manager] [!DNL Content Fragment]編輯器支援公共編輯器會話中的嵌套片段結構，並增強了諸如結構樹視圖和通過片段層次的頁簽式瀏覽路徑標籤導航。

* **GraphQL API，適[!DNL Content Fragments]**&#x200B;用於：全新的GraphQL API是以JSON格式傳送結構化內容的標準方法。GraphQL查詢可讓用戶端僅要求相關內容項目來呈現體驗。 這種選擇消除了需要在用戶端剖析內容的內容過傳送（在HTTP REST API中可能）。 GraphQL結構衍生自[!DNL Content Fragment]模型，而API回應則採用JSON格式。 在作為[!DNL Cloud Service]的[!DNL Experience Manager]中， [GraphQL查詢會保留](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching)並處理快取友好GET請求。 在[!DNL Experience Manager] 6.5中尚不可能。

* **階層管理與未來預覽**:使用者現在有介面可存取其啟動的內容結 [!DNL Experience Manager] 構，包括在啟動中新增和移除頁面的功能。此功能增強了[!DNL Experience Manager]啟動以製作內容版本以供未來發佈的靈活性。 [時間扭曲功](/help/sites-authoring/working-with-page-versions.md#timewarp) 能可讓使用者將啟動次數預覽為未來內容狀態。

* **連線資產**: [!DNL Experience Manager] 將功 [!DNL Connected Assets] 能擴充至適用核 [!DNL Dynamic Media] 心元件中的影像使用。請參閱[使用連線資產](/help/assets/use-assets-across-connected-assets-instances.md)。

* **連結共用選項以下載資產或轉譯**:將資產和集合共用為連結時，使用者可以選擇是否允許下載原始資產或其轉譯，或是同時使用共用連結。此外，透過連結下載與他們共用之資產的使用者也可以選擇只下載原始資產、僅下載轉譯或兩者。

* **限制產生的子資產**:管理員可以限制為複合資產( [!DNL Experience Manager] 例如PDF、PowerPoint、InDesign和Keynote檔案)產生的子資產數量。請參閱[管理複合資產](/help/assets/managing-linked-subassets.md#generate-subassets)。

* **Camera Raw支援**:提供支 [!DNL Camera Raw] 援v10.4的 [!DNL Adobe Camera Raw] 新套件。請參閱 [使用 [!DNL Camera Raw]](/help/assets/camera-raw.md)處理影像。

* 內建存放庫(Apache Jackrabbit Oak)更新至1.22.8。

* **協助工具增強功能**:

   * [!DNL Dynamic Media] 為檢視器提供許多協助工具增強功能。請參閱[[!DNL Dynamic Media] 更新](#dynamic-media-65100)。

   * Platform提供幾項協助工具增強功能。 請參閱[平台更新](#platform-65100)。

* **使用者體驗增強功能**:

   * [!DNL Experience Manager] 直接在資料夾下顯示所有內容模型的清單，內容作者不必瀏覽檔案結構。此功能現在需要的點按次數更少，而且可改善製作效率。

   * [!DNL Sites]編輯器中的路徑欄位可讓作者從[!DNL Content Finder]拖曳資產。

如需[!DNL Experience Manager] 6.5.10.0中推出的所有功能和增強功能的清單，請參閱[ [!DNL Adobe Experience Manager] 6.5 Service Pack 10](new-features-latest-service-pack.md)中的新功能。

以下是[!DNL Experience Manager] 6.5.10.0版中提供的修正清單。

### [!DNL Sites] {#sites-65100}

* 在內容片段編輯器的&#x200B;**[!UICONTROL 屬性]**&#x200B;標籤下的&#x200B;**[!UICONTROL 預設值]**&#x200B;欄位中輸入時，焦點會移至另一個欄位(NPR-36992)。

* 在指定路徑下篩選[!DNL Content Fragment]模型時， [!DNL Experience Manager]搜尋會傳回所有具有`cq:Template`的節點，而非僅傳回[!DNL Content Fragment]模型(SITES-1453)的路徑和節點。
* [!DNL Content Fragments] 以資 `null` 料夾的狀態返回(SITES-1157)。
* [!DNL Experience Manager] 不會讓使用者停用並啟 [!DNL Content Fragment] 用模型(SITES-1088)。
* 當使用者移動、重新命名或刪除[!DNL Content Fragments]或媒體資產時，參照的[!DNL Content Fragments]不會自動更新(SITES-196)。
* 將元件從一個頁面貼到另一個頁面會產生JavaScript錯誤(NPR-37030)。
* 快速檢視頁面屬性時，會開啟不同頁面的頁面屬性(NPR-37025)。
* 內容片段可讓內容片段參考本身。 選擇器不支援操作(NPR-36993)。
* 升級至Service Pack 9後，某些使用者無法移動Experience Manager中的資料夾，且在記錄中看到錯誤(SITES-1481)。
* 在編輯模式下調整版面容器中元件的寬度時，發現忽隱忽現的情況(NPR-36961)。
* 促銷啟動時，促銷的啟動中的變更會雙重推出至其他啟動。 如果使用者促銷雙重推出的啟動，來源頁面上會反映雙重內容(NPR-36893)。
* [!DNL Experience Manager] 如果您使用「影像核心元件」將影像新增至頁面，或使用Foundation Image元件調整大小，則會為某些PNG影像新增灰色邊框，且具有透明度(NPR-36879)。
* [!DNL Experience Manager Sites] 管理員UI含有大量範本，導覽速度緩慢(NPR-36870)。
* 升級到Service Pack 9會阻止編寫一些元件。 此問題不允許[!DNL Sites]使用者建立新頁面(NPR-36857)。
* `ContextHubImpl`方法建立未關閉的`ResourceResolver`。 這會導致有關長時間執行`ResourceResolver`的警告訊息，且服務有時會傳回未預期的結果(NPR-36853)。
* 從Blueprint頁面屬性同步單一即時副本時，所有其他即時副本也會同步(NPR-36829、NPR-36522)。
* 只使用XLS MIME類型時，檔案上傳函式無法如預期運作(NPR-36785)。
* 帶有pascal大小寫和所有大寫字的新標籤沒有顯示在[!DNL Content Fragments]內的標籤欄位中(NPR-36742)。
* 新增[!DNL Content Fragment]時的「單一文字元素」選項會造成文字遺失，並建立與清單和巢狀清單相關的奇數格式(NPR-36565)。
* 當作者註解頁面上的任何元件、刪除元件並對刪除操作執行還原時，嘗試在網站主控台中檢視頁面的時間軸資料時，會發生錯誤(NPR-36528)。
* 頁面屬性大量編輯器的[!UICONTROL 儲存並關閉]選項會儲存變更但不會關閉編輯器(NPR-36527)。
* 當使用者嘗試將新的文字元件拖放至頁面時，元件會立即消失(NPR-36442)。
* 當使用者在包含空格的隨需標籤中輸入內容時（系統上不存在的標籤），按下Enter鍵，標籤就會顯示在欄位下。 不過，當[!DNL Content Fragment]儲存並重新開啟時，不會顯示隨選標籤(NPR-36441)。
* 透過Dispatcher存取執行個體時，無法刪除範本(NPR-36385)。
* 移動頁面時，需要手動重新整理瀏覽器，才能轉譯變更(NPR-36381)。
* 選取元件時，可以按Ctrl+X或Ctrl+C（在Mac上按Command+X或Command+C）剪下或複製元件。 按一下其他元件時，您可以貼上工具列，但無法貼上鍵盤（Ctrl+V或Command+V）(NPR-36379)。
* 當使用者嘗試使用剪刀圖示將元件移至其他位置時，會發生主控台錯誤。 此外，在貼上單一元件時會移動(NPR-36378)。
* [!DNL Experience Manager] 在WCM或通知上有沒有索引的查詢，會降低效能(NPR-36303)。
* 當作者還原已刪除繼承元件的繼承時，可用選項是同步所有頁面內容。 即使繼承僅還原於一個元件，內容作者仍須同步完成的頁面。 完全同步可能會導致不想要的內容同步(NPR-34456、CQ-4310183)。
* 製作例項上元件的即時使用不會顯示所有發生次數。 某些元件用於超過1000個頁面，但報表只會顯示約40個頁面(CQ-4323724)。
* 當網站結構中有許多子頁面時，在欄檢視中載入子頁面的Experience Manager6.5.8比Experience Manager6.4.8.2(CQ-4322766)需要更多時間。
* 在「轉出頁面」選項上取消勾選「全部」無法運作(NPR-37070)。
* 開啟現有的v3元件版本頁面時，不會開啟頁面屬性對話方塊，並記錄`NullPointerException`(SITES-1830)。

### [!DNL Assets] {#assets-65100}

在[!DNL Assets]中修正了下列問題：

* 移動資料夾後，屬性`jcr:title`的值不會在Publish執行個體上更新。 在作者內重新命名和重新發佈資料夾時，不會更新發佈執行個體中相同資料夾的`jcr:title`屬性值(NPR-36369)。

* 如果選取兩個或多個資產並編輯一個或多個中繼資料欄位，儲存作業會在Safari瀏覽器中失敗，錯誤代碼為500(NPR-36413)。

* 由於日期格式錯誤，大量中繼資料匯入失敗(NPR-36428)。

* 在[!UICONTROL 屬性]頁面中選取以更新中繼資料時，架構提供許多選項時介面回應速度緩慢(NPR-36430)。

* 使用[!UICONTROL Expiry Status]述詞的搜尋篩選器無法運作(NPR-36436)。

* [!UICONTROL 資料夾中繼資料]屬性中各欄位的快顯功能表未顯示最後選取的值(NPR-36937、CQ-4314429)。

* 搜尋檔案和資料夾時，如果使用者套用篩選器並選取[!UICONTROL 檔案和資料夾]，則只會顯示檔案，但不會顯示資料夾(CQ-4319543、NPR-36627)。

* 從資料夾內選取相同集合，以及從搜尋結果選取集合時，工具列選項不同(NPR-36620)。

* 搜尋結果頁面上沒有[!UICONTROL 快速發佈]選項可用(NPR-36904、CQ-4317748)。

* 使用者在未指定副檔名的情況下建立資產的即時副本時，下載後即時副本檔案無法使用(NPR-36903、CQ-4326305)。

* 將用戶添加為子資料夾的所有者時，用戶也獲得其父資料夾的所有者權限，因此也獲得父資料夾的其他子資料夾的所有者權限。 此外，嘗試移除時，不會將使用者移除為父資料夾的擁有者。 (NPR-36801、CQ-4323737)。

* [!DNL Experience Manager] 嘗試為複合資產（如PowerPoint演示文稿）建立子資產時，會產生記憶體不足的例外狀況(NPR-36668)。

* 當使用者移動已在已發佈網站頁面中使用的資產時，即使未選取發佈選項，網站頁面仍會再次發佈(NPR-36636、CQ-4323500)。

* 使用Apache Tika MIME類型偵測功能時，使用`AssetManager.createAsset`方法上傳的資產會將名為`apache-tika-*.tmp`檔案的暫存檔案保留在暫存目錄中。 此臨時檔案使用所有可用的可用磁碟空間(NPR-36545)。

* 所有受DRM保護的資產都會下載，且使用者不會選擇下載特定資產(CQ-4327422)。

* 無法將資產拖曳至使用者介面上的`pathfield`(NPR-36849)。

* 在欄檢視中選取資產時，資產詳細資訊面板會消失(NPR-36667)。

### [!DNL Dynamic Media] {#dynamic-media-65100}

**協助工具增強功能**

[!DNL Dynamic Media Viewers]中提供下列協助工具增強功能。

* 螢幕助讀程式現在會提供旁白，說明預留位置文字以搜尋和新增電子郵件地址作為共用資產作為連結對話方塊的必要欄位，並朗讀[!UICONTROL 請填寫此欄位]工具提示(CQ-4327761)。

* 螢幕助讀程式現在可在使用鍵盤存取使用者介面欄位時，正確敘述[!UICONTROL 影像預設集編輯器]中各欄位的名稱和用途(CQ-4325677)。

* 鍵盤焦點現在可從[!UICONTROL 多媒體類型]選項的資產選擇器(CQ-4324736)，適當移至[!UICONTROL 檢視器預設集]對話方塊的搜尋標籤。

* 使用鍵盤鍵在表單模式中導覽時，螢幕助讀程式會提供與[!UICONTROL 影像預設集]的[!UICONTROL 建立]標籤上的遞增和遞減選項對應的標籤旁白(CQ-4323900)。

* 螢幕助讀程式現在會朗讀關於以連結方式共用資產的[!UICONTROL 搜尋並新增電子郵件地址]選項(CQ-4323352)。

* 使用鍵盤鍵導覽資產時，工具列上會保留鍵盤焦點(CQ-4322037)。

* 現在，螢幕助讀程式會在[!UICONTROL 編輯影像處理設定檔]頁面(CQ-4290734)上選取[!UICONTROL 回應式影像裁切]中的[!UICONTROL 新增裁切]選項後，旁白新增的[!UICONTROL 編輯]欄位資訊。

* 在[!UICONTROL 編輯影像預設集]和[!UICONTROL 建立互動式視訊]頁面上，螢幕助讀程式現在會在使用標題鍵盤快速鍵(CQ-4290730)(CQ-4290701)導覽頁面時，適當地宣佈頁面標題。

* 現在，在導覽下列頁面時，螢幕助讀程式可以使用里程碑和區域快捷鍵，來識別螢幕的各個區域（例如右面板區域、左面板、動作工具列、檢視器工具列地標和可縮放的影像地標）。

   * [!UICONTROL 檢視器預設集編輯器] (CQ-4290729)

   * [!UICONTROL 影像集編輯器] (CQ-4290710)

   * [!UICONTROL 建立互動式視訊] (CQ-4290702)。

* 使用向下鍵導覽時，螢幕助讀程式現在會朗讀視訊影格中的共用選項名稱(CQ-4290728)。

* 螢幕助讀程式現在會提供[!UICONTROL 檢視器預設集編輯器](CQ-4290727)中[!UICONTROL Appearance]標籤中[!UICONTROL Sprite]和[!UICONTROL Background]標籤中各種選項的名稱旁白。

* [!UICONTROL 編輯視訊編碼]頁面的[!UICONTROL Basic]標籤中的必填欄位，如編輯[!UICONTROL 寬度]的欄位，現在具有星號符號(*)(CQ-4290725)。

* 螢幕助讀程式現在會在[!UICONTROL 影像設定檔]頁面上宣佈選項的標籤(CQ-4290723)。

* 當焦點位於CSS編輯器時，Windows使用者現在可以在[!UICONTROL 檢視器預設集編輯器]上導覽出展開的CSS編輯器(CQ-4290720)。

* 在「表單」模式中導覽時，在[!UICONTROL 「Basic]」標籤上的[!UICONTROL 「編輯影像預設集」]，螢幕助讀程式現在會提供各種編輯欄位和選項的標籤旁白(CQ-4290717)。

* 螢幕助讀程式現在會在資產詳細資訊頁面的左側導覽中，提供角色和狀態（選取或未選取）的旁白，以供使用者介面選項使用(CQ-4290709)。

* 螢幕助讀程式現在能正確提供狀態旁白（已選取或未選取），且影像的連結會在[!UICONTROL 建立互動式視訊]頁面的[!UICONTROL Content]標籤中切換(CQ-4290707)。

* 使用向下鍵導覽至[!UICONTROL 建立互動式視訊]頁面時，螢幕助讀程式現在會正確提供視訊時間軸比例中各區段的名稱、角色和狀態旁白(CQ-4290706)。

* 螢幕助讀程式現在會在導覽[!UICONTROL 建立互動式視訊]頁面(CQ-4290704)中的選項時，提供名稱、角色、預設狀態（選取或未選取）和屬性的旁白。

* 螢幕助讀程式現在會在導覽[!UICONTROL Publish]頁面(CQ-4290705)時，提供[!UICONTROL 所有資產]和[!UICONTROL 所有集合]選項的名稱、角色和預設狀態（已選取或未選取）的旁白。

* 當您在[!UICONTROL 建立互動式視訊]頁面上上傳不支援的視訊格式（MP4除外）時，Experience Manager會顯示並朗讀錯誤訊息(CQ-4290700)。

* [!UICONTROL 建立互動式視訊]頁面上時間軸比例中數字的對比度（秒）現在符合最低的必要明度比，讓對顏色有限的使用者可輕鬆閱讀(CQ-4290699)。

* 螢幕助讀程式現在會在導覽[!UICONTROL 建立互動式視訊]頁面時，朗讀[!UICONTROL 產品名稱]欄位的標籤(CQ-4290697)。

**已修正的問題**

[!DNL Dynamic Media]提供下列錯誤修正。

* 在啟用`dynamicmedia_scene7`執行模式且停用同步後，上傳至[!DNL Experience Manager]的視訊會顯示`Process failed`(CQ-4327791)。

### 平台 {#platform-65100}

此Service Pack提供下列增強功能：

* 當使用者在樹狀檢視中選取項目時，螢幕助讀程式會宣佈選取項目，而頂端會顯示工具列選項(NPR-36504)。
* 有些文字和控制項名稱較容易閱讀，因為明度比符合4.5:1的最低需求比率(NPR-36503)。
* 使用者使用日曆控制項時，螢幕助讀程式會提供描述性日期、月份和工作日資訊的旁白。 使用者使用日曆快捷鍵時，螢幕助讀程式會提供日期、月份和年份變更的旁白(NPR-36498)。
* 提供支援，以使用ECMAScript 6功能執行自訂JavaScript `Clientlibs`，而不遵循嚴格模式。 具體來說， `emitUseStrict`標幟已新增至`GCCScriptProcessor`(NPR-36411)。

下列錯誤修正是此Service Pack的一部分：

* 自訂健全狀態檢查的執行頻率比排程的更高(NPR-36985)。
* `Resourceresolver map`方法針對別名頁面傳回錯誤的結果(NPR-36767)。
* [!DNL Experience Manager] 啟動因載入工作流程而延遲(NPR-36615)。

### Integrations {#integrations-65100}

* 當主要MongoDB節點切換至其他節點時，Experience Manager會停止回應(NPR-36566)。
* [!DNL Sling content distribution] 執行收整合員刪除操作時失敗(NPR-36521、CQ-4323578)。

### 使用者介面 {#user-interface-65100}

* **[!UICONTROL References]**&#x200B;側面板不會顯示資產和網站參考(GRANITE-35078、GRANITE-34892)。

### 翻譯專案 {#translation-65100}

* 刪除多翻譯專案語言副本中的額外子頁面(NPR-36622)。

### 工作流程 {#workflow-65100}

* 如果伺服器收到不在辦公室的訊息，則會回報記憶體警報並停止回應(NPR-36768)。

### [!DNL Communities] {#communities-65100}

* 匿名訪客使用者的社群網站頁面在`LoggedIn`狀態中開啟(NPR-36908)。

* 當&#x200B;**[!UICONTROL Community]** > **[!UICONTROL Ideas]** > **[!UICONTROL Comments]**&#x200B;頁面中有多個頁面時，頁面導覽無法運作(NPR-36541)。

<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65100}

*
-->

### [!DNL Forms] {#forms-65100}

>[!NOTE]
>
>* [!DNL Experience Manager Forms] 會在排程的 [!DNL Experience Manager] Service Pack 發行日期一週後發行附加元件的套件。


### 商務 {#commerce-65100}

* 顯示的&#x200B;**[!UICONTROL Published By]**&#x200B;欄位中的值在欄檢視中不正確(NPR-36902)。
* 推出目錄時，新產品未正確標示為修改的產品(NPR-36666)。
* 當您重新建立已刪除的產品時，不會重新建立產品頁面(NPR-36665)。
* 已修改的頁面已更新，但目錄轉出時沒有更新對應的連結產品(CQ-4321409、NPR-36422)。
* **[!UICONTROL 稍後發佈]**&#x200B;和&#x200B;**[!UICONTROL 稍後取消發佈]**&#x200B;工作流程無法運作(CQ-4327679)。

如需安全性更新的資訊，請參閱[[!DNL Experience Manager] 安全性佈告欄頁面](https://helpx.adobe.com/security/products/experience-manager.html)。

## 安裝6.5.10.0 {#install}

**設定需求和詳細資訊**

* Experience Manager6.5.10.0需要Experience Manager6.5。有關詳細說明，請參閱[升級文檔](/help/sites-deploying/upgrade.md)。
* Service Pack下載可在Adobe[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)上取得。
* 在具有MongoDB和多個執行個體的部署上，使用套件管理器在其中一個製作執行個體上安裝Experience Manager6.5.10.0。

>[!NOTE]
>
>Adobe不建議移除或解除安裝[!DNL Adobe Experience Manager] 6.5.10.0套件。

### 安裝Service Pack {#install-service-pack}

要在[!DNL Adobe Experience Manager] 6.5實例上安裝Service Pack，請執行以下步驟：

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請先重新啟動執行個體再進行安裝。 Adobe建議，如果執行個體的目前正常運行時間很長，則重新啟動。

1. 安裝之前，請拍攝快照或對[!DNL Experience Manager]實例進行新的備份。

1. 從[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip)下載Service Pack。

1. 開啟套件管理器，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。如需詳細資訊，請參閱[套件管理器](/help/sites-administering/package-manager.md)。

1. 選擇包，然後按一下&#x200B;**[!UICONTROL Install]**。

1. 若要更新S3連接器，請在安裝Service Pack後停止執行個體，以安裝資料夾中提供的新二進位檔案取代現有連接器，然後重新啟動執行個體。 請參閱[Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)。

>[!NOTE]
>
>安裝Service Pack時，有時會退出Package Manager UI上的對話方塊。 Adobe建議您先等待錯誤記錄穩定，再存取部署。 請等待與卸載更新程式捆綁相關的特定日誌，然後確保安裝成功。 此問題通常會在[!DNL Safari]瀏覽器中發生，但可能在任何瀏覽器上間歇性發生。

**自動安裝**

有兩種方式可自動在工作執行個體上安裝[!DNL Experience Manager] 6.5.10.0:

A.當伺服器可聯機時，將包放入`../crx-quickstart/install`資料夾。 程式包會自動安裝。

B.使用套件管理器](/help/sites-administering/package-manager.md#package-share)中的[HTTP API。 使用`cmd=install&recursive=true`以安裝嵌套的包。

>[!NOTE]
>
>Adobe Experience Manager 6.5.10.0不支援安裝Bootstrap。

**驗證安裝**

1. 產品資訊頁面(`/system/console/productinfo`)在[!UICONTROL Installed Products]下顯示更新的版本字串`Adobe Experience Manager (6.5.10.0)`。

1. 在OSGi控制台（使用Web控制台）中，所有OSGi套件組合均為&#x200B;**[!UICONTROL ACTIVE]**&#x200B;或&#x200B;**[!UICONTROL FRAGMENT]**:`/system/console/bundles`)。

1. OSGi套件組合`org.apache.jackrabbit.oak-core`為1.22.3版或更新版本(使用Web控制台：`/system/console/bundles`)。

若要了解經認證可與此版本搭配使用的平台，請參閱[技術需求](/help/sites-deploying/technical-requirements.md)。

<!--

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

適用於Experience Manager6.5.10.0的UberJar位於[Maven Central存放庫](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.10/)中。

若要在Maven專案中使用UberJar，請參閱[如何使用UberJar](/help/sites-developing/ht-projects-maven.md)，並在您的專案POM中加入下列相依性：

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.10.0</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相關成品可在Maven中央儲存庫中使用，而非AdobePublic Maven儲存庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為`uber-jar-<version>.jar`。 因此，`dependency`標籤沒有以`apis`作為值的`classifier`。

## 過時的功能 {#removed-deprecated-features}

以下是[!DNL Experience Manager] 6.5.7.0中標籤為過時的功能清單。在以後的版本中，標籤為過時的功能將先後刪除。 提供替代選項。

查看您是否在部署中使用了功能。 此外，計畫變更實作，以使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| 整合 | **[!UICONTROL AEM雲端服務選擇加入]**&#x200B;畫面已淘汰，因為[!DNL Experience Manager]和[!DNL Adobe Target]整合已在Experience Manager6.5中更新。整合支援Adobe Target標準API。 此API使用透過AdobeIMS和[!DNL Adobe I/O]的驗證，並支援AdobeLaunch日益發揮的作用，以檢測[!DNL Experience Manager]頁面以供分析和個人化，選擇加入精靈在功能上與您無關。 | 透過個別的[!DNL Experience Manager]雲端服務，設定系統連線、AdobeIMS驗證和[!DNL Adobe I/O]整合。 |
| 連接器 | Experience Manager6.5已不再使用Microsoft® SharePoint 2010和Microsoft® SharePoint 2013的AdobeJCR連接器。 | N/A |

## 已知問題 {#known-issues}

* 如果您要將[!DNL Experience Manager]實例從6.5升級到6.5.10.0版，則可以在`error.log`檔案中查看`RRD4JReporter`異常。 若要解決問題，請重新啟動執行個體。

* 如果您在[!DNL Experience Manager] 6.5上安裝[!DNL Experience Manager] 6.5 Service Pack 10或先前的Service Pack，則會刪除資產自訂工作流程模型（在`/var/workflow/models/dam`中建立）的執行階段副本。
若要擷取執行階段副本，Adobe建議使用HTTP API，將自訂工作流程模型的設計時間副本與其執行階段副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 使用者可以重新命名[!DNL Assets]階層中的資料夾，並將巢狀資料夾發佈至[!DNL Brand Portal]。 不過，在重新發佈根資料夾之前，資料夾的標題不會在[!DNL Brand Portal]中更新。

* 當使用者首次選取以最適化表單設定欄位時，「屬性瀏覽器」中不會顯示儲存設定的選項。 在相同編輯器中選取以設定最適化表單的其他一些欄位，即可解決問題。

* 安裝Experience Manager6.5.x.x期間可能會顯示下列錯誤和警告訊息：
   * 「使用Target Standard API（IMS驗證）在Experience Manager中設定Adobe Target整合時，將體驗片段匯出至Target會導致建立錯誤的選件類型。 Target會建立數個選件，並改為類型「HTML」/來源「Adobe Target Classic」，而非「體驗片段」/來源「Adobe Experience Manager」。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`:在granite/operations/maintenance找不到維護窗口。
   * 使用SUM、MAX和MIN等匯總函式時(CQ-4274424)，適用性表單伺服器端驗證會失敗。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance處找不到維護窗口。
   * 透過Shopbable Banner檢視器預覽資產時，Dynamic Media互動式影像中的熱點不會顯示。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待登錄更改完成解除登錄的超時。

## 包含的OSGi套件組合和內容套件 {#osgi-bundles-and-content-packages-included}

以下文本文檔列出[!DNL Experience Manager] 6.5.10.0中包含的OSGi套件組合和內容包：

* [Experience Manager6.5.10.0中包含的OSGi套件組合清單](assets/65100_bundles.txt)

* [Experience Manager6.5.10.0中包含的內容套件清單](assets/65100_packages.txt)

## 受限網站 {#restricted-sites}

這些網站僅供客戶使用。 如果您是Adobe，且需要存取權，請聯絡您的客戶經理。

* [透過licensing.adobe.com下載產品](https://licensing.adobe.com/)
* 請參閱[如何聯絡Adobe客戶服務](https://experienceleague.adobe.com/docs/customer-one/using/home.html)。

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5發行說明](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/subscription/priority-product-update.html)

