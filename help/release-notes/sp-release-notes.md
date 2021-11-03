---
title: '[!DNL Experience Manager] 6.5 service pack發行說明'
description: 專屬於 [!DNL Adobe Experience Manager] 6.5 service pack 10
docset: aem65
mini-toc-levels: 1
exl-id: 28a5ed58-b024-4dde-a849-0b3edc7b8472
source-git-commit: 14339f6a34952c00351c6dee8537b5df6f6fbcd3
workflow-type: tm+mt
source-wordcount: '4436'
ht-degree: 2%

---

# [!DNL Adobe Experience Manager] 6.5 service pack發行說明 {#aem-service-pack-release-notes}

## 發行資訊 {#release-information}

| 產品 | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| 版本 | 6.5.10.0 |
| 類型 | Service Pack發行 |
| 日期 | 2021 年 8 月 26 日 |
| 下載URL | [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip) |

## 包含的項目 [!DNL Adobe Experience Manager] 6.5.10.0 {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] 6.5.10.0包含自2019年4月發行6.5版以來所發行的新功能、客戶要求的重要增強功能，以及效能、穩定性和安全性等改善項目。 Service Pack安裝在 [!DNL Adobe Experience Manager] 6.5。

中推出的主要功能和增強功能 [!DNL Adobe Experience Manager] 6.5.10.0為：

* **增強功能 [!DNL Content Fragment] 模型與編輯器**:您現在可以使用巢狀內容，為結構化內容建立複雜的自訂模型 [!DNL Content Fragment] 模型。 內容結構被模組化為基本元素，這些基本元素被建模為子片段。 較高層級片段會參考這些子片段。 進階驗證規則等更多資料類型增強功能，可進一步增強內容模型的彈性，具有 [!DNL Content Fragments]. 此 [!DNL Experience Manager] [!DNL Content Fragment] 編輯器支援通用編輯器工作階段中的巢狀片段結構，並增強功能，例如結構樹檢視和透過片段階層的標籤式階層連結導覽。

* **GraphQL API，適用於[!DNL Content Fragments]**:全新的GraphQL API是以JSON格式傳送結構化內容的標準方法。 GraphQL查詢可讓用戶端僅要求相關內容項目來呈現體驗。 這種選擇消除了需要在用戶端剖析內容的內容過傳送（在HTTP REST API中可能）。 GraphQL結構衍生自 [!DNL Content Fragment] 模型和API回應會以JSON格式產生。 在 [!DNL Experience Manager] as a [!DNL Cloud Service], [GraphQL查詢持續存在](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/graphql-api-content-fragments.html#persisted-queries-caching) 和處理快取友好GET請求。 在 [!DNL Experience Manager] 6.5.10.0。

* **階層管理與未來預覽**:使用者現在有介面可存取其內容結構 [!DNL Experience Manager] 啟動，包括在啟動中新增和移除頁面的功能。 此功能增強了 [!DNL Experience Manager] 啟動以製作鎖定於未來發佈的內容版本。 [時間扭曲功能](/help/sites-authoring/working-with-page-versions.md#timewarp) 可讓使用者將啟動預覽為未來的內容狀態。

* **連線資產**: [!DNL Experience Manager] 延伸 [!DNL Connected Assets] 功能以使用 [!DNL Dynamic Media] 影像。 請參閱 [使用連線資產](/help/assets/use-assets-across-connected-assets-instances.md).

* **連結共用選項以下載資產或轉譯**:將資產和集合共用為連結時，使用者可以選擇是否允許下載原始資產或其轉譯，或是同時使用共用連結。 此外，透過連結下載與他們共用之資產的使用者也可以選擇只下載原始資產、僅下載轉譯或兩者。

* **限制產生的子資產**:管理員可以限制 [!DNL Experience Manager] 為複合資產(如PDF、PowerPoint、InDesign和Keynote檔案)生成。 請參閱 [管理複合資產](/help/assets/managing-linked-subassets.md#generate-subassets).

* **Camera Raw支援**:新 [!DNL Camera Raw] 套件可支援 [!DNL Adobe Camera Raw] v10.4。見 [使用 [!DNL Camera Raw]](/help/assets/camera-raw.md).

* 內建存放庫(Apache Jackrabbit Oak)更新至1.22.8。

* **協助工具增強功能**:

   * [!DNL Dynamic Media] 為檢視器提供許多協助工具增強功能。 請參閱 [[!DNL Dynamic Media] 更新](#dynamic-media-65100).

   * Platform提供幾項協助工具增強功能。 請參閱 [平台更新](#platform-65100).

* **使用者體驗增強功能**:

   * [!DNL Experience Manager] 直接在資料夾下顯示所有內容模型的清單，內容作者不必瀏覽檔案結構。 此功能現在需要的點按次數更少，而且可改善製作效率。

   * 路徑欄位 [!DNL Sites] 編輯器可讓作者從 [!DNL Content Finder].

* 新增 `GuideBridge#getGuidePath` API [!DNL AEM Forms].

* 您現在可以使用Automated forms conversion服務 [以法文、德文、西班牙文、義大利文和葡萄牙文轉換PDF forms](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html#language-specific-meta-model) 最適化表單。

* **屬性瀏覽器中的錯誤訊息**:已針對適用性Forms屬性瀏覽器中的每個屬性新增錯誤訊息。 這些訊息有助於了解欄位的允許值。

* **支援使用常值選項來設定JSON類型變數的值**:您可以在AEM工作流程的設定變數步驟中使用文字選項來設定JSON類型變數的值。 文字選項可讓您以字串的形式指定JSON。

* [平台更新](../forms/using/aem-forms-jee-supported-platforms.md): [!DNL Adobe Experience Manager Forms] on JEE已新增對下列平台的支援：
   * [!DNL Adobe Acrobat 2020]
   * [!DNL Ubuntu 20.04]
   * [!DNL Open Office 4.1.10]
   * [!DNL Microsoft Office 2019]
   * [!DNL Microsoft Windows Server 2019]
   * [!DNL RHEL8]

如需中推出的所有功能和增強功能的清單，請參閱 [!DNL Experience Manager] 6.5.10.0，見 [新增功能 [!DNL Adobe Experience Manager] 6.5 Service Pack 10](new-features-latest-service-pack.md).

以下是中提供的修正清單 [!DNL Experience Manager] 6.5.10.0版。

### [!DNL Sites] {#sites-65100}

* 輸入 **[!UICONTROL 預設值]** 欄位 **[!UICONTROL 屬性]** (NPR-36992)。

* 篩選時 [!DNL Content Fragment] 模型， [!DNL Experience Manager] 搜索返回所有節點 `cq:Template` 而非僅傳迴路徑和節點 [!DNL Content Fragment] 型號(SITES-1453)。
* [!DNL Content Fragments] 傳回 `null` 作為資料夾的狀態(SITES-1157)。
* [!DNL Experience Manager] 不讓使用者停用和啟用 [!DNL Content Fragment] 型號(SITES-1088)。
* 使用者移動、重新命名或刪除 [!DNL Content Fragments] 或媒體資產，參考 [!DNL Content Fragments] 不會自動更新(SITES-196)。
* 將元件從一個頁面貼到另一個頁面會產生JavaScript錯誤(NPR-37030)。
* 快速檢視頁面屬性時，會開啟不同頁面的頁面屬性(NPR-37025)。
* 內容片段可讓內容片段參考本身。 選擇器不支援操作(NPR-36993)。
* 升級至Service Pack 9後，某些使用者無法移動Experience Manager中的資料夾，且在記錄中看到錯誤(SITES-1481)。
* 在編輯模式下調整版面容器中元件的寬度時，發現忽隱忽現的情況(NPR-36961)。
* 促銷啟動時，促銷的啟動中的變更會雙重推出至其他啟動。 如果使用者促銷雙重推出的啟動，來源頁面上會反映雙重內容(NPR-36893)。
* [!DNL Experience Manager] 如果您使用「影像核心元件」將影像新增至頁面，或使用Foundation Image元件調整大小，則會為某些PNG影像新增灰色邊框，且具有透明度(NPR-36879)。
* [!DNL Experience Manager Sites] 管理員UI含有大量範本，導覽速度緩慢(NPR-36870)。
* 升級到Service Pack 9會阻止編寫一些元件。 此問題不允許 [!DNL Sites] 建立新頁面的使用者(NPR-36857)。
* 此 `ContextHubImpl` 方法建立 `ResourceResolver` 沒有關閉。 這會導致有關長時間執行的警告訊息 `ResourceResolver` 而服務有時會傳回非預期的結果(NPR-36853)。
* 從Blueprint頁面屬性同步單一即時副本時，所有其他即時副本也會同步(NPR-36829、NPR-36522)。
* 只使用XLS MIME類型時，檔案上傳函式無法如預期運作(NPR-36785)。
* 帶有帕斯卡大小寫和所有大寫字詞的新標籤不會顯示在 [!DNL Content Fragments] (NPR-36742)。
* 新增 [!DNL Content Fragment] 導致文字遺失，並產生與清單和巢狀清單相關的奇數格式(NPR-36565)。
* 當作者註解頁面上的任何元件、刪除元件並對刪除操作執行還原時，嘗試在網站主控台中檢視頁面的時間軸資料時，會發生錯誤(NPR-36528)。
* 頁面屬性大量編輯器的 [!UICONTROL 儲存並關閉] 選項會儲存變更但不會關閉編輯器(NPR-36527)。
* 當使用者嘗試將新的文字元件拖放至頁面時，元件會立即消失(NPR-36442)。
* 當使用者在包含空格的隨需標籤中輸入內容時（系統上不存在的標籤），按下Enter鍵，標籤就會顯示在欄位下。 但若 [!DNL Content Fragment] 儲存並重新開啟，不會顯示隨選標籤(NPR-36441)。
* 透過Dispatcher存取執行個體時，無法刪除範本(NPR-36385)。
* 移動頁面時，需要手動重新整理瀏覽器，才能轉譯變更(NPR-36381)。
* 選取元件時，您可以按Ctrl+X或Ctrl+C(以及Mac上的Command+X或Command+C)來剪下或複製元件。 按一下其他元件時，您可以貼上工具列，但無法貼上鍵盤（Ctrl+V或Command+V）(NPR-36379)。
* 當使用者嘗試使用剪刀圖示將元件移至其他位置時，會發生主控台錯誤。 此外，在貼上單一元件時會移動(NPR-36378)。
* [!DNL Experience Manager] 在WCM或通知上有沒有索引的查詢，會降低效能(NPR-36303)。
* 當作者還原已刪除繼承元件的繼承時，可用選項是同步所有頁面內容。 即使繼承僅還原於一個元件，內容作者仍須同步完成的頁面。 完全同步可能會導致不想要的內容同步(NPR-34456、CQ-4310183)。
* 製作例項上元件的即時使用不會顯示所有發生次數。 某些元件用於超過1000個頁面，但報表只會顯示約40個頁面(CQ-4323724)。
* 當網站結構中有許多子頁面時，在欄檢視中載入子頁面的Experience Manager6.5.8比Experience Manager6.4.8.2(CQ-4322766)需要更多時間。
* 在「轉出頁面」選項上取消勾選「全部」無法運作(NPR-37070)。
* 開啟現有的v3元件版本頁面時，頁面屬性對話方塊不會開啟，且 `NullPointerException` 已記錄(SITES-1830)。

### [!DNL Assets] {#assets-65100}

已在 [!DNL Assets]:

* 屬性的值 `jcr:title` 移動資料夾後，不會在Publish例項上更新。 在作者中重新命名和重新發佈資料夾不會更新 `jcr:title` 發佈執行個體中相同的屬性值(NPR-36369)。

* 如果選取兩個或多個資產並編輯一個或多個中繼資料欄位，儲存作業會在Safari瀏覽器中失敗，錯誤代碼為500(NPR-36413)。

* 由於日期格式錯誤，大量中繼資料匯入失敗(NPR-36428)。

* 當在 [!UICONTROL 屬性] 頁面更新中繼資料時，當結構提供許多選項時介面回應速度緩慢(NPR-36430)。

* 使用 [!UICONTROL 到期狀態] 述詞無法運作(NPR-36436)。

* 中各欄位的快顯功能表 [!UICONTROL 資料夾中繼資料] 屬性不會顯示最後選取的值(NPR-36937、CQ-4314429)。

* 搜索檔案和資料夾時，如果用戶應用了篩選器並選擇 [!UICONTROL 檔案和資料夾]，只會顯示檔案，但不會顯示資料夾(CQ-4319543、NPR-36627)。

* 從資料夾內選取相同集合，以及從搜尋結果選取集合時，工具列選項不同(NPR-36620)。

* 此 [!UICONTROL 快速發佈] 選項在搜尋結果頁面上無法使用(NPR-36904、CQ-4317748)。

* 使用者在未指定副檔名的情況下建立資產的即時副本時，下載後即時副本檔案無法使用(NPR-36903、CQ-4326305)。

* 將用戶添加為子資料夾的所有者時，用戶也獲得其父資料夾的所有者權限，因此也獲得父資料夾的其他子資料夾的所有者權限。 此外，嘗試移除時，不會將使用者移除為父資料夾的擁有者。 (NPR-36801、CQ-4323737)。

* [!DNL Experience Manager] 嘗試為複合資產（如PowerPoint演示文稿）建立子資產時，會產生記憶體不足的例外狀況(NPR-36668)。

* 當使用者移動已在已發佈網站頁面中使用的資產時，即使未選取發佈選項，網站頁面仍會再次發佈(NPR-36636、CQ-4323500)。

* 使用Apache Tika MIME類型偵測功能時，會使用 `AssetManager.createAsset` 方法保留名為的臨時檔案 `apache-tika-*.tmp` 檔案。 此臨時檔案使用所有可用的可用磁碟空間(NPR-36545)。

* 所有受DRM保護的資產都會下載，且使用者不會選擇下載特定資產(CQ-4327422)。

* 無法將資產拖曳至 `pathfield` (NPR-36849)。

* 在欄檢視中選取資產時，資產詳細資訊面板會消失(NPR-36667)。

### [!DNL Dynamic Media] {#dynamic-media-65100}

**協助工具增強功能**

下列協助工具增強功能適用於 [!DNL Dynamic Media Viewers].

* 螢幕助讀程式現在會提供旁白，說明預留位置文字以供搜尋，並新增電子郵件地址作為共用資產作為連結對話方塊的必要欄位，同時也會朗讀 [!UICONTROL 請填寫此欄位] 工具提示(CQ-4327761)。

* 螢幕助讀程式現在會正確提供 [!UICONTROL 影像預設集編輯器] 使用鍵盤存取使用者介面欄位時(CQ-4325677)。

* 鍵盤焦點現在可適當移至的搜尋標籤 [!UICONTROL 檢視器預設集] 對話框， [!UICONTROL 多媒體類型] 選項(CQ-4324736)。

* 使用鍵盤鍵在表單模式中導覽時，螢幕助讀程式會提供與上的遞增和遞減選項對應的標籤旁白 [!UICONTROL 建立] 標籤 [!UICONTROL 影像預設集] (CQ-4323900)。

* 螢幕助讀程式現在會宣佈 [!UICONTROL 搜尋及新增電子郵件地址] 選項(CQ-4323352)。

* 使用鍵盤鍵導覽資產時，工具列上會保留鍵盤焦點(CQ-4322037)。

* 螢幕助讀程式現在會提供新增的旁白 [!UICONTROL 編輯] 欄位資訊 [!UICONTROL 新增裁切] 選項 [!UICONTROL 回應式影像裁切] on [!UICONTROL 編輯影像處理設定檔] 第(CQ-4290734)頁。

* 開啟 [!UICONTROL 編輯影像預設集] 和 [!UICONTROL 建立互動式影片] 頁面時，螢幕助讀程式現在會在使用標題鍵盤快速鍵(CQ-4290730)(CQ-4290701)導覽頁面時適當地朗讀頁面標題。

* 現在，在導覽下列頁面時，螢幕助讀程式可以使用里程碑和區域快捷鍵，來識別螢幕的各個區域（例如右面板區域、左面板、動作工具列、檢視器工具列地標和可縮放的影像地標）。

   * [!UICONTROL 檢視器預設集編輯器] (CQ-4290729)

   * [!UICONTROL 影像集編輯器] (CQ-4290710)

   * [!UICONTROL 建立互動式影片] (CQ-4290702)。

* 使用向下鍵導覽時，螢幕助讀程式現在會朗讀視訊影格中的共用選項名稱(CQ-4290728)。

* 螢幕助讀程式現在會提供 [!UICONTROL Sprite] 和 [!UICONTROL 背景] 標籤 [!UICONTROL 外觀] 標籤 [!UICONTROL 檢視器預設集編輯器] (CQ-4290727)。

* 必填欄位，例如要編輯的欄位 [!UICONTROL 寬度]，在 [!UICONTROL 基本] 標籤 [!UICONTROL 編輯視訊編碼] 頁面現在有星號符號(*)(CQ-4290725)。

* 螢幕助讀程式現在會朗讀 [!UICONTROL 影像設定檔] 第(CQ-4290723)頁。

* Windows使用者現在可以在上導覽至展開的CSS編輯器外 [!UICONTROL 檢視器預設集編輯器] 時(CQ-4290720)。

* 開啟 [!UICONTROL 基本] 標籤 [!UICONTROL 編輯影像預設集] 在表單模式中導覽時，螢幕助讀程式現在會提供各種編輯欄位和選項的標籤旁白(CQ-4290717)。

* 螢幕助讀程式現在會在資產詳細資訊頁面的左側導覽中，提供角色和狀態（選取或未選取）的旁白，以供使用者介面選項使用(CQ-4290709)。

* 螢幕助讀程式現在會正確提供狀態旁白（已選取或未選取），而影像的連結會切換至 [!UICONTROL 內容] 標籤 [!UICONTROL 建立互動式影片] 第(CQ-4290707)頁。

* 使用向下鍵導覽時，螢幕助讀程式現在會正確提供視訊時間軸縮放中各區段的名稱、角色和狀態旁白 [!UICONTROL 建立互動式影片] 第(CQ-4290706)頁。

* 螢幕助讀程式現在會在導覽中的選項時，提供名稱、角色和預設狀態（選取或未選取）及屬性的旁白 [!UICONTROL 建立互動式影片] 第(CQ-4290704)頁。

* 螢幕助讀程式現在會提供旁白，說明 [!UICONTROL 所有資產] 和 [!UICONTROL 所有集合] 選項 [!UICONTROL 發佈] 第(CQ-4290705)頁。

* 上傳不支援的視訊格式（MP4除外）時， [!UICONTROL 建立互動式影片] 頁面、Experience Manager顯示並朗讀錯誤訊息(CQ-4290700)。

* 時間軸中數字的對比（以秒為單位） [!UICONTROL 建立互動式影片] 頁面現在符合最低的明度比例，因此對顏色有限的使用者可輕鬆閱讀(CQ-4290699)。

* 螢幕助讀程式現在會朗讀 [!UICONTROL 產品名稱] 欄位 [!UICONTROL 建立互動式影片] 第(CQ-4290697)頁。

**已修正的問題**

下列錯誤修正適用於 [!DNL Dynamic Media].

* 上傳的影片至 [!DNL Experience Manager] 顯示 `Process failed` after `dynamicmedia_scene7` 執行模式已啟用且同步已停用(CQ-4327791)。

### 平台 {#platform-65100}

此Service Pack提供下列增強功能：

* 當使用者在樹狀檢視中選取項目時，螢幕助讀程式會宣佈選取項目，而頂端會顯示工具列選項(NPR-36504)。
* 有些文字和控制項名稱較容易閱讀，因為明度比符合4.5:1的最低需求比率(NPR-36503)。
* 使用者使用日曆控制項時，螢幕助讀程式會提供描述性日期、月份和工作日資訊的旁白。 使用者使用日曆快捷鍵時，螢幕助讀程式會提供日期、月份和年份變更的旁白(NPR-36498)。
* 提供執行自訂JavaScript的支援 `Clientlibs` 使用ECMAScript 6功能，而不遵循嚴格模式。 具體來說， `emitUseStrict` 旗標會新增至 `GCCScriptProcessor` (NPR-36411)。

下列錯誤修正是此Service Pack的一部分：

* 自訂健全狀態檢查的執行頻率比排程的更高(NPR-36985)。
* 此 `Resourceresolver map` 方法針對別名頁面傳回錯誤的結果(NPR-36767)。
* [!DNL Experience Manager] 啟動因載入工作流程而延遲(NPR-36615)。

### Integrations {#integrations-65100}

* 當主要MongoDB節點切換至其他節點時，Experience Manager會停止回應(NPR-36566)。
* [!DNL Sling content distribution] 執行收整合員刪除操作時失敗(NPR-36521、CQ-4323578)。

### 使用者介面 {#user-interface-65100}

* 此 **[!UICONTROL 參考]** 側面板不會顯示資產和網站參考(GRANITE-35078、GRANITE-34892)。

### 翻譯專案 {#translation-65100}

* 刪除多翻譯專案語言副本中的額外子頁面(NPR-36622)。

### 工作流程 {#workflow-65100}

* 如果伺服器收到不在辦公室的訊息，則會回報記憶體警報並停止回應(NPR-36768)。

### [!DNL Communities] {#communities-65100}

* 在中開啟社群網站頁面 `LoggedIn` 匿名訪客使用者的狀態(NPR-36908)。

* 當 **[!UICONTROL 社群]** > **[!UICONTROL 構想]** > **[!UICONTROL 註解]** 頁面，頁面導覽無法運作(NPR-36541)。

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


[!DNL AEM 6.5.10.0 Forms] 包含下列錯誤修正：

* 安裝時 [!DNL AEM 6.5 Forms]，會自動安裝下列第三方程式庫(CQDOC-18373):
   * [!DNL Microsoft Visual C++ 2008 Service Pack 1 (x86)]
   * [!DNL Microsoft Visual C++ 2010 Service Pack 1 (x86)]

**調適型表單**

* 如果適用性表單中欄位值的驗證成功， [!DNL AEM Forms] 無法叫用表單資料模型(CQ-4325491)。

* 在翻譯專案中新增語言字典，然後開啟專案時， [!DNL AEM Forms] 顯示錯誤訊息(CQ-4324933):

   ```TXT
   Uncaught TypeError: Cannot read property 'PROJECT_LISTING_PATH' of undefined
   at openButtonClickHandler (clientlibs.js:245)
   at HTMLButtonElement.onclick (clientlibs.js:258)
   ```

* 安裝後出現效能問題 [!DNL AEM Forms] Service Pack 7(CQ-4326828)。

* 當您從Apple iOS裝置提交包含標準HTML上傳欄位的表單時，有時不會傳送檔案內容，而會在另一端收到0位元組檔案。 Apple iOS 15.1提供了問題的修正(CQ-4325361)。

**通信管理**

* 在 [!UICONTROL 資料] 標籤以及HTML信函預覽(NPR-37020)。

* 編輯文字檔案片段時，儲存片段後新字詞會顯示為HTML標籤(NPR-36837)。

* 無法檢視另存為草稿的信函(NPR-36816)。

* 當您編輯文字檔案片段並預覽信函時，AEM Forms會在HTML信函預覽中顯示運算式語言(CQ-4322331)。

* 使用自助信函範本轉譯資料時發生問題(NPR-37161)。


**互動式通訊**

* 編輯文字檔案片段後，每次您列印預覽互動式通訊時，索引標籤字元會在兩個字之間重複(NPR-37021)。

* [!DNL AEM Forms] 儲存超過最大大小限制的文字檔案片段時顯示錯誤(NPR-36874)。

* 將影像新增至互動式通訊時，影像後面會顯示另一個空白區塊(NPR-36659)。

* 在編輯器中選取所有文字時，無法將字型文字變更為Arial(NPR-36646)。

* 在編輯器中建立URL並預覽變更時，畫面會顯示黑色背景，而非URL文字(NPR-36640)。

* 將文字複製並貼到編輯器時，針對檔案中可用的項目符號將字型變更為Arial時會發生問題(NPR-36628)。

* 文字編輯器中的項目符號縮排問題(NPR-36513)。

**設計工具**

* 螢幕Reader無法讀取動態PDF中，置於主版頁面或子表單頁面文字標籤內的浮動欄位資料(CQ-4321587)。

**文件服務**

* 將XDP檔案轉換為PDF檔案，然後組合產生的PDF時，PDF層代會失敗，並顯示下列錯誤訊息：

   ```TXT
   Caused by: com.adobe.fd.assembler.client.AssemblerException$ClientException: Document is in a disposed state!
   ```

**表單工作流程**

* 升級至AEM Forms Service Pack 8後，無法將表單提交至Workbench程式(CQ-4325846)。

**HTML5 Forms**

* 當您為 `mfAllowAttachments` 屬性為 `True` 在CRX DE存放庫中， `dataXml` 提交HTML5表單時損毀(NPR-37035)。

* 將XDP呈現為HTML時，請使用 `dataXml`, [!DNL AEM Forms] 顯示 `Page Unresponsive` 錯誤(NPR-36631)。

### 商務 {#commerce-65100}

* 中的值 **[!UICONTROL 發佈者]** 欄檢視中顯示的欄位不正確(NPR-36902)。
* 推出目錄時，新產品未正確標示為修改的產品(NPR-36666)。
* 當您重新建立已刪除的產品時，不會重新建立產品頁面(NPR-36665)。
* 已修改的頁面已更新，但目錄轉出時沒有更新對應的連結產品(CQ-4321409、NPR-36422)。
* 此 **[!UICONTROL 稍後發佈]** 和 **[!UICONTROL 稍後取消發佈]** 工作流程無法運作(CQ-4327679)。

如需安全性更新的詳細資訊，請參閱 [[!DNL Experience Manager] 安全性佈告欄頁面](https://helpx.adobe.com/security/products/experience-manager.html).

## 安裝6.5.10.0 {#install}

**設定需求和詳細資訊**

* Experience Manager6.5.10.0需要Experience Manager6.5。請參閱 [升級檔案](/help/sites-deploying/upgrade.md) 以取得詳細指示。
* Service Pack下載可在Adobe上取得 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html).
* 在具有MongoDB和多個執行個體的部署上，使用套件管理器在其中一個製作執行個體上安裝Experience Manager6.5.10.0。

>[!NOTE]
>
>Adobe不建議移除或解除安裝 [!DNL Adobe Experience Manager] 6.5.10.0包。

### 安裝Service Pack {#install-service-pack}

在 [!DNL Adobe Experience Manager] 6.5執行個體，請依照下列步驟操作：

1. 如果執行個體處於更新模式（從舊版更新執行個體時），請先重新啟動執行個體再進行安裝。 Adobe建議，如果執行個體的目前正常運行時間很長，則重新啟動。

1. 安裝之前，請拍攝快照或對 [!DNL Experience Manager] 例項。

1. 從下載Service Pack [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.10.zip).

1. 開啟套件管理器，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。要了解更多資訊，請參閱 [封裝管理員](/help/sites-administering/package-manager.md).

1. 選取套件，然後按一下 **[!UICONTROL 安裝]**.

1. 若要更新S3連接器，請在安裝Service Pack後停止執行個體，以安裝資料夾中提供的新二進位檔案取代現有連接器，然後重新啟動執行個體。 請參閱 [Amazon S3 Data Store](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector).

>[!NOTE]
>
>安裝Service Pack時，有時會退出Package Manager UI上的對話方塊。 Adobe建議您先等待錯誤記錄穩定，再存取部署。 請等待與卸載更新程式捆綁相關的特定日誌，然後確保安裝成功。 通常，此問題會發生在 [!DNL Safari] 瀏覽器，但可在任何瀏覽器上間歇性發生。

**自動安裝**

自動安裝有兩種方式 [!DNL Experience Manager] 6.5.10.0（工作實例）:

A.將包裹放入 `../crx-quickstart/install` 資料夾。 程式包會自動安裝。

B.使用 [來自套件管理器的HTTP API](/help/sites-administering/package-manager.md#package-share). 使用 `cmd=install&recursive=true` 以便安裝嵌套包。

>[!NOTE]
>
>Adobe Experience Manager 6.5.10.0不支援安裝Bootstrap。

**驗證安裝**

1. 產品資訊頁面(`/system/console/productinfo`)顯示更新的版本字串 `Adobe Experience Manager (6.5.10.0)` 在 [!UICONTROL 已安裝的產品].

1. 所有OSGi套件組合 **[!UICONTROL 活動]** 或 **[!UICONTROL 片段]** 在OSGi控制台中(使用Web控制台： `/system/console/bundles`)。

1. OSGi捆綁 `org.apache.jackrabbit.oak-core` 為1.22.3版或更新版本(使用Web控制台： `/system/console/bundles`)。

若要了解經認證可與此版本搭配使用的平台，請參閱 [技術要求](/help/sites-deploying/technical-requirements.md).

### 安裝Adobe Experience Manager Forms附加元件套件 {#install-aem-forms-add-on-package}

>[!NOTE]
>
>如果您未使用Experience Manager Forms，請略過。 Experience Manager Forms中的修正會在排程後一週透過個別的附加套件提供 [!DNL Experience Manager] Service Pack版本。

1. 確認您已安裝Adobe Experience Manager Service Pack。
1. 下載適用於您作業系統的 [AEM Forms 發行版本](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates)所列出的對應 Forms 附加套件。
1. 依照 [安裝AEM Forms附加元件套件](../forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager6.5.10.0包含 [AEM Forms相容性套件](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). 如果您使用舊版AEM Forms相容性套件並更新至Experience Manager6.5.10.0，請在安裝Forms附加元件套件後安裝最新版本的套件。

### 在JEE上安裝Adobe Experience Manager Forms {#install-aem-forms-jee-installer}

>[!NOTE]
>
>如果您沒有在JEE上使用AEM Forms，請略過。 JEE版Adobe Experience Manager Forms中的修正是透過個別安裝程式提供。

如需在JEE上安裝Experience Manager Forms的累積安裝程式和部署後設定的相關資訊，請參閱 [發行說明](jee-patch-installer-65.md).

>[!NOTE]
>
>在JEE上安裝Experience Manager Forms的Cumulative Installer後，請安裝最新的Forms附加元件套件，從 `crx-repository\install` ，然後重新啟動伺服器。


### UberJar {#uber-jar}

適用於Experience Manager6.5.10.0的UberJar可於 [Maven Central存放庫](https://repo1.maven.org/maven2/com/adobe/aem/uber-jar/6.5.10/).

若要在Maven專案中使用UberJar，請參閱 [如何使用UberJar](/help/sites-developing/ht-projects-maven.md) 並在您的專案POM中加入下列相依性：

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.10</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>UberJar和其他相關成品可在Maven中央存放庫中取得，而非AdobePublic Maven存放庫(`repo.adobe.com`)。 主要UberJar檔案已重新命名為 `uber-jar-<version>.jar`. 所以，沒有 `classifier`，使用 `apis` 作為值，對於 `dependency` 標籤。

## 過時的功能 {#removed-deprecated-features}

以下是標示為過時的功能清單 [!DNL Experience Manager] 6.5.7.0。功能在日後的版本中已被標示為過時，且在稍後的版本中已移除。 提供替代選項。

查看您是否在部署中使用了功能。 此外，計畫變更實作，以使用替代選項。

| 區域 | 功能 | 替代方案 |
|---|---|---|
| 整合 | 此 **[!UICONTROL AEM雲端服務選擇加入]** 螢幕已過時，因為 [!DNL Experience Manager] 和 [!DNL Adobe Target] Experience Manager6.5已更新整合。整合支援Adobe Target Standard API。 此API使用透過Adobe IMS的驗證，以及 [!DNL Adobe I/O] 並支援AdobeLaunch在儀器方面日益發揮的作用 [!DNL Experience Manager] 分析和個人化的頁面，選擇加入精靈的功能與您無關。 | 設定系統連線、Adobe IMS驗證，以及 [!DNL Adobe I/O] 透過個別 [!DNL Experience Manager] 雲端服務。 |
| 連接器 | 適用於Microsoft® SharePoint 2010和Microsoft® SharePoint 2013的AdobeJCR連接器已於Experience Manager6.5中淘汰。 | N/A |

## 已知問題 {#known-issues}

* As [!DNL Microsoft Windows Server 2019] 不支援 [!DNL MySQL 5.7] 和 [!DNL JBoss EAP 7.1], [!DNL Microsoft Windows Server 2019] 不支援全包安裝 [!DNL AEM Forms 6.5.10.0].

* 如果您要升級 [!DNL Experience Manager] 執行個體(從6.5版到6.5.10.0版)，您可以檢視 `RRD4JReporter` 例外 `error.log` 檔案。 若要解決問題，請重新啟動執行個體。

* 如果您安裝 [!DNL Experience Manager] 6.5 Service Pack 10或上一個Service Pack [!DNL Experience Manager] 6.5，資產自訂工作流程模型的執行階段副本(在 `/var/workflow/models/dam`)。
若要擷取執行階段副本，Adobe建議使用HTTP API，將自訂工作流程模型的設計時間副本與其執行階段副本同步：
   `<designModelPath>/jcr:content.generate.json`。

* 使用者可以在 [!DNL Assets] 並將巢狀資料夾發佈至 [!DNL Brand Portal]. 不過，資料夾的標題不會在 [!DNL Brand Portal] 直到重新發佈根資料夾為止。

* 當使用者首次選取以最適化表單設定欄位時，「屬性瀏覽器」中不會顯示儲存設定的選項。 在相同編輯器中選取以設定最適化表單的其他一些欄位，即可解決問題。

* 安裝Experience Manager6.5.x.x期間可能會顯示下列錯誤和警告訊息：
   * 「使用Target Standard API（IMS驗證）在Experience Manager中設定Adobe Target整合時，將體驗片段匯出至Target會導致建立錯誤的選件類型。 Target會建立數個具有「HTML」/來源「Adobe Target Classic」類型的選件，而非「體驗片段」/來源「Adobe Experience Manager」。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`:在granite/operations/maintenance找不到維護窗口。
   * 使用SUM、MAX和MIN等匯總函式時(CQ-4274424)，適用性表單伺服器端驗證會失敗。
   * `com.adobe.granite.maintenance.impl.TaskScheduler`  — 在granite/operations/maintenance處找不到維護窗口。
   * 透過Shopbable Banner檢視器預覽資產時，Dynamic Media互動式影像中的熱點不會顯示。
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]` :等待登錄更改完成解除登錄的超時。

## 包含的OSGi套件組合和內容套件 {#osgi-bundles-and-content-packages-included}

以下文字檔案列出包含在 [!DNL Experience Manager] 6.5.10.0:

* [Experience Manager6.5.10.0中包含的OSGi套件組合清單](assets/65100_bundles.txt)

* [Experience Manager6.5.10.0中包含的內容套件清單](assets/65100_packages.txt)

## 受限網站 {#restricted-sites}

這些網站僅供客戶使用。 如果您是Adobe，且需要存取權，請聯絡您的客戶經理。

* [透過licensing.adobe.com下載產品](https://licensing.adobe.com/)
* 請參閱 [如何聯絡Adobe客戶支援](https://experienceleague.adobe.com/docs/customer-one/using/home.html).

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] 6.5發行說明](/help/release-notes/release-notes.md)
>* [[!DNL Experience Manager] 產品頁面](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] 6.5檔案](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=zh-Hant)
>* [訂閱 Adobe 優先產品更新](https://www.adobe.com/tw/subscription/priority-product-update.html)

